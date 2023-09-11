Tutorial Reference: https://docs.oracle.com/javase/tutorial/deployment/jar/intro.html

1. Compile classes.
    ```bash
    javac app/*.java
    ```

2. Create unsigned jar.
    ```bash
    jar cfe unsigned.jar app.Main app/Life.class app/Main.class
    ```

3. Create certifcate for signing.
    1. Create keystore.
        ```bash
        keytool -genkey -alias server -keyalg RSA -keypass password -storepass password -keystore keystore.jks
        ```
        > Creates `keystore.jks` file.
    2. Create certificate.
        ```bash
        keytool -export -alias server -storepass password -file server.cer -keystore keystore.jks
        ```
        > Creates `server.cer` file.

4. Sign jar.
    ```bash
    jarsigner -keystore keystore.jks -signedjar signed.jar unsigned.jar server
    ```
    > Creates `signed.jar` file.
    > Password is `password` when prompted.

5. Verify jar.
    ```bash
    jarsigner -verify signed.jar
    ```

6. Tamper with jar and verify.
