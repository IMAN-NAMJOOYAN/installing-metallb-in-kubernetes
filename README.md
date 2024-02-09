# Install MetallLB on Kubernetes By Helm

**Enabling strictARP on kube-proxy config:**

```
kubectl get configmap kube-proxy -n kube-system -o yaml | \
sed -e "s/strictARP: false/strictARP: true/" | \
kubectl apply -f - -n kube-system
```

```
helm install metallb bitnami/metallb
```

![image](https://github.com/IMAN-NAMJOOYAN/installing-metallb-in-kubernetes/assets/16554389/80636e23-3fe3-40fd-9f18-ef9320fae1e0)


---

![image](https://github.com/IMAN-NAMJOOYAN/installing-metallb-in-kubernetes/assets/16554389/ca7fdf1b-42fc-4514-9c33-b6cef0580b2f)

---


**Create a "IPAddressPool":**

```
apiVersion: metallb.io/v1beta1
kind: IPAddressPool
metadata:
  name: default
  namespace: metallb-system
spec:
  addresses:
  - < Your Desired IP Address As LoadBalancer >
```

```
kubectl apply -f ipPoolAddress.yaml
```

**Create a "L2Advertisement:"**

```
apiVersion: metallb.io/v1beta1
kind: L2Advertisement
metadata:
  name: default
  namespace: metallb-system
spec:
  ipAddressPools:
  - default
  interfaces:
  - ens192
```

```
kubectl apply -f l2advertisement.yaml
```

**Check Loadbalancer:**

![image](https://github.com/IMAN-NAMJOOYAN/installing-metallb-in-kubernetes/assets/16554389/e52fd612-7c7b-4bcb-b7b3-6f3e93fedf59)




