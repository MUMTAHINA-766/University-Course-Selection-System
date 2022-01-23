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

### User interfaces:

![login1](https://user-images.githubusercontent.com/64628178/150663766-025813b3-43a6-46be-a206-703f8b4dd648.PNG)

![course selection ui1](https://user-images.githubusercontent.com/64628178/150663771-0cf6378c-fe66-40a2-b8f5-c96184dbf032.PNG)

![ui course sel](https://user-images.githubusercontent.com/64628178/150663782-3e9d4f69-1176-4bd5-95d4-43e20fcc867f.PNG)

![sco1](https://user-images.githubusercontent.com/64628178/150663812-a96ada0b-c885-47a5-9533-1f67e86d2f1c.PNG)

![sco2](https://user-images.githubusercontent.com/64628178/150663818-3ecf9f19-1d41-4290-8185-68aa6a134e64.PNG)

![sco3](https://user-images.githubusercontent.com/64628178/150663822-54be6547-85a9-4841-8523-555cfd020413.PNG)

![sco4](https://user-images.githubusercontent.com/64628178/150663826-e8411353-5e1b-4a2f-951f-0c17072fee71.PNG)

![scoreUi](https://user-images.githubusercontent.com/64628178/150663841-f6cef0d2-0ca9-4c8d-ab4d-e8a2fdaf2d7c.PNG)

![ui withdraw](https://user-images.githubusercontent.com/64628178/150663870-54daf811-1c07-4096-8c2c-28794eeda8ad.PNG)

![create course ui](https://user-images.githubusercontent.com/64628178/150663878-51155b9e-3dbc-4e0d-a2e5-f2a580a0cbd1.PNG)

![create course ui1](https://user-images.githubusercontent.com/64628178/150663883-f705da1d-0b73-4d0f-bb4b-6861d09d28fe.PNG)

![create teacher1 UI](https://user-images.githubusercontent.com/64628178/150663898-93b78e2b-1041-4597-9169-1216eac750cc.PNG)

![create teacher2 UI](https://user-images.githubusercontent.com/64628178/150663905-a0016780-955b-4d12-a193-850657b73601.PNG)

![createClass1 UI](https://user-images.githubusercontent.com/64628178/150663918-72f4483e-94bd-4278-9d05-b66405427dba.PNG)

![createClass2 UI](https://user-images.githubusercontent.com/64628178/150663922-67abfb8a-8722-48a5-963f-785c8b584441.PNG)

![createClass3 UI](https://user-images.githubusercontent.com/64628178/150663925-970ab836-4af3-470e-a280-f61162d0f660.PNG)

![stim1](https://user-images.githubusercontent.com/64628178/150663938-3c29e3ca-d443-4edb-9731-f251b091a910.PNG)

![teacher table ui](https://user-images.githubusercontent.com/64628178/150663944-bb1f3eee-dc79-4f45-a157-0995467cec72.PNG)

![showScore UI](https://user-images.githubusercontent.com/64628178/150663959-0e0eb52b-dc4a-4eaf-b2c7-f9120ca8d61e.PNG)

![showClassfcourse UI1](https://user-images.githubusercontent.com/64628178/150663963-dfd675ca-e484-47ab-9a74-3e76d0a7e5d2.PNG)

![showClassfcourse UI2](https://user-images.githubusercontent.com/64628178/150663964-b2599d53-8d0f-4c58-9b39-c4e04cb77b0e.PNG)
