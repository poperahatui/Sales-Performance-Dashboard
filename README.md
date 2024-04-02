# Sales Performance Dashboard Final task PBI Big Data Analytics Kimia farma
**Name : Majangga | Email : majanggaabdullah@gmail.com | Linkedin : https://www.linkedin.com/in/majangga/**

In this project, I acted as a Big Data Analyst Intern who was asked to analyse and create company sales reports using the data provided. From this project, I also learned a lot about Data Warehouse, Querying, Data Analysing, Data Visualisation, Data Storytelling, Dashboarding, and Datamart. And here I will create a datamart design (base table and aggregate table) and create a company sales report visualisation/dashboard.

## Data Source
- The data for this project is sourced from Kimia Farma to be processed and utilized in order to obtain the desired results.
- The title of the dataset used is Data_Source_Task and will be divided into two tables_base and table_aggregate.

## Design Datamart
### Base Table
Base tables are tables that contain original data or raw data collected from the source and contain information needed to answer questions or solve certain problems.

Here is the query for the base table :
```
-- Create Base Table
CREATE TABLE tabel_base AS (
  SELECT
    pj.id_invoice,
  	pj.tanggal,
  	pl.cabang_sales,
  	pl.nama AS nama_customer,
  	pl.group,
  	b.nama_barang,
  	b.lini AS brand,
  	pj.jumlah_barang,
  	pj.unit,
  	pj.harga
  FROM
  	penjualan AS pj
  	JOIN pelanggan AS pl ON pl.id_customer = pj.id_customer
  	JOIN barang AS b ON pj.id_barang = b.kode_barang
);
ALTER TABLE `final_task_pbi`.`tabel_base` 
CHANGE COLUMN `id_invoice` `id_invoice` VARCHAR(255) NOT NULL,
ADD PRIMARY KEY (`id_invoice`);
CREATE INDEX idx_orderlist ON tabel_base (id_invoice(50), nama_customer(50));
CREATE INDEX idx_salelist ON tabel_base (nama_customer(50), nama_barang(50));
```
### Aggregate Table
Aggregate tables are tables created by collecting and calculating data from base tables. This aggregate table contains more concise information and is used to analyze data more quickly and efficiently. The results of this table will be used as a source for creating sales report dashboards.

Here is the query for the aggregate table :
```
-- Create Aggregate Table --
CREATE TABLE tabel_aggregate AS (SELECT id_invoice,
    tanggal,
    cabang_sales,
    nama_customer,
    'group',
    nama_barang,
    brand,
    jumlah_barang,
    unit,
    harga,
    ROUND(jumlah_barang * harga) total_harga,
    AVG(harga) AS average_price,
    SUM(jumlah_barang) AS total_quantity FROM
    tabel_base
GROUP BY id_invoice , tanggal , cabang_sales , nama_customer , 'group' , nama_barang , brand , jumlah_barang , unit , harga);
```
## Data Visualization
[View on Looker Data Studio page](https://lookerstudio.google.com/u/0/reporting/e5ebe447-dd3a-448f-a3e1-40e3b4a51a14/page/8CSbD)
