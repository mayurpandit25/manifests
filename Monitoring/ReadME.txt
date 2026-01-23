MONITORING WITH PROMETHEUS AND GRAFANA

1.Install helm 
  1.curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-4  
  2.chmod 700 get_helm.sh
  3../get_helm.sh
  4.helm version

2.create namespace
  namespace.yml

3.Installations
  1.helm install prometheus-stack prometheus-community/kube-prometheus-stack --namespace monitoring --set prometheus.service.nodePort=30000 --set grafana.service.nodePort=31000 --set grafana.service.type=NodePort --set prometheus.service.type=NodePort
  2.kubectl get pods -n monitoring
  3.kubectl get svc -n monitoring
    { check_only:- prometheus-stack-grafana / prometheus-stack-kube-prom-prometheus }
  
4.Forward the ports
  1.kubectl port-forward svc/prometheus-stack-kube-prom-prometheus 9090:9090 -n monitoring --address=0.0.0.0 &
    { public_ip:9090 }

  2.kubectl port-forward svc/prometheus-stack-grafana 3000:80 -n monitoring --address=0.0.0.0 &
    { public_ip:3000 }

  3.To get the password
    kubectl get secret prometheus-stack-grafana -n monitoring -o jsonpath="{.data.admin-password}" | base64 --decode
  
  4.public_ip:3000
    username: admin
    password: (paste_here)

5.Deploy project to monitor 
1.git clone https://github.com/mayurpandit25/k8s-kind-voting-app.git
2.cd k8s-kind-voting-app
3.cd k8s-specifications
4.kubectl apply -f .
5.kubectl get svc

Forward the port
1.kubectl port-forward svc/vote 5000:5000 --address=0.0.0.0 &
2.kubectl port-forward svc/result 5001:5001 --address=0.0.0.0 &

Grafana Dashboard
  1.click on dashboard --> select --> Kubernetes networking workload
  2.namespace --> default
  3.workload ---> vote

6.u can add the custom dashboard as well
  

