
# Multi-Tier Java-MySQL Application Demo

## 1. Create a Virtual Machine
- Create a Virtual Machine with **Ubuntu LTS** version on your preferred cloud provider.
- Run the following commands to install the necessary packages:

   ```bash
   # Update the package manager
   sudo apt update

   # Install Java 17
   sudo apt install openjdk-17-jre-headless -y

   # Install Maven
   sudo apt install maven

   # Install net-tools
   sudo apt install net-tools -y
   ```

---

## 2. Clone the Repository
- Clone the project repository into the virtual machine:
   ```bash
   git clone https://github.com/SudheerKumarP0357/multi-tier-java-mysql.git
   ```

---

## 3. Set Up MySQL Server
- Install and set up MySQL Server by running the following commands:

   ```bash
   sudo apt update
   sudo apt install mysql-server -y

   # Log in as the root user
   sudo mysql -u root
   ```

### MySQL Configuration
- Once logged in as the root user, execute the following queries in the MySQL command line to configure the database:

   ```mysql
   ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Test@123'; 
   FLUSH PRIVILEGES;

   CREATE DATABASE bankappdb;
   SHOW DATABASES;
   exit;
   ```

   **Note:** If you wish to change the password, replace `Test@123` with your preferred password.

### Verify MySQL Service
- Ensure that the MySQL server is running on **PORT 3306** by executing:
   ```bash
   sudo netstat -tuln | grep 3306
   ```

### Update `application.properties`
- If you changed the MySQL password from `Test@123`, update the password in the `application.properties` file located in the `src/main/resources/` directory.

---

## 4. Build the Java Application
### Maven Lifecycle
Maven follows a specific build lifecycle. Below is a quick reference for Maven lifecycle commands. The commands at the bottom depend on the execution of the commands above:

   ```text
   mvn validate
   mvn compile
   mvn test
   mvn package
   mvn verify
   mvn install
   mvn deploy
   ```

### Build the Artifact
- Navigate to the project directory where the `pom.xml` file is located. This directory also contains the `src` and `test` folders.
- Run the following command to build the `.jar` artifact:
   ```bash
   mvn package
   ```
   - To skip running tests, use:
     ```bash
     mvn package -DskipTests=true
     ```
- Verify that a `target` directory has been created and contains the `.jar` file.

---

## 5. Run the Application
- Use the following command to run the application:
   ```bash
   java -jar ./target/*.jar
   ```
   **Note:** Replace `*.jar` with the exact name of your generated `.jar` file.

---

## 6. Browse the Application
- Once the application is running, open a web browser and navigate to the following URL:
   ```
   http://<VM_IP>:<APPLICATION_PORT>
   ```
   Replace `<VM_IP>` with the public IP address of your virtual machine and `<APPLICATION_PORT>` with the port on which your application is running (default is typically `8080`).

- Example:
   ```
   http://192.168.0.1:8080
   ```

---
## Additional Notes
- Ensure all dependencies are correctly configured in `pom.xml`.
- Verify database connectivity before running the application.
- For any issues, review the logs and ensure the MySQL server and application configurations are aligned.

--- 
