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