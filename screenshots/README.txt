- Kubernetes kubectl get pods output
NAME                            READY   STATUS    RESTARTS   AGE
backend-feed-569978f4f8-5qnnc   1/1     Running   0          29m
backend-feed-569978f4f8-9767k   1/1     Running   0          29m
backend-user-64965dfd66-7ppqq   1/1     Running   0          2m12s
backend-user-64965dfd66-pkp2k   1/1     Running   0          29m
backend-user-64965dfd66-z2pn8   1/1     Running   0          29m
frontend-86dd7547bd-9vztd       1/1     Running   0          15m
frontend-86dd7547bd-vp4lc       1/1     Running   0          15m
reverseproxy-7cc58b654c-54wj2   1/1     Running   0          28m
reverseproxy-7cc58b654c-dxv72   1/1     Running   0          28m

- Kubernetes kubectl describe services output
Name:              backend-feed
Namespace:         default
Labels:            run=backend-feed
Annotations:       <none>
Selector:          run=backend-feed
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.100.87.149
IPs:               10.100.87.149
Port:              <unset>  8080/TCP
TargetPort:        8080/TCP
Endpoints:         172.31.25.220:8080,172.31.37.79:8080
Session Affinity:  None
Events:            <none>


Name:              backend-user
Namespace:         default
Labels:            run=backend-user
Annotations:       <none>
Selector:          run=backend-user
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.100.143.31
IPs:               10.100.143.31
Port:              <unset>  8080/TCP
TargetPort:        8080/TCP
Endpoints:         172.31.29.108:8080,172.31.33.158:8080,172.31.44.31:8080
Session Affinity:  None
Events:            <none>


Name:              frontend
Namespace:         default
Labels:            service=frontend
Annotations:       <none>
Selector:          service=frontend
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.100.171.34
IPs:               10.100.171.34
Port:              8100  8100/TCP
TargetPort:        80/TCP
Endpoints:         172.31.20.139:80,172.31.43.70:80
Session Affinity:  None
Events:            <none>


Name:              kubernetes
Namespace:         default
Labels:            component=apiserver
                   provider=kubernetes
Annotations:       <none>
Selector:          <none>
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.100.0.1
IPs:               10.100.0.1
Port:              https  443/TCP
TargetPort:        443/TCP
Endpoints:         172.31.24.63:443,172.31.36.54:443
Session Affinity:  None
Events:            <none>


Name:                     publicfrontend
Namespace:                default
Labels:                   service=frontend
Annotations:              <none>
Selector:                 service=frontend
Type:                     LoadBalancer
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.100.131.5
IPs:                      10.100.131.5
LoadBalancer Ingress:     a79358ef2e4f249888a09f54e568dae0-798666285.us-east-2.elb.amazonaws.com
Port:                     <unset>  80/TCP
TargetPort:               80/TCP
NodePort:                 <unset>  30438/TCP
Endpoints:                172.31.20.139:80,172.31.43.70:80
Session Affinity:         None
External Traffic Policy:  Cluster
Events:
  Type    Reason                Age   From                Message
  ----    ------                ----  ----                -------
  Normal  EnsuringLoadBalancer  12m   service-controller  Ensuring load balancer
  Normal  EnsuredLoadBalancer   12m   service-controller  Ensured load balancer


Name:                     publicreverseproxy
Namespace:                default
Labels:                   <none>
Annotations:              <none>
Selector:                 run=reverseproxy
Type:                     LoadBalancer
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.100.142.211
IPs:                      10.100.142.211
LoadBalancer Ingress:     aa511c62d34f94261bc602b5a685e7e1-698510115.us-east-2.elb.amazonaws.com
Port:                     <unset>  8080/TCP
TargetPort:               8080/TCP
NodePort:                 <unset>  30650/TCP
Endpoints:                172.31.17.218:8080,172.31.40.234:8080
Session Affinity:         None
External Traffic Policy:  Cluster
Events:
  Type    Reason                Age   From                Message
  ----    ------                ----  ----                -------
  Normal  EnsuringLoadBalancer  27m   service-controller  Ensuring load balancer
  Normal  EnsuredLoadBalancer   27m   service-controller  Ensured load balancer


Name:              reverseproxy
Namespace:         default
Labels:            service=reverseproxy
Annotations:       <none>
Selector:          service=reverseproxy
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.100.233.52
IPs:               10.100.233.52
Port:              8080  8080/TCP
TargetPort:        8080/TCP
Endpoints:         <none>
Session Affinity:  None
Events:            <none>


- Kubernetes kubectl describe hpa output
Name:                                                  backend-user
Namespace:                                             default
Labels:                                                <none>
Annotations:                                           <none>
CreationTimestamp:                                     Mon, 23 May 2022 22:01:11 +0700
Reference:                                             Deployment/backend-user
Metrics:                                               ( current / target )
  resource cpu on pods  (as a percentage of request):  <unknown> / 70%
Min replicas:                                          3
Max replicas:                                          5
Deployment pods:                                       3 current / 3 desired
Conditions:
  Type           Status  Reason                   Message
  ----           ------  ------                   -------
  AbleToScale    True    SucceededGetScale        the HPA controller was able to get the target's current scale
  ScalingActive  False   FailedGetResourceMetric  the HPA was unable to compute the replica count: failed to get cpu utilization: unable to get metrics for resource cpu: unable to fetch metrics from resource metrics API: the server could not find the requested resource (get pods.metrics.k8s.io)
Events:
  Type     Reason                        Age                   From                       Message
  ----     ------                        ----                  ----                       -------
  Normal   SuccessfulRescale             3m41s                 horizontal-pod-autoscaler  New size: 3; reason: Current number of replicas below Spec.MinReplicas
  Warning  FailedGetResourceMetric       41s (x12 over 3m26s)  horizontal-pod-autoscaler  failed to get cpu utilization: unable to get metrics for resource cpu: unable to fetch metrics from resource metrics API: the server could not find the requested resource (get pods.metrics.k8s.io)
  Warning  FailedComputeMetricsReplicas  41s (x12 over 3m26s)  horizontal-pod-autoscaler  invalid metrics (1 invalid out of 1), first error is: failed to get cpu utilization: unable to get metrics for resource cpu: unable to fetch metrics from resource metrics API: the server could not find the requested resource (get pods.metrics.k8s.io)

Kubernetes kubectl logs <your pod name> output
kubectl logs backend-user-64965dfd66-7ppqq

> udagram-api@2.0.0 prod /usr/src/app
> tsc && node ./www/server.js

Initialize database connection...
Executing (default): CREATE TABLE IF NOT EXISTS "User" ("email" VARCHAR(255) , "passwordHash" VARCHAR(255), "createdAt" TIMESTAMP WITH TIME ZONE, "updatedAt" TIMESTAMP WITH TIME ZONE, PRIMARY KEY ("email"));
Executing (default): SELECT i.relname AS name, ix.indisprimary AS primary, ix.indisunique AS unique, ix.indkey AS indkey, array_agg(a.attnum) as column_indexes, array_agg(a.attname) AS column_names, pg_get_indexdef(ix.indexrelid) AS definition FROM pg_class t, pg_class i, pg_index ix, pg_attribute a WHERE t.oid = ix.indrelid AND i.oid = ix.indexrelid AND a.attrelid = t.oid AND t.relkind = 'r' and t.relname = 'User' GROUP BY i.relname, ix.indexrelid, ix.indisprimary, ix.indisunique, ix.indkey ORDER BY i.relname;
process.env.AWS_PROFILE udacity udagran-dev us-east-2
server running http://localhost:8100
press CTRL+C to stop server