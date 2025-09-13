# 📡 Telecom ETL SSIS Project

This ETL project was developed using SQL Server Integration Services (SSIS) for a telecom company. 
The goal is to extract transactional data from CSV files, apply business transformation rules, and load clean records into a SQL Server database while isolating erroneous data for review.

## 🎯 Project Overview

The telecom company generates a CSV file every 5 minutes containing customer transaction data. The SSIS package performs the following operations:

- Iterates over incoming files using a **Foreach Loop Container**
- Extracts data from flat files via **Flat File Source**
- Applies transformation logic using **Derived Columns**, **Lookups**, and **Conditional Splits**
- Loads valid records into the main transaction table
- Redirects invalid records to error tables with source tracking

## 🧰 Tools & Technologies

- Microsoft Visual Studio (SSDT) – SSIS package development
- SQL Server Management Studio (SSMS) – Database management
- SSIS Components – Foreach Loop, Data Flow Task, File System Task, OLE DB Destination, etc.
- File Handling – Source files from `C:\SSIS_Source_Files`, processed files moved to `C:\Processed_Files`

## 📁 Project Structure

Telecom_ETL_SSIS_Project/
├── Packages/ # SSIS .dtsx files
├── Config/ # Connection and environment settings 
├── SQL_Scripts/ # Table creation and cleanup scripts 
├── README.md # This documentation file 
└── Telecom_ETL_SSIS.dtproj # Main SSIS project file


## 🧪 Transformation Rules

| Column        | Rule Description                                                                 |
|---------------|-----------------------------------------------------------------------------------|
| `ID`          | Stored as `transaction_id`                                                        |
| `IMSI`        | Required; rows with null values are rejected                                      |
| `IMEI`        | First 8 digits extracted as `TAC`, last 6 as `SNR`; `-99999` added if invalid     |
| `CELL`        | Required; rows with null values are rejected                                      |
| `LAC`         | Required; rows with null values are rejected                                      |
| `EVENT_TYPE`  | Stored as-is                                                                      |
| `EVENT_TS`    | Validated for proper datetime format; invalid or null values are rejected         |

## 🗃️ Database & Tables

Database used: `SSIS_Telecom_DB`  
Tables involved:

- `[dbo].[dim_imsi_reference]` – Reference table for IMSI validation   🔍
- `[dbo].[error_source_output]` – Tracks error source and original file name   📄
- `[dbo].[telecom_transaction]` – Stores clean, validated records  ✅
- `[dbo].[error_transaction]` – Stores rejected rows based on transformation rules  ❌

## ⚙️ Requirements

- Visual Studio with SSDT installed  
- SQL Server 2019 or later  
- Properly formatted CSV files from the telecom system  
- Execution permissions for SSIS packages and database access  

## 🚀 Execution Steps

1. Open the SSIS project in Visual Studio  
2. Configure connection settings as per your environment  
3. Run the package via Data Flow or Foreach Loop  
4. Verify data in `telecom_transaction` and error tables  
5. Review `error_source_output` for file-level error tracking  

## 📌 Developer

**Eng. Ahmed Youssef**  
     ETL Developer & Data Engineer  
     Computer Science Student – Misr Higher Institute  
     Participant in the Digital Egypt Pioneers Initiative
     **Thanks**  **Eng. Mohammed Hamed**
                                      
