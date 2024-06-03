# Spring Boot Shopping Cart Web App

## About

This is a demo project for practicing Spring + Thymeleaf. The idea was to build some basic shopping cart web app.

It was made using **Spring Boot**, **Spring Security**, **Thymeleaf**, **Spring Data JPA**, **Spring Data REST and Docker**. 
Database is in memory **H2**.

There is a login and registration functionality included.

Users can shop for products. Each user has his own shopping cart (session functionality).
Checkout is transactional.

## Configuration

### Configuration Files

Folder **src/resources/** contains config files for **shopping-cart** Spring Boot application.

* **src/resources/application.properties** - main configuration file. Here it is possible to change admin username/password,
as well as change the port number.

## How to run

There are several ways to run the application. You can run it from the command line with included Maven Wrapper, Maven or Docker. 

Once the app starts, go to the web browser and visit `http://ec2-54-175-86-109.compute-1.amazonaws.com:8070/home`

Admin username: **admin**

Admin password: **admin**

User username: **user**

User password: **password**


### Docker

It is possible to run **shopping-cart** using Docker:

Build Docker image:
```bash
$ docker build -t shopping-cart:v1 .
```

Run Docker container:
```bash
$ docker run --rm -i -p 80:8070 \
      --name shopping-cart \
      shopping-cart:v1
```

### HAL REST Browser

Go to the web browser and visit `http://ec2-54-175-86-109.compute-1.amazonaws.com:8070/`

You will need to be authenticated to be able to see this page.

### H2 Database web interface

Go to the web browser and visit `http://ec2-54-175-86-109.compute-1.amazonaws.com:8070/h2-console`

In field **JDBC URL** put 
```
jdbc:h2:mem:shopping_cart_db
```

In `/src/main/resources/application.properties` file it is possible to change both
web interface url path, as well as the datasource url.
