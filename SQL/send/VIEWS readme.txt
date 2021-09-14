	; VIEWS


	; Creating invoice view

CREATE VIEW INVOICE_VIEW AS
SELECT * FROM INVOICE NATURAL JOIN ORDER_DUMPSTER;




	; Creating a view to see customer status, if ordered or not


 CREATE VIEW CUSTOMER_ORDER AS
 SELECT CUSTOMER.customerId, CUSTOMER.firstname, CUSTOMER.lastName, ORDER_DUMPSTER.pickup_date, ORDER_DUMPSTER.dropoff_date, DUMPSTER.dumpsterid, INVOICE.total_price
 FROM CUSTOMER, ORDER_DUMPSTER, DUMPSTER, INVOICE
 WHERE CUSTOMER.customerId = ORDER_DUMPSTER.customerId AND DUMPSTER.dumpsterid = ORDER_DUMPSTER.dumpsterId AND INVOICE.customerId = ORDER_DUMPSTER.customerId
 ORDER BY ORDER_DUMPSTER.customerId;





	; Creating a view for customer information

CREATE VIEW CUSTOMER_INFO AS
SELECT * FROM CUSTOMER;


	; Creating a view to see dumpster AVAILABLE

CREATE VIEW DUMPSTER_AVAILABLE AS
SELECT * FROM DUMPSTER
WHERE Available = 'Y';

	Creating view to see if there is a driver available

CREATE VIEW DRIVER_AVAILABLE AS 
SELECT * FROM DRIVER
WHERE Available = 'Y';


	; Creating view for next PICKUP dates (driver and dumpster)


CREATE VIEW PICKUP_ORDERS AS
SELECT CUSTOMER.customerId, ORDER_DUMPSTER.dumpsterId,  ORDER_DUMPSTER.pickup_date, ORDER_DUMPSTER.to_street, ORDER_DUMPSTER.to_city, DUMPSTER.driverid
FROM CUSTOMER, ORDER_DUMPSTER, DUMPSTER
WHERE CUSTOMER.customerId = ORDER_DUMPSTER.customerId AND DUMPSTER.dumpsterid = ORDER_DUMPSTER.dumpsterId
ORDER BY ORDER_DUMPSTER.pickup_date;
	
	; Creating view for next drop off dates (driver and dumpster)


CREATE VIEW DROPOFF_ORDERS AS
SELECT CUSTOMER.customerId, ORDER_DUMPSTER.dumpsterId,  ORDER_DUMPSTER.dropoff_date, ORDER_DUMPSTER.to_street, ORDER_DUMPSTER.to_city, DUMPSTER.driverid
FROM CUSTOMER, ORDER_DUMPSTER, DUMPSTER
WHERE CUSTOMER.customerId = ORDER_DUMPSTER.customerId AND DUMPSTER.dumpsterid = ORDER_DUMPSTER.dumpsterId
ORDER BY ORDER_DUMPSTER.dropoff_date;



	; Creating view to see all expenses

CREATE VIEW YEAR_EXPENSE AS
SELECT * FROM EXPENSES;