1.create a cluster
  minikube start

2.Install headlamp using helm
  1.helm repo add headlamp https://kubernetes-sigs.github.io/headlamp/
  2.helm install my-headlamp headlamp/headlamp --namespace kube-system
  3.kubectl get pods -n kube-system -w

3.Create a service-account
  1.kubectl create serviceaccount headlamp-admin -n kube-system
  2.kubectl get sa -n kube-system

4.Grant admin rights
  kubectl create clusterrolebinding headlamp-admin --serviceaccount=kube-system:headlamp-admin --clusterrole=cluster-admin

5.Create a token
  kubectl create token headlamp-admin -n kube-system
  { copy the token }

3.Forward the Headlamp service
  kubectl port-forward -n kube-system svc/my-headlamp 8080:80 --address=0.0.0.0 &
  { http://<PUBLIC_IP>:8080 }
  { paste the token }

