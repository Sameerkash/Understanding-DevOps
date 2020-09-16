# Understanding Kubernetes ☸

**This is a documentation of my learning process of Kubernentes Architecture, Contanirization, Orchestration and probably the entire DevOps process**

**Check List**

- [x] Kubernetes Setup using Docker Desktop
- [x] Setup WaveScope and Kubernetes DashBoard
- [ ] Deploying stacks to Kuberentes
- [ ] Managing and monitoring Pods
- [ ] Chaos Testing

### Setup

The setup process might be a bit tedious, especially if you google something and refer the official [documentation](https://kubernetes.io/blog/2020/05/21/wsl-docker-kubernetes-on-the-windows-desktop/). There is very little instruction on how to install Kubernetes out there. The documentation in specific goes about installing using [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10) and MiniKube, but the problem is, it is a bit complicated for a beginner and can easily get stuck, as did I.

Until my friend pointed out that Docker Desktop comes with Kubernetes pre-installed and all we have to do it enable it.
So that took me a few minutes compared to spending an entire day following the official documentation. So yeah,

- Go to settings, Kubernetes, and click on enable Kubernetes and you are done1, pretty much.
- Well, Almost, We'll also have to install the Kubernetes Dashboard for managing our Nodes and Pods and also an optional tool called WaveScope for managing our pods.

**Kubernetes Dashboard**

- The Dashboard UI needs to be installed using a config file.

apply the config file

```bash
kubectl apply -f kubedashboard.yaml
```

- generate an admin-account and get the token

```bash
$ kubectl create serviceaccount krishiadmin -n default
$ kubectl create clusterrolebinding krishi-admin -n default --clusterrole=cluster-admin --serviceaccount=default:krishiadmin
$ kubectl get secret $(kubectl get serviceaccount krishiadmin -o jsonpath="{.secrets[0].name}") -o jsonpath="{.data.token}" | base64 --decode
```
* If you are on Windows Powershell, You might want to use this to obtain the base64 decoded JWT
```
PS > iconv -f ASCII -t UTF-16LE filename.txt |base64 -w 0  
``` 
* where, filename.txt contains the base64 encoded JWT



- run the proxy

```bash
kubectl proxy
```

* navigate to 
```
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
```

and enter the token 

- to stop the dashboard

```bash
$ kubectl delete -f kubedashboard.yaml
```

**WaveScope**

```bash
kubectl apply -f scope.yaml
```

expose port 4040 to localhost

```bash
kubectl port-forward -n weave "$(kubectl get -n weave pod --selector=weave-scope-component=app -o jsonpath='{.items..metadata.name}')" 4040
```

open `http://localhost:4040/`

Special Thanks to [Satyajit](https://github.com/satyajitghana) for helping me get started.
