# About

https://docs.openshift.org/latest/dev_guide/integrating_external_services.html

Lab

    fanhonglingdeMacBook-Pro:external-service-auto-discovery fanhongling$ kubectl --namespace=helm create -f hadoop2-configmap.yaml 
    fanhonglingdeMacBook-Pro:external-service-auto-discovery fanhongling$ export KUBECONFIG=/Users/fanhongling/Downloads/github.com/openshift/origin/kubeconfig

    fanhonglingdeMacBook-Pro:external-service-auto-discovery fanhongling$ kubectl --namespace=helm create -f hadoop2-configmap.yaml 
    configmap "hadoop2-config" created
    fanhonglingdeMacBook-Pro:external-service-auto-discovery fanhongling$ kubectl --namespace=helm get configmap
    NAME             DATA      AGE
    hadoop2-config   6         9s
    fanhonglingdeMacBook-Pro:external-service-auto-discovery fanhongling$ kubectl --namespace=helm get configmap -o yaml
    apiVersion: v1
    items:
    - apiVersion: v1
      data:
        core-site.xml: |-
          <configuration>
              <property>
                  <name>fs.defaultFS</name>
                  <value>hdfs://10.64.200.47/</value>
                  <description>NameNode URI</description>
              </property>
          </configuration>
        hdfs-site.xml: |-
          <configuration>
              <property>
                  <name>dfs.namenode.name.dir</name>
                  <value>file:///usr/local/hadoop/data/namenode</value>
                  <description>NameNode directory for namespace and transaction logs storage.</description>
              </property>
              <property>
                  <name>dfs.replication</name>
                  <value>3</value>
              </property>
              <property>
                  <name>dfs.permissions</name>
                  <value>false</value>
              </property>
              <property>
                  <name>dfs.datanode.use.datanode.hostname</name>
                  <value>false</value>
              </property>
              <property>
                  <name>dfs.namenode.datanode.registration.ip-hostname-check</name>
                  <value>false</value>
              </property>
              <property>
                   <name>dfs.namenode.http-address</name>
                   <value>10.64.200.47:50070</value>
                   <description>Your NameNode hostname for http access.</description>
              </property>
              <property>
                   <name>dfs.namenode.secondary.http-address</name>
                   <value>10.64.200.47:50090</value>
                   <description>Your Secondary NameNode hostname for http access.</description>
              </property>
          </configuration>
        mapred-site.xml: |-
          <configuration>
              <property>
                  <name>mapreduce.framework.name</name>
                  <value>yarn</value>
              </property>
          </configuration>
        masters: 10.64.200.47
        salves: |-
          10.64.200.48
          10.64.200.49
          10.64.200.50
          10.64.200.51
        yarn-site.xml: |
          <configuration>
              <property>
                  <name>yarn.nodemanager.aux-services</name>
                  <value>mapreduce_shuffle</value>
              </property>
              <property>
                  <name>yarn.nodemanager.aux-services.mapreduce_shuffle.class</name>
                  <value>org.apache.hadoop.mapred.ShuffleHandler</value>
              </property>
              <property>
                  <name>yarn.resourcemanager.resource-tracker.address</name>
                  <value>10.64.200.47:8025</value>
              </property>
              <property>
                  <name>yarn.resourcemanager.scheduler.address</name>
                  <value>10.64.200.47:8030</value>
              </property>
              <property>
                  <name>yarn.resourcemanager.address</name>
                  <value>10.64.200.47:8050</value>
              </property>
          </configuration>
      kind: ConfigMap
      metadata:
        creationTimestamp: 2016-07-12T18:51:16Z
        name: hadoop2-config
        namespace: helm
        resourceVersion: "80040126"
        selfLink: /api/v1/namespaces/helm/configmaps/hadoop2-config
        uid: 9d11191f-4861-11e6-8d89-0800274654e7
    kind: List
    metadata: {}

