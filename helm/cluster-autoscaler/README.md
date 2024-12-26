## IAM Policy 및 role 생성

Cluster Autoscaler 가 IAM role 을 사용하기 위해 필요한 권한을 주기 위해 IAM Policy 생성이 필요하다.

### IAM Policy 생성

1. 아래와 같이 `cluster-autoscaler-policy.json` 파일을 생성한다.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "autoscaling:DescribeAutoScalingGroups",
                "autoscaling:DescribeAutoScalingInstances",
                "autoscaling:DescribeLaunchConfigurations",
                "autoscaling:DescribeTags",
                "autoscaling:SetDesiredCapacity",
                "autoscaling:TerminateInstanceInAutoScalingGroup",
                "ec2:DescribeLaunchTemplateVersions"
            ],
            "Resource": "*",
            "Effect": "Allow"
        }
    ]
}
```

### IAM role 생성

아래와 같이 `eksctl`을 사용하여 IAM role을 생성할 수 있다.

```bash
eksctl create iamserviceaccount \
  --cluster=eks-demo \
  --namespace=kube-system \
  --name=cluster-autoscaler \
  --attach-policy-arn=<위에서 생성한 policy의 arn> \
  --override-existing-serviceaccounts \
  --approve
```

## Deploy Cluster Autoscaler

1. 우선 Cluster Autoscaler YALM 파일을 다운로드 한다.
    
    ```bash
    curl -o cluster-autoscaler-autodiscover.yaml https://raw.githubusercontent.com/kubernetes/autoscaler/master/cluster-autoscaler/cloudprovider/aws/examples/cluster-autoscaler-autodiscover.yaml
    ```
    
2. YAML 파일을 열어서 `<YOUR CLUSTER NAME>` 을 찾아서 `eks-demo` 로 replace 한다.
3. 그리고 적용한다.
    
    ```bash
    kubectl apply -f cluster-autoscaler-autodiscover.yaml
    ```
    
    ℹ️ 문서에는 이 다음에 service account을 annotate 하는 부분이 있는데 확인해보면 이미 되어있다.
    
4. `cluster-autoscaler.kubernetes.io.safe-to-evict`를 추가하기 위해 아래와 같이 patch 한다.
    
    ```bash
    kubectl patch deployment cluster-autoscaler \
      -n kube-system \
      -p '{"spec":{"template":{"metadata":{"annotations":{"cluster-autoscaler.kubernetes.io/safe-to-evict": "false"}}}}}'
    ```
    
5. 그리고 `cluster-autoscaler` deployment를 수정한다.
    
    ```bash
    kubectl -n kube-system edit deployment.apps/cluster-autoscaler
    ```
    
    `<YOUR CLUSTER NAME>` 을 `eks-demo` 로 수정하고 container command 에 `--balance-similar-node-groups` 와 `--skip-nodes-with-system-pods=false` 를 추가하여 아래와 같이 수정한다.
    
    ```yaml
        spec:
          containers:
          - command
            - ./cluster-autoscaler
            - --v=4
            - --stderrthreshold=info
            - --cloud-provider=aws
            - --skip-nodes-with-local-storage=false
            - --expander=least-waste
            - --node-group-auto-discovery=asg:tag=k8s.io/cluster-autoscaler/enabled,k8s.io/cluster-autoscaler/<YOUR CLUSTER NAME>
            - --balance-similar-node-groups
            - --skip-nodes-with-system-pods=false
    ```
    
6. Cluster Autoscaler [release](https://github.com/kubernetes/autoscaler/releases) 페이지를 열어서 설치한 kubernetes 버전의 최신 cluster autoscaler 를 확인한다.
7. 위에서 확인한 버전을 아래와 같이 적용한다. (v1.21.2를 가정한다.)
    
    ```
    kubectl set image deployment cluster-autoscaler \
      -n kube-system \
      cluster-autoscaler=k8s.gcr.io/autoscaling/cluster-autoscaler:v1.21.2
    ```
    

## Cluster Autoscaler 로그 확인

Cluster Autoscaler 를 deploy 한 후에 로그를 확인하여 제대로 동작하는지 확인한다.

```
kubectl -n kube-system logs -f deployment.apps/cluster-autoscaler
```

✋ 참고로 최근에는 [Karpenter](https://karpenter.sh/)가 나와서 Cluster Autoscaler 대신 이걸 활용 할 수도 있다.

출처 : https://velog.io/@airoasis/eks-cluster-autoscaler