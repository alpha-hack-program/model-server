# model-server

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: vllm-mistral-7b
  namespace: openshift-gitops
  annotations:
    argocd.argoproj.io/compare-options: IgnoreExtraneous
spec:
  project: default
  destination:
    server: 'https://kubernetes.default.svc'
    namespace: vllm-mistral-7b
  source:
    path: .
    repoURL: https://github.com/alpha-hack-program/model-server.git
    targetRevision: main
    helm:
      parameters:
        - name: instanceName
          value: "vllm-mistral-7b"
        - name: dataScienceProjectNamespace
          value: "vllm-mistral-7b"
        - name: dataScienceProjectDisplayName
          value: "vllm-mistral-7b"
        - name: model.root
          value: mistralai
        - name: model.id
          value: Mistral-7B-Instruct-v0.2
        - name: model.name
          value: mistral-7b
        - name: model.displayName
          value: "Mistral 7b"
        - name: model.accelerator.productName
          value: "NVIDIA-A10G"
        - name: model.accelerator.min
          value: 1
        - name: model.accelerator.max
          value: 1
  syncPolicy:
    automated:
      # prune: true
      selfHeal: true
```