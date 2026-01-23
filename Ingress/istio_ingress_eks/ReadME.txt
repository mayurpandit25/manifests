1.create a EKS cluster

2.access on terminal
  1.aws eks update-kubeconfig --name eks --region ap-southeast-1
  2.kubectl get nodes

3.Install Istio CLI
  1.curl -L https://istio.io/downloadIstio | sh -
  2.cd istio-*
  3.export PATH=$PWD/bin:$PATH
  4.istioctl version

4.Install Istio with Ingress Gateway
  1.istioctl install --set profile=demo -y
  2.kubectl get pods -n istio-system

5.Enable Sidecar Injection
  1.kubectl label namespace default istio-injection=enabled
  2.kubectl get ns --show-labels

6.Get or Copy Istio LoadBalancer DNS
  1.kubectl get svc istio-ingressgateway -n istio-system

7.verify everything 
  1.kubectl get pods
  2.kubectl get svc
  3.kubectl get pods -n istio-system
  4.kubectl get svc -n istio-system
  5.kubectl get gateway
  6.kubectl get virtualservice

8.URLs
<istio_load_balancer>     -------------> nginx-home page
<istio_load_balancer>/mobile ----------> httpd-mobile page
<istio_load_balancer>/laptop ----------> tomcat-laptop page















