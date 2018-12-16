# obsidian - K8s Deployment

This is a k8s deployment that'll deploy eletrumx and allow it to commuincate with the k8s daemon deployment.

### Prerequisites

You need to make sure that you have kubectl access to your kubernetes cluster.

Follow the kubernetes docs on whatever system you're on to get local access.

```
kubectl get nodes - Should return the nodes in the cluster.
```
You'll also need a running obsidian daemon with rpc access configured. Make sure you know what your connection details are for your daemon. 

Example: http://user:password@host:port

### Installing

You'll need to change this in your electrumx.json to suite your network setup.
```
"env": [
                {
                   "name": "DAEMON_URL",
                   "value": "http://user:password@10.39.246.35:1988"
                }

```
We'll want to create the volume. In order to do so run this:

```
kubectl create -f "path\to\electrumx_pv.json"
```

Once that is completed then go ahead and create the electrumx deployment and in order to do so then run this:
```
kubectl create -f "path\to\odnelectrumx_pv.json"
```

Next, you'll need to create your service in order for this to be accessed from the outside. Run this:
```
kubectl expose deployment obsidian-electrumx --type=LoadBalancer --name=obsidianelectrumx --port=50443
```
Get your external IP and use that as your connection in your client.

## Viewing screen data

Get your pod name:
```
kubectl get pods 
```
It should show something like this.
```
obsidian-electrumx-78f87cb869-mdqlz
```
Then you want to view the logs of this pod.
```
kubectl logs obsidian-electrumx-78f87cb869-mdqlz
```
You can filter the output data as you wish.

