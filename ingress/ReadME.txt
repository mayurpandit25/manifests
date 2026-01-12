THESE PRACTICAL IS ON LOCAL 

1.start the ingress in minikube
  minikube addons enable ingress

2.vim /etc/hosts
  (minikube_ip)   cbz.com

3.run minikube tunnel on another terminal
  minikube tunnel

4.On terminal
  curl cbz.com
  curl cbz.com/mobile/

5.On Browser
  http://cbz.com
  http://cbz.com/mobile
