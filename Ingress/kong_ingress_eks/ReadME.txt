1.create a EKS cluster

2.access on terminal
  1.aws eks update-kubeconfig --name eks --region ap-southeast-1
  2.kubectl get nodes

3.Install Helm
  1.curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
  2.helm version

4.Install kong-ingress
  1.helm repo add kong https://charts.konghq.com
  2.helm repo update
  3.kubectl create namespace kong
  4.helm install kong kong/kong \
      --namespace kong \
      --set ingressController.installCRDs=false \
      --set ingressController.enabled=true \
      --set proxy.type=LoadBalancer \
      --set proxy.annotations."service\.beta\.kubernetes\.io/aws-load-balancer-type"="nlb"

5.Verify kong pods
  1.kubectl get pods -n kong
  2.kubectl get svc -n kong
