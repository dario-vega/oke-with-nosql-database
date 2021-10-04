# oke-with-nosql-database

Draft version

Building the image and pushing to OCI docker registry
````
docker login ${ocir_docker_repository} --username ${ocir_namespace}/${ocir_user_name}
docker build -t express-nosql .
docker tag express-nosql:latest ${ocir_docker_repository}/${ocir_namespace}/nosqldemos/express-nosql:latest
docker push ${ocir_docker_repository}/${ocir_namespace}/nosqldemos/express-nosql:latest
````

Deploy using OKE
````
kubectl create secret docker-registry ocirsecret --docker-server=${ocir_docker_repository} --docker-username='${ocir_namespace}/${ocir_user_name}' --docker-password=TheAuthToken --docker-email='dario.vega@oracle.com'
kubectl apply -f express-nosql-oke.yaml
#test the app kubectl get svc and kubectl get pods -o wide
kubectl delete -f express-nosql-oke.yaml
````

