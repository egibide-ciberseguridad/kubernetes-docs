# Utilizar el controlador Ingress de HAProxy

## Comprobar la funcionalidad

1. Acceder al controlador:

    ```
    make ssh
    ```

2. Comprobar que tengamos comunicación con el Ingress:

    ```
    calicoctl node status
    ```

    ```
    Calico process is running.
    
    IPv4 BGP status
    +----------------+-------------------+-------+----------+-------------+
    |  PEER ADDRESS  |     PEER TYPE     | STATE |  SINCE   |    INFO     |
    +----------------+-------------------+-------+----------+-------------+
    | 172.20.227.245 | global            | up    | 15:02:12 | Established |
    | 172.20.227.244 | node-to-node mesh | up    | 14:54:22 | Established |
    | 172.20.227.243 | node-to-node mesh | up    | 14:54:24 | Established |
    +----------------+-------------------+-------+----------+-------------+
    
    IPv6 BGP status
    No IPv6 peers found.
    ```

3. Acceder al balanceador:

    ```
    make ssh-ha
    ```

4. Comprobar que tengamos comunicación con el cluster:

    ```
    birdc show protocols
    ```

    ```
    BIRD 1.6.8 ready.
    name     proto    table    state  since       info
    bgp1     BGP      master   up     15:02:12    Established
    bgp2     BGP      master   up     15:02:12    Established
    bgp3     BGP      master   up     15:02:12    Established
    kernel1  Kernel   master   up     15:02:10
    device1  Device   master   up     15:02:10
    ```

## Despliegue

1. Acceder al controlador:

    ```
    make ssh
    ```

2. Desplegar los servicios y el ingress en el cluster:

    ```
    kubectl apply -f https://raw.githubusercontent.com/egibide-ciberseguridad/kubernetes/main/03_exponer_pods/ingress.yml
    ```

3. Acceder a la IP del HAProxy y comprobar si responde.

## Panel de estadísticas de HAProxy

Está disponible en el puerto 1024 del servidor.

Si no se tiene acceso directo, se puede usar un tunel local así:

```
ssh -L 9999:127.0.0.1:1024 -N -f -l root 150.241.173.160
```
