I recently had a desire to deploy the vertical pod autoscaler on EKS with ArgoCD and kustomize. 
However, the instructions for EKS and in the project weren't quite in the right format for me. 
I ran into three main problems with 0.9.2 that I had to overcome:

1. Installation uses hack/vpa-up.sh which calls a script which generates self-signed certificates and loads a secret. Further, the keys/names of the files in the secret don't match the ones auto-populated by tools like cert-manager.
2. The stored CustomResourceDefinition manifest in the project's git source contains optional, yet empty keys. ArgoCD loses it's mind on that.
3. The images referenced in the manifests are versioned 0.8.1, not the correct 0.9.2 ones.

To overcome these issues, I was able to identify a straightforward kustomization.yaml. 
Recording those here in case they are useful to anybody else
