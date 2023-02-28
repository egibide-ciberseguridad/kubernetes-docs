# Comprobar si el cluster de almacenamiento funciona correctamente

1. Acceder al controlador:

    ```
    make ssh
    ```

2. Entrar al toolbox de Rook:

    ```
    kubectl -n rook-ceph exec -it deploy/rook-ceph-tools -- bash
    ```

3. Comprobar el estado del cluster de almacenamiento:

    ```
    ceph status
    ```

    ```
      cluster:
        id:     727a967c-f0b2-4431-b966-757bb5dfb954
        health: HEALTH_WARN
                mons a,b,c are low on available space
    
      services:
        mon: 3 daemons, quorum a,b,c (age 94s)
        mgr: a(active, since 42s), standbys: b
        mds: 1/1 daemons up, 1 hot standby
        osd: 3 osds: 3 up (since 34s), 3 in (since 59s)
    
      data:
        volumes: 1/1 healthy
        pools:   4 pools, 4 pgs
        objects: 25 objects, 451 KiB
        usage:   63 MiB used, 24 GiB / 24 GiB avail
        pgs:     4 active+clean
    
      io:
        client:   1.5 KiB/s rd, 1.1 KiB/s wr, 2 op/s rd, 3 op/s wr
    ```
