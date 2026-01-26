DEPLOYMENT OF STUDENTAPP WITH HELM

1.helm package studentapp-helm
2.helm install studentapp studentapp-helm -n student --create-namespace 

3.kubectl get pods -n student
4.kubectl get svc -n student

5.kubectl port-forward svc/studentapp 8080:8080 --address=0.0.0.0 -n student &

UPGRADE:-
helm upgrade studentapp studentapp-helm -n student --set studentapp.replicas=3

ROLLBACK:-
helm history studentapp -n student 
helm rollback studentapp 1 -n student 

Note:-
when package studentapp we get { studentapp-0.1.0.tgz } we can push these into the helm repo.
when deployed with helm only change the values.yaml and add manifests in the template folder
