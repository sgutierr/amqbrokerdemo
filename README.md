# amqbrokerdemo

##  Demo story

Developers deploying Red Hat AMQ on Red Hat OpenShift often wonder how to connect external clients to AMQ Broker using the Transport Layer Security (TLS) protocol, which is an improved successor to the Secure Sockets Layer (SSL) protocol.

In this article, you will learn how to do just that. The steps are as follows:

    • Generate TLS credentials.
    • Install the AMQ Broker Operator.
    • Deploying Prometheus for AMQ.
    • Deploy an AMQ Broker instance defining an acceptor that uses TLS.
    • Create an Anycast address.
    • Connect an external CORE/OpenWire client and send and receive messages.

**Generate TLS credentials**
**Install the AMQ Broker Operator**   
**Deploying Prometheus for AMQ**
**Deploy an AMQ Broker instance defining an acceptor that uses TLS**
    • oc rsh ex-aao-ss-0
    • oc rsync ex-aao-ss-0:/home/jboss/broker.ks .
    • oc rsync ex-aao-ss-0:/home/jboss/broker.ts .
    • oc create secret generic ex-aao-amqp-secret --from-file=broker.ks=broker.ks  --from-literal=keyStorePassword=password --from-file=client.ts=broker.ts --from-literal=trustStorePassword=password    
    • oc create -f conf/ActiveMQArtemis.yaml 
    • oc apply -f conf/addresses.yaml 
**Delete commands to remove the demo**        

    • oc delete ActiveMQArtemis ex-aao
    • oc delete secret ex-aao-amqp-secret
 
 
 
 
 




