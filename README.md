# sf4-stack

An empty Symfony 4.1 project with an Entity, a Migration and a full nginx+php-fpm+mysql Docker stack.


### Helpers

* composer stack-up: Bring up the development containers, create the databse and run the migrations
* composer stack-stop: Stop the containers but don't delete them.
* composer stack-start: Restart previously stopped containers (or create them from scratch, but don't run the migrations)
* composer stack-down: Remove all containers and their associated volumes and network.

The console has to be run from inside the PHP container, otherwise Symfony won't find the database.

```sh
$ php bin/console doctrine:migrations:migrate
                                                              
                    Application Migrations                    
                                                              

2018-09-04T23:18:25+02:00 [error] Error thrown while running command "doctrine:migrations:migrate". Message: "An exception occurred in driver: SQLSTATE[HY000] [2002] php_network_getaddresses: getaddrinfo failed: Name or service not known"

In AbstractMySQLDriver.php line 113:
                                                                                                                             
  An exception occurred in driver: SQLSTATE[HY000] [2002] php_network_getaddresses: getaddrinfo failed: Name or service not known



$ docker exec -it sf4stack_php-fpm_1 sh -l
$ php bin/console doctrine:migrations:migrate
                                                              
                    Application Migrations                    
                                                              

No migrations to execute.
```
