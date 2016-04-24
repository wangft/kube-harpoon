# docker registry & kubernetes

## registry use kubernetes pv & pvc (nfs)

### Docker Engine 1.9 or Docker Engine 1.11

* pv use openstack cinder volume from ceph RBD

pv.yaml

   

    apiVersion: v1
	    kind: PersistentVolume
      metadata:
        name: registry-nfs
        namespace: kube-system
      spec:
        capacity:
          storage: 900Gi
        accessModes:
          - ReadWriteMany
        nfs:
          # FIXME: use the right IP
          server: 192.168.1.34
          path: "/mnt/data" 

  
pvc.yaml

	kind: PersistentVolumeClaim
	apiVersion: v1
	metadata:
	  name: registry-nfs
	  namespace: kube-system
	spec:
	  accessModes:
	    - ReadWriteMany
	  resources:
	    requests:
	      storage: 800Gi

registry.yaml

	apiVersion: v1
	kind: ReplicationController
	metadata:
	  name: kube-registry-v0
	  namespace: kube-system
	  labels:
	    k8s-app: kube-registry
	    version: v0
	    kubernetes.io/cluster-service: "true"
	spec:
	  replicas: 1
	  selector:
	    k8s-app: kube-registry
	    version: v0
	  template:
	    metadata:
	      labels:
	        k8s-app: kube-registry
	        version: v0
	        kubernetes.io/cluster-service: "true"
	    spec:
	      containers:
	      - name: registry
	        image: registry:2
	        resources:
	          limits:
	            cpu: 100m
	            memory: 100Mi
	        env:
	        - name: REGISTRY_HTTP_ADDR
	          value: :5000
	        - name: REGISTRY_STORAGE_FILESYSTEM_ROOTDIRECTORY
	          value: /var/lib/registry
	        - name: REGISTRY_AUTH
	          value: token
	        - name: REGISTRY_AUTH_TOKEN_REALM
	          value: https://domain.com:5001/auth
	        - name: REGISTRY_AUTH_TOKEN_SERVICE
	          value: docker-registry
	        - name: REGISTRY_AUTH_TOKEN_ISSUER
	          value: AuthService
	        - name: REGISTRY_AUTH_TOKEN_ROOTCERTBUNDLE
	          value: /ssl/qy-auth-server.crt
	        - name: REGISTRY_HTTP_SECRET
	          value: admin
	        - name: REGISTRY_HTTP_TLS_CERTIFICATE
	          value: /ssl/qy-auth-server.crt
	        - name: REGISTRY_HTTP_TLS_KEY
	          value: /ssl/qy.key
	        volumeMounts:
	        - name: image-store
	          mountPath: /var/lib/registry
	        - name: ssl
	          mountPath: /ssl
	        ports:
	        - containerPort: 5000
	          name: registry
	          protocol: TCP
	      volumes:
	      - name: image-store
	        persistentVolumeClaim:
	          claimName: registry-nfs
	      - name: ssl
	        hostPath:
	          path: /etc/kubernetes/ssl

service.yaml

	apiVersion: v1
	kind: Service
	metadata:
	  name: kube-registry
	  namespace: kube-system
	  labels:
	    k8s-app: kube-registry
	    kubernetes.io/cluster-service: "true"
	    kubernetes.io/name: "KubeRegistry"
	spec:
	  type: NodePort
	  selector:
	    k8s-app: kube-registry
	  ports:
	  - name: registry
	    port: 5000
	    protocol: TCP

 
## registry use openstack swift storage

### Docker Engine 1.9 or Docker Engine 1.11

* registry config yaml file

config.yml

	version: 0.1
	log:
	  level: debug
	  formatter: text
	  fields:
	    service: registry
	  hooks:
	    - type: mail
	      disabled: true
	      levels:
	        - panic
	      options:
	        smtp:
	          addr: mail.example.com:25
	          username: mailuser
	          password: password
	          insecure: true
	        from: sender@example.com
	        to:
	          - errors@example.com
	storage:
	  swift:
	    username: admin
	    password: qy_dcos
	    authurl: http://10.0.0.40:5000/v2.0
	    tenant: admin
	    insecureskipverify: true
	    container: docker-registry
	    rootdirectory: /swift/object/name/prefix
	  delete:
	    enabled: true
	  redirect:
	    disable: false
	  cache:
	    blobdescriptor: redis
	auth:
	  token:
	    realm: your auth url 
	    service: docker-registry
	    issuer: AuthService
	    rootcertbundle: /ssl/qy-auth-server.crt
	http:
	  addr: :5000
	  secret: admin
	  host: your host
	  tls:
	    certificate: /ssl/qy-auth-server.crt
	    key: /ssl/qy.key
	redis:
	  addr: localhost:6379
	  pool:
	      maxidle: 16
	      maxactive: 64
	      idletimeout: 300s
	health:
	  storagedriver:
	    enabled: true
	    interval: 10s
	    threshold: 3

