# Istio_Dataflow_Overview
This is to walk through the key parts of inter-pod commnunication with a Istio service mesh. <br>
Suppose the frontend pod issued a request http://webservice to a virtual service set up between two pods webapp-deplpoyment-4.0 and webapp-deplpoyment-4.1. <br>
<pre>
controlplane $ kubectl get pods -o wide
NAME                                     READY   STATUS    RESTARTS   AGE   IP            NODE     NOMINATED NODE   READINESS GATES
frontend-deployment-76bfb868d-drkc9      2/2     Running   0          89s   192.168.1.6   node01   <none>           <none>
webapp-deployment-4.0-8f9c8b795-x975v    2/2     Running   0          89s   192.168.1.8   node01   <none>           <none>
webapp-deployment-4.1-56dd87c469-294h9   2/2     Running   0          89s   192.168.1.7   node01   <none>           <none>
controlplane $ kubectl get svc -o wide
NAME              TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE   SELECTOR
frontendservice   ClusterIP   10.105.154.212   <none>        80/TCP    37s   app=frontend
kubernetes        ClusterIP   10.96.0.1        <none>        443/TCP   25h   <none>
webservice        ClusterIP   10.108.40.239    <none>        80/TCP    36s   app=webapp
controlplane $ kubectl get virtualservice
NAME                   GATEWAYS   HOSTS            AGE
webservice-wtdist-vs              ["webservice"]   38m
</pre>
