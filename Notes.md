## Local Persistent Volumes

https://kubernetes.io/blog/2019/04/04/kubernetes-1.14-local-persistent-volumes-ga/

## Kuberentes opertor

https://operatorhub.io/

## Resources

https://upcloud.com/community/tutorials/install-kubernetes-cluster-centos-8/?utm_term=&utm_campaign=DSA&utm_source=adwords&utm_medium=ppc&hsa_acc=9391663435&hsa_cam=7185608860&hsa_grp=81739862313&hsa_ad=391197952986&hsa_src=g&hsa_tgt=dsa-460992423274&hsa_kw=&hsa_mt=b&hsa_net=adwords&hsa_ver=3&gclid=Cj0KCQiAk53-BRD0ARIsAJuNhpuwmK1horxTQt_5Q0o87vcu0pDaXhHHj6gbMkK10a6kjwHXhIJiqUcaAl7iEALw_wcB


## Minio run

podman run -d --name minio -p 9000:9000 -v /minio:/data minio server /data


/etc/systemd/system/minio-container.service:

[Unit]
Description=Minio container

[Service]
Restart=always
ExecStart=/usr/bin/podman start -a minio
ExecStop=/usr/bin/podman stop -t 2 minio

[Install]
WantedBy=local.target
