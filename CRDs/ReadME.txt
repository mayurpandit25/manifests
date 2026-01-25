1.kubectl apply -f devops-crd.yaml
2.kubect get crd
  { devopsbatches.mayur.com }

3.kubectl apply -f devops-cr1.yaml
4.kubectl get devopsbatches -n devops-batch
  { batch-1 }

5.kubectl apply -f devops-cr2.yaml
6.kubectl get devopsbatches -n devops-batch
  { batch-1 / batch-2 }

7.kubectl describe devopsbatch batch-1 -n devops-batch
8.kubectl describe devopsbatch batch-2 -n devops-batch

Note:-
1.crd is a cluster specific
2.while the cr is a namespace specific so its ur default as well as custom namespace

