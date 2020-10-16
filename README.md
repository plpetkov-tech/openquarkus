# Openquarkus project

This project uses Quarkus, the Supersonic Subatomic Java Framework.

If you want to learn more about Quarkus, please visit its website: https://quarkus.io/ .
## This project is intended for training and demo purposes using Openshift and Quarkus
### Steps followed
1. ```mvn build```
2. ``` oc new-build --strategy docker --dockerfile - --code . --name openquarkus-java11-v2 < src/main/docker/Dockerfile.jvm   ```
3. ``` oc start-build --from-dir . openquarkus-java11-v2    ```
4. ``` oc new-app --image-stream projectName/openquarkus-java11-v2:latest --name openquarkus-java11-v2 
5. ``` oc expose svc/openquarkus-java11-v2 ```
6. To view the details : ``` oc describe route openquarkus-java11-v2 ```

### Steps for the webhook 
1. ```ultrahook granhook https://internal-openshift-hook-url/```
2. With above command we get the external hook url and we just need to set it in GitHub
3. Now everytime we push, is going to initiate a build in Openshift

## Running the application in dev mode

You can run your application in dev mode that enables live coding using:
```
./mvnw quarkus:dev
```

## Packaging and running the application

The application can be packaged using `./mvnw package`.
It produces the `openquarkus-1.0-SNAPSHOT-runner.jar` file in the `/target` directory.
Be aware that it’s not an _über-jar_ as the dependencies are copied into the `target/lib` directory.

The application is now runnable using `java -jar target/openquarkus-1.0-SNAPSHOT-runner.jar`.

# Openshift commands and steps

## Creating a native executable

You can create a native executable using: `./mvnw package -Pnative`.

Or, if you don't have GraalVM installed, you can run the native executable build in a container using: `./mvnw package -Pnative -Dquarkus.native.container-build=true`.

You can then execute your native executable with: `./target/openquarkus-1.0-SNAPSHOT-runner`

If you want to learn more about building native executables, please consult https://quarkus.io/guides/building-native-image.
