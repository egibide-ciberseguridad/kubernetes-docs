# Instalar y configurar el balanceador MetalLB en el cluster

1. Acceder al controlador:

    ```
    make ssh
    ```

2. Configurar el parámetro `strictARP` a `true` en el `kube-proxy`:

    ```
    kubectl get configmap kube-proxy -n kube-system -o yaml | \
    sed -e "s/strictARP: false/strictARP: true/" | \
    kubectl apply -f - -n kube-system
    ```

3. Instalar el balanceador MetalLB:

    ```
    kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/master/config/manifests/metallb-native.yaml
    ```

4. Crear el _pool_ de direcciones disponibles para el balanceador:

    ```yaml
    apiVersion: metallb.io/v1beta1
    kind: IPAddressPool
    metadata:
      name: demo-pool
      namespace: metallb-system
    spec:
      addresses:
        - 172.20.227.220-172.20.227.230
    ---
    apiVersion: metallb.io/v1beta1
    kind: L2Advertisement
    metadata:
      name: demo-pool-advertise
      namespace: metallb-system
    spec:
      ipAddressPools:
        - demo-pool
    ```

5. Crear un servicio de tipo LoadBalancer y exponerlo:

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: nginx-hello-loadbalancer
      annotations:
        metallb.universe.tf/address-pool: demo-pool
        #metallb.universe.tf/loadBalancerIPs: 172.20.227.222
    spec:
      type: LoadBalancer
      selector:
        app: nginx-hello
      ports:
        - targetPort: 80  # endpoint
          port: 80        # loadbalancer
    ```

## Referencias

- [MetalLB - Installation](https://metallb.org/installation/)
- [MetalLB - Configuration](https://metallb.org/configuration/)
- [MetalLB - Usage](https://metallb.org/usage/)
