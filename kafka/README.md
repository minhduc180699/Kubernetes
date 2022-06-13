Install Kafka using Bitnami Helm Chart

helm install

NAME: my-release
LAST DEPLOYED: Sun Mar 20 17:31:03 2022
NAMESPACE: ds-ns
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: kafka
CHART VERSION: 15.5.0
APP VERSION: 3.1.0

** Please be patient while the chart is being deployed **

Kafka can be accessed by consumers via port 9092 on the following DNS name from within your cluster:

    my-release-kafka.ds-ns.svc.cluster.local

Each Kafka broker can be accessed by producers via port 9092 on the following DNS name(s) from within your cluster:

    my-release-kafka-0.my-release-kafka-headless.ds-ns.svc.cluster.local:9092

To create a pod that you can use as a Kafka client run the following commands:

    kubectl run my-release-kafka-client --restart='Never' --image docker.io/bitnami/kafka:3.1.0-debian-10-r49 --namespace ds-ns --command -- sleep infinity
    kubectl exec --tty -i my-release-kafka-client --namespace ds-ns -- bash

    PRODUCER:
        kafka-console-producer.sh \
            
            --broker-list my-release-kafka-0.my-release-kafka-headless.ds-ns.svc.cluster.local:9092 \
            --topic test

    CONSUMER:
        kafka-console-consumer.sh \
            
            --bootstrap-server my-release-kafka.ds-ns.svc.cluster.local:9092 \
            --topic test \
            --from-beginning

