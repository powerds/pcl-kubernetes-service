# P.CL Kubernetes Sample Applications
## Echo App
```
# Deploy a sample echo application.

# Download Sample Apps.
git clone https://github.com/powerds/pcl-kubernetes-service.git
cd pcl-kubernetes-service/sample-apps

# Deploy a deployment.
kubectl apply -f echo-1-deployment.yaml

# Check the deployment is ready.
watch "kubectl get deployment echo"

# Deploy a service.
kubectl apply -f echo-2-service.yaml

# Check the service is ready.
kubectl get service echo-service

# Deploy an ingress.
kubectl apply -f echo-3-ingress.yaml

# Check the ingress is ready.
kubectl get ingress echo-ingress

# Add ingress domain name to your local hosts file for access to the echo app.
echo "$EXTERNAL_IP echo.pcl.com" | sudo tee -a /etc/hosts

# Access to the echo app.
curl http://echo.pcl.com
```
## Nginx with PVC
```
# Deploy a sample nginx appication with 1G persistent volume.

# Download Sample Apps.
git clone https://github.com/powerds/pcl-kubernetes-service.git
cd pcl-kubernetes-service/sample-apps

# Deploy a persistent volume.
kubectl apply -f nginx-1-pvc.yaml

# Check the persistent volume is ready.
kubectl get pvc

# Deploy a pod.
kubectl apply -f nginx-2-pod.yaml

# Check the deployment is ready.
watch "kubectl get pod nginx"

# Deploy a service.
kubectl apply -f nginx-3-service.yaml

# Check the service is ready.
kubectl get service nginx-service

# Deploy an ingress.
kubectl apply -f nginx-4-ingress.yaml

# Check the ingress is ready.
kubectl get ingress nginx-ingress

# Add ingress domain name to your local hosts file for access to the nginx app
echo "$EXTERNAL_IP nginx.pcl.com" | sudo tee -a /etc/hosts

# Access to the nginx app
curl http://nginx.pcl.com
```
