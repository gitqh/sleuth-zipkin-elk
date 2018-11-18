# Logging management with sleuth, zipkin and elk

This project aims to showcase 2 key features of a microservices application. The first is distributed tracing. The second is the implementation of a centralised log management system. This application has been developed using Spring Boot

## Spring Cloud Sleuth & Zipkin

I am using Spring Cloud Sleuth for distributed tracing and Zipkin for visualisation.

## Logstash, Elasticsearch & Kibana

Spring is logging using Slf4j with Logback configured to write to Logstash. Logstash is writing to Elasticsearch. Kinana is used to visualise the logs

## Running the application

### How to run the services

* Build the project

``` bash
./gradlew build
```

* Copy the springboot jars to docker folder

``` bash
./gradlew copyTask
```

* Start the demo

``` bash
cd ./docker
docker-compose up
```

### How to start continuous build

``` bash
./gradlew build --continuous
```

### Project structure and flow

``` bash
├── README.md
├── docker
├── zipkin-server
├── order-service
├── user-service
├── product-service
└── logistics-service


http://localhost:8080/order-service/orders/1234567890
-> orderId -> Order User -> userId      -> User Service
                         -> productId   -> Product Service
                         -> logisticsId -> Logistics Service

```

## Configure Kibana and view the logs

1. Open Kibana [http://localhost:5601/](http://localhost:5601/)
2. Under "Management" create an Index Pattern. `logstash-*` and `@timestamp`
3. Choose "Discover" to view the log entries

NB. If you want to filter on a particular trace you can use something similar to this

``` bash
message: ">>> Call*" AND traceId: "7f3a243d1b53720f"
```

## View the tracing in Zipkin

1. Open Zipkin [http://localhost:9411/](http://localhost:9411/)
2. Choose "Find Traces"



