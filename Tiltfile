# microservice image name and parent path of Dockerfile
docker_build('weaveworksdemos/front-end','front-end')

# kubernetes resourses which tilt would build-deploy
k8s_yaml('microservices-demo/deploy/kubernetes/manifests/front-end-dep.yaml')

# Pause tilt 
#k8s_resource('front-end', trigger_mode=TRIGGER_MODE_MANUAL)


# microservice-orders image name and parent path of Dockerfile
#local('./orders/scripts/build.sh')
#docker_build('weaveworksdemos/orders','orders/target/docker/orders')



# kubernetes resourses which tilt would build-deploy
#k8s_yaml('microservices-demo/deploy/kubernetes/manifests/orders-dep.yaml')


#running rest of the microservices using a single file
k8s_yaml('microservices-demo/deploy/kubernetes/complete-demo.yaml')


