# Enable Database Vault in Autonomous Database

## Introduction

Database Vault implements powerful, unique security controls that restrict access to application data by privileged database users and enforce context-aware policies for data access by any user. Database Vault reduces the risk of insider and outside threats and addresses common compliance requirements.


### Objectives

In this lab, you will:

-   Enable Database Vault in Autonomous Database

## Task 1: Create Database Vault users in ADB-S

Database Vault enables separation of duties by implementing two dedicated database roles DV\_OWNER (used to create and manage security policies enforced by Database Vault) and DV\_ACCTMGR (used to separate the duty of database user management – including password resets – from the DBA role)

1. Set up separate users for DV\_OWNER and DV\_ACCTMGR accounts

For DV_OWNER:

---

    
    CREATE USER ADV_OWNER IDENTIFIED BY ######
    DEFAULT TABLESPACE "DATA"
    TEMPORARY TABLESPACE "TEMP";
    GRANT "DV_OWNER" TO "ADV_OWNER" WITH ADMIN OPTION;
    ALTER USER "ADV_OWNER" DEFAULT ROLE ALL; 
    GRANT CREATE SESSION TO "ADV_OWNER";


For DV_ACCTMGR :

---


    CREATE USER "ADV_ACCT_ADMIN" IDENTIFIED BY #######
    DEFAULT TABLESPACE "DATA"
    TEMPORARY TABLESPACE "TEMP";
    GRANT "DV_ACCTMGR" TO "ADV_ACCT_ADMIN" WITH ADMIN OPTION;
    ALTER USER "ADV_ACCT_ADMIN" DEFAULT ROLE ALL;
    GRANT CREATE SESSION TO "ADV_ACCT_ADMIN";

---

2. Enable Oracle Database Vault on Autonomous Database

Oracle Database Vault is disabled by default on Autonomous Database. To configure and enable Oracle Database Vault on Autonomous Database, do the following:


-	Configure Oracle Database Vault using the following command using the user and role created in above step:



---
    EXEC DBMS_CLOUD_MACADM.CONFIGURE_DATABASE_VAULT('ADV_OWNER', 'ADV_ACCT_ADMIN');


-	Enable Oracle Database Vault:


---
    EXEC DBMS_CLOUD_MACADM.ENABLE_DATABASE_VAULT;
-	Restart the Autonomous Transaction Processing instance from OCI console.


Use the following command to check if Oracle Database Vault is enabled or disabled:

---

    SELECT * FROM DBA_DV_STATUS;


Output similar to the following appears:

---
     CopyNAME                 		STATUS
     -------------------- 			-----------
     DV_CONFIGURE_STATUS  			TRUE
     DV_ENABLE_STATUS     			TRUE





The DV\_ENABLE\_STATUS value TRUE indicates Oracle Database Vault is enabled.

You may now [proceed to the next lab](#next).

## Learn more

* [Oracle Autonomous Database Documentation](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/index.html)
* [Additional Autonomous Database Tutorials](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/tutorials.html)


## Acknowledgements
* **Author** - Goutam Pal, Senior Cloud Engineer
