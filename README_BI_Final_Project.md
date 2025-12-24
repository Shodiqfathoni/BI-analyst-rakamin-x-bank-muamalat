
# 📊 Final Project – Business Intelligence Analyst  
**Sales Data Analysis & Dashboard Visualization**

## 📌 Project Overview
Project ini bertujuan untuk membangun end-to-end Business Intelligence workflow, dimulai dari data modeling, pembuatan ERD, proses ETL, hingga visualisasi dashboard menggunakan Looker Studio.  
Output utama dari project ini adalah tabel master yang siap digunakan untuk analisis bisnis dan pengambilan keputusan.

---

## 🛠️ Tools & Technologies
- Database: MySQL (MySQL Workbench)
- Query Language: SQL
- Data Visualization: Looker Studio
- File Format: CSV

---

## 🧱 Data Modeling & ERD
Tahap ini berfokus pada perancangan struktur database dengan menentukan Primary Key dan Foreign Key, kemudian divisualisasikan dalam bentuk Entity Relationship Diagram (ERD).

### Tables Used
- customers
- orders
- products
- productcategory

### Primary Key
| Table | Primary Key |
|------|------------|
| customers | CustomerID |
| orders | OrderID |
| products | ProdNumber |
| productcategory | CategoryID |

### Relationship
- Customers 1 : N Orders  
- Products 1 : N Orders  
- ProductCategory 1 : N Products  

---

## 🧩 Database Setup & ERD Creation
Langkah-langkah pembuatan ERD dilakukan menggunakan MySQL Workbench dengan metode reverse engineering setelah data diimport dan relasi ditentukan.

### Set Primary Key
```sql
ALTER TABLE customers ADD PRIMARY KEY (CustomerID);
ALTER TABLE orders ADD PRIMARY KEY (OrderID);
ALTER TABLE products ADD PRIMARY KEY (ProdNumber);
ALTER TABLE productcategory ADD PRIMARY KEY (CategoryID);
```

### Set Foreign Key
```sql
ALTER TABLE orders
ADD CONSTRAINT fk_orders_customer
FOREIGN KEY (CustomerID)
REFERENCES customers(CustomerID);

ALTER TABLE orders
ADD CONSTRAINT fk_orders_product
FOREIGN KEY (ProdNumber)
REFERENCES products(ProdNumber);

ALTER TABLE products
ADD CONSTRAINT fk_products_category
FOREIGN KEY (Category)
REFERENCES productcategory(CategoryID);
```

---

## 🔄 ETL Process & Master Table
Setelah ERD selesai, seluruh tabel digabungkan menjadi satu tabel master menggunakan query SQL join.

```sql
SELECT
    o.Date AS order_date,
    pc.CategoryName AS category_name,
    p.ProdName AS product_name,
    p.Price AS product_price,
    o.Quantity AS order_qty,
    (o.Quantity * p.Price) AS total_sales,
    c.CustomerEmail AS cust_email,
    c.CustomerCity AS cust_city
FROM orders o
JOIN customers c
    ON o.CustomerID = c.CustomerID
JOIN products p
    ON o.ProdNumber = p.ProdNumber
JOIN productcategory pc
    ON p.Category = pc.CategoryID
ORDER BY o.Date ASC;
```

Output tabel master digunakan sebagai sumber data utama untuk visualisasi.

---

## 📈 Data Visualization
Visualisasi dilakukan menggunakan Looker Studio untuk menampilkan insight penjualan secara interaktif.
![alt text](https://github.com/Shodiqfathoni/BI-analyst-rakamin-x-bank-muamalat/blob/main/image/dashboard.jpg?raw=true)
### Dashboard Insight:
- Total Sales
- Sales Trend Over Time
- Sales by Product Category
- Top Selling Products
- Customer Distribution by City

---

## 🎯 Business Insights
- Produk dengan performa penjualan tertinggi dapat diidentifikasi
- Tren penjualan dapat dianalisis berdasarkan waktu
- Distribusi pelanggan berdasarkan lokasi
- Kontribusi tiap kategori terhadap total penjualan

---

## ✅ Conclusion
Project ini menunjukkan proses lengkap Business Intelligence mulai dari data modeling, ETL process, hingga dashboard visualization yang dapat mendukung pengambilan keputusan bisnis berbasis data.

---

## 📁 Project Structure
```
├── data/
│   ├── customers.csv
│   ├── orders.csv
│   ├── products.csv
│   └── productcategory.csv
├── sql/
│   ├── create_pk_fk.sql
│   └── master_table.sql
├── dashboard/
│   └── looker_studio_link.txt
└── README.md
```
