### Cards Microservices

### Refresh Actuator Path

    management:
      endpoints:
        web:
          exposure:
            include: "*"
    
    in the application.yml, I have set spring actuator management config, where we have /actuator/refresh endpoint.
    this is a post endpoint, so when we hit it we can see if any configuration from github repo for this cards microservice is changed
    or not.


### Section-7 :: Start

    1. Firstly remove bus amqp related dependency and rabbitmq related config from this branch, 
        because I am not going to track config changes using the rabbitmq bus

    2. Run the MySql docker container for account microservice , this microservice will use accountsdb database
        
        sudo docker run -p 3308:3306 --name <CONTAINER_NAME> -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=<DB_NAME> -d <MYSQL_IMAGE>

        ex : sudo docker run -p 3308:3306 --name cardsdb -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=cardsdb -d mysql
        here, d is detached mode for running container

    3. Download sqlectron app from https://github.com/sqlectron/sqlectron-gui/releases/tag/v1.38.0
        download the sqlectron-1.38.0.tar.gz version
    
    4. Extract the folder and goto the folder,
    5. then run ./sqlectron command to run the GUI
    6. click add option and set configuration, username and password is root and port is 3308:3306 <PC_PORT:CONTAINER_PORT>


### Section-7 :: MySql docker compose container

    1. Firstly create new docker images for all services with tag s7
        like: configserver:s7, accounts:s7, loans:s7, cards:s7

    2. Then, chaange docker compose with mysql container related changes
    3. Change application datasource properties as per docker compose
    4. Make package before creating new docker image
    5. so run mysql docker container for cardsdb locally first, before creating package. otherwise it
       will throw exception
    6. then create docker image with tag s7


### Section-8 :: Service Discovery and Service Registration

    1. Add eureka client maven dependency to connect with eureka server

    <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>

    2. Add service registration related dependency in application.yml
    3. Settnig some information properties using info tag in application.yml to show in eureka dashboard
    4. enable shutdown properties in actuator section, to enable deregistering from eureka server when account microservice is disabled or stopped
    5. Run the application, and before running make sure eureka server, configserver and docker container for mysql db is running


### Shutdown and DeRegistering from eureka server

    we have enabled spring actuator shutdown and also setting endpoints shutdown enabled in the application.yml .
    this, will enable shutting down out application without closing it from intelliJ.
    So, spring actuator provide us a POST api which is : http://localhost:8080/actuator/shutdown
    when, we hit it our application will be shutting down and also deregistering from eureka server.