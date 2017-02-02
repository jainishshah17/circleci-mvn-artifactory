#Artifactory Integration with Travis-CI using Maven Artifactory Plugin

## Build Status

[![Circle CI](https://circleci.com/gh/jainishshah17/circleci-mvn-artifactory/tree/master.svg?style=svg)](https://circleci.com/gh/jainishshah17/circleci-mvn-artifactory/tree/master)

`To make this integration work you will need to have running Artifactory-pro/Artifactory SAAS/Artifactory Enterprise which is acccessible form outside.`

##Steps to Integrate Circle CI with Artifactory.

Step 1:

copy `circle.yml` file to your project.

Step 2:

Configure artifactory-maven-plugin to your project by copying following to your pom.xml:
```
            <plugins>
                        <plugin>
                            <groupId>org.jfrog.buildinfo</groupId>
                            <artifactId>artifactory-maven-plugin</artifactId>
                            <version>2.4.1</version>
                            <inherited>false</inherited>
                            <executions>
                                <execution>
                                    <id>build-info</id>
                                    <goals>
                                        <goal>publish</goal>
                                    </goals>
                                    <configuration>
                                        <deployProperties>
                                            <gradle>awesome</gradle>
                                        </deployProperties>
                                        <artifactory>
                                            <includeEnvVars>true</includeEnvVars>
                                            <timeoutSec>60</timeoutSec>
                                            <propertiesFile>publish.properties</propertiesFile>
                                        </artifactory>
                                        <publisher>
                                            <contextUrl>https://gcartifactory-us.jfrog.info/artifactory</contextUrl>
                                            <username>${username}</username>
                                            <password>${password}</password>
                                            <excludePatterns>*-tests.jar</excludePatterns>
                                            <repoKey>libs-release-local</repoKey>
                                            <snapshotRepoKey>libs-snapshot-local</snapshotRepoKey>
                                        </publisher>
                                        <buildInfo>
                                            <buildName>circle-ci-demo</buildName>
                                            <buildNumber>${buildNumber}</buildNumber>
                                            <buildUrl>${buildUrl}</buildUrl>
                                        </buildInfo>
                                        <licenses>
                                            <autoDiscover>true</autoDiscover>
                                            <includePublishedArtifacts>false</includePublishedArtifacts>
                                            <runChecks>true</runChecks>
                                            <scopes>compile,runtime</scopes>
                                            <violationRecipients>build@organisation.com</violationRecipients>
                                        </licenses>
                                    </configuration>
                                </execution>
                            </executions>
                        </plugin>
            </plugins>   
```

Edit the pom.xml file and set the value of the *contextUrl* with your Artifactory URL, as well as the other Artifactory properties.
For more configuration information see the [Maven Artifactory Plugin documentation](https://www.jfrog.com/confluence/display/RTF/Maven+Artifactory+Plugin).
          
               
Step 3:

Enable your project in CircleCI.

![screenshot](img/Screen_Shot1.png)

Step 4:

add Environment Variables ARTIFACTORY_USERNAME and ARTIFACTORY_PASSWORD in build settings of CircleCI.

![screenshot](img/Screen_Shot2.png)

Step 5:

You should be able to see published artifacts and build info in artifactory.

![screenshot](img/Screen_Shot3.png)

---
## Plugin documentation

The full plugin documentation is available [here](https://www.jfrog.com/confluence/display/RTF/Maven+Artifactory+Plugin).







# Maven Artifactory Plugin

## Overview

This example is using the Maven Artifactory Plugin for artifacts abd build-info deployment to Artifactory. 

## Running this example

To run this example, please do the following:
* Edit the pom.xml file and set the value of the *contextUrl* with your Artifactory URL, as well as the other Artifactory properties.
For more configuration information see the [Maven Artifactory Plugin documentation](https://www.jfrog.com/confluence/display/RTF/Maven+Artifactory+Plugin).
* CD to the project directory and run the following command (replace *admin* and *password* with your Artifactory credentials):
```console
> mvn deploy -Dusername=admin -Dpassword=password
```

This would deploy the produced artifacts to the configured Artifactory server:

```console
 [INFO] Artifactory Build Info Recorder: Saving Build Info to 'C:\dev\project-examples\artifactory-maven-plugin-example\target\build-info.json'
 [INFO] Deploying artifact: http://localhost:8081/artifactory/libs-snapshot-local/org/jfrog/test/multi3/2.17-SNAPSHOT/multi3-2.17-SNAPSHOT.war
 [INFO] Deploying artifact: http://localhost:8081/artifactory/libs-snapshot-local/org/jfrog/test/multi3/2.17-SNAPSHOT/multi3-2.17-SNAPSHOT.pom
 [INFO] Deploying artifact: http://localhost:8081/artifactory/libs-snapshot-local/org/jfrog/test/multi/2.17-SNAPSHOT/multi-2.17-SNAPSHOT.pom
 [INFO] Deploying artifact: http://localhost:8081/artifactory/libs-snapshot-local/org/jfrog/test/multi1/2.17-SNAPSHOT/multi1-2.17-SNAPSHOT.jar
 [INFO] Deploying artifact: http://localhost:8081/artifactory/libs-snapshot-local/org/jfrog/test/multi1/2.17-SNAPSHOT/multi1-2.17-SNAPSHOT.pom
 [INFO] Artifactory Build Info Recorder: Skipping the deployment of 'org/jfrog/test/multi1/2.17-SNAPSHOT/multi1-2.17-SNAPSHOT-tests.jar' due to the defined include-exclude patterns.
 [INFO] Deploying artifact: http://localhost:8081/artifactory/libs-snapshot-local/org/jfrog/test/multi1/2.17-SNAPSHOT/multi1-2.17-SNAPSHOT-sources.jar
 [INFO] Deploying artifact: http://localhost:8081/artifactory/libs-snapshot-local/org/jfrog/test/multi2/2.17-SNAPSHOT/multi2-2.17-SNAPSHOT.jar
 [INFO] Deploying artifact: http://localhost:8081/artifactory/libs-snapshot-local/org/jfrog/test/multi2/2.17-SNAPSHOT/multi2-2.17-SNAPSHOT.pom
 [INFO] Artifactory Build Info Recorder: Deploying build info ...
 [INFO] Deploying build descriptor to: http://localhost:8081/artifactory/api/build
 [INFO] Build successfully deployed. Browse it in Artifactory under http://localhost:8081/artifactory/webapp/builds/plugin-demo/1
```

## Sending parameters to the pom file

You can send parameters as system properties, and then use them inside the pom file, the same way the *username* and *password*
properties are sent as shown above.

## Plugin documentation

The full plugin documentation is available [here](https://www.jfrog.com/confluence/display/RTF/Maven+Artifactory+Plugin).


##Circle CI
