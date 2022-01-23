Course Selection System
# java-server

## Environment requirements

- java 11
- mysql 8
- redis 5.0.12

Create mysql and redis via docker
Consider using [docker-compose.yml] (resources/javaAppContainer/docker-compose.yml) to start mysql and redis

## Database Initialization (MYSQL)

1. Create a library
```sql
CREATE USER 'appBase'@'%' IDENTIFIED BY 'appBase';
CREATE DATABASE appBase DEFAULT CHARACTER SET utf8mb4;
GRANT ALL PRIVILEGES ON appBase.* TO appBase@'%';
CREATE DATABASE appBase_test DEFAULT CHARACTER SET utf8mb4;
GRANT ALL PRIVILEGES ON appBase_test.* TO appBase@'%';
FLUSH PRIVILEGES;
```
2. Initialize the underlying table
   2.1 Start liquibase, liquibase, enable:true
   2.2 Via jpa, enable application-base.yml, generate-ddl:true, ddl-auto:update
   
3. Initialize the default user
```sql
INSERT INTO t_sys_organization (created_date, last_modified_date, parent_id, name, code, sort, enabled) VALUES (DEFAULT, DEFAULT, DEFAULT, 'Yunnan Branch', null, null, DEFAULT);
INSERT INTO t_sys_user (created_date, last_modified_date, email, enabled, organization_id, organization_name, sort, password, username, name, title, tags, credentials_non_expired, account_non_locked, account_non_expired, credentials_expired_date, account_expired_date) VALUES (DEFAULT, DEFAULT, null, DEFAULT, 1, 'Yunnan Branch', null, '{noop}123456', 'admin', 'System Administrator', 'Background', 'Admin', DEFAULT, DEFAULT, DEFAULT, null, null);
```
## Project structure
1. Common infrastructure and common features
   1.1 Data abstract dao and conform to the query constructor
   1.2 Controller, service type and controller and service base class (currently some parameters require constructor injection)
2.sys.controller Login controller
   2.1 Replace the return structure after login in the sampleLogin of AuthenticationSuccessHandlerImpl. 
3. Education an instance package with no actual functionality. Can be deleted 
   3.1 Currently only a few base classes for the project support jpa generation. Other entities only do liquibase configuration.

## Development Instructions
1. Encoding assist, a lot of use of lookok to assist get, set and so on generation. Plugin support required.

## Packaging
1. Packaging 
   1.1 Format correction, run mvn spring-javaformat:apply formatting code. 
   1.2 Or comment pom.xml, plugins->io.spring.javaformat
   1.3 mvn package

## Code Formatting Specification

The code specification used in this project is adapted to the Spring Framework code format conventions.

The formatting profile format is eclipse format, and some styles and configuration files may be inconsistent when using formatting after idea import. Therefore, ide does not require that configuration files must be imported

Use the maven command in the project to format code directly,

```
mvn spring-javaformat:apply
```

So as long as the formatted configuration of the ide does not cause too many obstacles to its own development

Originally, it was considered to integrate formatting with git hooks, but after formatting, you need to rerun git add to add the formatted code to the scratchpad, but this may lead to the destruction of code that you did not want to commit. So for the time being, run the format manually

## Configuration file

1. Compile-time configuration: --spring.profiles.active=local
2. Runtime select configuration: --spring.config.location=/config/application.yml

## Generate offline documentation

Run the test of 'io.naccoll.boilerplate.DocumentationTest'

```bash
mvn swagger2markup:convertSwagger2markup 
mvn asciidoctor:process-asciidoc 
mvn package
```

Last build file location: 1
`target/generated-docs/index.html`

# hello_vue_2

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).



