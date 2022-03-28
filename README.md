# CloudHack_1
A repository containing files and data for the CloudHack assignment as part of the Cloud Computing course UE19CS352

# Implementation:

1. Start the minikube cluster,

                        minikube start
      
                        eval $(minikube docker-env)
      
2. Build the docker image for the flask app,

                        docker build -t cloudhack_ccteam10 -f flask-app-image.dockerfile .


3. Apply all the '.yaml' files OR run the ./start.sh script.

                        kubectl apply -f secret.yaml
                        
                        kubectl apply -f deployments.yaml
      
                        kubectl apply -f services.yaml
      
                        kubectl get all -n mongodb-namespace
      
4. Port forwarding:
      Apply the following commands for port forwarding OR run the ./start_portforwarding.sh script,
      
                        kubectl port-forward deployment.apps/flask-app-deployment 28016:5001 -n mongodb-namespace
                  
                        kubectl port-forward replicaset.apps/mongodb-express-deployment-58b4bfcffd 28015:8081 -n mongodb-namespace

      The flask app will now be available at http://localhost:28016/ and mongodb-express admin console will be available at http://localhost:28015/

      Start port forwarding using -
      
                        kubectl port-forward deployment.apps/mongodb-deployment 28017:27017 -n mongodb-namespace
                  
      If this does not run apply,
      
                        lsof -i :28017
                  
                        kill -9 <pid number>
                  
      then execute the above command.
      
5. Connecting to mongodb via mongosh -

                  mongosh --username ccteam10 --password jjji10 --host localhost --port 28017
  
6.Minikube Tunnel :
      By running the following commands, the containers will get ip addresses which can be accessed via the browser,
      
                        minikube tunnel
                        
  In another terminal run, (must be in the same directory with all the files)
      
                        kubectl get svc -n mongodb-namespace
  
 Once this is run we will be able to access the flask app and mongodb-express admin console at the resulting cluster ip addresses with their port numbers.
  

