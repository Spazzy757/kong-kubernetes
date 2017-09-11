# kong-kubernetes
This is configuration for kong on minikube with konga ui

## Install Minikube
https://kubernetes.io/docs/tasks/tools/install-minikube/

## Deploy Kong
>To deploy kong on a minikube instance use the following commadn within the minikube directory

```bash
kubectl create -f cassandra.yml
kubectl create -f kong.migration.yml
```

> Once the migration has run, start kong

```bash
kubectl create -f kong.yml
```

## Deploy Konga
>To deploy konga on a minkube instance run the mongodb configuration

```bash
kubectl create -f mongo.yml
```
>Then once up run the konga configuration (when in development mode it will run migration,
so run NODE_ENV = development once, then once able to log in (see username and password below)
change NODE_ENV = production and restart konga

```bash
kubectl create -f konga.yml
```
```text
konga-username: admin
konga-password: adminadminadmin
```

## Find Konga URL

>To find the URL for konga

```bash
kubectl describe service konga
```
>This will give the following output

```text
Name:			konga
Namespace:		default
Labels:			name=konga
Annotations:		<none>
Selector:		name=konga
Type:			NodePort
IP:			10.0.0.145
Port:			<unset>	1337/TCP
NodePort:		<unset>	31927/TCP <--- use this PORT
Endpoints:		172.17.0.9:1337
Session Affinity:	None
Events:			<none>

```
> Your konga instance will be running on

```
http://<minikube ip>:<konga PORT>
```

## Road Map
* fix bugs with setup
* create setup for production kubernetes
