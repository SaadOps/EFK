# Elasticsearch, Fleutd, Kibana Deployment on K8's.

![EFK](https://github.com/user-attachments/assets/cd1fb063-5075-4423-8023-fb900647ee61)



Elasticsearch will be installed first as a Statefulset which will store all the data as indexed
Fluend will be installed as daemonset so that logs can be captured from all Nodes
Kibana will be installed as deployment so that it can invokes the Elasticsearch Server and run all the dashboards.

# 1. Install Elasticsearch on Minikube Cluster:  


    cd elasticsearch
    kubectl create -f es-svc.yaml
    kubectl create -f es-st.yaml

#### Verify Elasticsearch Deployment

    kubectl port-forward es-cluster-0 9200:9200

#### To check the health of the Elasticsearch cluster:
     
    curl http://localhost:9200/_cluster/health/?pretty

### Output:  

# 2. Install Kibana on Minikube Cluster:  

    cd kibana
    kubectl create -f kibana-deployment.yaml
    kubectl create -f kibana-svc.yaml

# Verify Kibana Deployment

    kubectl port-forward <kibana-pod-name> 5601:5601
    
#### To check it's handling requests:

    curl http://localhost:5601/app/kibana

# 3. Install Fluentd on Minikube Cluster:  

    cd fluentd
    kubectl create -f fluentd-role.yaml
    kubectl create -f fluentd-sa.yaml
    kubectl create -f fluentd-rb.yaml
    kubectl create -f fluentd-ds.yaml

# 3. Validate the EFK Cluster  
Run one pod in the same namespace to capture the logs on cluster  
    
    kubectl create -f test.pod
    kubectl run nginx --image=nginx --restart=Never
    kubectl run mycurlpod --image=curlimages/curl -i --tty -- sh



