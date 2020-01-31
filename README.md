# Quarkus Quick Lab 

In this quick lab, you'll build and deploy a serverless application on the amazing Quarkus framework!

## Run and hack on a Quarkus project

Let's run a Quarkus project and play with it to get familiar with some basic commands and constructs!

### 0. Start Quarkus in Dev mode

    ```
    cd quarkus-quick-lab/
    ```

   ```
   ./mvnw quarkus:dev
   ```

> keep this running in a separate terminal window throughout this exercise!

### 1. View app in web browser
Go to http://localhost:8080/hello

### 2. Look at the code for the RESTful endpoint
Open this project in a Java editor/IDE

Open quarkus-quick-lab/src/main/java/org/example/exercise1/GreetingResource.java

### 3. Play around with hot-reloading 
Change the String in the last line:

```return "hello" ```

to something else. 

> Do not restart the anything, simply go to the web browser, and hit reload. Quarkus automatically loads your changes without restarting the app server!

### 4. Create an executable JAR file

   ```
   ./mvnw package
   ```
Then see what was produced, look into the target directory:

   ```
    // unix
   ls -l target

    // windows
    dir target
   ```

```
╰─ ls -1 target 
classes
exercise1-1.0-SNAPSHOT-runner.jar
exercise1-1.0-SNAPSHOT.jar
generated-sources
generated-test-sources
lib
maven-archiver
maven-status
quarkus
surefire-reports
test-classes
```

The *-runner is the file we can use to run the app!

### Run the application in standard mode

```
java -jar target/exercise1-1.0-SNAPSHOT-runner.jar 

```
Look for this on the first line:
" started in 0.663s. "

> Note how quickly this Quarkus application starts up!

### 4. Deploy as a serverless application!

#### Deploy your Quarkus app to the cloud!
 
In this exercise, we will run deploy your Quarkus project to IBM Cloud Functions and invoke it in the Cloud

> You will need an IBM Cloud Functions account (free) before starting on this exercise. 

If you haven't already done so, create and login to IBM Cloud Functions:

Do the setup here: [IBM Cloud Functions Setup](https://github.com/prpatel/Serverless-Workshop-Setup-All-Platforms)


#### Create an IBM Cloud function with this code

``` 
# from the quarkus-quick-lab/ folder
ibmcloud fn action create quarkustest target/exercise1-1.0-SNAPSHOT-runner.jar --docker prpatel/openwhisk-quarkus --web true
```

This creates the cloud function, passes in the jar source code, and uses a special Apache OpenWhisk container for easy Quarkus deployments. It is different than how we normally architect OpenWhisk / IBM Cloud Functions - it uses a URI proxy based approach. Your instructor can discuss this in detail if you wish.

Once the above command succeeds, get the URL for it by issuing this command:

```
ibmcloud fn action get quarkustest --url 
```

This should return something like this:

```
https://us-south.functions.cloud.ibm.com/api/v1/web/...../default/quarkustest/hello
```

> Make sure you add the endpoint, in the example above "hello", to the end of the URI

## Congrats! You've built and deployed a Quarkus app!

