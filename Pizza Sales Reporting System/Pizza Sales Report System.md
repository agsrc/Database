# Part I:

### Describe the organization and the purpose of the database to be designed
> This database is for a startup pizza company whose main purpose is to provide all the information related to pizza restaurants registered with the startup along with the entertainment order. Purpose of this project is to create well defined logical model that meets all the business logic constraints and easy to be upgraded in future as and when necessary.
### Identify and list the entity sets

>APP_USER

>AVAIL

>B_OWNER

>E_ORDER

>ENTERTAINER

>H_CUSTOMER

>ORDERS

>PIZZA

>PIZZA_RESTURANT

>RELATION_PO

  

### Identify the list of attributes and the ID for each entity set (this will be the possible natural key).

>APP_USER

>>ID

>>NAME

>>DATE_OF_BIRTH

>>ADDRESS

>>IDENTITY

> AVAIL

>>ENTERTAINER_ID

>>PIZZA_RESTURANT_NAME

>>WEEKDAYS,

> B_OWNER

>ID

>LINKEDIN

> E_ORDER

>>TYPE

>>DURATION

>>ENTERTAINER_ID

>>ID

> ENTERTAINER

>>ID

>>STAGE_NAME

>>SHORT_BIO

>>PRICE

> H_CUSTOMER

>>ID

>>DELIVERY_ADDRESS

> ORDERS

>>LATEST_TIME_OF_DELIVERY

>>PLACEMENT_TIME

>>PLACEMENT_DATE

>>ID

>>NR_OF_PEOPLE

>>H_CUSTOMER_ID

> PIZZA

>>NAME

>>RESTUARNT_NAME

>>CRUST_STRUCTURE

>>PRICE

> PIZZA_RESTURANT_NAME

>>PIZZA_RESTURANT

>>NAME

>>ZIP_CODE

>>OPENING_HOURS

>>ADDRESS

>>PHONE_NUMBER

>>WEBSITE

>>B_OWNER_ID

> RELATION_PO

>>ORDER_ID

>>PIZZA_NAME

### Identify and list the business rules associate with each entity set

  

> APP_USER(business owner, entertainer, hungry customer ). Here, business owner, entertainer and hungry customer are subtypes and partially constrained to APP_USER.

> Entertainment order is partially constrained to Order.

> All the Attributes should be non-null type.

> And, the size allocation to the data type should be considered wisely in order to reduce memory allocation space.

  
  
  
  
  
  

### Identify and list the relationships among the entity sets and indicate if they are on-to-one, one-to-many, or many-to-many.

- App_user to Entertainer – one to one.

- App_user to B_owner – one to one.

- App_user to H_Customer – one to one.

- App_user to avail – one to many.

- Avail to PIZZA_Restuarant – many to one.

- PIZZA_Restuarant to PIZZA– one to many.

- Relation_PO to ORDERS -many to one.

- Relation_PO to Pizza – many to one.

- ORDERS to H_CUSTOMER – many to one.

- E_ORDER to Entertainer – many to one.

- B_Owner to Pizza_Restuarant – one to many.

  

### For each entity set identify a surrogate key or artificial key. This will be the Primary Key on the relational diagram and the ID identified in “d” is the NATURAL KEY. Both, the Primary key and the natural key need to be given the UNIQUE and NOT NULL constraints. These are the basic properties of the Primary and candidate Key.

  

- APP_USER – ID (Primary key)

- AVAIL - ENTERTAINER_ID (Artificial key)

- B_OWNER – ID (Artificial key)

- E_ORDER - ENTERTAINER_ID (Artificial key)

- ENTERTAINER- ID (Artificial key)

- H_CUSTOMER -ID (Artificial key)

- ORDERS – ID (natural key)

- ORDERS - H_CUSTOMER_ID (Artificial key)

- PIZZA – NAME (Artificial key)

- PIZZA_RESTURANT - NAME(natural key)

- RELATION_PO - PIZZA_NAME (Artificial key)

  

### Using the Oracle Datamodeler, build a dataflow diagram for the “Pizza Sales Report System”.
![DFL](https://github.com/agsrc/Database/blob/master/Pizza%20Sales%20Reporting%20System/PSRS%20Images/DFL.png)
### Using the Oracle Datamodeler build the EER diagram (conceptual design). All business rules must be entered into the Oracle Data Modeler.
![EER](https://github.com/agsrc/Database/blob/master/Pizza%20Sales%20Reporting%20System/PSRS%20Images/EER.png)
### Proceed to convert the EER diagram into a Relational Diagram. Make sure all the constraints, naming convention, etc. have been followed in your Data Model.
![Relational](https://github.com/agsrc/Database/blob/master/Pizza%20Sales%20Reporting%20System/PSRS%20Images/Relational.png)
### Proceed to generate the DDL
- Processing part.
### Create a script similar the sample database schema “Create_HR_Database_Scheme.sql” to create your schema this assignment using the DDL created in the above step. This may require making updates in the Oracle Datamodeler to make sure all the needed REFERENTIAL INTEGRITY CONSTRAINTS are created (e.g. Primary Keys, UNIQUE Keys, Referential Integrity, NULL, NOT NULL, DEFAULT)

  [PSRS.sql](https://github.com/agsrc/Database/blob/master/Pizza%20Sales%20Reporting%20System/PSRS.sql)  

### Using the Oracle SQL Developer, create an Oracle database userid “<last-Name>_<first character of First name>_HWK2” in the Oracle database “. For example: fernandezr_HWK2
![Oracle Database](https://github.com/agsrc/Database/blob/master/Pizza%20Sales%20Reporting%20System/PSRS%20Images/Oracle%20databse.png)

### Run the script that creates the database schema into your userid created above.
    ![Directory in the server](https://github.com/agsrc/Database/blob/master/Pizza%20Sales%20Reporting%20System/PSRS%20Images/Directory.png)
  [PSRS.sql](https://github.com/agsrc/Database/blob/master/Pizza%20Sales%20Reporting%20System/PSRS.sql)  
### Create INSERT statement to insert at least 20 rows in each table. Make sure that you need to load the parent tables first to avoid errors.

  
  [PSRS.sql](https://github.com/agsrc/Database/blob/master/Pizza%20Sales%20Reporting%20System/PSRS.sql)  
  

### Create at least 5 select statements to display data from the database schema.

  
  [PSRS.sql](https://github.com/agsrc/Database/blob/master/Pizza%20Sales%20Reporting%20System/PSRS.sql)  

  

### Create at least 5 delete and 5 update SQL statements.


  [PSRS.sql](https://github.com/agsrc/Database/blob/master/Pizza%20Sales%20Reporting%20System/PSRS.sql)  


### Build a PL/SQL procedure that creates a “hungry Customers Report”. The reports contains the name, address, date of sale, pizza type, cost, and at the end the total costs.

  

NOTE: the number of entities in your design could be larger that in the solution below.

  
  [PSRS.sql](https://github.com/agsrc/Database/blob/master/Pizza%20Sales%20Reporting%20System/PSRS.sql)  

# Part II:

  

### Create an Oracle RDS Instance
![RDS Instance](https://github.com/agsrc/Database/blob/master/Pizza%20Sales%20Reporting%20System/PSRS%20Images/Oracle%20RDS%20instance.png)
### Connect to the Oracle RDS Database Schema to Execute steps “m” to “p” from part 1 to create the database schema in your new Oracle RDS instance.

![Connecting to Oracle RDS instance using Oracle SQL developer](https://github.com/agsrc/Database/blob/master/Pizza%20Sales%20Reporting%20System/PSRS%20Images/connecting%20to%20RDS.png)
  
  [PSRS.sql](https://github.com/agsrc/Database/blob/master/Pizza%20Sales%20Reporting%20System/PSRS.sql)  