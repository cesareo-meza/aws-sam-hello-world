# Pasos del workshops

1. Se instalo AWS CLI
2. Se configuraron las credenciales de aws
  ```aws configure```
   se guadan en este file
   ```~/.aws/credentials ```
3. Se instala SAM CLI
4. Se instala NODE
5. Se crea la app con el SAM CLI
  ```sam init```
  * va a pedir el nombre que le quieres poner a tu app
  * va a pedir que tipo de proyecto hacer, elegi la opcion 1 para que lo haga por template,
  * va a pedir que tipo de runtime, elegi node 12 
  * va a crear una carpeta archivos y carpetas, en el README deja explicado que es cada cosa
6. se abre la carpeta que te crea con el nombre que le pusiste a la app
  y luego adentro abrir la carpeta hello-world que es donde esta el codigo de la lambda
7. darle npm install
8. regresarte una carpeta y ejecutar la lambda
  ```sam local start-api```
  para esto ya uno debe tener docker corriendo
9. Para consumir la funcion ir a http://127.0.0.1/3000/hello
10. Para deployar se crea un bucket
  ```aws s3 mb s3://cesareo-examples```
11. luego se crea el paquete para subir el codigo al bucket
  ```sam package --template-file template.yaml --output-template-file packaged.yaml --s3-bucket cesareo-examples```
12. Se revisa el bucket para ver que si haya agregado el paquete
  ```aws s3 ls s3://cesareo-examples```
13. Se hace el deploy, se debe asignar un nombre al stack, puede ser cualquiera, debe ser unico en tu cuenta de aws, la region si se pone mal no importa te dice cual es la correcta y te pide reintentar
  ```sam deploy --template-file packaged.yaml --stack-name lp-workshop --capabilities CAPABILITY_IAM --region us-east-1```
14. Para obener la URL para poder consumirla hay que ver los detalles del stack, esta en OutpuValue.OutputKey
  ```aws cloudformation describe-stacks --stack-name lp-workshop```
15. Para ver los logs
  ```sam logs --stack-name lp-workshop --name HelloWorldFunction --start-time '5mins ago'```
16. Para ver los logs acumulados
  ```sam logs --stack-name lp-workshop --name HelloWorldFunction --tail```



