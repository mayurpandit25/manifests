1.create a eks cluster

2.access on terminal 
  1.aws eks update-kubeconfig --name eks --region ap-southeast-1
  2.kubectl get nodes

2.install helm
  1.curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
  2.helm version

3.install nginx-ingress using helm
  1.helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
  2.helm repo update
  3.kubectl create namespace ingress-nginx
  4.helm install ingress-nginx ingress-nginx/ingress-nginx \
     --namespace ingress-nginx \
     --set controller.service.type=LoadBalancer \
     --set controller.service.annotations."service\.beta\.kubernetes\.io/aws-load-balancer-type"="nlb" \
     --set controller.replicaCount=2

4.verify
  1.kubectl get pods -n ingress-nginx
  2.kubectl get svc -n ingress-nginx
