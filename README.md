# amqbrokerdemo

##  Demo story

Developers deploying Red Hat AMQ on Red Hat OpenShift often wonder how to connect external clients to AMQ Broker using the Transport Layer Security (TLS) protocol, which is an improved successor to the Secure Sockets Layer (SSL) protocol.

https://developers.redhat.com/blog/2020/08/26/connecting-external-clients-to-red-hat-amq-broker-on-red-hat-openshift#part_1__generating_credentials_for_tls_connections

In this article, you will learn how to do just that. The steps are as follows:

    • Generate TLS credentials.
    • Install the AMQ Broker Operator.
    • Deploying Prometheus for AMQ.
    • Deploy an AMQ Broker instance defining an acceptor that uses TLS.
    • Create an Anycast address.
    • Connect an external CORE/OpenWire client and send and receive messages.

**Generate TLS credentials**

In terms of files required the objective for implementing one side TLS is obtain these documents : 


      • broker1 keystore : broker.ks
      • amqclient keystore : client.ts
      • Trustore containing both broker1 and amqclient certtificates : broker.ts
  
** Remember keytool is a java tool and it is highly recommended to use the same Java version which uses the AMQ broker pod (JAVA 1.8). 


    • keytool -genkey -alias broker -keyalg RSA -keystore broker.ks -storetype PKCS12 -dname "cn=ex-aao-ss-0.ex-aao-hdls-svc.appdev-amqbroker.svc.cluster.local"
    • keytool -export -alias broker -keystore broker.ks -rfc -storepass password -file broker.pem
    • keytool -import -alias broker -keystore broker.ts -file broker.pem 

    • keytool -genkey -alias amqclient -keyalg RSA  -storetype PKCS12 -keystore amqclient.ks -dname "cn=amqclient"
    • keytool -export -alias amqclient -keystore amqclient.ks -rfc -storepass password -file amqclient.pem
    • keytool -import -alias amqclient -keystore broker.ts -file amqclient.pem 

You need to get these files: broker.ks, broker.ts and amqclient.ks

    • oc create secret generic ex-aao-amqp-secret --from-file=broker.ks=broker.ks  --from-literal=keyStorePassword=password --from-file=client.ts=broker.ts --from-literal=trustStorePassword=password   
    

**Install the AMQ Broker Operator**   

**Deploying Prometheus for AMQ**

**Deploy an AMQ Broker instance defining an acceptor that uses TLS**
 
    • oc create -f conf/ActiveMQArtemis.yaml 
    • oc apply -f conf/addresses.yaml 
    
**Delete commands to remove the demo**        

    • oc delete ActiveMQArtemis ex-aao
    • oc delete secret ex-aao-amqp-secret
 
 
 
 
 




