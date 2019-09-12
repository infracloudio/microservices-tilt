# microservices-tilt

# Installation: 
Installing the tilt binary is a one-step command:

`curl -fsSL https://raw.githubusercontent.com/windmilleng/tilt/master/scripts/install.sh | bash`

Follow the official documentation in case you want to install prerequisites like `docker`, `kubectl` as well  :- https://docs.tilt.dev/install.html (You can skip `Microk8s` Installation in case you want to use `minikube` for local deployment.)

Verify the installation by 

`tilt version`

# Using Tilt 
* Creating and Editing `Tiltfile`:
Considering we have multiple microservices checked out in different directories we can create and keep the `TiltFile` in any workspace directory from we can have microservice projects path relative to Tiltfile just to have simplicity. 
  
 * Writing Tiltfile
  
    Tilt offers us performing repeatetive tasks of local development workflow like docker build, deploying container image in     kubernetes cluster automatically and sorting up logs of deployments in a sigle terminal. For that we have to provide paths for respective Dockerfile/s and kubernetes resource yaml files. 
    In the given example we are working on a single micorservice(`front-end`) and we want to build-deploy that microservice     only while keeping rest of microservices (`microservices-demo/deploy/kubernetes/complete-demo.yaml`) running in kubernetes    cluster, so we have written the `Tiltfile` as given below.
  
  ```
  # microservice image name and parent path of Dockerfile
  docker_build('weaveworksdemos/front-end','front-end')

  # kubernetes resourses which tilt would build-deploy
  k8s_yaml('microservices-demo/deploy/kubernetes/manifests/front-end-dep.yaml')
  # k8s_yaml('microservices-demo/deploy/kubernetes/manifests/front-end-svc.yaml')

  #running rest of the microservices using a single file
  k8s_yaml('microservices-demo/deploy/kubernetes/complete-demo.yaml') 
  ```
  


 * Tilt commands:
  
    Once we are ready with our `Tiltfile` we need to go to Tiltfile parent path and fire the command 
   
    ``` > tilt up ```
   
      This will start the tilt in the terminal creating docker image/s and kubernetes resources as per configured. Once all   the  services are up running it shall show status of each service as green but if it doesnt then we can see the error on its console and status as red.
      Once all the services are up and running tilt will watch for changes in the project of which we have given `docker_build`, which is front-end in this case. If we make changes to the source code and save them tilt will automatically detect the changes and start building docker images, pushing it to registry (local registry in case of minikube which makes much faster. Just make sure that `minikube` has `registry addon` enabled.)

    After finishing work fire the below command to shut down the tilt and all the resources.
  
    ``` > tilt down ``` 
