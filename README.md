JENKINS

1)	Eclipse -> file -> new ->  project -> java_project -> finish
2)	Right_click_project -> class -> finish
3)	Enter code (some basic java code)
4)	Right_click_class -> run as -> java application
5)	After running -> right click project -> team -> share
6)	Create git hub repository
7)	Then again right click project -> team -> commit  X
8)	Then again right click project -> team -> remote -> push -> master -> add spec ->finish
9)	It will ask username (ShrriVarshsan) and password (password token access & classic)
10)	Then code will be pushed to git
11)	Go to Jenkins -> new item -> free style project -> ok
12)	Scroll to source code management -> select git ->paste repo URL 
13)	Scroll build steps -> Execute Shell or execute window bath command
    
#!/bin/bash
cd "$WORKSPACE"
mkdir -p bin
javac -d bin src/com/example/code.java
java -cp bin com.example.code



KUBERNATES

Open killercoda -> https://killercoda.com/playgrounds/scenario/kubernetes

kubectl get nodes

kubectl create deployment webapp --image=nginx

kubectl get pods

kubectl scale deployment webapp --replicas=3

kubectl get pods

kubectl expose deployment webapp --type=NodePort --port=80

kubectl get svc

nano limited.yaml

apiVersion: v1
kind: Pod
metadata:
##name: limited-pod
spec:
##containers:
##- name: nginx
####image: nginx
####resources:
######limits:
########cpu: "500m"
########memory: "128Mi"

For code -> paste -> ctrl x -> y -> enter

kubectl apply -f limited.yaml

kubectl get pods

kubectl describe pod limited-pod

kubectl get all


MAVEN

1)	File -> new -> maven project
a.	Group id:com.bank
b.	Artifactid:BankingMavenJUnit
c.	Version:1.0
2)	Paste pom.xml code
3)	Then create src/main/java -> package(com.bank) -> class(BankService)
4)	Then create src/test/java -> package(com.bank) -> class(BankServiceTest)
5)	Whole project right click -> run as -> Maven test


Pom.xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         https://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <groupId>com.bank</groupId>
    <artifactId>BankingMavenJUnit</artifactId>
    <version>1.0</version>

    <dependencies>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>5.10.0</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.1.2</version>
            </plugin>
        </plugins>
    </build>

</project>

BankService.java

package com.bank;

public class BankService {

public boolean transfer(double balance, double amount) {

if (balance >= amount && amount > 0) {
return true;
}

return false;
}
}

BankServiceTest.java

package com.bank;

import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

public class BankServiceTest {

@Test
public void validTransferTest() {

BankService service = new BankService();

int result = service.transfer(1000, 500) ? 1 : 0;

assertEquals(1, result);
}

@Test
public void invalidTransferTest() {

BankService service = new BankService();

int result = service.transfer(200, 500) ? 1 : 0;

assertEquals(0, result);
}
}



BUGZILLA

1)	File -> other -> spring -> spring starter project
a.	Name – demo 6
b.	Type – maven
2)	Add spring web -> finish
3)	Click -> src/main/java -> com.example.demo -> right click -> new class(HomeController) -> paste code
4)	Right click -> Demo6Application -> run as spring boot
5)	Open -> Bugzilla.mozilla.org -> new bug -> firefox -> version (unspecified)
6)	Enter -> home page not loading -> click Not listed
7)	Fill detail -> tick this is defect

HomeController.java

package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HomeController {

@GetMapping("/")
public String home() {
return "Application Running Successfully";
}
}

Step 7: Enter details

Example:

Field Value
Summary Home page not loading
Description Output not showing
Steps Open localhost:8080
Expected Proper message
Actual Wrong output
