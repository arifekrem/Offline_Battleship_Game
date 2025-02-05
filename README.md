# README - CPS610 Assignment 1

**Group Number:** Group 12 
**Course:** CPS610  
**Instructor:** Glaucia Melo
**TA:** Jorge Lopez 

---

## **Group Members**  
| Student Number | Full Name          |  
|----------------|--------------------|  
| 500981017       | Ekrem Yilmaz  |  
| 500981017       | Mohamed Shrief |  
| 500189282       | Chris Fontein  |  

--- 

## **Summary of Implementation**
This assignment involves replicating and synchronizing the `EMPLOYEES` table between two Oracle instances (Oracle 11g as **DB1** and Oracle 12c as **DB2**). The implementation includes:  
- **Lab 2:** Manual replication using `MERGE` statements and automation via triggers.  
- **Lab 3:** Synchronization using a stored procedure, logging changes, and an attempt to automate synchronization with `DBMS_SCHEDULER` (failed due to insufficient privileges).  

---

## **File Structure**
```
📁 CPS610_A1_Group12.zip  
├── 📄 README.pdf (this file)  
├── 📄 Lab_Report.pdf (detailed explanations and challenges)  
├── 📂 Lab2/  
│   ├── 📄 lab2_schema.sql (table creation for EMPLOYEES)  
│   ├── 📄 lab2_replication.sql (insert/update/delete replication scripts)  
│   └── 📄 lab2_triggers.sql (trigger for automated replication)  
├── 📂 Lab3/  
│   ├── 📄 lab3_stored_procedure.sql (synchronization procedure)  
│   ├── 📄 lab3_logging.sql (SYNC_LOG table and sequence)  
│   ├── 📄 lab3_scheduler.sql (failed automation script)  
│   └── 📄 lab3_test_cases.sql (test cases and verification)  
```

---

## **Implementation Overview**

### **Lab 2: Database Replication**  
1. **Table Creation**  
   - Created the `EMPLOYEES` table in both DB1 and DB2.  
2. **Database Link**  
   - Established a link (`db2`) from DB1 to DB2 using credentials and connection details.  
3. **Data Insertion**  
   - Inserted sample data into `EMPLOYEES` in DB1.  
4. **Trigger Automation**  
   - Created a trigger (`trg_replicate_to_db2`) to replicate inserts, updates, and deletes to DB2.  

### **Lab 3: Stored Procedure & Logging**  
1. **SYNC_LOG Table**  
   - Created a log table in DB1 to track synchronization operations.  
2. **Stored Procedure**  
   - Implemented `sync_employees_to_db2` to synchronize data between DB1 and DB2.  
3. **Automation Attempt**  
   - Tried to schedule the procedure using `DBMS_SCHEDULER`, but encountered **insufficient privileges** (see errors below).  

---

## **Challenges Faced**  
1. **Permission Issues**  
   - Attempting to grant `CREATE JOB` and `MANAGE SCHEDULER` privileges resulted in `ORA-01031: insufficient privileges`.  
   - Automation via `DBMS_SCHEDULER` failed due to restricted permissions on the school server.  
2. **Workaround**  
   - Automation could not be implemented. Manual execution of `sync_employees_to_db2` is required.  

---

## **Special Instructions**  
1. **Database Link Configuration**  
   - Replace `eyilmaz` and `"07238034"` in `CREATE DATABASE LINK` with your Oracle 12c credentials.  
   - Ensure VPN access is active for school server connections.  
2. **Testing Automation**  
   - To test synchronization, manually execute:  
     ```sql  
     BEGIN  
         sync_employees_to_db2;  
     END;  
     /  
     ```  
3. **Error Handling**  
   - The `DBMS_SCHEDULER` automation script will fail without DBA privileges. Document this limitation in the lab report.  
