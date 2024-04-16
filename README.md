# INT520 Power BI Project - Northwind Traders

**Dataset:** [https://www.kaggle.com/datasets/jeetahirwar/northwind-traders/data](https://www.kaggle.com/datasets/jeetahirwar/northwind-traders/data)

**Data ชุดเริ่มต้น มีทั้งหมด 7 ตาราง ได้แก่**

1. orders
2. order_details
3. customers
4. employees
5. products
6. categories
7. shippers

### Data Model

![](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%201.png)

- เป็น snowflake schema และเป็น normalization

| Fact Table | Dimension Table |
| --- | --- |
| - orders | - order_details |
|  | - customers |
|  | - employees |
|  | - products |
|  | - categories |
|  | - shippers |


---

**การ Clean and Transform Data**

1. Use First Row as Header มีบางตารางที่ชื่อ header ไม่ถูต้อง

![](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%202.png)

2. Merge Queries รวมตาราง employee เข้าด้วยกันเอง เพื่อสร้างคอลัมน์ managerName 

![](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%203.png)

3. Sorting Row เรียงข้อมูลเป็นลำดับตามมิติที่เราต้องการ เช่น เรียงตามลำดับ emloyeeID 

![](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%204.png)

4. Renaming Columns ปรับเปลี่ยนชื่อคอลัมน์ให้เป็นแบบที่เข้าใจง่าย

![](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%205.png)

5. Data Type Conversion เปลี่ยนประเภทข้อมูลในคอลัมน์ให้ถูกต้องและเหมาะสม เช่น number to text

![](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%206.png)

6. Handling Null Values ค้นหาคอลัมน์ที่มี Null Values และจัดการกับค่าเหล่านั้น

![](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%207.png)

7. Handling Date and Time จัดการกับข้อมูลวันที่และเวลาให้มีความถูกต้องและเป็นรูปแบบเดียวกัน

![](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%208.png)

8. Handling Currencies แปลงค่าตัวเลขในคอลัมน์ให้เป็นค่าเงิน เช่น เปลี่ยนเป็นค่าเงินดอลลาร์

![](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%209.png)

9. Genarate Date Table เป็นตารางที่ถูกสร้างขึ้นมาเฉพาะเพื่อเก็บข้อมูลวันที่ โดยใช้ฟังก์ชัน Power Query

![](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%2011.png)

10. Change Data Category ระบุว่าคอลัมน์ "Country" และ "City" เป็นข้อมูลประเภทที่อยู่

![](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%2012.png)

---

**การตั้งคำถามจาก Dataset แบ่งออกเป็นแต่ละหมวด**

Overview;

1. What is the net sales?
2. How many orders have been processed?
3. How many products have been sold?
4. What is the total amount of discounts?
5. What is the sales trend over the months?

Products;

1. How many products are in the catalog?
2. What are the top 10 selling products?
3. Which category has the most purchases?
4. How many products have been discontinued?
5. Which category has the most discounted products?

Customers;

1. How many customers have been attended to?
2. In which countries are these customers located?
3. Who are the top 5 customers by net sales?
4. Who are the top 5 customers by products bought and orders?
5. Which country has the most sales?

Shipping;

1. Which shipping company is used the most?
2. How many orders have been shipped and unshipped?
3. How much freight was paid to the shippers?
4. What is the on-time delivery rate?
5. How many products were delivered on time, late, and not shipped?

Employees;

1. How many employees work in the offices?
2. How many managers?
3. Who is the most active employee in terms of sales made?
4. Which employee has handled the most orders?
5. What are the offices’ order and sales performance?

---

คำสั่ง DAX Measures

1. Net Sales = CALCULATE(SUM(order_details[net sales]), USERELATIONSHIP(orders[orderDate], 'date_table'[Date]) )
2. Gross Sales = CALCULATE(SUM(order_details[gross sales]), USERELATIONSHIP(orders[orderDate], 'date_table'[Date]))
3. Discounts = [Gross Sales] - [Net Sales]
4. Freight Paid = CALCULATE(SUM(orders[freight]), USERELATIONSHIP(orders[orderDate], 'date_table'[Date]) )
5. Products Sold = CALCULATE(COUNT(order_details[orderID]), ISBLANK(order_details[orderID]) = FALSE(), USERELATIONSHIP('date_table'[Date], orders[orderDate]) )
6. Shipped Orders = CALCULATE(COUNT(orders[shippedDate]), USERELATIONSHIP('date_table'[Date], orders[shippedDate]) ) 
7. Total Orders = CALCULATE(COUNT(orders[orderDate]), USERELATIONSHIP('date_table'[Date], orders[orderDate]) )
8. On-time = CALCULATE(COUNT(orders[deliveryStatus]), orders[deliveryStatus] = "On-time")
9. Not Shipped =
VAR NotShippedCount =
CALCULATE(
COUNT(orders[orderID]),
ISBLANK(orders[shippedDate]),
USERELATIONSHIP(orders[shippedDate], 'date_table'[Date])
)
RETURN
IF(NotShippedCount = 0, 0, NotShippedCount)
10. On-time Delivery Rate = CALCULATE(DIVIDE([On-time], [Total Orders]) , USERELATIONSHIP(orders[shippedDate], 'date_table'[Date]))
11. Discontinued Products =
VAR DiscontinuedCount =
CALCULATE(
COUNT(products[discontinued]),
products[discontinued] = 1,
USERELATIONSHIP('date_table'[Date], orders[orderDate])
)
RETURN
IF(DiscontinuedCount = 0, 0, DiscontinuedCount)

คำสั่ง DAX Column

1. Month_EN = FORMAT(date_table[Date],"MMMM")
2. Day of WeekMonth_EN = FORMAT(date_table[Date],"dddd")
3. Net Sales = [UnitPrice] * [Quantity] * (1-[Discount])
4. Gross Sales = [UnitPrice] * [Quantity]
5. deliveryStatus = SWITCH(TRUE(),
ISBLANK(orders[shippedDate]), "Not Shipped",
orders[shippedDate] <= orders[requiredDate], "On-time",
orders[shippedDate] > orders[requiredDate], "Late")

---

**Data Visualization** 

[Power BI Report](https://app.powerbi.com/view?r=eyJrIjoiMDQ0ZmJlOTktMTRmOC00ZmE2LWJmZDktYTY5YTg5MDIwZDg2IiwidCI6IjZmNDQzMmRjLTIwZDItNDQxZC1iMWRiLWFjMzM4MGJhNjMzZCIsImMiOjEwfQ==)

- Overview

![Untitled](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%2013.png)

- Products

![Untitled](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%2014.png)

- Customers

![Untitled](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%2015.png)

- Shipping

![Untitled](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%2016.png)

- Employees

![Untitled](https://github.com/wongsakorn-s/PowerBI-NorthwindTraders/blob/b4a1d7d2a7f95c24b60ad8fcb2075852f96be97a/INT520%20Project/image/Untitled%2017.png)
