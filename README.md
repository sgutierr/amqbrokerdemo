# amqbrokerdemo

##  Demo story

We want to automate deployment of an API managed by 3scale across multiple environments, using pre-defined pipelines provided by the platform. The delivery pipelines must support environment-specific properties, testing, versioning, and the ability to rollback incomplete or failed deployments.

This demo is composed of the following components: 

**Preparation**

    • oc rsh ex-aao-ss-0
    • oc rsync ex-aao-ss-0:/home/jboss/broker.ks .
    • oc rsync ex-aao-ss-0:/home/jboss/broker.ts .
    • oc create secret generic ex-aao-amqp-secret --from-file=broker.ks=broker.ks  --from-literal=keyStorePassword=password --from-file=client.ts=broker.ts --from-literal=trustStorePassword=password

**Deploy broker and addresses**    
    
    • oc create -f conf/ActiveMQArtemis.yaml 
    • oc apply -f conf/addresses.yaml 

**Delete commands to remove the demo**        

    • oc delete ActiveMQArtemis ex-aao
    • oc delete secret ex-aao-amqp-secret
 
 
 
 
 




