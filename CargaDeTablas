  CREATE DATABASE creditcarddata;
 USE creditcarddata;

 CREATE TABLE cardbase (
    Card_Number VARCHAR(30),
    Card_Family VARCHAR(30),
    Credit_Limit VARCHAR(30),
    Cust_ID VARCHAR(30)
);
 
CREATE TABLE customerbase (
    Cust_ID VARCHAR(30),
    Age VARCHAR(30),
    Customer_Segment VARCHAR(30),
    Customer_Vintage_Group VARCHAR(30)
);

CREATE TABLE fraudbase (
    Transaction_ID VARCHAR(30),
    Fraud_Flag VARCHAR(30)
);

CREATE TABLE transactionbase (
    Transaction_ID VARCHAR(30),
    Transaction_Date VARCHAR(30),
    Credit_Card_ID VARCHAR(30),
    Transaction_Value VARCHAR(30),
    Transaction_Segment VARCHAR(30)
);

LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Data/datasets_46256_84261_CardBase.csv' 
INTO TABLE cardbase 
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\r\n'
IGNORE 1 ROWS;

LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Data/datasets_46256_84261_CustomerBase.csv' 
INTO TABLE customerbase
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\r\n'

IGNORE 1 ROWS;

LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Data/datasets_46256_84261_FraudBase.csv' 
INTO TABLE fraudbase
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\r\n'
IGNORE 1 ROWS;

LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Data/datasets_46256_84261_TransactionBase.csv' 
INTO TABLE transactionbase
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\r\n'
IGNORE 1 ROWS;



DROP view info_clientes_fraude;
CREATE VIEW info_clientes_fraude AS
    SELECT 
        cb.Cust_ID,
        crb.Cust_ID AS otro,
        crb.Age,
        crb.Customer_Segment,
        cb.Card_Number,
        tb.Transaction_ID,
        tb.Transaction_Date,
        tb.Transaction_Value,
        fb.Fraud_Flag
    FROM
        fraudbase fb
            LEFT JOIN
        transactionbase tb ON fb.Transaction_ID = tb.Transaction_ID
            LEFT JOIN
        cardbase cb ON cb.Card_Number = tb.Credit_Card_ID
            LEFT JOIN
        customerbase crb ON cb.Cust_ID = crb.Cust_ID;



DELIMITER $$
CREATE PROCEDURE fraudesPorEdad ( EDAD VARCHAR(10) )
BEGIN
	SELECT * FROM info_clientes_fraude info WHERE info.Age = EDAD;
END$$
DELIMITER ;
