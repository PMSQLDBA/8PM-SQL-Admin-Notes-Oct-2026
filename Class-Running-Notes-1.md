# **SQL Server Database Administration – Training Notes**

## **Part 1: SQL Server Fundamentals, Installation, Architecture and Configuration**

**Training scope:** SQL Server 2019, 2022 and 2025\
**Operating system:** Windows Server and supported Linux environments\
**Training level:** Beginner to Intermediate\
**Primary focus:** On-premises SQL Server DBA administration, with an introduction to cloud platforms.

# **Module 1: Introduction to SQL Server and DBA Responsibilities**

## **Lesson 1: Introduction to SQL Server**

### **1. What is SQL Server?**

- Microsoft SQL Server is a Relational Database Management System (RDBMS).
- It stores, manages, retrieves and protects organizational data.
- It uses Transact-SQL (T-SQL) to interact with databases.
- It supports transaction processing, reporting, business applications and data warehousing.

### **2. SQL Server – Developer vs DBA**

| SQL Server Developer           | SQL Server DBA                        |
| ------------------------------ | ------------------------------------- |
| Develops SQL queries           | Administers SQL Server instances      |
| Creates stored procedures      | Manages database availability         |
| Creates views and functions    | Configures backup and recovery        |
| Develops database applications | Manages security and permissions      |
| Optimizes application queries  | Performs database performance tuning  |
| Implements business logic      | Handles database incidents            |
| Works with application teams   | Coordinates with infrastructure teams |

**Important:** Developers and DBAs have overlapping responsibilities. Query optimization, execution plans, indexing and transaction management are shared areas.

### **3. Database Administrator responsibilities**

A SQL Server DBA typically handles:

1. SQL Server installation and configuration.
2. Database creation and administration.
3. Backup and restore management.
4. Database security.
5. SQL Server Agent job administration.
6. Database maintenance.
7. Monitoring and alerting.
8. High Availability and Disaster Recovery.
9. SQL Server and database migrations.
10. SQL Server patching and upgrades.
11. Performance monitoring and tuning.
12. Production incident management.
13. Automation of repetitive DBA activities.

### **4. Database platforms**

A multi-database-platform DBA may work with:

- Oracle Database.
- Microsoft SQL Server.
- PostgreSQL.
- MongoDB.

### **5. Operating systems**

- Windows Server.
- Linux distributions supported by the respective database platform.

# **Module 2: SQL Server Versions, Editions and Components**

## **Lesson 2: SQL Server Version History**

| SQL Server version | Internal major version |
| ------------------ | ---------------------- |
| SQL Server 2000    | 8.0                    |
| SQL Server 2005    | 9.0                    |
| SQL Server 2008    | 10.0                   |
| SQL Server 2008 R2 | 10.5                   |
| SQL Server 2012    | 11.0                   |
| SQL Server 2014    | 12.0                   |
| SQL Server 2016    | 13.0                   |
| SQL Server 2017    | 14.0                   |
| SQL Server 2019    | 15.0                   |
| SQL Server 2022    | 16.0                   |
| SQL Server 2025    | 17.0                   |

### **Important concepts**

- RTM: Release to Manufacturing, the original release baseline.
- GDR: General Distribution Release, primarily security and critical fixes.
- CU: Cumulative Update, containing accumulated fixes and improvements.
- Hotfix: An individual fix or targeted update.
- Service Pack: A historical servicing mechanism used by older SQL Server releases.

**Note:** SQL Server 2017 onwards uses the modern CU/GDR servicing approach. SQL Server 2019, 2022 and 2025 do not follow the old Service Pack model.

## **Lesson 3: SQL Server Editions**

| Edition    | Typical usage                                                                     |
| ---------- | --------------------------------------------------------------------------------- |
| Express    | Small applications and learning; free with limitations                            |
| Developer  | Development and testing; full Enterprise feature set, not licensed for production |
| Standard   | Production workloads requiring Standard features                                  |
| Enterprise | Production workloads requiring advanced capabilities                              |
| Evaluation | Temporary evaluation and testing                                                  |

Additional edition distinction for SQL Server 2025:

- Enterprise Developer.
- Standard Developer.

Always verify licensing and feature availability against the exact SQL Server release and edition.

## **Lesson 4: SQL Server and Client Tools**

### **SQL Server Database Engine**

The Database Engine is the core SQL Server component responsible for:

- Database storage.
- Query processing.
- Transaction management.
- Security enforcement.
- Data retrieval.
- Database recovery.

### **SQL Server Management Studio (SSMS)**

[SQL Server Management Studio (SSMS)](https://images.openai.com/static-rsc-4/5SlcHnAQxYid5i7dF4B7rTJt5GqIU6Weavg84Lc56qZGXOJ16l9pCtk5giB4lprlrY0zHU8C6atYmmYtdm9DzM6la75IVSYlDTMMswgO67blY4DSVYMWaK-Y1mb50IpG8KVrzg1NNjwVIprd7ZbOJhLPAjltfn54wKy1nSQ0bFo?purpose=inline)

[quackit.com](https://www.quackit.com/sql_server/sql_server_2016/tutorial/sql_server_management_studio.cfm)

SSMS is a graphical client tool used to:

- Create databases.
- Create logins and users.
- Execute T-SQL queries.
- Create SQL Server Agent jobs.
- Configure linked servers.
- Manage database objects.
- Monitor SQL Server.

SSMS is installed separately from the Database Engine in modern SQL Server installations.

### **SQL Server Configuration Manager (SSCM)**

[SmartData Fabric® v8.0 Help](https://images.openai.com/static-rsc-4/gl91HH5KSMzQD16KFY-U0rmuMZvf3Zl9q27aWU2Uqv3dFDu7qi-O9MqBGtv02qOqZ_N4GiTHzEJIKDA26ITDexbB73AIahme7VhqSUtwC-SYUQuxfjtYq9DDKmxv7wmxpvSqJL4fFM2eMXaunpwsmkTzLkV18KWZtjcyFMu9SXk?purpose=inline)

Used for:
- Starting SQL Server services.
- Stopping SQL Server services.
- Restarting SQL Server services.
- Configuring network protocols.
- Configuring TCP/IP.
- Reviewing service accounts.
- Managing SQL Server client network configurations.

### **Other DBA tools**

| Tool                 | Purpose                                      |
| -------------------- | -------------------------------------------- |
| SSMS                 | SQL Server administration                    |
| SSCM                 | SQL Server service and network configuration |
| CMD                  | Windows command-line administration          |
| SQLCMD               | SQL Server command-line connectivity         |
| Windows Event Viewer | Windows and application event investigation  |
| SQL Server Error Log | Database Engine event investigation          |
| PowerShell           | Administrative automation                    |

# **Module 3: SQL Server Instance Architecture**

## **Lesson 5: Understanding SQL Server Instances**

The following terms are commonly used:

- SQL Server Database Engine.
- SQL Server Instance.
- SQL Instance.
- SQL Server Engine.
- SQL Server Box (informal industry terminology).
- Database Server (context-dependent terminology).

### **1. Default instance**

A default instance uses the Windows hostname as its connection name.

Example:

```
Windows Hostname: SONY

SQL Server Instance: SONY

Service Name: MSSQLSERVER
```

Connection:

```
SONY
```

### **2. Named instance**

A named instance requires an instance name during installation.

Example:

```
Windows Hostname: SONY

Named Instance: Delhi

Connection Name: SONY\Delhi
```

Other examples:

```
SONY\Maryland
SONY\Texas
SONY\ProdSQL01
```

### **3. Connecting using local names**

| Connection   | Meaning                    |
| ------------ | -------------------------- |
| `.`          | Local default instance     |
| `localhost`  | Local default instance     |
| `(local)`    | Local default instance     |
| `.\Texas`    | Local named instance Texas |
| `SONY`       | Default instance on SONY   |
| `SONY\Delhi` | Named instance Delhi       |

### **4. Instance capacity**

A Windows Server can host multiple SQL Server instances.

Your original example of one default instance and 49 named instances is an illustration, not a universal maximum.

Actual supported instance limits depend on SQL Server version and platform.

### **5. SQL Server services**

**Database Engine service**

- Default instance: `MSSQLSERVER`
- Named instance: `MSSQL$InstanceName`

**SQL Server Agent service**

- Default instance: `SQLSERVERAGENT`
- Named instance: `SQLAgent$InstanceName`

SQL Server Agent runs scheduled jobs, maintenance plans and administrative automation. It is not available in SQL Server Express Edition.

## **Lesson 6: SQL Server Network Connectivity**

### **TCP/IP connectivity**

SQL Server commonly uses TCP port 1433 for a default instance, but the port can be configured differently.

Example:

```
Server Name: SONY
Protocol: TCP/IP
Port: 1433
```

Named instance example:

```
Server Name: SONY\Texas
Port: 56789
```

A named instance may use a dynamic port unless configured with a static port.

### **Required configuration**

1. Enable TCP/IP in SQL Server Configuration Manager.
2. Configure a static port where appropriate.
3. Restart the SQL Server service after protocol changes.
4. Configure Windows Firewall rules.
5. Validate client connectivity.
6. Review SQL Server Browser requirements for named instances using dynamic ports.

# **Module 4: Windows Server and Virtualization Fundamentals**

## **Lesson 7: Windows Server Fundamentals**

### **Windows Server versions**

Your training lab can cover:

- Windows Server 2016.
- Windows Server 2019.
- Windows Server 2022.
- Windows Server 2025.

Older versions such as 2000, 2003, 2008 and 2012 are useful for historical understanding, but should not be used for new production deployments.

### **Windows Server editions**

1. Standard.
2. Datacenter.

### **Windows Server environments**

**Stand-alone server**

- Operates independently.
- Can use local Windows accounts.
- Suitable for small environments and lab setups.

**Domain-based environment**

- Integrated with Active Directory.
- Centralized user and group management.
- Supports domain-based authentication.
- Common in enterprise environments.

### **Domain example**

```
Domain Controller:
Hyderabad.xyz.com

Member Servers:

Telangana.xyz.com
AP.xyz.com
Kerala.xyz.com
```

### **Important infrastructure teams**

| Team                   | Responsibilities                           |
| ---------------------- | ------------------------------------------ |
| Windows Administration | OS installation and configuration          |
| Storage Administration | SAN and disk provisioning                  |
| Network Administration | IP, DNS, routing and connectivity          |
| DBA Team               | SQL Server installation and administration |
| Application Team       | Application connectivity and validation    |

## **Lesson 8: Virtualization Software**

[VMware Workstation Pro / Fusion 25H2](https://images.openai.com/static-rsc-4/Dgms5TdpOG5ZluV1cpnNAZuKsq9jwcnXQHCRTU7ZPGycPjGL_uwEVVcs6QtWZfeHR2HZo6tPXb70Cina1nfQhL9s0bpNrvLsRmA8c4PEQhAdYnTkNI0qCBP-HlC-Hatu_BAftHlgl5xOqbSzc9lJZZGdEf6A8uaRB-tkLeJ5jY8?purpose=inline)

**VMware Workstation Pro**

Desktop virtualization platform

[Official VMware website](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion)

[Install Ubuntu 19.10 and Apps for Web Development – Michael S. Mikowski – SPA (UI/UX/server) architect and author](https://images.openai.com/static-rsc-4/H1aEcb5ZDbRX2Oqhp--rIxD2KbFUFa87_vWzj7ftSYO2YSViv7rWHYF9RY7TKjJJxTGad2PsOICFUP4wiWSKbTghP_DRRItvMfiJ5t52-3qlUXUhYGlTTdAfk8DHTMd-dIGCIKynr3HiK80sRi3VC2bz8mu-sX2M5mBjDQPJJmc?purpose=inline)

**Oracle VirtualBox**

Desktop virtualization platform

[Official VirtualBox website](https://www.virtualbox.org/)

Virtualization allows DBAs to create multiple virtual machines on a single physical computer.

### **Suggested laptop configuration**

| Component      | Suggested configuration                 |
| -------------- | --------------------------------------- |
| RAM            | 16 GB minimum for a limited lab         |
| RAM            | 32 GB recommended for a multi-VM HA lab |
| Disk           | 500 GB SSD                              |
| Processor      | Modern multi-core processor             |
| Virtualization | Intel VT-x or AMD-V enabled             |

### **Suggested three-node lab**

Your original RAM allocation:

| VM                | RAM   |
| ----------------- | ----- |
| Domain Controller | 2 GB  |
| SQL Node 1        | 3 GB  |
| SQL Node 2        | 3 GB  |
| SQL Node 3        | 3 GB  |
| Total             | 11 GB |

This is a tight allocation on a 16 GB host once Windows itself and virtualization overhead are considered. Use lightweight configurations for learning, and increase RAM for realistic clustering and performance exercises.

# **Module 5: SQL Server Installation**

## **Lesson 9: SQL Server Installation Types**

SQL Server can be installed using:

1. Graphical User Interface (GUI).
2. Command-line installation.
3. Configuration file.
4. PowerShell-based installation automation.

### **Installation environments**

| Environment | Typical edition       |
| ----------- | --------------------- |
| Development | Developer             |
| Testing     | Developer             |
| QA          | Developer             |
| Production  | Standard / Enterprise |

The edition must comply with Microsoft's licensing terms.

### **Installation types**

**1. Stand-alone SQL Server installation**

- Installed on an individual Windows Server.
- Does not require Windows Failover Clustering.
- Suitable for independent SQL Server workloads.

**2. SQL Server Failover Cluster Instance installation**

- Installed as a clustered SQL Server instance.
- Requires Windows Server Failover Clustering (WSFC).
- Uses shared storage or supported storage architecture.
- Provides instance-level high availability.

[Manage high availability and disaster recovery | Microsoft Press Store](https://images.openai.com/static-rsc-4/A_deAekCjtCabhkMDCLaK4Mvp1p9XKm-lz5n5gXYubMw0HsM5Yt2p2O1Dh3WxRlxMvuFI1MYriOFj17_R6QUOuMyP_t1x90yCcJp0IE4xJC3hYV-Ht_HZhIJ3r1wL70GX7JbFRIbVPnbUueotGX35xnX7rmrIyBQDOpMnZHRRrE?purpose=inline)

[SQL Server 2019 Installation Center to Setup New Instance](https://images.openai.com/static-rsc-4/0VV98KcUqgS_BM2PnK1sN92uyCv7d18zqq0OkAQ2Du19R-An8pMa9RhdfwS16cOk6KwI2j21V11nznT63zEtPxjEVX4LICtoY0YeV9CNa7u0qlhrAixmUiS1gAg9elnR8sfiZDEq4YFN_2GkkVxZu_D0jrND3m4yZZm34AeZvNE?purpose=inline)

[What is SQL Server AlwaysOn?](https://images.openai.com/static-rsc-4/g_x4Ef7hOfG5M3a0gngJv7-dX1Z50RN922yhYrI5e1hixctgqlGxHT72YE6-LJUftbINJPQ3bIfDpoUF7qDN2VAY5d3bAz2S8pH59e3uP7IyuuAKzp9OHPiUIGFUOpore64VHtt5YufES1u1Yf4axRSPyxAUg8tGBhqBf0YHLl0?purpose=inline)

6

## **Lesson 10: SQL Server Installation Prerequisites**

### **1. Pre-installation activities**

Before installation, collect the following details:

- Windows Server hostname.
- Windows Server version and edition.
- IP address.
- CPU and RAM.
- Available disk space.
- SQL Server version and edition.
- Default or named instance requirement.
- SQL Server service account.
- SQL Server Agent service account.
- Authentication mode.
- SQL Server port.
- Data, log, backup and TempDB locations.
- Required SQL Server components.

### **2. SQL Server components**

| Component                   | Purpose                          |
| --------------------------- | -------------------------------- |
| Database Engine             | Database storage and processing  |
| SQL Server Replication      | Data distribution                |
| Integration Services (SSIS) | Data integration and ETL         |
| Analysis Services (SSAS)    | Analytical processing            |
| Reporting Services (SSRS)   | Reporting platform               |
| Full-Text Search            | Full-text indexing and searching |

Component availability and installation methods vary by release.

### **3. Example installation configuration**

```
Windows Server: SONY

SQL Server Version: 2022
Edition: Developer
Instance Type: Named
Instance Name: PROD

SQL Server Name:
SONY\PROD

Authentication:
Windows Authentication

TCP/IP:
Enabled

Port:
1433 (example only)
```

### **4. Installation directory planning**

| Drive | Purpose                             | Example allocation |
| ----- | ----------------------------------- | ------------------ |
| C:\\  | Windows OS                          | 60 GB              |
| D:\\  | SQL installation media and software | 10 GB              |
| E:\\  | SQL Data files                      | 30 GB              |
| L:\\  | SQL Log files                       | 20 GB              |
| H:\\  | SQL Backups                         | 10 GB              |
| T:\\  | TempDB files                        | 10 GB              |

These are classroom examples, not recommended production sizing. Actual capacity must be determined from database size, workload, growth forecasts, IOPS, backup retention and recovery requirements.

## **Lesson 11: SQL Server Post-Installation Configuration**

After installing SQL Server, the DBA must perform post-installation validation and configuration.

### **1. SQL Server version and edition**

```
SELECT
    @@SERVERNAME AS ServerName,
    @@VERSION AS SQLServerVersion;
```

A more structured version query:

```
SELECT
    SERVERPROPERTY('ProductVersion') AS ProductVersion,
    SERVERPROPERTY('ProductLevel') AS ProductLevel,
    SERVERPROPERTY('Edition') AS Edition,
    SERVERPROPERTY('ProductMajorVersion') AS MajorVersion;
```

### **2. Verify SQL Server services**

Check:

- SQL Server Database Engine.
- SQL Server Agent.
- SQL Server Browser, if required.

### **3. Configure TCP/IP**

Navigate to:

```
SQL Server Configuration Manager
    |
    SQL Server Network Configuration
    |
    Protocols for Instance
    |
    TCP/IP
```

Enable TCP/IP and configure the required port.

### **4. Configure SQL Server service accounts**

Use appropriate dedicated service accounts or group Managed Service Accounts (gMSAs), where supported.

Important considerations:

- Apply least privilege.
- Avoid unnecessary local administrator membership.
- Use appropriate service account permissions.
- Follow Microsoft's service account recommendations.

### **5. Configure authentication mode**

SQL Server supports:

**Windows Authentication**

- Uses Windows or Active Directory identities.
- Preferred where practical in enterprise environments.

**SQL Server and Windows Authentication (Mixed Mode)**

- Supports both Windows and SQL Server authentication.
- SQL logins require strong password controls and appropriate security management.

### **6. Configure Max Server Memory**

Example:

```
Physical RAM: 16 GB

SQL Server maximum memory:
Set based on OS and other application requirements.
```

Do not automatically allocate 70% of server RAM. Reserve sufficient memory for Windows, SQL Server-related processes, backup tools, monitoring agents and other applications.

### **7. Configure default database paths**

Configure separate paths for:

- Data files.
- Log files.
- Backup files.

### **8. Configure database integrity checks**

Plan regular execution of:

```
DBCC CHECKDB ('DatabaseName')
WITH NO_INFOMSGS;
```

### **9. Configure Database Mail**

Database Mail is used to send email notifications from SQL Server.

Typical uses:

- SQL Agent job failures.
- Backup failures.
- Database integrity check failures.
- Monitoring alerts.
- Administrative notifications.

### **10. Configure SQL Server Agent alerts**

Configure alerts for appropriate severity levels and selected SQL Server errors.

### **11. Review SQL Server Error Log**

Check:

- Startup messages.
- Failed login attempts.
- Database recovery messages.
- Backup failures.
- Storage-related errors.
- Configuration warnings.

### **12. Review Windows Event Viewer**

Check:

```
Event Viewer
    |
Windows Logs
    |
Application
    |
System
```

Correlate Windows events with SQL Server error logs during incident investigation.

# **Module 6: SQL Server Startup Parameters and System Databases**

## **Lesson 12: SQL Server Startup Parameters**

SQL Server uses startup parameters to locate essential database files and its error log.

Three important parameters:

| Parameter | Purpose                          |
| --------- | -------------------------------- |
| `-d`      | Location of master data file     |
| `-l`      | Location of master log file      |
| `-e`      | Location of SQL Server Error Log |

### **Example**

```
-dC:\Program Files\Microsoft SQL Server\
MSSQL15.MSSQLSERVER\MSSQL\DATA\master.mdf

-lC:\Program Files\Microsoft SQL Server\
MSSQL15.MSSQLSERVER\MSSQL\DATA\mastlog.ldf

-eC:\Program Files\Microsoft SQL Server\
MSSQL15.MSSQLSERVER\MSSQL\Log\ERRORLOG
```

### **Practical scenario: SQL Server startup failure**

Error:

```
Error 2: The system cannot find the file specified.

An invalid startup option might have caused the error.
```

Possible causes:

1. Incorrect master database path.
2. Master database file moved or deleted.
3. Incorrect startup parameter.
4. Insufficient file-system permissions.
5. Incorrect SQL Server service account.

### **DBA troubleshooting approach**

1. Open SQL Server Configuration Manager.
2. Identify the affected SQL Server instance.
3. Review startup parameters.
4. Validate the master database file locations.
5. Check the SQL Server service account permissions.
6. Correct the configuration.
7. Start the SQL Server service.
8. Validate SQL Server Error Log.

**Production warning:** 
Do not modify startup parameters without validating the existing configuration and maintaining a recovery plan. 
Master database relocation requires a controlled procedure.

## **Lesson 13: SQL Server Database Architecture**

A SQL Server database consists primarily of:

1. Data files.
2. Transaction log files.

### **Data files**

| Extension | Purpose             |
| --------- | ------------------- |
| MDF       | Primary data file   |
| NDF       | Secondary data file |

### **Transaction log files**

| Extension | Purpose              |
| --------- | -------------------- |
| LDF       | Transaction log file |

Example:

```
Database: DEMODB

Data File:
DEMODB.mdf

Log File:
DEMODB_log.ldf
```

### **Logical and physical file names**

- Logical filename: SQL Server internal file identifier.
- Physical filename: Actual file-system path.

Example:

```
Logical Name: DEMODB
Physical Name: E:\SQLDATA\DEMODB.mdf
```

## **Lesson 14: SQL Server System Databases**

SQL Server has four primary system databases and one hidden system database.

**1. master**

Stores instance-level configuration, logins, database metadata and other critical system information.

Critical

**2. model**

Template database used when creating new databases. Its configuration can influence newly created databases.

**3. msdb**

Stores SQL Server Agent jobs, schedules, backup history, maintenance plans and related metadata.

**4. tempdb**

Temporary workspace used for temporary tables, sorts, hashes, row versioning and other internal operations. Recreated whenever SQL Server starts.

**5. Resource Database**

Hidden, read-only system database containing SQL Server system objects. It is not normally accessed directly by DBAs.

### **System database commands**

```
SELECT name, state_desc, recovery_model_desc
FROM sys.databases;
```

```
SELECT *
FROM sys.master_files;
```

```
EXEC sp_helpdb;
```

### **Important DBA responsibilities**

- Monitor system database health.
- Include system databases in backup strategy where applicable.
- Back up master, msdb and model according to recovery requirements.
- Monitor TempDB space and contention.
- Understand system database recovery procedures.

# **Module 7: SQL Server Configuration and Instance Administration**

## **Lesson 15: SQL Server Configuration Using SP_CONFIGURE**

`sp_configure` is a system stored procedure used to view and modify SQL Server instance-level configuration options.

### **1. View all configuration options**

```
EXEC sp_configure;
```

### **2. View advanced configuration options**

```
EXEC sp_configure 'show advanced options', 1;

RECONFIGURE;

EXEC sp_configure;
```

### **3. Important SQL Server configuration options**

| Configuration                  | Purpose                                                       |
| ------------------------------ | ------------------------------------------------------------- |
| Backup Compression Default     | Enables default backup compression                            |
| Max Server Memory              | Controls maximum SQL Server memory allocation                 |
| Min Server Memory              | Controls minimum memory allocation target                     |
| Max Degree of Parallelism      | Controls parallel query execution                             |
| Cost Threshold for Parallelism | Controls parallelism cost threshold                           |
| Optimize for Ad Hoc Workloads  | Reduces plan cache memory usage for certain ad hoc workloads  |
| Remote Admin Connections       | Controls dedicated administrator connection availability      |
| Database Mail XPs              | Enables Database Mail extended stored procedure functionality |
| Remote Access                  | Controls remote stored procedure execution                    |
| User Connections               | Configures the maximum number of concurrent user connections  |

### **4. Enable backup compression by default**

```
EXEC sp_configure
    'show advanced options', 1;

RECONFIGURE;

EXEC sp_configure
    'backup compression default', 1;

RECONFIGURE;
```

### **5. Configure Max Server Memory**

```
EXEC sp_configure
    'max server memory (MB)', 8192;

RECONFIGURE;
```

Example: 8192 MB = 8 GB.

The value must be determined using actual workload and server resource requirements.

### **6. Important configuration distinction**

Not all SQL Server configuration settings are controlled through `sp_configure`.

| Configuration              | Configuration location                         |
| -------------------------- | ---------------------------------------------- |
| Max Server Memory          | sp_configure                                   |
| MAXDOP                     | sp_configure                                   |
| Backup Compression Default | sp_configure                                   |
| TCP/IP                     | SQL Server Configuration Manager               |
| Service Account            | SQL Server Configuration Manager               |
| SQL Authentication Mode    | SSMS Server Properties                         |
| Default Data Path          | Server Properties / installation configuration |
| Default Backup Path        | Server Properties / installation configuration |
| TempDB File Configuration  | ALTER DATABASE                                 |
| Database Recovery Model    | ALTER DATABASE                                 |

## **Lesson 16: SQL Server Instance-Level and Database-Level Administration**

A DBA must understand the difference between instance-level and database-level administration.

| Instance-level administration | Database-level administration |
| ----------------------------- | ----------------------------- |
| SQL Server services           | Database creation             |
| SQL Server memory             | Database files                |
| Authentication mode           | Recovery model                |
| TCP/IP configuration          | Database security             |
| Server roles                  | Database roles                |
| SQL Agent                     | Index maintenance             |
| Server configuration          | Database integrity            |
| Linked servers                | Database backup and restore   |

### **Example: Retrieve server information**

```
SELECT
    @@SERVERNAME AS ServerName,
    SERVERPROPERTY('Edition') AS Edition,
    SERVERPROPERTY('ProductVersion') AS Version;
```

### **Example: Database inventory**

```
SELECT
    name,
    state_desc,
    recovery_model_desc,
    compatibility_level
FROM sys.databases;
```

# **Module 8: Database Creation and Storage Administration**

## **Lesson 17: Creating Databases**

A DBA creates databases according to application and client requirements.

### **Information required from the client**

1. Database name.
2. Initial database size.
3. Expected growth.
4. Data file location.
5. Log file location.
6. Autogrowth configuration.
7. Recovery model.
8. Availability requirements.
9. Backup retention requirements.
10. Performance and storage requirements.

### **Example: Create database**

```
CREATE DATABASE EmployeeDB;
```

### **Example: Create database with separate files**

```
CREATE DATABASE EmployeeDB
ON PRIMARY
(
    NAME = 'EmployeeDB_Data',
    FILENAME = 'E:\SQLDATA\EmployeeDB.mdf',
    SIZE = 500MB,
    FILEGROWTH = 256MB
)
LOG ON
(
    NAME = 'EmployeeDB_Log',
    FILENAME = 'L:\SQLLOGS\EmployeeDB_log.ldf',
    SIZE = 256MB,
    FILEGROWTH = 128MB
);
```

### **Verify database**

```
EXEC sp_helpdb 'EmployeeDB';
```

### **Verify database files**

```
USE EmployeeDB;
GO

SELECT
    name,
    physical_name,
    type_desc,
    size * 8 / 1024 AS SizeMB
FROM sys.database_files;
```

## **Lesson 18: Database Storage and File Management**

Important concepts:

- MDF files.
- NDF files.
- LDF files.
- Filegroups.
- Initial file size.
- Autogrowth.
- Maximum file size.
- Disk capacity.
- Storage latency.
- IOPS.

### **Example: Storage planning**

```
Database: XYZ

Data Files:
E:\SQLDATA\XYZ.mdf

Log Files:
L:\SQLLOGS\XYZ_log.ldf

Backup Files:
H:\SQLBACKUPS\

TempDB:
T:\SQLTEMPDB\
```

**Real-time DBA responsibility:** Coordinate with the Windows and Storage teams before creating or expanding database files. Verify available capacity, storage performance and redundancy.

# **Module 9: SQL Server Patching and Upgrades**

## **Lesson 19: SQL Server Servicing**

SQL Server requires periodic updates to address security vulnerabilities, defects and reliability issues.

### **Servicing types**

1. RTM.
2. GDR.
3. Cumulative Update (CU).
4. Hotfixes and applicable servicing packages.
5. Historical Service Packs.

### **Example: SQL Server 2019**

```
Before Patching:

15.0.2000.5

After Patching:

15.0.4510.2
```

These are illustrative build numbers from your lab notes. Always verify the applicable build against Microsoft's build history.

### **SQL Server patching procedure**

**Pre-patching activities**

1. Obtain approved Change Request.
2. Confirm application downtime.
3. Review SQL Server version and current build.
4. Review Microsoft release notes.
5. Check OS and SQL Server compatibility.
6. Review disk space.
7. Review SQL Server error logs.
8. Take required database backups.
9. Confirm rollback and recovery arrangements.
10. Coordinate with the Windows team.

**Patching activities**

1. Stop or drain application traffic as required.
2. Apply the approved SQL Server update.
3. Restart services or the server as required.
4. Validate the SQL Server build.
5. Validate SQL Server Agent.
6. Check database status.
7. Check application connectivity.

**Post-patching activities**

- Verify all databases are ONLINE.
- Verify SQL Agent jobs.
- Check backups.
- Check linked servers.
- Validate application transactions.
- Review error logs.
- Complete change documentation.

### **In-place vs. side-by-side upgrade**

| In-place upgrade                          | Side-by-side upgrade                 |
| ----------------------------------------- | ------------------------------------ |
| Upgrades existing instance                | Builds a new instance                |
| Existing server is upgraded               | New server is prepared               |
| Less infrastructure required              | More infrastructure required         |
| Rollback can be complex                   | Easier to retain the old environment |
| Requires careful compatibility assessment | Requires migration and validation    |

Example:

```
SQL Server 2019 → SQL Server 2025
```

**Important:** SQL Server patching and major-version upgrading are different activities. SQL Server 2019 to 2025 is a major-version upgrade, not a routine CU installation.

# **Module 10: Database Backup and Recovery**

## **Lesson 20: Backup Fundamentals**

### **Types of backups**

1. Full backup.
2. Differential backup.
3. Transaction log backup.
4. Copy-only backup.
5. File and filegroup backup.

### **Recovery models**

| Recovery model | Full backup | Differential backup | Log backup |
| -------------- | ----------- | ------------------- | ---------- |
| SIMPLE         | Yes         | Yes                 | No         |
| FULL           | Yes         | Yes                 | Yes        |
| BULK_LOGGED    | Yes         | Yes                 | Yes        |

### **Important concepts**

- LSN – Log Sequence Number.
- FLSN – First LSN.
- LLSN – Last LSN.
- Backup chain.
- Log truncation.
- Recovery Point Objective (RPO).
- Recovery Time Objective (RTO).
- Backup retention.
- Backup compression.
- Backup checksums.

### **Example: Full backup**

```
BACKUP DATABASE EmployeeDB
TO DISK = 'H:\SQLBACKUPS\EmployeeDB_Full.bak'
WITH
    COMPRESSION,
    CHECKSUM,
    STATS = 10;
```

### **Example: Differential backup**

```
BACKUP DATABASE EmployeeDB
TO DISK = 'H:\SQLBACKUPS\EmployeeDB_Diff.diff'
WITH
    DIFFERENTIAL,
    COMPRESSION,
    CHECKSUM,
    STATS = 10;
```

### **Example: Transaction log backup**

```
BACKUP LOG EmployeeDB
TO DISK = 'H:\SQLBACKUPS\EmployeeDB_Log.trn'
WITH
    COMPRESSION,
    CHECKSUM,
    STATS = 10;
```

The database must be configured with FULL or BULK_LOGGED recovery, and the required log backup chain must be established.

### **Example: Copy-only backup**

```
BACKUP DATABASE EmployeeDB
TO DISK = 'H:\SQLBACKUPS\EmployeeDB_CopyOnly.bak'
WITH
    COPY_ONLY,
    COMPRESSION,
    CHECKSUM;
```

Copy-only full backups do not change the differential base.

## **Lesson 21: Backup Scheduling and Retention**

### **Example: Small database environment**

| Backup type     | Frequency          |
| --------------- | ------------------ |
| Full            | Daily              |
| Differential    | Every 4–12 hours   |
| Transaction log | Every 5–30 minutes |

### **Example: Large database environment**

| Backup type     | Frequency          |
| --------------- | ------------------ |
| Full            | Weekly             |
| Differential    | Every 4–12 hours   |
| Transaction log | Every 5–30 minutes |

These are starting examples, not universal schedules. Frequency must be based on RPO, RTO, change rate, backup duration and restore capability.

### **Backup retention example**

```
Backup Drive: H:\SQLBACKUPS

Total Capacity: 1 TB

Retention: 7 days

Day 1: Full backup
Day 2: Differential + Log backups
Day 3: Differential + Log backups
Day 4: Differential + Log backups
Day 5: Differential + Log backups
Day 6: Differential + Log backups
Day 7: Differential + Log backups
```

Implement automated cleanup according to the approved retention policy. Do not delete backups that are still needed for recovery or compliance.

## **Lesson 22: Database Restore and Recovery**

### **Important restore options**

| Option     | Purpose                                                    |
| ---------- | ---------------------------------------------------------- |
| NORECOVERY | Leaves database in RESTORING state for subsequent restores |
| RECOVERY   | Completes restore and brings database online               |
| REPLACE    | Overrides certain existing database/file protections       |
| MOVE       | Relocates database files                                   |
| STOPAT     | Performs point-in-time recovery                            |
| STATS      | Displays restore progress                                  |

### **Example: Restore full backup**

```
RESTORE DATABASE EmployeeDB
FROM DISK = 'H:\SQLBACKUPS\EmployeeDB_Full.bak'
WITH NORECOVERY, STATS = 10;
```

### **Example: Restore differential backup**

```
RESTORE DATABASE EmployeeDB
FROM DISK = 'H:\SQLBACKUPS\EmployeeDB_Diff.diff'
WITH NORECOVERY, STATS = 10;
```

### **Example: Restore transaction log backup**

```
RESTORE LOG EmployeeDB
FROM DISK = 'H:\SQLBACKUPS\EmployeeDB_Log.trn'
WITH RECOVERY, STATS = 10;
```

The full backup, differential backup and log backups must belong to the correct recovery sequence. If multiple log backups exist, restore them in LSN order, using NORECOVERY until the final restore.

### **Restore database under a different name**

```
RESTORE FILELISTONLY
FROM DISK = 'H:\SQLBACKUPS\EmployeeDB_Full.bak';
GO

RESTORE DATABASE EmployeeDB_Refresh
FROM DISK = 'H:\SQLBACKUPS\EmployeeDB_Full.bak'
WITH
    RECOVERY,
    MOVE 'EmployeeDB_Data'
    TO 'E:\SQLDATA\EmployeeDB_Refresh.mdf',
    MOVE 'EmployeeDB_Log'
    TO 'L:\SQLLOGS\EmployeeDB_Refresh_log.ldf',
    STATS = 10;
```

Logical file names must be obtained from `RESTORE FILELISTONLY`; do not assume they match the database name.

### **Point-in-time recovery**

```
RESTORE LOG EmployeeDB
FROM DISK = 'H:\SQLBACKUPS\EmployeeDB_Log.trn'
WITH
    STOPAT = '2026-11-25T10:30:00',
    RECOVERY,
    STATS = 10;
```

This is an illustrative final log restore. The required preceding full, differential and log backups must already have been restored in sequence.

### **Backup validation commands**

```
RESTORE VERIFYONLY
FROM DISK = 'H:\SQLBACKUPS\EmployeeDB_Full.bak';
```

```
RESTORE HEADERONLY
FROM DISK = 'H:\SQLBACKUPS\EmployeeDB_Full.bak';
```

```
RESTORE FILELISTONLY
FROM DISK = 'H:\SQLBACKUPS\EmployeeDB_Full.bak';
```

Remember: a successful `VERIFYONLY` does not guarantee that a database can be fully restored. Regular test restores are mandatory.

# **Module 11: SQL Server Security Administration**

## **Lesson 23: SQL Server Authentication**

SQL Server supports two primary authentication methods.

### **1. Windows Authentication**

- Uses Windows local accounts or Active Directory accounts.
- Supports Windows security groups.
- Preferred for enterprise environments where practical.

### **2. SQL Server Authentication**

- Uses SQL Server-created logins.
- Requires a username and password.
- Requires appropriate password policies and security controls.

### **Example: Authentication error**

```
Login failed for user 'sa'.

Server is configured for
Integrated authentication only.
```

Possible reason:

- SQL Server is configured for Windows Authentication only.
- SQL Server Authentication is not enabled.

Solution:

1. Open SSMS.
2. Right-click the SQL Server instance.
3. Select Properties.
4. Select Security.
5. Choose SQL Server and Windows Authentication mode.
6. Apply the configuration.
7. Restart the SQL Server service.
8. Validate authentication.

Do not enable the `sa` login unnecessarily. Prefer individual, controlled administrative accounts.

## **Lesson 24: Login and Database User Management**

Understand the difference between:

| Login                                     | Database User                     |
| ----------------------------------------- | --------------------------------- |
| Instance-level security principal         | Database-level security principal |
| Created at SQL Server instance level      | Created inside a database         |
| Used to authenticate                      | Used to authorize database access |
| Can access multiple databases when mapped | Belongs to a particular database  |

### **Create Windows login**

```
USE master;
GO

CREATE LOGIN [SONY\Praveen]
FROM WINDOWS;
GO
```

### **Create SQL login**

```
CREATE LOGIN PraveenSQL
WITH PASSWORD = 'Use-A-Strong-Unique-Password';
GO
```

Use a securely managed password rather than storing production passwords in scripts.

### **Create database user**

```
USE EmployeeDB;
GO

CREATE USER PraveenUser
FOR LOGIN PraveenSQL;
GO
```

### **Verify logins**

```
SELECT
    name,
    type_desc,
    sid,
    is_disabled
FROM sys.server_principals;
```

### **Verify database users**

```
USE EmployeeDB;
GO

SELECT
    name,
    type_desc,
    sid
FROM sys.database_principals;
```

## **Lesson 25: SQL Server Roles and Permissions**

### **Fixed server roles**

| Role          | Responsibility                                       |
| ------------- | ---------------------------------------------------- |
| sysadmin      | Full instance administration                         |
| serveradmin   | Server-wide configuration                            |
| securityadmin | Login and security administration                    |
| processadmin  | Manage SQL Server processes                          |
| setupadmin    | Manage linked servers and certain startup procedures |
| bulkadmin     | Bulk insert operations                               |
| diskadmin     | Manage disk files                                    |
| dbcreator     | Create, alter, drop and restore databases            |
| public        | Default server role                                  |

### **Database roles**

| Role              | Responsibility                                  |
| ----------------- | ----------------------------------------------- |
| db_owner          | Full database-level control                     |
| db_datareader     | Read data from user tables and views            |
| db_datawriter     | Insert, update and delete data                  |
| db_ddladmin       | Execute supported DDL operations                |
| db_securityadmin  | Manage database permissions and role membership |
| db_backupoperator | Perform database backups                        |
| db_accessadmin    | Manage database access                          |

### **Add login to server role**

```
ALTER SERVER ROLE sysadmin
ADD MEMBER [SONY\Praveen];
```

Use this only when full instance administration is explicitly authorized.

### **Add user to database role**

```
USE EmployeeDB;
GO

ALTER ROLE db_datareader
ADD MEMBER PraveenUser;
```

### **Object-level permissions**

```
GRANT SELECT
ON dbo.Employee
TO PraveenUser;
```

```
GRANT INSERT
ON dbo.Employee
TO PraveenUser;
```

```
DENY DELETE
ON dbo.Employee
TO PraveenUser;
```

Explain the following concepts:

- GRANT.
- DENY.
- REVOKE.
- Schema-level permissions.
- Object-level permissions.
- Column-level permissions.
- Principle of least privilege.

## **Lesson 26: Windows Groups and SQL Server Security**

This is an important real-time enterprise DBA scenario from your original notes.

### **Scenario: New employee joins an organization**

1. Windows Administration team creates the employee's Active Directory account.
2. The employee is added to an appropriate Windows security group.
3. DBA creates a SQL Server login for the Windows group.
4. Individual group members receive access according to their group membership.

### **Example**

```
Windows Server: SONY

Windows Group:
SONY\SQLDBATeam

Members:

1. Mohd
2. Deepak
3. Praveen
4. Jyothi
```

Instead of creating four separate SQL Server logins, the DBA can create one Windows group login.

```
USE master;
GO

CREATE LOGIN [SONY\SQLDBATeam]
FROM WINDOWS;
GO
```

### **Add Windows group to server role**

```
ALTER SERVER ROLE
sysadmin
ADD MEMBER [SONY\SQLDBATeam];
```

Again, use sysadmin only if all group members genuinely require unrestricted instance-level privileges.

### **Verify Windows group membership**

```
EXEC xp_logininfo
    'SONY\SQLDBATeam',
    'members';
```

Expected output includes:

- Account name.
- Account type.
- Privilege.
- Mapped login name.
- Permission path.

## **Lesson 27: Orphaned Users and Database Refresh Security**

### **What is an orphaned user?**

An orphaned user occurs when a database user is not correctly mapped to its intended SQL Server login.

This commonly occurs during database migration or refresh when database users and server logins are transferred independently.

### **Identify orphaned users**

```
USE EmployeeDB;
GO

SELECT
    dp.name AS DatabaseUser,
    dp.sid
FROM sys.database_principals dp
LEFT JOIN sys.server_principals sp
    ON dp.sid = sp.sid
WHERE dp.type IN ('S', 'U', 'G')
  AND dp.authentication_type = 1
  AND sp.sid IS NULL;
```

### **Fix orphaned user**

```
USE EmployeeDB;
GO

ALTER USER EmployeeUser
WITH LOGIN = EmployeeLogin;
```

### **Important DBA responsibilities during DB refresh**

- Transfer or provision required logins.
- Preserve login SIDs when migrating SQL logins where appropriate.
- Verify database user mappings.
- Recreate required permissions.
- Validate server role membership.
- Review SQL Agent job ownership.
- Validate application connectivity.

**Important:** Windows group membership, contained database users and database-level permissions need separate consideration. Not every database user is necessarily orphaned just because a matching server login is absent.

# **Module 12: SQL Server Maintenance and Automation**

## **Lesson 28: Database Maintenance Activities**

A DBA must perform regular database maintenance.

| Maintenance activity   | Purpose                                            |
| ---------------------- | -------------------------------------------------- |
| Full backup            | Database recovery                                  |
| Differential backup    | Captures changes since differential base           |
| Transaction log backup | Supports log truncation and point-in-time recovery |
| Index rebuild          | Rebuilds an index                                  |
| Index reorganize       | Reorganizes leaf-level index pages                 |
| Update statistics      | Helps optimizer estimate cardinality               |
| DBCC CHECKDB           | Checks database consistency                        |
| Disk monitoring        | Prevents storage-related incidents                 |

### **Index maintenance**

Understand:

- Clustered indexes.
- Nonclustered indexes.
- Index fragmentation.
- Page density.
- Index rebuild.
- Index reorganize.
- Statistics updates.

**Important:** Do not rebuild every index on a fixed schedule simply because fragmentation exists. Consider page count, fragmentation, page density, workload and maintenance cost.

### **DBCC CHECKDB**

```
DBCC CHECKDB ('EmployeeDB')
WITH NO_INFOMSGS;
```

This checks logical and physical integrity of the database.

Never make repair options the default response to integrity errors. Investigate the underlying issue and prioritize recovery from a valid backup.

## **Lesson 29: SQL Server Agent**

[sql server - Backup of Job's List only - Database Administrators Stack Exchange](https://images.openai.com/static-rsc-4/6IspasoHmLg6c-zqK3iAum4ulEloLeLXTHNjiRVswMsa1hRaaKtdx738Dw-TqIAUM7FKwRUQqN81NKl0ewRgReYp3cm-F5f3WfsDy8eHA8Rz4woC7UlJJuluRnA9lKmlcCdCUX8huhOLlx-o2SV5do90gVLtVnlWJ6XkoPZLCfI?purpose=inline)

[dba.stackexchange.com](https://dba.stackexchange.com/questions/54202/backup-of-jobs-list-only)

SQL Server Agent automates recurring administrative activities.

### **Important components**

1. Jobs.
2. Job Steps.
3. Schedules.
4. Operators.
5. Alerts.
6. Proxies.

### **Common DBA jobs**

- Full backup jobs.
- Differential backup jobs.
- Transaction log backup jobs.
- Index maintenance jobs.
- Statistics update jobs.
- DBCC CHECKDB jobs.
- Database cleanup jobs.
- Monitoring jobs.

### **SQL Server Agent limitations**

SQL Server Agent is not included in Express Edition. Alternative scheduling and automation methods must be considered for Express environments.

## **Lesson 30: Database Mail and Alerts**

### **Database Mail**

Used for sending email notifications from SQL Server.

Example:

```
EXEC msdb.dbo.sp_send_dbmail
    @profile_name = 'DBA_Profile',
    @recipients = 'dba@example.com',
    @subject = 'SQL Server DBA Notification',
    @body = 'Database maintenance completed.';
```

The mail profile and SMTP configuration must already be established.

### **SQL Server alerts**

Configure alerts for:

- Severity-based errors.
- Selected SQL Server error numbers.
- Job failures.
- Backup failures.
- Database availability issues.

# **Module 13: High Availability and Disaster Recovery**

## **Lesson 31: Introduction to HA and DR**

### **High Availability (HA)**

HA aims to minimize service interruption when a component fails.

### **Disaster Recovery (DR)**

DR focuses on restoring services following major failures such as:

- Server failure.
- Storage failure.
- Data center failure.
- Site-level disaster.
- Major infrastructure outage.

### **RPO and RTO**

| Term | Meaning                                       |
| ---- | --------------------------------------------- |
| RPO  | Maximum acceptable data loss measured in time |
| RTO  | Maximum acceptable service recovery time      |

## **Lesson 32: SQL Server HA/DR Technologies**

## **SQL Server HA/DR technologies**

**1. Log Shipping**

[Manage high availability and disaster recovery | Microsoft Press Store](https://images.openai.com/static-rsc-4/BAY1l6nta450x2vB0CnDZlESdbPN_4mTF4lcLhLeWmFStXv0LQUsI0nB98Ho_S4J0o9B4Gzcbs8xPMtmkmXm_Q2OuSvYyGDax5BIN5uzYfSgdpMIZr8_LLU7-GqD3mnj4eU0MvjN6U784p5qPTO4AD4CSyfM9q_sZZPb4J_w8Bw?purpose=inline)

[microsoftpressstore.com](https://www.microsoftpressstore.com/articles/article.aspx?p=2832586\&seqNum=3\)

- Transaction log backups are copied and restored to secondary databases.
- Primarily used for DR and warm standby scenarios.
- Failover is manual.

**2. Database Mirroring**

[How to Design HA/DR Strategy - Microsoft SQL Server](https://images.openai.com/static-rsc-4/Br2y779xswrCKQXGrJKZMusO5Pz5Gf-kgA7WApBtbBGleDl9YdI-8Y3BQGItFIE5WNcuTTgVwI9siyUVzOuBkLit2pbTb_3GJeOT7pGY2VELP7yEXyw2lgqxizWsYo38WegbeAKQqB9g5WN3AER91FFwykd_g5htVTLPL-zSnIg?purpose=inline)

[jadeglobal.com](https://www.jadeglobal.com/blog/how-design-hadr-strategy-microsoft-sql-server)

- Uses principal and mirror databases.
- Supports synchronous and asynchronous operating modes.
- Automatic failover requires a witness and synchronous configuration.
- Deprecated technology; do not select it for new designs.

**3. SQL Server Replication**

[Transactional Replication | Professional SQL Server High Availability and Disaster Recovery](https://images.openai.com/static-rsc-4/jFWa1yEHo70PuD6IAajyTw8xUuF5PHtY-aNza9Jw3yTdlejKbLN8eq4eOxlb4I72Ekv5qi1m3hhp8O1uiG-a_7ImlIsTettQX4W130nOdzzsak1_veeuw_g0PrvGDjk1tQSuwot1Xc_-Fhjmnnod_emnjdnadDuScduwjXiTnE4?purpose=inline)

[subscription.packtpub.com](https://subscription.packtpub.com/book/web_development/9781789802597/2/ch02lvl1sec12/understanding-transactional-replication)

- Publisher.
- Distributor.
- Subscriber.
- Supports data distribution and synchronization.
- It is not a substitute for a complete HA/DR strategy.

**4. Failover Cluster Instance (FCI)**

[Manage high availability and disaster recovery | Microsoft Press Store](https://images.openai.com/static-rsc-4/A_deAekCjtCabhkMDCLaK4Mvp1p9XKm-lz5n5gXYubMw0HsM5Yt2p2O1Dh3WxRlxMvuFI1MYriOFj17_R6QUOuMyP_t1x90yCcJp0IE4xJC3hYV-Ht_HZhIJ3r1wL70GX7JbFRIbVPnbUueotGX35xnX7rmrIyBQDOpMnZHRRrE?purpose=inline)

[microsoftpressstore.com](https://www.microsoftpressstore.com/articles/article.aspx?p=2832586\&seqNum=5\)

- Provides instance-level high availability.
- Uses Windows Server Failover Clustering.
- Requires supported shared storage architecture.
- Database files remain on the shared storage.

**5. Always On Availability Groups**

[SQL Server Infrastructure & High Availability: RAID, Backup & DR](https://images.openai.com/static-rsc-4/oxtjm8EdJXwBv-0Om5l-pqFhFG0OSDvtS1gDAIkh8Mg716It5ABAzjDmDFyukwAu7IKrozBWrZAvNNHF4lz3wiONGI6NZN5FqvuZqgnjSUAtSbv1jtG6heDrwUTt1SfHmyIgX2krOvMFfPdZxwhc5x3UQ5K-_E3uO7l3nS8oQig?purpose=inline)

[rileylog.com](https://rileylog.com/blog/db-07-infrastructure-ha/)

- Provides database-level availability.
- Supports synchronous and asynchronous commit.
- Supports manual and automatic failover under appropriate configurations.
- Does not require shared storage for database files.

**6. Distributed Availability Groups**

[An overview of distributed SQL Server Always On Availability Groups](https://images.openai.com/static-rsc-4/vKABvaCsobZc-7wAz7NGZSs_POdkX0AIzYGBGudoUd6DAnavv1KB66lCc99meoQa0P4ZDFfuVt8UBrDzXNtbpb6qLa-9QaLAWchGDD2qJYV7k_bQQpjuHbMl2T8zzpqqkfiEWJmwr1P3wyyeWZLe1CpYlN0PrYcof86cLTv73m0?purpose=inline)

[sqlshack.com](https://www.sqlshack.com/an-overview-of-distributed-sql-server-always-on-availability-groups/)

- Connects two separate Availability Groups.
- Supports multi-site and migration architectures.
- Commonly used in advanced HA/DR designs.

## **Lesson 33: SQL Server Always On Availability Groups**

### **Important components**

1. Primary replica.
2. Secondary replica.
3. Availability databases.
4. Availability Group Listener.
5. Windows Server Failover Cluster.
6. Synchronous commit.
7. Asynchronous commit.

### **Synchronous commit**

- Primary and secondary replicas coordinate transaction hardening.
- Can support automatic failover when all required conditions are met.
- Provides stronger protection against data loss during supported failover conditions.

### **Asynchronous commit**

- Primary does not wait for secondary hardening before acknowledging the transaction.
- Suitable for geographically distant DR replicas.
- Forced failover may involve data loss.

### **Standard vs. advanced Availability Group capabilities**

Teach students to distinguish:

- Basic Availability Groups available in supported Standard Edition configurations.
- Advanced Availability Groups available with Enterprise Edition.
- Distributed Availability Groups and their prerequisites.

Do not assume all Availability Group capabilities are available in every edition.

## **Lesson 34: Failover and Failback**

### **What is failover?**

Failover is the process of transferring the database service role from one replica or server to another.

Example:

```
Before Failover:

Server A = Primary
Server B = Secondary

After Failover:

Server A = Secondary
Server B = Primary
```

### **Types of failover**

1. Planned manual failover.
2. Automatic failover.
3. Forced failover.

The actual options depend on the HA technology and configuration.

### **What is failback?**

Failback means returning the service to the preferred original server or site after the issue is resolved.

Example:

```
Before:

Server A = Primary
Server B = Secondary

Failover:

Server A = Secondary
Server B = Primary

Failback:

Server A = Primary
Server B = Secondary
```

**Important:** Failback is not necessarily automatic. It requires validation, synchronization and a controlled role transition.

### **Your President and VP analogy**

A simpler teaching analogy:

- President = Primary replica.
- Vice President = Secondary replica.
- President becomes unavailable.
- Vice President assumes the President's responsibilities.
- Original President returns.
- Responsibilities are transferred back through an approved transition.

This helps beginners understand role switching.

# **Module 14: SQL Server Migrations and Upgrades**

## **Lesson 35: SQL Server Migration vs. Database Migration**

These are different activities.

| SQL Server migration                                     | Database migration                               |
| -------------------------------------------------------- | ------------------------------------------------ |
| Moves an instance or workload to another server/platform | Moves a particular database                      |
| May include logins, jobs and linked servers              | Primarily includes database files and metadata   |
| Requires instance configuration                          | Requires database-level validation               |
| Requires application connectivity changes                | May require application database mapping changes |

### **Migration scenarios**

1. On-premises to on-premises.
2. On-premises to AWS.
3. On-premises to Azure.
4. SQL Server to SQL Server.
5. SQL Server to Azure SQL Managed Instance.
6. SQL Server to Azure SQL Database.

### **Example**

```
Source:
SQL Server 2019

Destination:
SQL Server 2025
```

### **Database migration checklist**

- Database backup.
- Database restore.
- Database compatibility assessment.
- Login migration.
- User migration.
- SQL Agent jobs.
- Linked servers.
- Credentials.
- Database Mail.
- Server configuration.
- Application validation.
- Performance validation.

## **Lesson 36: SQL Server Upgrade Methods**

### **1. In-place upgrade**

Existing SQL Server installation is upgraded.

Example:

```
SQL Server 2019
       |
       V
SQL Server 2025
```

### **2. Side-by-side upgrade**

New SQL Server instance is installed, and databases are migrated.

```
Old Server:
SQL Server 2019

        |
        | Database migration
        V

New Server:
SQL Server 2025
```

### **Important upgrade checks**

- Supported upgrade paths.
- Windows Server compatibility.
- SQL Server edition.
- Application compatibility.
- Deprecated features.
- Database compatibility level.
- Linked server dependencies.
- SQL Agent jobs.
- Backup and recovery plan.
- Rollback strategy.

# **Module 15: SQL Server Performance Tuning and Troubleshooting**

## **Lesson 37: Four Levels of Performance Troubleshooting**

Your four-level classification is correct and should be taught as a standard troubleshooting framework.

**1. Windows Level**

Infrastructure

- CPU utilization.
- Physical memory.
- Disk latency.
- Storage throughput.
- Network connectivity.
- Windows resource pressure.

**2. SQL Server Instance Level**

- SQL Server memory configuration.
- MAXDOP.
- Cost Threshold for Parallelism.
- Worker threads.
- Wait statistics.
- SQL Server error logs.
- Instance configuration.

**3. Database Level**

- Indexes.
- Statistics.
- Database file growth.
- Transaction log usage.
- Blocking.
- Deadlocks.
- Database configuration.

**4. Application Level**

- Inefficient SQL queries.
- Poor transaction design.
- Excessive database calls.
- Connection pooling.
- Application timeouts.
- Parameterization problems.

## **Lesson 38: Performance Tuning Topics**

Students should learn:

1. SQL Server architecture.
2. Query processing architecture.
3. Execution plans.
4. Clustered and nonclustered indexes.
5. Index fragmentation and page density.
6. Statistics and cardinality estimation.
7. Blocking and deadlocks.
8. Wait statistics.
9. CPU and memory pressure.
10. Disk I/O performance.
11. TempDB contention.
12. Parallelism.
13. Parameter sniffing.
14. Query Store.
15. Extended Events.
16. Dynamic Management Views (DMVs).

### **Basic monitoring example**

```
SELECT
    session_id,
    status,
    command,
    cpu_time,
    total_elapsed_time,
    wait_type,
    blocking_session_id
FROM sys.dm_exec_requests
WHERE session_id > 50;
```

# **Module 16: DBA Automation and Database Refresh**

## **Lesson 39: Automation of Administrative Activities**

A DBA should automate repetitive administrative activities.

| Activity             | Automation method              |
| -------------------- | ------------------------------ |
| Full backups         | SQL Server Agent               |
| Differential backups | SQL Server Agent               |
| Log backups          | SQL Server Agent               |
| Index maintenance    | SQL Server Agent               |
| Statistics updates   | SQL Server Agent               |
| DBCC CHECKDB         | SQL Server Agent               |
| Database refresh     | PowerShell / T-SQL / SQL Agent |
| Monitoring           | DMVs / PowerShell              |
| Email notifications  | Database Mail                  |

## **Lesson 40: Database Refresh – Source to Destination**

### **Real-time scenario**

```
Source Environment:

Delhi SQL Server

Database: XYZ

Data File: E:\XYZ.mdf
Log File: H:\XYZ_log.ldf


Destination Environment:

Chennai SQL Server

Data File: P:\XYZ.mdf
Log File: Q:\XYZ_log.ldf
```

### **Database refresh process**

1. Confirm source and destination database details.
2. Obtain approved Service Request or Change Request.
3. Confirm database backup.
4. Transfer backup files.
5. Restore database to destination.
6. Use MOVE for destination file locations.
7. Fix login and database user mappings.
8. Validate permissions.
9. Disable or adjust production-specific jobs where necessary.
10. Validate database objects and data.
11. Obtain application team confirmation.
12. Close the request.

### **Important production considerations**

- Do not overwrite production databases without authorization.
- Validate database names and destination paths.
- Preserve required security mappings.
- Avoid accidentally executing production integrations from a refreshed non-production database.
- Mask sensitive data when required by organizational policy.

# **Module 17: Production DBA Operations and ITIL**

## **Lesson 41: Incident, Change and Service Request Management**

A production DBA does not simply execute SQL scripts. Every change must follow organizational operational procedures.

### **1. Incident Management**

Used when an existing service is interrupted or degraded.

Examples:

- SQL Server is down.
- Database is inaccessible.
- Transaction log is full.
- Blocking affects application transactions.
- Backup job failed.

### **2. Change Request**

Used when making a controlled change to the production environment.

Types:

- Normal Change.
- Emergency Change.
- Expedited Change, depending on the organization's process.

Normal changes generally require formal assessment and approval, often through a Change Advisory Board (CAB).

Emergency changes follow the organization's emergency approval process. They do not automatically bypass governance.

### **3. Service Request**

Examples:

- Create a new database.
- Create a login.
- Grant database access.
- Perform a database refresh.
- Configure a SQL Agent job.

### **4. Incident priority**

| Priority | Example                                                |
| -------- | ------------------------------------------------------ |
| P1       | Complete production database outage                    |
| P2       | Major application database degradation                 |
| P3       | Limited application or database functionality affected |
| P4       | Low-impact issue or routine request                    |

Actual priority definitions should follow the organization's SLA.

## **Lesson 42: Production Incident Escalation**

Example:

```
Application Team reports P1
          |
          V
Command Center
          |
          V
Incident Manager
          |
          +----------------+
          |                |
          V                V
Windows Team           Network Team
          |                |
          +--------+-------+
                   |
                   V
               DBA Team
                   |
                   V
             Application Team
                   |
                   V
             Service Restored
                   |
                   V
             Root Cause Analysis
```

The DBA should:

- Understand the reported issue.
- Identify business impact.
- Check database availability.
- Investigate SQL Server error logs.
- Check blocking and active transactions.
- Check storage and CPU pressure.
- Coordinate with infrastructure and application teams.
- Document findings.
- Provide incident updates.
- Prepare root cause analysis (RCA).

# **Final Consolidated Training Roadmap**

The following structure incorporates your original 45-day syllabus and the additional topics.

| Days  | Module                     | Lessons                                                      |
| ----- | -------------------------- | ------------------------------------------------------------ |
| 1–3   | SQL Server Fundamentals    | Developer vs DBA, versions, editions, components             |
| 4–6   | Architecture               | Instances, services, connectivity, SQL tools                 |
| 7–9   | Virtualization and OS      | Windows Server, domains, VM setup                            |
| 10–12 | Installation               | Pre-installation, SQL Server installation, post-installation |
| 13–14 | Configuration              | Startup parameters, system databases, SP_CONFIGURE           |
| 15–17 | Database Administration    | Database creation, storage, recovery models                  |
| 18–19 | SQL Security               | Logins, users, roles, permissions                            |
| 20–23 | Backup and Recovery        | Full, differential, log, copy-only, restore, PITR            |
| 24–26 | Maintenance and Automation | SQL Agent, indexes, statistics, CHECKDB, Database Mail       |
| 27–30 | Monitoring and Performance | DMVs, blocking, deadlocks, CPU, memory, I/O                  |
| 31–35 | HA and DR                  | Log shipping, mirroring, replication, FCI, AG                |
| 36–37 | Migration and Upgrades     | In-place, side-by-side, database refresh                     |
| 38–40 | Production Operations      | Patching, troubleshooting, ITIL, incident management         |
| 41–43 | Practical Scenarios        | Backup failures, database recovery, production incidents     |
| 44–45 | Assessment                 | End-to-end DBA lab and interview preparation                 |

This is a sequencing recommendation; the detailed 45-day syllabus can retain its existing daily lesson breakdown.

# **Official Microsoft Learning References**

Students should use official documentation as their primary technical reference.

| Subject                  | Microsoft documentation                                                                                                                                                                          |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| SQL Server installation  | [Install SQL Server](https://learn.microsoft.com/en-us/sql/database-engine/install-windows/install-sql-server)                                                            |
| SQL Server editions      | [Editions and components](https://learn.microsoft.com/en-us/sql/sql-server/editions-and-components-of-sql-server)                                                         |
| SQL Server Configuration | [Server configuration options](https://learn.microsoft.com/en-us/sql/database-engine/configure-windows/server-configuration-options-sql-server)                           |
| Database architecture    | [Databases](https://learn.microsoft.com/en-us/sql/relational-databases/databases/databases)                                                                               |
| Backup and restore       | [Backup and restore](https://learn.microsoft.com/en-us/sql/relational-databases/backup-restore/backup-and-restore-of-sql-server-databases)                                |
| Security                 | [Database Engine permissions](https://learn.microsoft.com/en-us/sql/relational-databases/security/authentication-access/getting-started-with-database-engine-permissions) |
| Always On AG             | [Always On Availability Groups](https://learn.microsoft.com/en-us/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server)   |
| SQL Server Agent         | [SQL Server Agent](https://learn.microsoft.com/en-us/ssms/agent/sql-server-agent)                                                                                         |
| Database integrity       | [DBCC CHECKDB](https://learn.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)                                                           |
| SQL Server upgrades      | [Upgrade SQL Server](https://learn.microsoft.com/en-us/sql/database-engine/install-windows/upgrade-sql-server)                                                            |

