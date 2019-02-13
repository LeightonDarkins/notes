# General Notes

## Java 11 PSS Build

General

- Install JDK 11
- Install JavaFX 11

In IDEA:

- CMD + ;
- "Modules"
- "nm-trunk"
- "dependencies"
- "+" or CMD + N
- "JARs or directories"
- /path/to/JavaFX/lib

## Tomcat 8.5 Install

- Download zip from: https://tomcat.apache.org/download-80.cgi#8.5.37
- Extract and put somewhere
- CD to where you put it
- `chmod a+x ./bin/catalina.sh`
- `./bin/catalina.sh start`
- open `localhost:8080`

### Add Tomcat User

- `/path/to/tomcat/conf/tomcat-users.xml`
- create role `<role rolename="manager-gui"/>`
- create user with role and password `<user username="tomcat" password="tomcat" roles="manager-gui"/>`

### PSS Exploded WAR

- `path/to/tomcat/conf/Catalina/localhost/`
- create file `pss.xml`
- with content
  - `<?xml version="1.0" encoding="UTF-8"?><Context docBase="/Users/leightondarkins/Code/telus/emr/build/artifacts/pss" path="/pss" reloadable="true" workDir="/Users/leightondarkins/code/tomcat/work/Catalina/localhost/pss"><Logger className="org.apache.catalina.logger.SystemOutLogger" timestamp="true" verbosity="4" /></Context>`
- adjust the doc base to point to the correct artifact directory

### Get PSS Compile Output Into WAR

- `emr/out/production/nm-trunk`
- copy ALL the things...
