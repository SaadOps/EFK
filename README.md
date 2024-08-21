# EFK (Elasticsearch, Fluentd, Kibana) Deployment on Minikube Kubernetes Cluster.

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
    
    kubectl create -f test-pod.yaml
    kubectl run nginx --image=nginx --restart=Never
    kubectl run mycurlpod --image=curlimages/curl -i --tty -- sh

# 4. Create index patterns
![image](https://github.com/user-attachments/assets/f7b09b54-314a-41aa-9091-4f61d7463fe9)
![screencapture-localhost-5601-app-management-kibana-indexPatterns-patterns-e5af2e30-5f20-11ef-afa8-95e5563d0291-2024-08-20-23_50_56](https://github.com/user-attachments/assets/018f59a5-6ed9-4105-9a4f-d41738015aa6)

# 5. Click on Discover
### Output:
![screencapture-localhost-5601-app-discover-2024-08-20-23_51_47](https://github.com/user-attachments/assets/f8931f52-e53c-4a70-855e-7c0700acd6e2)
![screencapture-localhost-5601-app-discover-2024-08-20-23_57_26](https://github.com/user-attachments/assets/269e2800-4dac-4c87-b9af-6973dba93388)
![screencapture-localhost-5601-app-discover-2024-08-21-00_03_24](https://github.com/user-attachments/assets/33379c58-0692-4026-b759-08e7301d613a)
![screencapture-localhost-5601-app-discover-2024-08-21-00_04_24](https://github.com/user-attachments/assets/14da24f3-84ff-44a2-9d24-e2a01400e309)
![screencapture-localhost-5601-app-discover-2024-08-21-00_06_20](https://github.com/user-attachments/assets/b209d2c1-f6f4-4da8-be5e-27aebbcb8ce6)
![image](https://github.com/user-attachments/assets/41f31b74-afa9-4259-9a76-5d0ad72b21f7)
![image](https://github.com/user-attachments/assets/3c514f41-2fc7-44fb-9905-5e16527775e1)



### Other Implementation Screenshots:
![image](https://github.com/user-attachments/assets/d982051a-db0d-4837-b09e-bae1ce542b0f)
![Screenshot from 2024-08-20 23-53-14](https://github.com/user-attachments/assets/69d81b7b-4289-46a8-a770-743a8033e494)
![Screenshot from 2024-08-21 00-01-36](https://github.com/user-attachments/assets/fee5e561-e6b4-4b92-aadd-d00102384b28)
![Screenshot from 2024-08-21 00-01-10](https://github.com/user-attachments/assets/cf9e0b08-fce1-4563-b480-f935b03e76b7)
![Screenshot from 2024-08-21 00-00-20](https://github.com/user-attachments/assets/dc002578-c63f-4739-86ee-01beec11a6b7)
![Screenshot from 2024-08-20 23-53-29](https://github.com/user-attachments/assets/bda209ef-50bc-4a3d-bfc1-0afb26954363)
![Screenshot from 2024-08-20 23-54-05](https://github.com/user-attachments/assets/f7852037-aba3-4482-bbc5-98409cae5eee)
![Screenshot from 2024-08-20 23-57-04](https://github.com/user-attachments/assets/5f902c77-e4dd-4304-b7c2-f1b8396e7535)
![Screenshot from 2024-08-20 23-53-48](https://github.com/user-attachments/assets/49be4528-3f9c-4853-90a0-afdcf4d52f10)
![image](https://github.com/user-attachments/assets/7c46295e-56bc-428e-adb9-1f361529dbe2)
![Screenshot from 2024-08-21 00-09-12](https://github.com/user-attachments/assets/baca7c8d-bfc1-4c56-ba95-7029e2b670a0)














