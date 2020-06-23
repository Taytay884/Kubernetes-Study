<h1 id="kubernetes-study---itay">Kubernetes study - Itay</h1>
<p><em>23.06.2020</em></p>
<p>I’m covering the <a href="http://Kubernetes.io">Kubernetes.io</a> tutorial, I will write useful stuff here.<br>
At the moment I’m on <a href="https://kubernetes.io/docs/tutorials/kubernetes-basics/scale/scale-interactive/"><strong>Module 5 - Scale up your app.</strong></a></p>
<h1 id="kubernetes-cheatsheet">Kubernetes Cheatsheet</h1>
<p>Hi! This is a cheat sheet to make our job easier on Kubernetes.<br>
I will mention the commands that used in <a href="https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/">Kubernetes.io</a> tutorial.</p>
<h1 id="minikube">minikube</h1>
<pre><code>minikube version
minikube start
</code></pre>
<h1 id="kubectl">kubectl</h1>
<pre><code>kubectl version
kubectl cluster-info
kubectl proxy
</code></pre>
<h2 id="nodes">Nodes</h2>
<pre><code>kubectl get nodes
</code></pre>
<h2 id="deployments">Deployments</h2>
<pre><code>kubectl get deployments
kubectl describe deployment // To get the label of a deployment
kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1
kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080 // Creates a service
</code></pre>
<h2 id="pods">Pods</h2>
<pre><code>kubectl get pods
kubectl get pods -l run=kubernetes-bootcamp // Get pods by label.
kubectl describe pods
kubectl describe pods $POD_NAME
kubectl logs $POD_NAME
kubectl label pod $POD_NAME app=v1 // Label a pod.

// kubectl exec
kubectl exec $POD_NAME env
kubectl exec -ti $POD_NAME bash
kubectl exec -ti $POD_NAME curl localhost:8080 // When the service is deleted the pod is still running.

// Save $POD_NAME on a variable.
export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}') echo Name of the Pod: $POD_NAME
</code></pre>
<h2 id="services">Services</h2>
<pre><code>kubectl get services
kubectl get services -l run=kubernetes-bootcamp // Get services by label.
kubectl describe services/kubernetes-bootcamp
kubectl delete service -l run=kubernetes-bootcamp

// Save $NODE_PORT on a variable.
export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}') echo NODE_PORT=$NODE_PORT
</code></pre>
<h1 id="curl">curl</h1>
<pre><code>curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/

// We can send a request from the Pod's bash.
curl localhost:8080

// Sending a request to an exposed service. 
curl $(minikube ip):$NODE_PORT
</code></pre>
<h1 id="terminal">terminal</h1>
<pre><code>exit
</code></pre>

