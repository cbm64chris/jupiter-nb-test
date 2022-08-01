# jupiter-nb-test

Recording shows first attempting to run the a focused test method from the inline control and then from the context menu where only junit-jupiter-api is on the class path coupled with 2.20 of surefire.
Upon adding junit-jupiter-engine to the classpath the tests execute as expected from the control. The messages at the bottom of the screen indicate an inappropriate surefire or missing junit4.


https://user-images.githubusercontent.com/20171342/182127717-bd599fbf-f5a9-49fe-aa9c-31dffd473119.mov


Appreciating this is an edge case and could be described as a misconfigured dependency tree, it could lead to confusion given the tests will run from the CLI.

The correct dependency is junit-jupiter not the api because it transitively includes the engine.

``` XML
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>5.8.2</version>
            <scope>test</scope>
        </dependency>
```

The current NetBeans context menu Navigate->Go to Test/Tested Class will add the API, Enginer and Params dependencies, if not present not the the parent dependency, as above.

``` XML
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>5.6.0</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-params</artifactId>
            <version>5.6.0</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <version>5.6.0</version>
            <scope>test</scope>
        </dependency>
```






