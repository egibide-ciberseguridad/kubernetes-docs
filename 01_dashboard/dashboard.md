# Instalar el Dashboard UI en el cluster Kubernetes

1. Acceder al controlador:

    ```
    make ssh
    ```

2. Instalar el Dashboard:

    ```
    kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
    ```

3. Configurar el puerto de acceso:

    ```
    kubectl apply -f https://raw.githubusercontent.com/egibide-ciberseguridad/kubernetes/main/01_dashboard/nodeport.yml
    ```

4. Crear el usuario admin y obtener el token de acceso:

    ```
    kubectl apply -f https://raw.githubusercontent.com/egibide-ciberseguridad/kubernetes/main/01_dashboard/service-account.yml
    kubectl apply -f https://raw.githubusercontent.com/egibide-ciberseguridad/kubernetes/main/01_dashboard/role-binding.yml
    ```

    ```
    kubectl -n kubernetes-dashboard create token admin-user
    ```

   Ejemplo de token:

    ```
    eyJhbGciOiJSUzI1NiIsImtpZCI6IlJsaTBuc0ktZm5QQ2NPSDdsSXgxZDBFclUzbHVMaTM0Z05JcE90QW9nLWsifQ.eyJhdWQiOlsiaHR0cHM6Ly9rdWJlcm5ldGVzLmRlZmF1bHQuc3ZjLmNsdXN0ZXIubG9jYWwiXSwiZXhwIjoxNjc1MTYwNjkwLCJpYXQiOjE2NzUxNTcwOTAsImlzcyI6Imh0dHBzOi8va3ViZXJuZXRlcy5kZWZhdWx0LnN2Yy5jbHVzdGVyLmxvY2FsIiwia3ViZXJuZXRlcy5pbyI6eyJuYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsInNlcnZpY2VhY2NvdW50Ijp7Im5hbWUiOiJhZG1pbi11c2VyIiwidWlkIjoiNTU4ZGIwMWMtM2E4My00NTU4LWEwMzUtYTliNzIyODkzMDk4In19LCJuYmYiOjE2NzUxNTcwOTAsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDprdWJlcm5ldGVzLWRhc2hib2FyZDphZG1pbi11c2VyIn0.EktZUbngZrs6HrG9nP5MQlhUp_ubRbV8QlhGaaN5JRFIBwDtNnYLfzZh7ubkcFFIrHFs4V3_rSzUCanrl4y8gRvyyNlCH6ii0wj1vy21OXYyVR87zqlix7tY5o74agG4wo5Pi4t3ovWbVriIGEnKRVBUeX9IMyc-cNFPKkthkV2sRKf8pffmMJ4EpWtIZSHGqGH8tRh4oSvNENAdelp-SqXhb3tQ2yv5owemHNGVSqciu9UuWXWKJ8f8kjBDzQTaZywgyxaMeXMoVOYh0f7Z4a-kVyOmPIg4NLtc6snjylnYfsPS_pYcR8emsntQ0AYgG19llhRBWo33GdKYXnxaxw
    ```

5. Acceder al Dashboard con la IP de cualquiera de los nodos del cluster:

   https://172.20.227.15:32000

## Referencias

- https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
- https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md
- https://stackoverflow.com/questions/59020970/kubernetes-remote-access-dashboard
- https://bobcares.com/blog/install-kubernetes-dashboard-with-nodeport/
