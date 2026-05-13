# asdf
* Node.js (for Angular) - Download from nodejs.org
* Java JDK 17 or later - Download from oracle.com or use OpenJDK
* Angular CLI - Install via `npm install -g @angular/cli`
* Maven - Download from maven.apache.org
* MySQL (or any SQL database) - Download from mysql.com
* IDEs: VS Code for Angular, IntelliJ IDEA or Eclipse for Spring Boot
* WSL

# VERSIONS
* node
```
node --version
v20.19.2

which node
/home/foo/.nvm/versions/node/v20.19.2/bin/node
```
* npm
```
npm --version
10.8.2

which npm
/home/foo/.nvm/versions/node/v20.19.2/bin/npm
```
* nvm
```
nvm --version 
0.40.3
```
* np
```
np --version
20.0.1
```
* java
```
java --version
openjdk 21.0.7 2025-04-15
OpenJDK Runtime Environment (build 21.0.7+6-Ubuntu-0ubuntu124.04)
OpenJDK 64-Bit Server VM (build 21.0.7+6-Ubuntu-0ubuntu124.04, mixed mode, sharing)
```
* nvm
```
mvn --version
Apache Maven 3.8.7
Maven home: /usr/share/maven
Java version: 21.0.7, vendor: Ubuntu, runtime: /usr/lib/jvm/java-21-openjdk-amd64
Default locale: en, platform encoding: UTF-8
OS name: "linux", version: "6.6.87.1-microsoft-standard-wsl2", arch: "amd64", family: "unix"

which mvn
/usr/bin/mvn
```
* mysql
```
mysql --version
mysql  Ver 8.0.42-0ubuntu0.24.04.1 for Linux on x86_64 ((Ubuntu))

which mysql
/usr/bin/mysql
```
* bash
```
bash --version
GNU bash, version 5.2.21(1)-release (x86_64-pc-linux-gnu)
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>

This is free software; you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

which bash
/usr/bin/bash
```

# 1. Backend: Spring Boot Setup

- [Spring Initializr](https://start.spring.io/)
* Project: Maven
* Language: Java
* Spring Boot: 3.5.0 (latest stable)
* Dependencies: 
    * Lombok
    * Spring Web 
    * MySQL Driver (mysql-connector-java)
    * [Spring Data JPA](https://docs.spring.io/spring-boot/reference/data/sql.html#data.sql.jpa-and-spring-data) 
    * [Rest Repositories](https://spring.io/projects/spring-data-rest) 
    * [Spring Boot DevTools](https://docs.spring.io/spring-boot/reference/using/devtools.html)
* Project Metadata
    * Group: com.yourcompany
    * Artifact: task-app
    * Name: Task Management App
    * Description: A simple CRUD app for managing tasks
    * Package name: com.yourcompany.task-app
    * Packaging: Jar
    * Java: 21

### Verify Maven Configuration:
* pom.xml
```
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-rest</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>com.mysql</groupId>
			<artifactId>mysql-connector-j</artifactId>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.projectlombok</groupId>
			<artifactId>lombok</artifactId>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>
```

### Configure Database:
* Install MySQL
```sudo apt install mysql-server```
* create a database: `create database taskdb;`
* start MySQL server `sudo service mysql start`
* check MySQL status `sudo service mysql status`
* secure MySQL `sudo mysql_secure_installation`
    * set a root password ``
    * remove anonymous users `yes`
    * disallow root login remotely `yes`
    * remove test database `yes`
    * reload privilege tables `yes`
* log in to mysql `sudo mysql -u root -p`
* check the version `SELECT VERSION();`
* when running the code from the udemy business course
```
export NODE_OPTIONS=--openssl-legacy-provider
ng serve
```

* create a test database
```
CREATE DATABASE testdb;
SHOW DATABASES;
```
* exit with `exit`
* to auto-start mysql add to `~/.bashrc`
```
echo "sudo service mysql start >> ~/.bashrc
```
* note: MySQL runs on localhost (127.0.0.1) and port 3306 by default in WSL

* Edit `src/main/resources/application.properties`
```
spring.datasource.url=jdbc:mysql://localhost:3306/taskdb
spring.datasource.username=root
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.data.rest.base-path=/api
```
### Entity
* In `com.yourcompany.taskapp.model`, create `Task.java` using Lombok:



### Repository

### Controller (Optional)

### CORS Configuration:

# 2. Database: SQL Setup

# 3. Frontend: Angular Setup





# install angular cli
```
npm install -g @angular/cli
```
# create new angular app 
```
ng new <your-project-name>
```
# build angular app (compile/transpile) 
* builds the app (compile / transpile)
* starts the server
* watches the source files
* rebuilds the apps when source is updated (hot reload)
	* http://localhost:4200
```
ng serve
```
# change angular server port
```
ng serve --port 5100
```

# [Angular File Structure](https://v17.angular.io/guide/file-structure)
| Workspace configuration files | Purpose |
| ------------- | ------------- |
| .editorconfig | Configuration for code editors. See EditorConfig. |
| .gitignore | Specifies intentionally untracked files that Git should ignore. |
| README.md | Introductory documentation for the root application. |
| angular.json |  	CLI configuration defaults for all projects in the workspace, including configuration options for build, serve, and test tools that the CLI uses, such as Karma, and Protractor. For details, see Angular Workspace Configuration. |
| package.json | Configures npm package dependencies that are available to all projects in the workspace. See npm documentation for the specific format and contents of this file. |
| package-lock.json | Provides version information for all packages installed into node_modules by the npm client. See npm documentation for details. If you use the yarn client, this file will be yarn.lock instead. |
| src/ | Source files for the root-level application project. |
| node_modules/ | Provides npm packages to the entire workspace. Workspace-wide node_modules dependencies are visible to all projects. |
| tsconfig.json | The base TypeScript configuration for projects in the workspace. All other configuration files inherit from this base file. For more information, see the Configuration inheritance with extends section of the TypeScript documentation. |

# aka
|  |  |
| --- | --- |
| angular.json | Angular workspace config list of execution targets |
| node_modules/ | local repo of node modules |
| package.json | project meta data list of node dependencies |
| src/app/ | app components,templates, etc |
| src/assets/ | images, etc |
| src/environments/ | profiles for environment: dev, test, prod, etc |
| index.html | main launch page |
| polyfills.ts | add supports for different browser versions |
| test.ts | unit test cases |
| tsconfig.json | typescript compiler configs |

# `tree -I ".vscode|.git|node_modules"`
```
.
└── camo-brand
    ├── README.md
    ├── angular.json
    ├── package-lock.json
    ├── package.json
    ├── public
    │   └── favicon.ico
    ├── src
    │   ├── app
    │   │   ├── app.config.ts
    │   │   ├── app.css
    │   │   ├── app.html
    │   │   ├── app.routes.ts
    │   │   ├── app.spec.ts
    │   │   └── app.ts
    │   ├── index.html
    │   ├── main.ts
    │   └── styles.css
    ├── tsconfig.app.json
    ├── tsconfig.json
    └── tsconfig.spec.json

5 directories, 18 files
```



# [ng generate](https://v17.angular.io/cli/generate)


# `ng generate component home` example
* `selector`: to describe how Angular refers to the component in templates.
* `standalone`: to describe whether the component requires a NgModule.
* `imports`: to describe the component's dependencies.
* `template`: to describe the component's HTML markup and layout.
* `styleUrls`: to list the URLs of the CSS files that the component uses in an array


# files working in tandem
* components
	* src/app/.../component/home/home.ts
	* src/app/app.ts
		* `import {Home} from './home/home';`
	* 






spring-boot-starter-data-jpa
spring-boot-starter-data-rest
mysql-connector-java
Lombok

Create a new MySQL user for our application
user id: ecommerceapp
password: ecommerceapp

databases
• 01-create-user.sql
• 02-create-products.sql


* angular cli should be installed locally for every project
* locally `npm install --save-dev @angular/cli`
* globally `npm install -g @angular/cli`

* building existing spring `./mvnw clean install`
* running spring `./mvnw spring-boot:run`

# angular set up
mkdir <project-folder>
cd <project-folder>
npm install --save-dev @angular/cli
npm install --save bootstrap jquery


# spring set up
install OpenJDK
build
run
port 8080


# MySQL set up
brew install MySQL
MySQL.server start
MySQL.server stop


# porting
`lsof -i`:PORT. Here PORT can be either 4200 or 8080.
`kill -9 PID`. Here PID is the process id you get from running the above command.




# resources
* [](https://www.reddit.com/r/WGU_CompSci/comments/1g2bi3w/d288_backend_programming_2024_guide/)
* [](https://www.reddit.com/r/WGU_CompSci/comments/168qz83/d288_backend_programming_guide/)
* [](https://www.reddit.com/r/WGU_CompSci/comments/1dt4dbj/final_project_setup_guide_for_no_lab_environment/)
* [](https://wgu.udemy.com/course/spring-framework-5-beginner-to-guru/learn/lecture/7496692#overview)
* [](https://www.baeldung.com/jpa-persisting-enums-in-jpa)
* [](https://wgu.udemy.com/course/spring-framework-5-beginner-to-guru/learn/lecture/7497518#overview)
* [](https://nodejs.org/en/download/)

# WGU assignment guidelines

A.   Create a new Java project using Spring Initializr, with each of the following dependencies:
•    Spring Data JPA (spring-boot starter-data-jpa)
•    Rest Repositories (spring-boot-starter-data-rest)
•    MySQL Driver (mysql-connector-java)
•    Lombok
B.   Create your subgroup and project by logging into GitLab using the web link provided and do the following:
•    connect your new Java project
•    commit with a message and push when you complete each of the tasks listed below (parts B to F, etc.)
•    Submit a copy of the git repository URL and a copy of the repository branch history retrieved from your repository, which must include the commit messages and dates.
C.   Construct four new packages, one for each of the following: controllers, entities, dao, and services. The packages will need to be used for a checkout form and vacations packages list.
D.   Write code for the entities package that includes entity classes and the enum designed to match the UML diagram.
E.   Write code for the dao package that includes repository interfaces for the entities that extend JpaRepository, and add cross-origin support.
F.   Write code for the services package that includes each of the following:
•    a purchase data class with a customer cart and a set of cart items
•    a purchase response data class that contains an order tracking number
•    a checkout service interface
•    a checkout service implementation class
G.   Write code to include validation to enforce the inputs needed by the Angular front-end.
H.   Write code for the controllers package that includes a REST controller checkout controller class with a post mapping to place orders.
I.   Add five sample customers to the application programmatically.
J.   Run your integrated application by adding a customer order for a vacation with two excursions using the unmodified Angular front-end. Provide screenshots for the following:
•    that your application does not generate a network error when adding the data
•    your database tables using MySQL Workbench to show the data was successfully added

# [](https://www.reddit.com/r/WGU_CompSci/comments/1g2bi3w/d288_backend_programming_2024_guide/) guideline summary

## C. 
* go to `src/main/java/com.your.groupname`
* right click > new > Package, Do that 4 times
* construct a fifth package named "config" and copy the RestDataConfig.java
* Replace the application.properties file with the one in the lab files directory
* RestDataConfig.java will have an error in it right now, but don't worry about it. We will fix that later
*  commit and push task C. 

## D.
*  read the UML diagram
* https://www.freecodecamp.org/news/crows-foot-notation-relationship-symbols-and-how-to-read-diagrams/
* Use @Getter and @Setter instead of @Data
* columns in @Column(name = ___), mirror the column properties in the SQL database
* Read each CREATE TABLE statement and copy each name and data type exactly. 
* variable names in your entities, mirror the ones in the angular front-end
* drilling down to src/app/model/ and reading the .ts file for each entity
* Do not create a separate file for excursion_cartitem
* versions
```
Spring: <version>3.3.6</version>
Lombok: <version>1.18.36</version>
``` 
* `pom.xml`
```
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter-parent</artifactId>
<version>3.3.6</version>
```
```
<groupId>org.projectlombok</groupId>
<artifactId>lombok</artifactId>
<version>1.18.36</version>
```
* refresh maven, or invalidate your caches
* Creating your getters and setters using the IDEs built-in getter and setter generator
* division is entirely dependent on what country you select when creating a customer, you need to reactively set the country ID for Division
* OneToMany and ManyToMany relationships to configure
* entity that is generally considered the "owner" of the other entity is where you put the @JoinTable tag
* put the @JoinTable tag in CartItem
* spell the third option as "canceled", not "cancelled"
* mapping the Cart's status property to the database
* annotate your enumeration in Cart properly
* RestDataConfig.java file now and fix the import statement
* should be something like like com.your.groupname.entities.*
* Get rid of import edu.wgu.d288_backend.entities.*
* commit and push for task D.

## E.
* create repository files for ALL of your entity files
* Don't do anything with the RepositoryRestResource section
* add a @CrossOrigin tag above each interface declaration to enable cross-origin support
* this tag enables the back-end, which broadcasts on port 8080, to communicate with the front-end, which broadcasts on port 4200.
* Go ahead and run both the back-end and front-end, go to localhost:4200
* triple check your column mappings, variable names, and entity relationships
* Once you've got your front-end and database linked up, commit and push task E.

## tasks F, G, H, and I

### F.
* don't worry if it's not fully correct
* Create a "services" package and put the following 4 files in it:
	* Purchase.java: using @Getter and @Setter, Ignore everything with shippingaddress and billingaddress
	* PurchaseResponse.java
	* CheckoutService.java
	* CheckoutServiceImpl.java
* associate a customer with a cart, and our Cart entity has a Customer ID field. Go ahead and autowire a customerRepository. 
* his Order is our Cart, and his OrderItem is our CartItem, Ignore EVERYTHING that has to do with shippingaddress and billingaddress. 
* set the status of the cart to ordered
* you've got a setter generated for you by lombok (something like setStatus) so just use that and pass in the correct enum value. I do this as soon as I get the cart from the purchase object. 
* Confirm we aren't adding a null item. 
* Initialize the cart's set for CartItem and the customer's variable for Car. these variables are declared, but aren't defined. And while we have our database relationships defined between our entities, Spring isn't adding our cart items to our cart or our cart to our customer. That's what the service is for! 
* Actually add the item to it's respective object
* Make item recognizes its owner, This performs all 4 functions we need. Add this to your Cart entity, and modify it to fit your Customer entity.
```
    public void add(CartItem cartItem) {
        if (cartItem != null) {
            if (cart_items == null) {
                cart_items = new HashSet<>();
            }
            cart_items.add(cartItem);
            cartItem.setCart(this);
        }
    }
```
*  Everything else that happens in the videos you should be able to copy. 
* we have no way of testing if this code actually works, as we don't have a controller to actually grab the data the front-end is sending via our browser. So commit and push task F. 

### G.
* Go ahead and run your project and take a look at the front-end
* Click the person and then the "Add Customer" button.
* For each one of those fields, we need to add validations.
* Although, they don't let us use Spring Boot Validation, So all you have to do is track down each variable that corresponds to the field in the front-end and add nullable = "false" in the @Column tag. 
* when someone tries to place an order with an empty cart.  implement an if/else branch for the return statement of your placeOrder function
* check if the cart is null, then if the cart's cartItems is null, then lastly if the cart's cartItems are empty.
If you don't know what to do for the error message here are a few hints:
1. You can't edit the front-end, so it doesn't have anything to do with that.
2. Your error message can't crash the program.
3. PurchaseResponse returns a string.
*  Commit and push task G. 

### H.
* Watch Udemy video 208. Copy what the instructor does exactly. 
*  test if you're getting an order tracking number and if your database tables are updating.
*  Watch the "Demonstration of a completed performance assessment" video 
*  Once everything is working, commit and push task H. 

### I.
* adding 5 customers + the one that's added in the database script for a total of 6
* “Spring Framework 5: Beginner to Guru” on Udemy, section 2 video 17.
* instructor-provided video in D287 on Task E
* create overloaded constructors for both Customer and Division, use the setter methods created by Lombok if you desire. you need a no-argument constructor in your entity still, but we have Lombok! Just slap a @NoArgsConstructor on there
* Ensure when you're adding your customers, you're initializing every fillable field. Don't input manual values for the auto-generated fields. 
* Confirm all the code that adds the customers only runs if there's less than or equal to one customer in the database. 
* I used a logger object, which I added to my BootStrapData class with this line of code: 
```
private static final Logger 
logger 
= LoggerFactory.
getLogger
(BootStrapData.class);
```
* send info messages using logger.info()
* pass the number of customers in the database with customerRepository.count()
* checking your Customer table to ensure it populates correctly
* Ensure your customers aren't getting overwritten when re-running the application,
*  Once everything is working, commit and push part I. 

### J.
* test the application in the lab environment 
* testing in chrome like the instructor




# install java
* `sudo apt/dnf/pacman search openjdk`
```
foo@DESKTOP-PAI48Q8:~/ecom-ang-spring-mysql/backend-spring-boot$ sudo apt search openjdk
Sorting... Done
Full Text Search... Done
default-jdk/noble 2:1.21-75+exp1 amd64
  Standard Java or Java compatible Development Kit

default-jdk-doc/noble 2:1.21-75+exp1 amd64
  Standard Java or Java compatible Development Kit (documentation)

default-jdk-headless/noble 2:1.21-75+exp1 amd64
  Standard Java or Java compatible Development Kit (headless)

default-jre/noble 2:1.21-75+exp1 amd64
  Standard Java or Java compatible Runtime

default-jre-headless/noble 2:1.21-75+exp1 amd64
  Standard Java or Java compatible Runtime (headless)

google-android-tools-installer/noble 26.1.1+1710437545-3build2 amd64
  Google's 'Android SDK Tools' Installer

java-package/noble 0.64 all
  Utility for creating Java Debian packages

...
```
* `sudo apt install openjdk-21-jdk`

# Recommended Versions - follow directions [install-linux.md](https://github.com/vva1kerr/a-sb-ss-5june25/blob/main/GUIDES/01-install-devtools-linux/install-linux.md)
* Java: 11 (LTS, compatible with Spring Boot 2.4.0)


* Node.js: 16.20.2 (LTS, suits older Angular versions)
* MySQL: 8.0 or 5.7 (works with mysql-connector-java)
* Maven: 3.9.6 or later
* Lombok: 1.18.34 (fixes compatibility)
* Maven Compiler Plugin: 3.13.0

* `sudo apt install openjdk-11-jdk`
* `apt-cache search nodejs`
* `nvm ls-remote`
* `nvm install 16.20.2`
* ` nvm use 16.20.2`

* `java -version`
* `node -v`
* `npm -v`
* `mvn -v`
* `mysql --version`
* `ng --version`

* `update-alternatives --list java`
* `sudo update-alternatives --config java`
* `chmod +x mvnw`
* `./mvnw clean install`
* `mvn clean install`

```
cd backend-spring-boot
sudo rm -rf target/
sudo chown -R $USER:$USER .
```
```
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.30</version>
    <scope>provided</scope>
</dependency>
```










# Development Environment Setup Guide for Angular, Spring, and MySQL on WSL2 (Linux kernel)

This guide explains how to set up a development environment on **WSL2** (Linux) for a **Java Spring Boot + Angular** project.

---

## Prerequisites

- **WSL2** installed on Windows with a Linux distribution (e.g., Ubuntu 24.04)
- Familiarity with Linux terminal commands
- Internet connection for downloading packages

---

## Resources
* [WSL2](https://learn.microsoft.com/en-us/windows/wsl/)
* [APT User's Guide - Debian](https://www.debian.org/doc/manuals/apt-guide/index.en.html)
* [NVM - Github](https://github.com/nvm-sh/nvm)
* [NodeJS](https://nodejs.org/en)
* [NodeJS - Github](https://github.com/nodejs/node)
* [Angular](https://angular.dev/)
* [Angular - Github](https://github.com/angular)
* [Angular-CLI - Github](https://github.com/angular/angular-cli)

---

## 1. Install and Configure Development Tools

### 1.1 Install Java (OpenJDK)
```bash
sudo apt update
sudo apt search openjdk
sudo apt install openjdk-21-jdk
java --version
update-alternatives --list java
sudo update-alternatives --config java
dpkg --list | grep openjdk
sudo apt remove openjdk-11-jdk
sudo apt autoremove
```
## 1.2 Install Node.js with NVM
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
source ~/.bashrc
nvm --version
nvm ls-remote
nvm install 20.19.2
nvm use 20.19.2
nvm alias default 20.19.2
node --version
npm --version
```

## 1.2.1 System library if trouble installing
```bash
sed: /tmp/.mount_VSCodi77hQMM/lib/x86_64-linux-gnu/libselinux.so.1: no version information available (required by sed)
xz: /tmp/.mount_VSCodi77hQMM/lib/x86_64-linux-gnu/liblzma.so.5: version `XZ_5.2' not found (required by xz)
```
then
```bash
sudo apt-get install -y liblzma5 libselinux1
```
or, close the code editor and install with the terminal, worked for me
```bash
foobar@Z999999999:~$ nvm use 22
Now using node v22.16.0 (npm v10.9.2)
foobar@Z999999999:~$ nvm --version
0.40.3
foobar@Z999999999:~$ npm --version
10.9.2
foobar@Z999999999:~$ node --version
v22.16.0
foobar@Z999999999:~$
```

## 1.3 Install Maven
```bash
sudo apt install maven
mvn --version
```

## 1.4 Install MySQL
```bash
sudo apt install mysql-server
sudo service mysql start
sudo mysql_secure_installation
# Answer yes to all prompts
sudo mysql -u root -p
CREATE DATABASE taskdb;
SHOW DATABASES;
EXIT;
echo "sudo service mysql start" >> ~/.bashrc
source ~/.bashrc
```

## 1.5 Install Angular CLI
```bash
npm install -g @angular/cli
ng --version
```
install per angular app
```
npm install --save-dev @angular/cli
```

# 2

## Project Structure:
```
my-angular-app/
├── angular.json
├── package.json
├── src/
│   ├── app/
│   ├── assets/
│   ├── environments/
│   ├── index.html
│   ├── main.ts
│   ├── styles.css
├── tsconfig.json
```

## 2.1 Angular Frontend
```bash
ng new my-angular-app
cd my-angular-app
npm install --save bootstrap jquery
ng generate component home
ng serve --port 5100 --open
```

## 2.2 Spring Boot Backend
```bash
cd my-spring-boot-app
./mvnw clean install
./mvnw spring-boot:run
```

## Dependencies in pom.xml:
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-rest</artifactId>
    </dependency>
    <dependency>
        <groupId>com.mysql</groupId>
        <artifactId>mysql-connector-j</artifactId>
        <scope>runtime</scope>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.18.36</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <scope>runtime</scope>
        <optional>true</optional>
    </dependency>
</dependencies>
```






# Java Spring

## /src/main/resources/application.properties
```bash
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/full-stack-ecommerce?useSSL=false&useUnicode=yes&characterEncoding=UTF-8&allowPublicKeyRetrieval=true&serverTimezone=UTC
spring.datasource.username=ecommerceapp
spring.datasource.password=ecommerceapp
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
spring.data.rest.base-path=/api
```



# Server and Port stuff
```bash
lsof -i :8080    # Check process on port 8080
kill -9 <PID>    # Kill process
sudo chown -R $USER:$USER .
sudo rm -rf target/
npm cache clean --force
```



# Git Repository Setup
```bash
mkdir my-docs
cd my-docs
git init
git remote add origin <your-repo-url>
git checkout newbranch
git add .
git commit -m "Add setup guide for WSL2"
git push -u origin main
```

# Access the Applications
* Angular: `http://localhost:4200` or `http://localhost:5100`
* Spring Boot: `http://localhost:8080`



### remove java version
* https://stackoverflow.com/questions/29964042/how-to-remove-old-version-of-java-and-install-new-version
```bash
ls /usr/local/java/
sudo apt-get purge openjdk-\*
```

### find java install path
list installed java versions
```
which java
ls -la /usr/bin/java
readlink -f $(which java)
update-java-alternatives -l
dpkg -l | grep java
```

### delete remove java
* search the entire filesystem `find / -name "java" 2>/dev/null`
```bash
sudo apt remove --purge openjdk-\*
sudo apt remove openjdk-11-jre openjdk-11-jdk
sudo update-alternatives --remove java /path/to/java/bin/java
sudo apt purge 'openjdk*'
sudo apt autoremove
sudo apt autoclean
```
