## Lab 3: MongoDB Data Model Analysis and Scalability Study

### Objective
- Analyze the MongoDB data model.
- Study horizontal scalability and high availability features.

### Report

#### 👩‍💻👨‍💻 Task 1: Installing MongoDB
![image](https://github.com/BSUIR-IPE/lab-3-mongodb-data-model-analysis-and-scalability-study-tdotv/assets/91983402/410b2915-fbe9-4631-a223-d2e1a266584c)
![image](https://github.com/BSUIR-IPE/lab-3-mongodb-data-model-analysis-and-scalability-study-tdotv/assets/91983402/3603c8e6-ca2c-4dca-9ae7-a1d8e3f2b8ac)

#### 👩‍💻👨‍💻 Task 2: Obtaining and Adding a Dataset
![image](https://github.com/BSUIR-IPE/lab-3-mongodb-data-model-analysis-and-scalability-study-tdotv/assets/91983402/1b9ecf0d-1652-474d-b8cd-2dc1569c2e06)

#### 👩‍💻👨‍💻 Task 3: Exploring MongoDB Features
- **Document Model**
Documents are grouped together in collections. However, the documents in a single collection don't necessarily need to have exactly the same set of fields. This is what we call a “flexible schema.” This flexibility allows developers to iterate faster and migrate data between different schemas without any downtime. However, if you want to lock down your schema at a certain point, you can do so by applying validation rules to your collections.
- **Sharding**
Sharding in MongoDB allows for much greater horizontal scalability. Horizontal scaling means that each shard in every cluster houses a portion of the dataset in question, essentially functioning as a separate database. Combining the data of the distributed shards forms a single, comprehensive database much better suited to handling the needs of a popular, growing application with zero downtime.
- **Replication**
Replication allows you to sidestep these vulnerabilities by deploying multiple servers for disaster recovery and backup. Horizontal scaling across multiple servers greatly increases data availability, reliability, and fault tolerance. Potentially, replication can help spread the read load to the secondary members of the replica set with the use of read preference.
- **Authentication**
MongoDB provides a number of authentication mechanisms for users to access the database. The most common is the Salted Challenge Response Authentication Mechanism (SCRAM), which is the default. When used, SCRAM requires the user to provide an authentication database, username, and password.
- **Database Triggers**
Database triggers are a great way to perform audits, ensure data consistency and data integrity, and to perform complex event processing. Check out the dedicated Database Triggers article to learn more about the different types of triggers and how to use them.

#### 👩‍💻👨‍💻 Task 4: Working with MongoDB
![image](https://github.com/BSUIR-IPE/lab-3-mongodb-data-model-analysis-and-scalability-study-tdotv/assets/91983402/5c39c53a-7ac2-422e-a80d-0c1ac071f5a3)
![image](https://github.com/BSUIR-IPE/lab-3-mongodb-data-model-analysis-and-scalability-study-tdotv/assets/91983402/7478eead-884d-4ece-8411-392caa945741)
![image](https://github.com/BSUIR-IPE/lab-3-mongodb-data-model-analysis-and-scalability-study-tdotv/assets/91983402/ba896672-9da4-4bd3-bb69-5c203136f4be)

#### Task 5: Analyze and Draw Conclusions
- In conclusion, the analysis of the MongoDB data model focuses on the optimization of the data scheme, the horizontal scalability study evaluates the scalability, and the study of high availability evaluates the fault tolerance and availability of the system. Following the above recommendations, they can solve problems and take advantage of opportunities to develop efficient data models, horizontally expand the deployment of MongoDB and ensure high availability of their systems.

#### 📌 Documentation Links
[MongoDB Manual](https://docs.mongodb.com/manual/)
[MongoDB Features](https://www.mongodb.com/features)
[Docker and MongoDB](https://www.mongodb.com/compatibility/docker)
[MongoDB Shell](https://www.mongodbtutorial.org/getting-started/mongodb-shell/)
