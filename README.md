
`docker-compose up --build`

It will create four containers:

 - my_private_ca
 - mq_broker
 - client_a
 - client_b

These containers are emulating real devices in our system.

Once we have containers running our setup will proceed as follows:

 1. attach to the `my_private_ca` container
    1. generate the Private Key
    2. generate the self-signed CA Certificate
 2. attach to the `mq_broker` container
    1. generate the Private Key
    2. generate the CSR (Certificate Sign Request)
 3. attach to the `my_private_ca` container
    1. sign the CSR from MQTT Broker to create the MQTT Broker certificate
 4. attach to the `mq_broker` container
    1. move the certificate to the proper directory
 5. attach to the `client_a` container
    1. generate the Private Key
    2. generate the CSR
 6. attach to the `client_b` container
    1. generate the Private Key
    2. generate the CSR
 7. attach to the `my_private_ca` container
    1. sign CSR from Client A to create the certificate for that device
    2. sign CSR from Client B to create the certificate for that device
 8. attach to the `mq_broker` container
    1. start the MQTT sever and leave it running
 9. attach to the `client_a` container
    1. subscribe to the test topic at MQTT Broker
 10. attach to the `client_b` container
    1. publish the MQTT message to the test topic at MQTT Broker       

