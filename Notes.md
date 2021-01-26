## Local Persistent Volumes

https://kubernetes.io/blog/2019/04/04/kubernetes-1.14-local-persistent-volumes-ga/

## Kuberentes opertor

https://operatorhub.io/

## Resources

https://upcloud.com/community/tutorials/install-kubernetes-cluster-centos-8/?utm_term=&utm_campaign=DSA&utm_source=adwords&utm_medium=ppc&hsa_acc=9391663435&hsa_cam=7185608860&hsa_grp=81739862313&hsa_ad=391197952986&hsa_src=g&hsa_tgt=dsa-460992423274&hsa_kw=&hsa_mt=b&hsa_net=adwords&hsa_ver=3&gclid=Cj0KCQiAk53-BRD0ARIsAJuNhpuwmK1horxTQt_5Q0o87vcu0pDaXhHHj6gbMkK10a6kjwHXhIJiqUcaAl7iEALw_wcB


## Minio run

podman run -d --name minio --env-file=/etc/minio.cfg -p 9000:9000 -v /minio:/data minio server /data


/etc/systemd/system/minio-container.service:

[Unit]
Description=Minio container
After=network-online.target
Wants=network-online.target

[Service]
Restart=always
ExecStart=/usr/bin/podman start -a minio
ExecStop=/usr/bin/podman stop -t 2 minio

[Install]
WantedBy=multi-user.target


Minio config with mc:

https://docs.min.io/docs/minio-client-quickstart-guide.html
https://docs.min.io/docs/minio-multi-user-quickstart-guide.html
cat > fullaccess.json << EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": ["s3:ListBucket"],
      "Effect": "Allow",
      "Resource": ["arn:aws:s3:::vkub"]
    },
    {
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Effect": "Allow",
      "Resource": ["arn:aws:s3:::vkub/*"]
    }
  ]
}
EOF

mc admin policy add <host> vkub_fullaccess fullaccess.json
mc admin user add <host> <user> <pass>


Gitlab options:

global.hosts.domain

gitlab.kub.voucher.gov.gr
registry.kub.voucher.gov.gr
minio.kub.voucher.gov.gr
pages.kub.voucher.gov.gr

global.hosts.externalIP

postgresql.install

global.smtp
global.email
global.smtp.authentication
global.smtp.password.secret

global.operator.enabled

certmanager.install
global.ingress.configureCertmanager = false
#global.ingress.annotations."kubernetes\.io/tls-acme"
global.ingress.tls.enabled
gitlab.webservice.ingress.tls.secretName
registry.ingress.tls.secretName
minio.ingress.tls.secretName
global.pagesenabled
global.gitlab-pages.ingress.tls.secretName

gitlab runner priviledged

global.kas.enabled

global.ingress.annotations."nginx.ingress.kuberentes.io/ssl-redirect": false

nginx-ingress.enabled: false

certmanager.install = false