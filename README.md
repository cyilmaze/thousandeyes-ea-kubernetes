# ThousandEyes Enterprise Agent Kubernetes
## Deploy ThousandEyes Enterprise Agent on Kubernetes Cluster

<ins>Installation</ins>
1. Run the following commands on your host
```
curl -Os https://downloads.thousandeyes.com/bbot/configure_docker.sh
chmod +x configure_docker.sh
sudo ./configure_docker.sh
```
2. Kuberentes requires seccomp profiles files under directory /var/lib/kubelet/seccomp. Crete the seccomp directory.
```
sudo mkdir /var/lib/kubelet/seccomp
```
3. Copy ThousandEyes seccomp files from its original location to new seccomp path.
```
sudo cp /var/docker/configs/te-seccomp.json /var/lib/kubelet/seccomp/
```
4. Clone this repository to your server or management machines
```
git clone https://github.com/cyilmaze/thousandeyes-ea-kubernetes.git
```
5.Update the TEAGENT_ACCOUNT_TOKEN variable in thousandeyes-secret.yaml with your ThousandEyes Account Group Token
```
---
apiVersion: v1
kind: Secret
metadata:
  name: thousandeyes-credentials
  namespace: thousandeyes
  labels:
    app: thousandeyes
type: Opaque
stringData:
  TEAGENT_ACCOUNT_TOKEN: ""
```
6. Apply manifests files to deploy agent
```
kubectl apply -f thousandeyes-ea-kubernetes
```
7. Verify agent is Running
```
kubectl get pods -n thousandeyes
```