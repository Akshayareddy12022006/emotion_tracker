KESHAV MEMORIAL INSTITUTE OF TECHNOLOGY
(AN AUTONOMOUS INSTITUTE)
Accredited by NBA & NAAC, Approved by AICTE, Affiliated to JNTUH, Hyderabad
A.Y 2025-2026
Department of Computer Science & Engineering (DS)

Lab Internal I - Software Engineering
Subject Code: 23CC501PC
Year/Sem: III/I
Branch/Section: CSD-B
Faculty: Y Deepthi
Lab Internal: 10/09/2025

SET-1

---

Part I – Software Requirement Specification (SRS) \[10 Marks]

1. Purpose / Abstract:
   Question: Write a detailed purpose and abstract for an Online Food Ordering System (OFOS) that explains why the system is needed, what problems it solves, and the benefits to customers and restaurant staff.
   Answer: The purpose of the Online Food Ordering System (OFOS) is to automate and streamline the process of browsing menus, placing food orders, making payments, and tracking deliveries in a restaurant environment. It addresses common problems like manual order errors, delayed deliveries, lack of payment options, and inefficient order management. The system benefits customers by providing convenience, faster ordering, multiple payment options, and real-time order status updates. For restaurant staff, it simplifies order handling, reduces errors, and improves delivery management.

2. Functional Requirements:
   Question: List and explain the key functional features the OFOS should include to solve common restaurant and customer problems.
   Answer:

* Menu browsing: Customers can view detailed menu items with images, descriptions, and prices.
* Food ordering: Users can add items to a cart, modify quantities, and place orders.
* Online payments: Secure integration with payment gateways for credit/debit cards and wallets.
* Order status tracking: Real-time updates on order preparation, dispatch, and delivery.
* User account management: Profile management, order history, and favorite items.

3. Non-Functional Requirements:
   Question: Describe how the system should behave in terms of performance, security, usability, scalability, and availability.
   Answer:

* Usability: Intuitive and user-friendly interface for all users.
* Performance: Fast response times even with hundreds of concurrent users.
* Security: Secure login, encrypted payments, role-based access for staff and admins.
* Scalability: Capable of handling increasing number of users and orders.
* Availability: High uptime to ensure system accessibility 24/7.

4. Users and Interaction:
   Question: Identify all types of users and explain their interaction with the system.
   Answer:

* Customer: Browses menu, places orders, makes payments, and tracks delivery.
* Restaurant Staff: Updates menu items, manages incoming orders, and tracks delivery.
* Admin: Oversees system configuration, user management, and monitors performance.

5. Modules:
   Question: Break the OFOS into logical modules and explain each module's function.
   Answer:

* Menu Module: Handles creation, update, and display of menu items.
* Order Module: Manages order placement, cart functionality, and order tracking.
* Payment Module: Processes payments securely through integrated gateways.
* Delivery Tracking Module: Monitors the status and location of orders.
* User Management Module: Manages customer and staff accounts and permissions.

---

Part II – Maven Web Application Development \[25 Marks]

1. Fix pom.xml dependency errors:
   Question: The project fails to build due to missing or incorrect dependencies. How would you fix the pom.xml?
   Answer: Ensure all required <dependencies> are listed correctly, <packaging> is set to war, and Maven compiler plugin is configured for Java 17.

2. Update Maven configuration for Java 17:
   Question: How do you update a Maven project that runs on Java 8 to Java 17?
   Answer: In pom.xml, set:
   \<maven.compiler.source>17\</maven.compiler.source>
   \<maven.compiler.target>17\</maven.compiler.target>

3. Force Maven to update dependencies:
   Question: Your local Maven cache has old versions. How do you force Maven to update dependencies?
   Answer: Run command: mvn clean install -U

4. Skip tests during Maven build:
   Question: Tests take too long. How can you skip them?
   Answer: Command: mvn clean package -DskipTests
   Or set in pom.xml: <skipTests>true</skipTests>

5. Resolve dependency conflict:
   Question: Maven shows conflicting versions. How do you resolve it?
   Answer: Use <dependencyManagement> to specify versions or exclude duplicates using <exclusions>.

6. Add JSTL support for JSP pages:
   Question: Which Maven dependency adds JSTL support?
   Answer:

   <dependency>

<groupId>javax.servlet</groupId> <artifactId>jstl</artifactId> <version>1.2</version> </dependency>

---

Part III – Git & GitHub Integration \[15 Marks]

1. Initialize Git repo and push to GitHub:
   Question: The project is not under version control. How do you start using Git and push to GitHub?
   Answer:

* git init
* git add .
* git commit -m "Initial commit"
* git remote add origin <repo-URL>
* git push -u origin main

2. Fix incorrect commit message:
   Question: You wrote “Added Payement Module” instead of “Added Payment Module”. How to correct it?
   Answer:

* git commit --amend -m "Added Payment Module"

3. Check modified files:
   Question: How to see uncommitted changes?
   Answer: git status

4. View commit history compactly:
   Question: How to quickly see a compact log?
   Answer: git log --oneline

5. Recover deleted file before commit:
   Question: You deleted menu.jsp by mistake. How to restore?
   Answer: git checkout -- menu.jsp

6. Clone and switch branch:
   Question: How to clone a teammate’s repo and switch to a branch?
   Answer:

* git clone <repo-url>
* cd <repo-folder>
* git checkout feature-payment

---

Part IV – Git Collaboration, Patch & Merge Conflict \[20 Marks]

1. Create and switch branch:
   Question: You are assigned to add a delivery tracking feature without affecting main code. How?
   Answer: git checkout -b feature/delivery

2. List all branches:
   Question: How to see all local and remote branches?
   Answer: git branch -a

3. Delete local branch safely:
   Question: Wrong branch created. How to delete it?
   Answer: git branch -d feature/delivery

4. Create a patch file:
   Question: Bug in OrderServlet.java. How to create patch?
   Answer: git diff > bugfix.patch

5. Apply a patch:
   Question: Teammate sent a patch. How to apply?
   Answer: git apply bugfix.patch

6. Combine multiple commits:
   Question: How to squash commits before pushing?
   Answer: git rebase -i HEAD\~n (replace n with number of commits)

7. Clone repository:
   Question: How to make a local copy of remote repository?
   Answer: git clone <repo-url>

---

Part V – Dockerization \[15 Marks]

1. Dockerfile to build OFOS:


FROM maven:3.8.7-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

FROM tomcat:9.0
COPY --from=build /app/target/OFOS.war /usr/local/tomcat/webapps/OFOS.war
EXPOSE 8080
CMD ["catalina.sh", "run"]


2. Build and run container:

* docker build -t ofos-app .
* docker run -p 8080:8080 ofos-app
* Access: [http://localhost:8080/OFOS](http://localhost:8080/OFOS)

3. Push image to Docker Hub:

* docker tag ofos-app username/ofos-app\:v1
* docker push username/ofos-app\:v1

---

Part VI – Docker Compose Multi-Container Setup \[15 Marks]

1. docker-compose.yml:


version: '3.8'
services:
  ofos-app:
    image: username/ofos-app:v1
    ports:
      - "8080:8080"
    depends_on:
      - db

  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: ofos_db
      MYSQL_USER: ofos_user
      MYSQL_PASSWORD: ofos_pass
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:


2. Run containers:

* docker-compose up --build

3. Rebuild service after changes:

* docker-compose up --build --force-recreate

4. Verify data persistence:

* Insert orders → restart containers → check data remains in database

5. Stop containers but keep data:

* docker-compose down

* //divya
* KESHAV MEMORIAL INSTITUTE OF TECHNOLOGY
(AN AUTONOMOUS INSTITUTE)
Accredited by NBA & NAAC, Approved by AICTE, Affiliated to JNTUH, Hyderabad
A.Y 2025-2026
Department of Computer Science & Engineering (AI\&ML)

Lab Internal I – Set 1
Subject Name: Software Engineering
Subject Code: 23CC505PC
Year/Semester: III / I
Duration: 5 hrs | Max Marks: 100
Faculty: Dr. PATIL YOGITA DATTATRAYA
Location: 508

---

Q1. Online Learning Platform

1. Abstract (3 Marks)
   The problem is to develop an online learning platform for students, teachers, and administrators. Students can enroll in courses, submit assignments, take quizzes, and track their progress. Teachers can create and manage courses, upload materials, and assess students. Administrators manage users and oversee platform security and performance. The platform aims for efficient, scalable, and user-friendly learning.

2. Functional Requirements (2 Marks)

* User registration and authentication (students, teachers, admins).
* Course creation, modification, and deletion by teachers.
* Enrollment management for students.
* Upload/download of course materials.
* Online quizzes, assignments, and grading.
* Notifications for deadlines and updates.

3. Non-Functional Requirements (3 Marks)

* Performance: Handle multiple concurrent users efficiently.
* Security: Secure authentication and encrypted data storage.
* Scalability: Add more courses and users without performance issues.
* Usability: Simple, intuitive interface.
* Availability: Accessible 24/7 with minimal downtime.

4. Users (2 Marks)

* Students: Access courses, submit assignments, participate in quizzes.
* Teachers: Create courses, upload materials, grade students.
* Administrators: Manage users, oversee platform operations, ensure security.

---

Q2. Maven Project Building (30 Marks)

Step-by-Step Instructions:

1. Clone the Project

* Method I (Eclipse):

  * File → Import → Git → Projects from Git → Clone URI → Next
  * Enter: [https://github.com/anujyog1/flightrepo.git](https://github.com/anujyog1/flightrepo.git) → Next
  * Select branch main → Next → Choose local folder → Finish
* Method II (Git Bash):
  git clone [https://github.com/anujyog1/flightrepo.git](https://github.com/anujyog1/flightrepo.git)

  * Open Eclipse: File → Open Projects from File System → Browse cloned folder → Finish

2. Resolve Dependencies

* Open pom.xml → Right-click → Maven → Update Project → OK

3. Build Project

* Right-click project → Run As → Maven build → Goals: clean install
* Verify WAR/JAR in target/ folder

---

Q3. Git & GitHub (30 Marks)

**Step-by-Step Instructions and Commands:**

1. Initialize Git and Add Files (5 Marks)

```bash
git init
git add .
git commit -m "Initial commit"
```

2. Set Global Config and Push to GitHub (5 Marks)

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git remote add origin <GitHub URL>
git push -u origin main
```

3. SQB (10 x 2 Marks = 20 Marks)

* **a. Create new feature branch and push**

```bash
git checkout -b feature/search_flights_by_airline
git add .
git commit -m "Add flight search by airline"
git push -u origin feature/search_flights_by_airline
```

* **b. Incorporate updates from main to another branch**

```bash
git checkout main
git pull origin main
git checkout paymentintegration
git merge main
```

* **c. Resolve merge conflict in login.jsp**

  * Open login.jsp, remove conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) manually.

```bash
git add login.jsp
git commit -m "Resolved merge conflict in login.jsp"
```

* **d. Delete a branch locally and remotely**

```bash
git branch -d search_flights_by_airline  # local deletion
git push origin --delete search_flights_by_airline  # remote deletion
```

* **e. Push modifications to BookingRegister.jsp**

```bash
git add BookingRegister.jsp
git commit -m "Updated BookingRegister.jsp"
git push
```

* **f. Clone repository for a new developer**

```bash
git clone https://github.com/org/repo.git
```

* **g. Undo wrong commit but keep history clean**

```bash
git revert <commit-hash>
git push origin main
```

* **h. See all remote branches**

```bash
git fetch --all
git branch -r
```

* **i. Last modification of register.jsp**

```bash
git log -1 -- register.jsp
```

* **j. Full details of commits**

```bash
# Last commit details
git show
# Specific commit details
git show <commit-hash>
```

---

Q4. Docker (20 Marks)

1. **Dockerfile Creation (3 Marks)**

```dockerfile
# Use Tomcat 9 as base image
FROM tomcat:9.0

# Copy built WAR into Tomcat webapps
COPY target/*.war /usr/local/tomcat/webapps/ROOT.war

# Start Tomcat
CMD ["catalina.sh", "run"]
```

2. **Build and Run Image (2 Marks)**

```bash
docker build -t flightimage .
docker run --name flightcontainer -d flightimage
```

3. **Push to Docker Hub (5 Marks)**

```bash
docker login
docker commit flightcontainer <dockerhubusername>/flightimage
docker push <dockerhubusername>/flightimage
```

4. **SQB (10 x 1 Mark = 10 Marks)**
   \| Scenario | Command |
   \|----------|--------|
   \| a. Run nginx on port 8080 | docker run -d -p 8080:80 nginx |
   \| b. List running containers | docker ps |
   \| c. Stop flightcontainer | docker stop flightcontainer |
   \| d. Check logs of container | docker logs \<container\_name\_or\_id> |
   \| e. Check CPU/RAM usage | docker stats |
   \| f. Open shell inside container ubuntu | docker exec -it ubuntu /bin/bash |
   \| g. Run 3 instances with docker-compose | docker-compose up --scale app=3 |
   \| h. Check which container uses port 3000 | docker ps |
   \| i. Start container and open shell | docker run -it your-image /bin/bash |
   \| j. Delete Docker image | docker rmi flightimage |

---

Q5. Docker Compose (10 Marks)

**docker-compose.yml**

```yaml
version: "3.9"

services:
  app:
    build: .
    image: flightimageyog
    container_name: tomcat-app
    ports:
      - "8080:8080"
    depends_on:
      - db
    environment:
      DB_HOST: db
      DB_PORT: 3306
      DB_NAME: mydb
      DB_USER: myuser
      DB_PASS: mypassword

  db:
    image: mysql:8.0
    container_name: mysql-db
    restart: always
    environment:
      MYSQL_DATABASE: mydb
      MYSQL_USER: myuser
      MYSQL_PASSWORD: mypassword
      MYSQL_ROOT_PASSWORD: rootpassword
    ports:
      - "3307:3306"
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
```

* Start services:

```bash
docker-compose up
```

* Both app and database containers will run together successfully.
  
//vaishnavi
•  You made changes to one file in the above project but haven't staged them yet. You realize they were a mistake. What Git command will you use to discard the local changes?
•	Command: git checkout -- <file-name> or git restore <file-name>
•  You made a commit but typed the wrong commit message. You haven't pushed it yet. How do you fix it?
•	Command: git commit --amend -m "your new message"
•  You want to view the commit history of the current branch in a readable format. What Git command should you use?
•	Command: git log --oneline or git log --oneline --graph
•  You're on the main branch. Create the branch Featuer/patient and switch to that branch. What commands do you use?
•	Command: git checkout -b Featuer/patient
•  You've made some commits locally and now want to upload them to the remote repository. What do you run?
•	Command: git push
•  You want to see all the branches that exist both locally and on the remote. How?
•	Command: git branch -a
•  Create a branch Suggestions and merge with patient branch, how can it be?
•	Commands:
1.	git checkout patient (to move to the patient branch)
2.	git merge Suggestions (to merge the Suggestions branch into patient)
•  How do you pull the latest changes from the remote repository and merge them into your local branch?
•	Command: git pull or git pull origin <branch-name>
•  Specify the git command when pushing for the first time and want to set the remote branch.
•	Command: git push -u origin <branch-name> or git push --set-upstream origin <branch-name>
•  You cloned a remote repository, but later you find that you need to push your changes to a different remote repository. How do you configure your local repository to push to this new remote?
•	Command: git remote set-url origin <new-remote-url>
•  After running git pull, you notice that your local branch is behind the remote branch. How would you proceed to bring your local branch up to date without losing your local changes?
•	Command: git pull (This is the correct command; Git is designed to merge changes automatically without losing your local work.)
•  You've pushed a patient branch to a remote repository, but now you need to delete the branch from the remote. How would you do that?
•	Command: git push origin --delete patient
•  How do you apply a .patch file provided by your teammate and include it in your commit history?
•	Commands:
1.	git apply <patch-file-name.patch>
2.	git add .
3.	git commit -m "Applied patch from teammate"











Based on the images provided, here are the questions and their answers, clearly broken down with simple explanations and commands.
________________________________________
Questions 1-6
1.	Download the given repository and show the list of the files?
o	Command: git clone https://github.com/KumbhamBhargavi75/HospitalMgmtSystem
o	Explanation: After this, you need to navigate into the new folder and list the files.
o	Command: cd HospitalMgmtSystem followed by ls (on Linux/macOS) or dir (on Windows).
2.	mvn CLEAN package, when I run this getting an unknown lifecycle phase error why?
o	Explanation: This error usually happens when there's a spelling mistake in the command or the Maven pom.xml file has an error. The command clean package is correct, but Maven cannot understand an unknown lifecycle phase if it is not a correct phase name. A common mistake is a typo, for example, packege instead of package.
3.	Add the dependency servlet-api of 2.5 to your project.
o	Answer: You need to add this dependency block inside the <dependencies> section of your pom.xml file.
o	Code:
XML
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>servlet-api</artifactId>
    <version>2.5</version>
</dependency>
4.	You try to build the project with JDK 21, but compilation fails. Why might this happen? How to fix in pom.xml?
o	Explanation: This happens because newer JDK versions (like JDK 21) have strict rules. The code in your project might be using features that are removed or changed in newer JDKs.
o	Fix: You need to tell Maven which Java version your project should use. You can do this by adding the maven-compiler-plugin to your pom.xml.
o	Code:
XML
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
        </plugin>
    </plugins>
</build>
	Note: Here, 1.8 is used as an example for Java 8, which is often a safe choice for older projects.
5.	In the dependency section: <dependency> <groupId>SE</groupId> <artifactId>junit</artifactId> <version>4.6.0</version> </dependency> What will Maven do in this case? How can you solve?
o	Explanation: Maven will fail to download this dependency. The groupId and artifactId are not correct for JUnit. Maven looks for these details on the Maven Central Repository, and it won't find anything with groupId as "SE".
o	Fix: You need to use the correct groupId and artifactId for the JUnit dependency.
o	Correct Code:
XML
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.6.0</version>
    <scope>test</scope>
</dependency>
6.	After building the WAR, you notice the generated file is named hospitalmgmtSys-1.0-SNAPSHOT.war instead of HospitalMgmtSystem.war, how to fix it?
o	Explanation: Maven adds the project's <version> to the final file name by default.
o	Fix: You can remove the version from the final file name by adding a <finalName> property inside the <build> section of your pom.xml.
o	Code:
XML
<build>
    <finalName>HospitalMgmtSystem</finalName>
</build>
________________________________________
Questions 7-13
7.	Add the central dependency of Java Servlet API 4.0.0-b01 to your existing project. Check the complete pom.xml file and run it.
o	Answer: You need to add the following dependency block inside the <dependencies> section of your pom.xml.
o	Code:
XML
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.0-b01</version>
    <scope>provided</scope>
</dependency>
8.	A developer removes the <dependencies> section completely. Will Maven still build the project? What issues might occur during testing?
o	Explanation: Maven will still build the project if there are no dependencies required for compilation. However, issues will occur during testing.
o	Issues during testing: The test code will fail because it won't be able to find the necessary libraries like JUnit or Mockito, which are required to run the tests.
9.	Failed to execute goal [org.apache.maven.plugins:maven-compiler-plugin:3.13.0:compile] on project [project-name] [ERROR] No compiler is provided in this environment. Perhaps you are running on a JRE rather than a JDK? Identify the error?
o	Explanation: The error is exactly as stated: "No compiler is provided in this environment. Perhaps you are running on a JRE rather than a JDK?" Maven needs the JDK (Java Development Kit) to compile the code. The JRE (Java Runtime Environment) is only for running Java applications, not compiling them.
10.	In Build is having finalname as <finalName>localhost:8080/FoodSystem</finalName>, is it works, if not how can you fix it?
o	Explanation: This will not work. The <finalName> is only meant for the name of the final build file (like a .jar or .war file). It should not contain a URL or any special characters like : or /.
o	Fix: The correct finalName should be just the name of the file, such as FoodSystem.
o	Code:
XML
<build>
    <finalName>FoodSystem</finalName>
</build>
11.	Your project is meant to deploy on Tomcat, but <packaging>jar</packaging> is like this in pom.xml. How do you solve it?
o	Explanation: To deploy a project on Tomcat, it must be packaged as a .war file. The <packaging> element in pom.xml must be set to war.
o	Fix: Change the packaging type to war.
o	Code:
XML
<packaging>war</packaging>
12.	In the <url> tag, written <url>http://maven.java.org12</url>. Will Maven accept this? What is the correct purpose of the <url> element in pom.xml?
o	Explanation: Yes, Maven will accept this URL. Maven does not check if the URL is valid or exists.
o	Purpose: The <url> element's purpose is to provide the URL for the project's website. It is used for documentation and information, not for any functional part of the build process.
