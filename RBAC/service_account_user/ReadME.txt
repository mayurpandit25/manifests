TESTING COMMANDS:-

1.kubectl apply -f .
1.kubectl auth can-i get pods --as=system:serviceaccount:apache:apache-user -n apache
2.kubectl auth can-i get deployments --as=system:serviceaccount:apache:apache-user -n apache

{ its working because u add all the resources in the role }

-----------------------------------------------------------------------------------------------

UPDATE ROLE (LIMIT PERMISSIONS)-ONLY get pods

1.vim role.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: apache-manager
  namespace: apache
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get"]

2.kubectl apply -f role.yaml

3.kubectl auth can-i get pods --as=system:serviceaccount:apache:apache-user -n apache
  yes

4.kubectl auth can-i get deployments --as=system:serviceaccount:apache:apache-user -n apache
  no

5.kubectl auth can-i delete pods --as=system:serviceaccount:apache:apache-user -n apache
  no

{ NOTE:- because these role has only the permission to get the pods }

-----------------------------------------------------------------------------------------------

UPDATE ROLE AGAIN (READ-ONLY MULTIPLE RESOURCES) - GET only

1.vim role.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: apache-manager
  namespace: apache
rules:
- apiGroups: [""]
  resources: ["pods", "services"]
  verbs: ["get"]
- apiGroups: ["apps"]
  resources: ["deployments"]
  verbs: ["get"]

2.kubectl apply -f role.yaml

3.kubectl auth can-i get pods --as=system:serviceaccount:apache:apache-user -n apache
  yes

4.kubectl auth can-i delete pods --as=system:serviceaccount:apache:apache-user -n apache
  no

---------------------------------------------------------------------------------------------------

IF I WANT TO SEE THE PODS / DEPLOYMENTS / SERVICE USING THE USER

1.kubectl get pods -n apache --as=system:serviceaccount:apache:apache-user

2.kubectl get deployments -n apache --as=system:serviceaccount:apache:apache-user

3.kubectl get services -n apache --as=system:serviceaccount:apache:apache-user

4.kubectl delete pod apache-deployment -n apache --as=system:serviceaccount:apache:apache-user

---------------------------------------------------------------------------------------------------
