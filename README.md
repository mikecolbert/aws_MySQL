# Creating a MySQL RDS service in AWS
Create an AWS RDS MySQL server service. Connect to it with MySQL Workbench and creates specific tables and data. This assignment is in preparation for connecing to this database with a Python Flask, Elastic Beanstalk application.

### Step 1: Create a VPC
Create a MySQL database.

* A. From the AWS console, under **Database**, choose **RDS**
* B. Choose **Create database**
* C. Select **Standard Create** --> **MySQL** --> Version **MySQL 8.0.20**
* D. Choose **Dev/Test**
* E. Database Instance Identifier should be set to *hawkid-movie-db* (i.e. colbert-movie-db)
* F. Leave Master username as admin. Create a 30 character password and confirm it.
* G. In the *DB instance size* section, choose **Burstabable classes** and *db.t3.micro
* H. In the *Storage* section, choose **General Purpose (SSD)**, **10** GiB allocated storage, and **uncheck** autoscaling.
* I. **Do not create aa standby instance** in the *Availabilty & durabiltiy* section
* J. In the *Connectivity* section, leave the VPC set as **Default VPD** and click the triangle to expand *Additional connectivity configuration* --> Choose **Yes** to *Public access*. **Create new** VPC security group named *hawkid-movie-db-sg* (i.e. colbert-movie-db-sg)
* K. Leave all other choices with the default selections and click **Create database** at the bottom.

*It takes a few minutes for this to create*

***

### Step 2: Download and Install MySQL Workbench
We will use MySQL Workbench to connect to and manage our MySQL database running on AWS. Visit https://dev.mysql.com/downloads/workbench/ and download the Workbench package for your OS. We are only installing Workbench. Do not install anything server related.

* A. Click on **Download**. You will need to sign up for a free account if you don't already have one. 

![Donwload MySQL Workbench](/images/download.jpg)

* B. After logging in, choose **Download Now**

-- Installation instructions for Windows --
* C. Double click the downloaded file to begin installation
* D. **Next** at the Welcome screen
* E. **Next** at the Destination Folder screen
* F. **Next** at the Setup Type screen to choose *Complete*
* G. **Install** at the Ready to Install the Program screen
* H. **Yes** to allow the program to make changes on your computer
* I. **Finish** when installation is complete

***

### Step 3: Connect MySQL Workbench to Your AWS Server
We will use MySQL Workbench to connect to and manage our MySQL database running on AWS.

* A. From the AWS RDS console, click on **Databases** in the left menu. Wait for the database status to show *Available*. Refresh if necessary.
* B. Click on your database so you can view details
* C. Copy the Endpoint URL - you will need it to connect.
* D. In the Security column, click on the security group for your database.
* E. From the **Inbound rules** tab, choose **Edit inbound rules**
* F. Modify **Source** to be *My IP* with a **Description** of *MySQL Workbench from my home computer*, then **Save rules**
* G. Visit the RDS console again to make sure your database status is *Available*

![Connect MySQL Workbench to your database](/images/connection.jpg)

* H. From MySQL Workbench, click to **add** a new connection.
* I. Connection Name: *AWS Movies* (it can be anything descriptive)
* J. Hostname: *Database endpoint URL you copied earlier*
* K. Click **Test Connection** --> **paste** in your database password --> **check** Save password in vault --> OK 

![Connection successful](/images/connection-successful.jpg)

* L. Double-click the connection tile to open a connection to your database.

***

### Step 4: Populate Your Database
Use the database scripts provided to create users, tables, and data in your AWS MySQL service.

* A. Open movies_users_and_tables.txt. Copy the contents and paste in your MySQL Workbench query editor. Run the query and ensure they all finish without errors.

* B. Open movies_data.txt. Copy the contents and paste in your MySQL Workbench query editor. Run the query and ensure they finish without errors. *This takes several minutes*

***

### Step 5: Verify Your Data
*Note: There is no data in the 'genres' table*

Show all tables: ` SHOW TABLES; `

Show table structure:  ` DESCRIBE movies; `

Count the number of records:  ` SELECT COUNT(*) FROM movies; `

Return all the fields of all the records:  ` SELECT * FROM Movies; `

Show movies released in 1972:  ` SELECT * FROM movies WHERE releaseYear LIKE '%1972%'; `

