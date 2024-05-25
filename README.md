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