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

### PSS Compiler Args (for 11 JVM)

"java compiler -> compilation options (for nm-trunk)" in IDEA settings

- --add-exports=java.rmi/sun.rmi.server=ALL-UNNAMED
- --add-exports=java.desktop/sun.swing=ALL-UNNAMED
- --add-exports=java.desktop/sun.print=ALL-UNNAMED

### Elastic Search Tasks

- add new jars, address compiler issues (unit testing)
- Lucene Transform: do we need this anymore?
- ElasticSearch/Index/Store/FS: related to Lucene-Transform? (remove if item above is no longer needed)

- create/validate/recreate index on startup

- deployment/config (without docker)

- deployment/config (with docker)

- shareback/documentation

### ElasticSearch Libs

- guava v16 ???

### ElasticSearch Code Changes

#### FieldIndex .not_analyzed

- `@Field(type=FieldType.String index=FieldIndex.not_analyzed)` is now `@Field(type=FieldType.Keyword)`
  - https://stackoverflow.com/questions/45406577/how-to-config-not-analyzed-with-field-annotation-in-spring-data-elasticsearch-3
  - https://www.elastic.co/guide/en/elasticsearch/reference/5.5/breaking_50_mapping_changes.html

#### @NestedField

- `@NestedField()` is now `@InnerField()`
  - [commit where the change was made](https://github.com/spring-projects/spring-data-elasticsearch/commit/61880671a45e6c25d751bd50737647fc84c7306a#diff-864bb378fdcbab1d7233f1943b59177d)

#### FieldIndex .no

- anywhere you see `FieldIndex.no` now should be `false` i.e. this field cannot be searched
- `@Field(type=FieldType.Long, index=FieldIndex.no)` is now `@Field(type=FieldType.Long, index=false)`
  - [commit where INDEX was changed from an ENUM to a BOOLEAN](https://github.com/spring-projects/spring-data-elasticsearch/commit/089d7746be2f2fc4a395bd5c814f664729121f21#diff-864bb378fdcbab1d7233f1943b59177d)

## Outcomes Questions

### Entry Points?

    - know where to look
    - what to expect

#### 16640

RiskFactorCategoryBuilder.java
RFAlcoholResourceItem.java

#### 23289

UserManager
getActiveDoctors

### General?

pss.properties file
add a value
com.pss.outcomes.IsODA = true

OutcomesDashboardModule.java

In the UI
Reports -> Outcomes Dashboard
??? -> Scheduled Reports Setup

    Record Window
      Settings
        EditMeasureDefinitions
          Measure == group of metrics
          Metric == search

    Records Window
      Edit Searches
        outcomes have the guage icon

    Records Window
      Add Search Criterion
        wysiwyg query editor
        stores the values, the generates SQL on demand

### 16388

in scope?
big change?
might just be changing some API?

CriterionSearchImportExportHelper

toolbars == custom form

Records -> Settings -> Edit Custom Forms

### 21415

- seems simple
- TableSearch.java
  - changing this seems scary
- SearchReportTableSearch.java
  - this could be what we need
- SearchReport.java
  - something to do here?

OutcomesDashboardPresenter.java??
somehow meaningful

### 20736 / 23193 / 16792

- doing this "per-physician" may not ahve any effect
- issue are more likely to be realted to like's and wildcards

### 22730

- basically a project, not some small thing
- there's an epic for this
