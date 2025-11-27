# 🐬 AWS Aurora Serverless v2 Lab — Create Aurora MySQL Cluster & Query with RDS Query Editor

In this lab, I learned how to **create an Aurora MySQL Serverless v2 DB cluster, connect via EC2 using the MySQL client, enable the RDS Data API, and run SQL queries through the RDS Query Editor**.

---

## 📋 Lab Overview

**Goal:**

* Understand what Amazon Aurora is
* Deploy an **Aurora MySQL Serverless v2** DB cluster
* Configure capacity scaling and Data API access
* Connect manually from EC2 using MySQL CLI
* Use **RDS Query Editor** to execute SQL queries in the console

**Learning Outcomes:**

* Understand Aurora’s performance benefits
* Deploy Aurora MySQL-compatible clusters
* Use Aurora Serverless v2 with controlled ACU scaling
* Connect to Aurora from EC2 via MySQL CLI
* Run SQL queries directly from the AWS console with Query Editor

---

## 🛠 Step-by-Step Journey

### **Step 1 — Log Into AWS Console**

Logged into the AWS Management Console using lab credentials.
Region: **US East (N. Virginia)**.

---

### **Step 2 — What Is Amazon Aurora? (Theory Review)**

Aurora is:

✔ A fully managed relational database engine
✔ Compatible with **MySQL** and **PostgreSQL**
✔ Up to **5× faster than MySQL**
✔ Up to **3× faster than PostgreSQL**
✔ Works with existing MySQL/PostgreSQL applications with no code changes
✔ High performance + cost-effective + highly scalable

---

### **Step 3 — Create an Aurora MySQL Serverless v2 DB Cluster**

Navigated to:

**RDS → Create Database → Standard Create**

**Configuration Details:**

| Setting               | Value                   |
| --------------------- | ----------------------- |
| Engine                | Aurora MySQL-Compatible |
| Engine Version        | Aurora MySQL 3.08.2     |
| Template              | Dev/Test                |
| DB Cluster Identifier | `kk-query-db`           |
| Master Username       | `CodeCloud`             |
| Master Password       | `codecloud`             |
| Storage               | Aurora Standard         |
| DB Instance Type      | **Serverless v2**       |
| Capacity Range        | Min 2 ACUs → Max 2 ACUs |
| Data API              | **Enabled**             |
| Initial DB Name       | `querydatabase`         |
| Deletion Protection   | Disabled                |

Clicked **Create Database**.

---

### **Step 4 — Confirm Cluster Availability**

Waited for cluster status to change to:

```
Available
```

Confirmed successfully.

---

### **Step 5 — Connect via EC2 Using MySQL CLI**

Used an existing EC2 instance named **RDS-connect-EC2-instance**.

**SSH Command:**

```bash
ssh -i "RDS-key-pair.pem" ubuntu@<EC2-Public-DNS>
```

Once inside the EC2 instance, connected to the database.

**MySQL Command:**

```bash
mysql -h <aurora-endpoint> -P 3306 -u CodeCloud -p querydatabase
```

Entered password:

```
codecloud
```

Successfully connected and able to insert sample data.

---

### **Step 6 — Use RDS Query Editor**

Navigated to:

**RDS → Query Editor**

Logged in with:

| Field             | Value           |
| ----------------- | --------------- |
| Database Instance | `kk-query-db`   |
| Username          | `CodeCloud`     |
| Password          | `codecloud`     |
| Database          | `querydatabase` |

Clicked **Connect to Database**.

Now able to run SQL queries such as:

```sql
SELECT * FROM employees;
```

Results returned successfully.

---

## 💡 Notes / Tips

* Aurora Serverless v2 supports **fine-grained** capacity scaling (ACUs).
* The **RDS Data API** allows running SQL over HTTPS — no persistent connections needed.
* Query Editor is ideal for light querying/testing without needing a local client.
* EC2 MySQL client is still useful for learning real-world connection patterns.
* Always disable deletion protection in labs to avoid issues during cleanup.

---

## 📌 Lab Summary

| Step                              | Status | Key Takeaways                                      |
| --------------------------------- | ------ | -------------------------------------------------- |
| Review Aurora basics              | ✅      | Fast, scalable, MySQL/PostgreSQL-compatible engine |
| Create Aurora MySQL Serverless v2 | ✅      | Configured ACU scaling + Data API                  |
| Connect from EC2 via MySQL        | ✅      | Verified connection + inserted sample data         |
| Use Query Editor                  | ✅      | Executed SQL queries directly in AWS Console       |

---

## 🔗 References

* [Amazon Aurora Overview](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html)
* [Aurora MySQL Documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.html)
* [Query Editor Documentation](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/query-editor.html)
* [RDS Data API](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/data-api.html)
