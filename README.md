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
          value: '1'
        - name: model.accelerator.max
          value: '1'
  syncPolicy:
    automated:
      # prune: true
      selfHeal: true
```

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: vllm-llama-3-8b
  namespace: openshift-gitops
  annotations:
    argocd.argoproj.io/compare-options: IgnoreExtraneous
spec:
  project: default
  destination:
    server: 'https://kubernetes.default.svc'
    namespace: vllm-llama-3-8b
  source:
    path: .
    repoURL: https://github.com/alpha-hack-program/model-server.git
    targetRevision: main
    helm:
      parameters:
        - name: instanceName
          value: "vllm-llama-3-8b"
        - name: dataScienceProjectNamespace
          value: "vllm-llama-3-8b"
        - name: dataScienceProjectDisplayName
          value: "vllm-llama-3-8b"
        - name: model.root
          value: meta-llama
        - name: model.id
          value: Meta-Llama-3-8B-Instruct
        - name: model.name
          value: llama-3-8b
        - name: model.displayName
          value: "Llama 3 8B"
        - name: model.accelerator.productName
          value: "NVIDIA-A10G"
        - name: model.accelerator.min
          value: '1'
        - name: model.accelerator.max
          value: '1'
  syncPolicy:
    automated:
      # prune: true
      selfHeal: true
```