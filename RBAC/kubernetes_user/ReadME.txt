STEP 1: CREATE KUBERNETES USER (CERTIFICATE)
1.Generate private key
  openssl genrsa -out mayur.key 2048
2.Generate CSR (Certificate Signing Request)
  openssl req -new -key mayur.key -out mayur.csr -subj "/CN=mayur"

STEP 2: SIGN CERTIFICATE USING MINIKUBE CA
sudo openssl x509 -req -in mayur.csr -CA ~/.minikube/ca.crt -CAkey ~/.minikube/ca.key -CAcreateserial -out mayur.crt -days 365

STEP 3: ADD USER TO KUBECONFIG
kubectl config set-credentials mayur --client-certificate=mayur.crt --client-key=mayur.key

STEP 4: CREATE CONTEXT FOR mayur USER
kubectl config set-context mayur-context --cluster=minikube --user=mayur --namespace=apache

STEP 5: SWITCH TO mayur USER
kubectl config use-context mayur-context
kubectl auth whoami

STEP 6: TRY ACCESS (BEFORE RBAC)
kubectl get pods
error:- Error from server (Forbidden) ----> it means that RBAC properly working

STEP 7: CREATE ROLE (ADMIN CONTEXT)
1.kubectl config use-context minikube
2.kubectl apply -f role.yaml

STEP 8: CREATE ROLEBINDING FOR USER mayur
1.kubectl apply -f role-binding.yaml

STEP 9: TEST AS mayur USER
kubectl config use-context mayur-context

1.kubectl get pods
2.kubectl get services
3.kubectl get deployments

===================================================================================================================================================
