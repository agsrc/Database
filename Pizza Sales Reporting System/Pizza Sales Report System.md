# Part I:

### Describe the organization and the purpose of the database to be designed

> This database is for a startup pizza company whose main purpose is to provide all the information related to pizza restaurants registered with the startup along with the entertainment order. Purpose of this project is to create well defined logical model that meets all the business logic constraints and easy to be upgraded in future as and when necessary.

### Identify and list the entity sets
>	APP_USER
>	 AVAIL
>	 B_OWNER
>	 E_ORDER
>	 ENTERTAINER
>	 H_CUSTOMER
>	 ORDERS
>	 PIZZA
>	 PIZZA_RESTURANT
>	 RELATION_PO

# Identify the list of attributes and the ID for each entity set (this will be the possible natural key).
	APP_USER
ID
NAME
DATE_OF_BIRTH
ADDRESS
 	IDENTITY
	 AVAIL
 ENTERTAINER_ID
 	PIZZA_RESTURANT_NAME
 	WEEKDAYS,
	 B_OWNER
ID
LINKEDIN
	E_ORDER
TYPE
 DURATION
 	ENTERTAINER_ID
 	ID
	 ENTERTAINER
ID
STAGE_NAME
SHORT_BIO
 	PRICE
	 H_CUSTOMER
ID 
DELIVERY_ADDRESS
	 ORDERS
 	LATEST_TIME_OF_DELIVERY
 	PLACEMENT_TIME
 	PLACEMENT_DATE
 	ID
 NR_OF_PEOPLE
 	H_CUSTOMER_ID
	PIZZA
NAME
RESTUARNT_NAME
CRUST_STRUCTURE
PRICE
	 PIZZA_RESTURANT_NAME
 	PIZZA_RESTURANT
 	NAME
 ZIP_CODE
 	OPENING_HOURS
 	ADDRESS
 	PHONE_NUMBER
 	WEBSITE
 	B_OWNER_ID
	RELATION_PO
 ORDER_ID
 PIZZA_NAME

# Identify and list the business rules associate with each entity set

	APP_USER(business owner, entertainer, hungry customer ). Here, business owner, entertainer and hungry customer are subtypes and partially constrained to APP_USER.
	Entertainment order is partially constrained to Order.
	All the Attributes should be non-null type.
	And, the size allocation to the data type should be considered wisely in order to reduce memory allocation space.






### Identify and list the relationships among the entity sets and indicate if they are on-to-one, one-to-many, or many-to-many.
	App_user to Entertainer – one to one.
	App_user to B_owner – one to one.
	App_user to H_Customer – one to one.
	App_user to avail – one to many.
	avail to PIZZA_Restuarant – many to one.
	PIZZA_Restuarant to PIZZA– one to many.
	Relation_PO to ORDERS -many to one.
	Relation_PO to Pizza – many to one.
	ORDERS to H_CUSTOMER – many to one.
	E_ORDER to Entertainer – many to one.
	B_Owner to Pizza_Restuarant – one to many.

###	For each entity set identify a surrogate key or artificial key.  This will be the Primary Key on the relational diagram and the ID identified in “d” is the NATURAL KEY.  Both, the Primary key and the natural key need to be given the UNIQUE and NOT NULL constraints.  These are the basic properties of the Primary and candidate Key.

	APP_USER – ID (Primary key)
	AVAIL - ENTERTAINER_ID (Artificial key)
	B_OWNER – ID (Artificial key)
	E_ORDER -  ENTERTAINER_ID (Artificial key)
	ENTERTAINER- ID (Artificial key)
	H_CUSTOMER -ID (Artificial key)
	ORDERS – ID (natural key)
	ORDERS - H_CUSTOMER_ID (Artificial key)
	PIZZA – NAME (Artificial key)
	PIZZA_RESTURANT - NAME(natural key)
	RELATION_PO - PIZZA_NAME (Artificial key)

### Using the Oracle Datamodeler, build a dataflow diagram for the “Pizza Sales Report System”.
###	Using the Oracle Datamodeler build the EER diagram (conceptual design).  All business rules must be entered into the Oracle Data Modeler.
### Proceed to convert the EER diagram into a Relational Diagram.  Make sure all the constraints, naming convention, etc. have been followed in your Data Model.
### Proceed to generate the DDL
### Create a script similar the sample database schema “Create_HR_Database_Scheme.sql” to create your schema this assignment using the DDL created in the above step.  This may require making updates in the Oracle Datamodeler to make sure all the needed REFERENTIAL INTEGRITY CONSTRAINTS are created (e.g. Primary Keys, UNIQUE Keys, Referential Integrity, NULL, NOT NULL, DEFAULT)

-- Generated by Oracle SQL Developer Data Modeler 18.4.0.339.1532
--   at:        2019-04-13 17:50:02 EDT
--   site:      Oracle Database 11g
--   type:      Oracle Database 11g



CREATE TABLE app_user (
    id              NUMBER(9) NOT NULL,
    name            VARCHAR2(8) NOT NULL,
    date_of_birth   DATE NOT NULL,
    address         VARCHAR2(20) NOT NULL,
    identity        VARCHAR2(8) NOT NULL
);

ALTER TABLE app_user ADD CONSTRAINT app_user_pk PRIMARY KEY ( id );

CREATE TABLE avail (
    entertainer_id         NUMBER(9) NOT NULL,
    pizza_resturant_name   VARCHAR2(8) NOT NULL,
    weekdays               VARCHAR2(8) NOT NULL
);

ALTER TABLE avail ADD CONSTRAINT avail_pk PRIMARY KEY ( entertainer_id,
                                                        pizza_resturant_name );

CREATE TABLE b_owner (
    id         NUMBER(9) NOT NULL,
    linkedin   VARCHAR2(10) NOT NULL
);

ALTER TABLE b_owner ADD CONSTRAINT b_owner_pk PRIMARY KEY ( id );

CREATE TABLE e_order (
    type             VARCHAR2(8) NOT NULL,
    duration         DATE NOT NULL,
    entertainer_id   NUMBER(9) NOT NULL,
    id               NUMBER(9) NOT NULL
);

ALTER TABLE e_order ADD CONSTRAINT e_order_pk PRIMARY KEY ( id );

CREATE TABLE entertainer (
    id           NUMBER(9) NOT NULL,
    stage_name   VARCHAR2(8) NOT NULL,
    short_bio    VARCHAR2(20) NOT NULL,
    price        INTEGER NOT NULL
);

ALTER TABLE entertainer ADD CONSTRAINT entertainer_pk PRIMARY KEY ( id );

CREATE TABLE h_customer (
    id                 NUMBER(9) NOT NULL,
    delivery_address   VARCHAR2(20) NOT NULL
);

ALTER TABLE h_customer ADD CONSTRAINT h_customer_pk PRIMARY KEY ( id );

CREATE TABLE orders (
    latest_time_of_delivery   DATE NOT NULL,
    placement_time            DATE NOT NULL,
    placement_date            DATE NOT NULL,
    id                        NUMBER(9) NOT NULL,
    nr_of_people              NUMBER(9) NOT NULL,
    h_customer_id             NUMBER(9) NOT NULL
);

ALTER TABLE orders ADD CONSTRAINT orders_pk PRIMARY KEY ( id );

CREATE TABLE pizza (
    name                   VARCHAR2(8) NOT NULL,
    restuarnt_name         VARCHAR2(10) NOT NULL,
    crust_structure        VARCHAR2(8) NOT NULL,
    price                  INTEGER NOT NULL,
    pizza_resturant_name   VARCHAR2(8) NOT NULL
);

ALTER TABLE pizza ADD CONSTRAINT pizza_pk PRIMARY KEY ( name );

ALTER TABLE pizza ADD CONSTRAINT pizza_restuarnt_name_un UNIQUE ( restuarnt_name );

CREATE TABLE pizza_resturant (
    name            VARCHAR2(8) NOT NULL,
    zip_code        VARCHAR2(10) NOT NULL,
    opening_hours   DATE NOT NULL,
    address         VARCHAR2(20) NOT NULL,
    phone_number    VARCHAR2(8) NOT NULL,
    website         VARCHAR2(10) NOT NULL,
    b_owner_id      NUMBER(9) NOT NULL
);

ALTER TABLE pizza_resturant ADD CONSTRAINT pizza_resturant_pk PRIMARY KEY ( name );

CREATE TABLE relation_po (
    order_id     NUMBER(9) NOT NULL,
    pizza_name   VARCHAR2(8) NOT NULL
);

ALTER TABLE relation_po ADD CONSTRAINT "issues/is_issued_by_PK" PRIMARY KEY ( order_id,
                                                                              pizza_name );

ALTER TABLE avail
    ADD CONSTRAINT avail_entertainer_fk FOREIGN KEY ( entertainer_id )
        REFERENCES entertainer ( id );

ALTER TABLE avail
    ADD CONSTRAINT avail_pizza_resturant_fk FOREIGN KEY ( pizza_resturant_name )
        REFERENCES pizza_resturant ( name );

ALTER TABLE b_owner
    ADD CONSTRAINT b_owner_app_user_fk FOREIGN KEY ( id )
        REFERENCES app_user ( id );

ALTER TABLE e_order
    ADD CONSTRAINT e_order_entertainer_fk FOREIGN KEY ( entertainer_id )
        REFERENCES entertainer ( id );

ALTER TABLE e_order
    ADD CONSTRAINT e_order_order_fk FOREIGN KEY ( id )
        REFERENCES orders ( id );

ALTER TABLE entertainer
    ADD CONSTRAINT entertainer_app_user_fk FOREIGN KEY ( id )
        REFERENCES app_user ( id );

ALTER TABLE h_customer
    ADD CONSTRAINT h_customer_app_user_fk FOREIGN KEY ( id )
        REFERENCES app_user ( id );

ALTER TABLE relation_po
    ADD CONSTRAINT "issues/is_issued_by_Order_FK" FOREIGN KEY ( order_id )
        REFERENCES orders ( id );

ALTER TABLE relation_po
    ADD CONSTRAINT "issues/is_issued_by_Pizza_FK" FOREIGN KEY ( pizza_name )
        REFERENCES pizza ( name );

ALTER TABLE orders
    ADD CONSTRAINT orders_h_customer_fk FOREIGN KEY ( h_customer_id )
        REFERENCES h_customer ( id );

ALTER TABLE pizza
    ADD CONSTRAINT pizza_pizza_resturant_fk FOREIGN KEY ( pizza_resturant_name )
        REFERENCES pizza_resturant ( name );

ALTER TABLE pizza_resturant
    ADD CONSTRAINT pizza_resturant_b_owner_fk FOREIGN KEY ( b_owner_id )
        REFERENCES b_owner ( id );

CREATE OR REPLACE TRIGGER arc_fkarc_1_entertainer BEFORE
    INSERT OR UPDATE OF id ON entertainer
    FOR EACH ROW
DECLARE
    d VARCHAR2(8);
BEGIN
    SELECT
        a.identity
    INTO d
    FROM
        app_user a
    WHERE
        a.id = :new.id;

    IF ( d IS NULL OR d <> 'ENT' ) THEN
        raise_application_error(-20223, 'FK Entertainer_App_User_FK in Table Entertainer violates Arc constraint on Table App_User - discriminator column identity doesn''t have value ''ENT'''
        );
    END IF;

EXCEPTION
    WHEN no_data_found THEN
        NULL;
    WHEN OTHERS THEN
        RAISE;
END;
/

CREATE OR REPLACE TRIGGER arc_fkarc_1_h_customer BEFORE
    INSERT OR UPDATE OF id ON h_customer
    FOR EACH ROW
DECLARE
    d VARCHAR2(8);
BEGIN
    SELECT
        a.identity
    INTO d
    FROM
        app_user a
    WHERE
        a.id = :new.id;

    IF ( d IS NULL OR d <> 'HC' ) THEN
        raise_application_error(-20223, 'FK H_Customer_App_User_FK in Table H_Customer violates Arc constraint on Table App_User - discriminator column identity doesn''t have value ''HC'''
        );
    END IF;

EXCEPTION
    WHEN no_data_found THEN
        NULL;
    WHEN OTHERS THEN
        RAISE;
END;
/

CREATE OR REPLACE TRIGGER arc_fkarc_1_b_owner BEFORE
    INSERT OR UPDATE OF id ON b_owner
    FOR EACH ROW
DECLARE
    d VARCHAR2(8);
BEGIN
    SELECT
        a.identity
    INTO d
    FROM
        app_user a
    WHERE
        a.id = :new.id;

    IF ( d IS NULL OR d <> 'BU' ) THEN
        raise_application_error(-20223, 'FK B_Owner_App_User_FK in Table B_Owner violates Arc constraint on Table App_User - discriminator column identity doesn''t have value ''BU'''
        );
    END IF;

EXCEPTION
    WHEN no_data_found THEN
        NULL;
    WHEN OTHERS THEN
        RAISE;
END;
/



-- Oracle SQL Developer Data Modeler Summary Report: 
-- 
-- CREATE TABLE                            10
-- CREATE INDEX                             0
-- ALTER TABLE                             23
-- CREATE VIEW                              0
-- ALTER VIEW                               0
-- CREATE PACKAGE                           0
-- CREATE PACKAGE BODY                      0
-- CREATE PROCEDURE                         0
-- CREATE FUNCTION                          0
-- CREATE TRIGGER                           3
-- ALTER TRIGGER                            0
-- CREATE COLLECTION TYPE                   0
-- CREATE STRUCTURED TYPE                   0
-- CREATE STRUCTURED TYPE BODY              0
-- CREATE CLUSTER                           0
-- CREATE CONTEXT                           0
-- CREATE DATABASE                          0
-- CREATE DIMENSION                         0
-- CREATE DIRECTORY                         0
-- CREATE DISK GROUP                        0
-- CREATE ROLE                              0
-- CREATE ROLLBACK SEGMENT                  0
-- CREATE SEQUENCE                          0
-- CREATE MATERIALIZED VIEW                 0
-- CREATE MATERIALIZED VIEW LOG             0
-- CREATE SYNONYM                           0
-- CREATE TABLESPACE                        0
-- CREATE USER                              0
-- 
-- DROP TABLESPACE                          0
-- DROP DATABASE                            0
-- 
-- REDACTION POLICY                         0
-- 
-- ORDS DROP SCHEMA                         0
-- ORDS ENABLE SCHEMA                       0
-- ORDS ENABLE OBJECT                       0
-- 
-- ERRORS                                   0
-- WARNINGS                                 0

###	Using the Oracle SQL Developer, create an Oracle database userid “<last-Name>_<first character of First name>_HWK2” in the Oracle database “.  For example:  fernandezr_HWK2
###	Run the script that creates the database schema into your userid created above.
### Create INSERT statement to insert at least 20 rows in each table. Make sure that you need to load the parent tables first to avoid errors.

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('1', 'ak', TO_DATE('2019-04-12 20:01:10', 'YYYY-MM-DD HH24:MI:SS'), 'dc', 'EU')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('2', 'ritvik', TO_DATE('2019-04-12 20:02:36', 'YYYY-MM-DD HH24:MI:SS'), 'ca', 'BU')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('3', 'sahil', TO_DATE('2019-04-12 20:03:47', 'YYYY-MM-DD HH24:MI:SS'), 'bo', 'ENT')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('4', 'avinash', TO_DATE('2019-04-12 20:05:22', 'YYYY-MM-DD HH24:MI:SS'), 'tx', 'HU')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('5', 'domino', TO_DATE('2019-04-12 20:06:10', 'YYYY-MM-DD HH24:MI:SS'), 'hu', 'EU')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('6', 'teja', TO_DATE('2019-04-12 20:06:46', 'YYYY-MM-DD HH24:MI:SS'), 'al', 'ENT')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('7', 'thor', TO_DATE('2019-04-12 20:07:23', 'YYYY-MM-DD HH24:MI:SS'), 'ch', 'BU')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('8', 'helen', TO_DATE('2019-04-12 20:08:14', 'YYYY-MM-DD HH24:MI:SS'), 'ny', 'HU')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('9', 'zoom', TO_DATE('2019-04-12 20:09:26', 'YYYY-MM-DD HH24:MI:SS'), 'or', 'ENT')
INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('10', 'rice', TO_DATE('2019-04-12 20:10:15', 'YYYY-MM-DD HH24:MI:SS'), 'ny', 'BU')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('11', 'sam', TO_DATE('2019-04-12 20:10:51', 'YYYY-MM-DD HH24:MI:SS'), 'ca', 'BU')
INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('13', 'lesnar', TO_DATE('2019-04-12 20:12:10', 'YYYY-MM-DD HH24:MI:SS'), 'hu', 'ENT')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('14', 'nishant', TO_DATE('2019-04-12 20:12:52', 'YYYY-MM-DD HH24:MI:SS'), 'tx', 'HU')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('15', 'chris', TO_DATE('2019-04-12 20:13:53', 'YYYY-MM-DD HH24:MI:SS'), 'hu', 'BU')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('16', 'norman', TO_DATE('2019-04-12 20:14:28', 'YYYY-MM-DD HH24:MI:SS'), 'al', 'HU')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('17', 'surfer', TO_DATE('2019-04-12 20:15:42', 'YYYY-MM-DD HH24:MI:SS'), 'ca', 'ENT')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('18', 'tien', TO_DATE('2019-04-12 20:16:11', 'YYYY-MM-DD HH24:MI:SS'), 'ca', 'HU')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('19', 'slik', TO_DATE('2019-04-12 20:17:08', 'YYYY-MM-DD HH24:MI:SS'), 'tx', 'BU')

INSERT INTO "GUPTA_AKSHAY_HW2"."APP_USER" (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('20', 'reed', TO_DATE('2019-04-12 20:17:44', 'YYYY-MM-DD HH24:MI:SS'), 'fl', 'BU')

### Create at least 5 select statements to display data from the database schema.

select a.ID from APP_USER a; 
select * from APP_USER;
select a.identity from APP_USER a where identity ='EU'; 
select a.date_of_birth from APP_USER a where a.address='tx'; 
select a.name from APP_USER a where a.address='ny';

###	Create at least 5 delete and 5 update SQL statements.

DELETE

DELETE FROM "GUPTA_AKSHAY_HW2"."APP_USER" WHERE ROWID = 'AAAYGOAAEAAACOsAAR' AND ORA_ROWSCN = '3788091' and ( "ID" is null or "ID" is not null )
DELETE FROM "GUPTA_AKSHAY_HW2"."APP_USER" WHERE ROWID = 'AAAYGOAAEAAACOsAAP' AND ORA_ROWSCN = '3788117' and ( "ID" is null or "ID" is not null )

DELETE FROM "GUPTA_AKSHAY_HW2"."APP_USER" WHERE ROWID = 'AAAYGOAAEAAACOsAAA' AND ORA_ROWSCN = '3788133' and ( "ID" is null or "ID" is not null )

DELETE FROM "GUPTA_AKSHAY_HW2"."APP_USER" WHERE ROWID = 'AAAYGOAAEAAACOsAAD' AND ORA_ROWSCN = '3788151' and ( "ID" is null or "ID" is not null )

DELETE FROM "GUPTA_AKSHAY_HW2"."APP_USER" WHERE ROWID = 'AAAYGOAAEAAACOsAAJ' AND ORA_ROWSCN = '3788166' and ( "ID" is null or "ID" is not null )

UPDATE

UPDATE "GUPTA_AKSHAY_HW2"."APP_USER" SET IDENTITY = 'HC' WHERE ROWID = 'AAAYGOAAEAAACOsAAL' AND ORA_ROWSCN = '3788201'

UPDATE "GUPTA_AKSHAY_HW2"."APP_USER" SET IDENTITY = 'HC' WHERE ROWID = 'AAAYGOAAEAAACOsAAH' AND ORA_ROWSCN = '3788186'

UPDATE "GUPTA_AKSHAY_HW2"."APP_USER" SET DATE_OF_BIRTH = TO_DATE('2019-04-04 20:02:36', 'YYYY-MM-DD HH24:MI:SS'), IDENTITY = 'ENT' WHERE ROWID = 'AAAYGOAAEAAACOsAAB' AND ORA_ROWSCN = '3788235'

UPDATE "GUPTA_AKSHAY_HW2"."APP_USER" SET NAME = 'li', DATE_OF_BIRTH = TO_DATE('1978-04-11 20:12:52', 'YYYY-MM-DD HH24:MI:SS') WHERE ROWID = 'AAAYGOAAEAAACOsAAN' AND ORA_ROWSCN = '3788324'

UPDATE "GUPTA_AKSHAY_HW2"."APP_USER" SET DATE_OF_BIRTH = TO_DATE('1977-04-05 20:11:36', 'YYYY-MM-DD HH24:MI:SS') WHERE ROWID = 'AAAYGOAAEAAACOsAAL' AND ORA_ROWSCN = '3788338'

### Build a PL/SQL procedure that creates a “hungry Customers Report”.  The reports contains the name, address, date of sale, pizza type, cost, and at the end the total costs.

NOTE:  the number of entities in your design could be larger that in the solution below. 

create or replace PROCEDURE HUNGRY_CUSTOMER_REPORT AS 
  res SYS_REFCURSOR;  
  res_2 SYS_REFCURSOR;
  BEGIN
  open res for
  SELECT  APP_USER.NAME NAME, H_CUSTOMER.DELIVERY_ADDRESS ADDRESS, ORDERS.PLACEMENT_DATE SALEDATE, PIZZA.NAME PIZZA, PIZZA.CRUST_STRUCTURE TYPE, PIZZA.PRICE PRICE
FROM APP_USER
JOIN H_CUSTOMER ON APP_USER.ID = H_CUSTOMER.ID
JOIN ORDERS ON APP_USER.ID = ORDERS.H_CUSTOMER_ID
JOIN RELATION_PO ON ORDERS.ID = RELATION_PO.ORDER_ID
JOIN PIZZA ON RELATION_PO.PIZZA_NAME = PIZZA.NAME;
  dbms_output.put_line('Total Cost');
  open res_2 for
  SELECT SUM(PIZZA.PRICE)
  FROM H_CUSTOMER
    JOIN ORDERS on H_CUSTOMER.ID = ORDERS.H_CUSTOMER_ID
    JOIN RELATION_PO ON RELATION_PO.ORDER_ID = ORDERS.ID
    JOIN PIZZA ON PIZZA.NAME = RELATION_PO.PIZZA_NAME;

  DBMS_SQL.RETURN_RESULT(res);
  DBMS_SQL.RETURN_RESULT(res_2);

# Part II:

###	Create an Oracle RDS Instance
### Connect to the Oracle RDS Database Schema to Execute steps “m” to “p” from part 1 to create the database schema in your new Oracle RDS instance.

Create statements
INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('1', 'ak', TO_DATE('2019-04-12 20:01:10', 'YYYY-MM-DD HH24:MI:SS'), 'dc', 'EU');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('2', 'ritvik', TO_DATE('2019-04-12 20:02:36', 'YYYY-MM-DD HH24:MI:SS'), 'ca', 'BU');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('3', 'sahil', TO_DATE('2019-04-12 20:03:47', 'YYYY-MM-DD HH24:MI:SS'), 'bo', 'ENT');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('4', 'avinash', TO_DATE('2019-04-12 20:05:22', 'YYYY-MM-DD HH24:MI:SS'), 'tx', 'HU');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('5', 'domino', TO_DATE('2019-04-12 20:06:10', 'YYYY-MM-DD HH24:MI:SS'), 'hu', 'EU');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('6', 'teja', TO_DATE('2019-04-12 20:06:46', 'YYYY-MM-DD HH24:MI:SS'), 'al', 'ENT');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('7', 'thor', TO_DATE('2019-04-12 20:07:23', 'YYYY-MM-DD HH24:MI:SS'), 'ch', 'BU');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('8', 'helen', TO_DATE('2019-04-12 20:08:14', 'YYYY-MM-DD HH24:MI:SS'), 'ny', 'HU');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('9', 'zoom', TO_DATE('2019-04-12 20:09:26', 'YYYY-MM-DD HH24:MI:SS'), 'or', 'ENT');
INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('10', 'rice', TO_DATE('2019-04-12 20:10:15', 'YYYY-MM-DD HH24:MI:SS'), 'ny', 'BU');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('11', 'sam', TO_DATE('2019-04-12 20:10:51', 'YYYY-MM-DD HH24:MI:SS'), 'ca', 'BU');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('13', 'lesnar', TO_DATE('2019-04-12 20:12:10', 'YYYY-MM-DD HH24:MI:SS'), 'hu', 'ENT');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('14', 'nishant', TO_DATE('2019-04-12 20:12:52', 'YYYY-MM-DD HH24:MI:SS'), 'tx', 'HU');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('15', 'chris', TO_DATE('2019-04-12 20:13:53', 'YYYY-MM-DD HH24:MI:SS'), 'hu', 'BU');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('16', 'norman', TO_DATE('2019-04-12 20:14:28', 'YYYY-MM-DD HH24:MI:SS'), 'al', 'HU');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('17', 'surfer', TO_DATE('2019-04-12 20:15:42', 'YYYY-MM-DD HH24:MI:SS'), 'ca', 'ENT');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('18', 'tien', TO_DATE('2019-04-12 20:16:11', 'YYYY-MM-DD HH24:MI:SS'), 'ca', 'HU');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('19', 'slik', TO_DATE('2019-04-12 20:17:08', 'YYYY-MM-DD HH24:MI:SS'), 'tx', 'BU');

INSERT INTO APP_USER (ID, NAME, DATE_OF_BIRTH, ADDRESS, IDENTITY) VALUES ('20', 'reed', TO_DATE('2019-04-12 20:17:44', 'YYYY-MM-DD HH24:MI:SS'), 'fl', 'BU');




Select Statements

select a.ID from APP_USER a; 
select * from APP_USER;
select a.identity from APP_USER a where identity ='EU'; 
select a.date_of_birth from APP_USER a where a.address='tx'; 
select a.name from APP_USER a where a.address='ny'; 