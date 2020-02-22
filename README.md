# Setup a basic memcached & memcached service

```
{12:08}~/k8s-memcached/env/dev ➭ kubectl apply -k ./
service/memcached created
deployment.apps/memcached created
```

Check :
```
{12:09}~ ➭ kubectl get pods,rc,svc,deployments,cm,pv,pvc -o wide
NAME                             READY   STATUS      RESTARTS   AGE     IP           NODE       NOMINATED NODE   READINESS GATES
pod/memcached-79bd87856c-gnds9   1/1     Running     0          60s     172.17.0.4   minikube   <none>           <none>

NAME                 TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)     AGE   SELECTOR
service/kubernetes   ClusterIP   10.96.0.1      <none>        443/TCP     15m   <none>
service/memcached    ClusterIP   10.97.225.87   <none>        11211/TCP   60s   app=memcached,tier=memcached

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES                              SELECTOR
deployment.apps/memcached   1/1     1            1           60s   memcached    launcher.gcr.io/google/memcached1   app=memcached,tier=memcached
```

Connect to memcached an test :
```
{12:08}~/k8s-memcached/env/dev ➭ kubectl run -i --tty busybox-`date +%N` --image=busybox --restart=Never -- sh
If you don't see a command prompt, try pressing enter.
/ # telnet memcached 11211
Connected to memcached
set test 0 60 9
memcached
STORED
get test
VALUE test 0 9
memcached
END
```
