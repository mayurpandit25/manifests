CREATION OF KUBERNETES DASHBOARD

1.create a namespace
  namespace: kubernetes-dashboard

2.create a user with... 
  dashboard.yml

3.Install k8s_dashboard
  kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml 

4.create a token
  kubectl -n kubernetes-dashboard create token admin-user 

If u want to port-forward then run
kubectl port-forward svc/kubernetes-dashboard -n kubernetes-dashboard 8080:443 --address=0.0.0.0 &

access_on...
https://public_ip:8080

Paste the created token -> 

