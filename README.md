# 📊 Power BI Sales Analytics Dashboard

### 🚀 Project Overview
This Power BI dashboard provides insights into **sales trends, top customers, and product performance** using SQL Server data. It includes:

- **📈 Monthly Sales Trends (Line Chart)**
- **🛒 Best-Selling Products (Column Chart)**
- **🏆 Top 5 Customers by Revenue (Table)**
- **💰 Total Sales, Average Order Value, and Total Transactions (KPIs)**

---

## **📸 Dashboard Screenshots**
#### 📊 Full Dashboard  
![Dashboard](./PowerBI-Sales-Analytics_Project.png)

#### 🏆 KPI Cards  
![KPIs](./SAP%20Cards.png)

#### 🛒 Product by Sales Revenue  
![Product Sales](./SAP%20Product%20by%20Sales%20Revenue.png)

#### 🔥 Best-Selling Products (Quantity Sold)  
![Best Selling Products](./SAP%20Quantity%20by%20Best-Selling%20Product.png)

#### 💰 Top 5 Customers by Revenue  
![Top Customers](./SAP%20Table.png)

#### 📈 Monthly Sales Trends  
![Sales Trends](./SAP%20Total%20Amount%20by%20Year%20To%20Month.png)

---

## **🛠 Tech Stack Used**
- **Power BI** (Data Visualization)
- **SQL Server** (Database Management)
- **DAX** (Data Analysis Expressions for Calculations)
- **GitHub** (Version Control)

---

## **📂 SQL Code for Data Processing**
Below is the SQL code used to **create the database, tables, and insert sample data**.

### 📌 **1️⃣ Create Database**
```sql
CREATE DATABASE SalesDB;
GO

📌 2️⃣ Create Tables
-- Use the database
USE SalesDB;
GO

-- Create Customers Table
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY IDENTITY(1,1),
    CustomerName VARCHAR(100) NOT NULL,
    Email VARCHAR(100) UNIQUE,
    Phone VARCHAR(20),
    RegionID INT
);

-- Create Products Table
CREATE TABLE Products (
    ProductID INT PRIMARY KEY IDENTITY(1,1),
    ProductName VARCHAR(100) NOT NULL,
    Category VARCHAR(50),
    Price DECIMAL(10,2)
);

-- Create Sales Table
CREATE TABLE Sales (
    SaleID INT PRIMARY KEY IDENTITY(1,1),
    CustomerID INT,
    ProductID INT,
    SaleDate DATE,
    Quantity INT,
    TotalAmount DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);

-- Create Regions Table
CREATE TABLE Regions (
    RegionID INT PRIMARY KEY IDENTITY(1,1),
    RegionName VARCHAR(50) NOT NULL
);

📌 3️⃣ Insert Sample Data
-- Insert Customers
INSERT INTO Customers (CustomerName, Email, Phone, RegionID) VALUES
('John Doe', 'johndoe@email.com', '123-456-7890', 1),
('Jane Smith', 'janesmith@email.com', '987-654-3210', 2),
('Mike Johnson', 'mikejohnson@email.com', '555-123-4567', 3),
('Alice Brown', 'alice@email.com', '444-555-6666', 2),
('David White', 'david@email.com', '777-888-9999', 3);

-- Insert Products
INSERT INTO Products (ProductName, Category, Price) VALUES
('Laptop', 'Electronics', 800.00),
('Smartphone', 'Electronics', 600.00),
('Headphones', 'Accessories', 50.00);

-- Insert Sales Data
INSERT INTO Sales (CustomerID, ProductID, SaleDate, Quantity, TotalAmount) VALUES
(1, 1, '2024-01-01', 2, 1600.00),
(2, 2, '2024-01-03', 1, 600.00),
(3, 3, '2024-01-05', 5, 250.00),
(4, 2, '2024-03-10', 3, 1800.00),
(5, 1, '2024-04-15', 2, 1600.00);

-- Insert Regions
INSERT INTO Regions (RegionName) VALUES ('North'), ('South'), ('East'), ('West');

📊 Business Insights SQL Queries
These SQL queries were used to generate insights for the Power BI dashboard.

🛒 Total Sales Revenue by Region
SELECT r.RegionName, SUM(s.TotalAmount) AS TotalSales
FROM Sales s
JOIN Customers c ON s.CustomerID = c.CustomerID
JOIN Regions r ON c.RegionID = r.RegionID
GROUP BY r.RegionName;

🔥 Top-Selling Products
SELECT p.ProductName, SUM(s.Quantity) AS TotalQuantitySold
FROM Sales s
JOIN Products p ON s.ProductID = p.ProductID
GROUP BY p.ProductName
ORDER BY TotalQuantitySold DESC;

📈 Monthly Sales Trends
SELECT YEAR(SaleDate) AS SalesYear, MONTH(SaleDate) AS SalesMonth, SUM(TotalAmount) AS TotalRevenue
FROM Sales
GROUP BY YEAR(SaleDate), MONTH(SaleDate)
ORDER BY SalesYear, SalesMonth;

🏆 Top 5 Customers by Revenue
SELECT TOP 5 c.CustomerName, SUM(s.TotalAmount) AS TotalSpent
FROM Sales s
JOIN Customers c ON s.CustomerID = c.CustomerID
GROUP BY c.CustomerName
ORDER BY TotalSpent DESC;

🚀 How to Use This Project
1. Clone this repository using:
git clone https://github.com/yourusername/PowerBI-Sales-Analytics.git
2. Open SQL Server Management Studio (SSMS) and run the provided SQL scripts.
3. Open Power BI Desktop, connect to SalesDB, and refresh the dataset.
4. Explore the dashboard to gain insights!

---

🔗 Connect with Me
📧 Email: Nicholas.castillo2000@gmail.com
🔗 LinkedIn: Nicholas Castillo
