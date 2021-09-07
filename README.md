# amqbrokerdemo


 oc rsh ex-aao-ss-0
 oc rsync ex-aao-ss-0:/home/jboss/broker.ks .
 oc rsync ex-aao-ss-0:/home/jboss/broker.ts .
 oc delete ActiveMQArtemis ex-aao
 oc delete secret ex-aao-amqp-secret
 
 /home/sgutierr/development/software/oc/oc create secret generic ex-aao-amqp-secret --from-file=broker.ks=broker.ks  --from-literal=keyStorePassword=password --from-file=client.ts=broker.ts --from-literal=trustStorePassword=password
 oc create -f ../ActiveMQArtemis.yaml 


oc apply -f conf/addresses.yaml 
