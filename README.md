# GDP_analysis_sql.sql
GDP Inequality Analysis: Kenya vs Ghana vs South Korea

Description:

This project analyzes GDP per capita trends between Kenya, Ghana and South Korea using World Bank data.
The project demonstrates a full data analytics workflow including:

Data extraction and cleaning in Excel

Data storage and querying in SQL Server

Exploratory Data Analysis (EDA)

Data visualization in Power BI

The goal is to explore economic divergence between countries that once had similar income levels.

 =====================================================
   GDP DATA ANALYSIS PROJECT
   Countries: Kenya, Ghana, South Korea
   Tools: Excel, SQL Server, Power BI
   Data Source: World Bank - World Development Indicators


 =====================================================
   1. CREATE DATABASE

CREATE DATABASE GDP_Analysis;

USE GDP_Analysis;



 =====================================================
   2. CREATE RAW TABLE
   This stores the original imported dataset

CREATE TABLE gdp_raw (
    Country_Name VARCHAR(100),
    Country_Code VARCHAR(10),
    Indicator_Name VARCHAR(200),
    Indicator_Code VARCHAR(50),
    Year INT,
    GDP_Per_Capita DECIMAL(18,2)
);


 
===================================================== 
  3. CHECK IMPORTED DATA

SELECT TOP 100 *
FROM gdp_raw;



 =====================================================
   4. DATA CLEANING
   Removing null values and preparing data for analysis

SELECT *
FROM gdp_raw
WHERE GDP_Per_Capita IS NOT NULL;


===================================================== 
  5. FILTER FOR TARGET COUNTRIES
     
SELECT *
FROM gdp_raw
WHERE Country_Name IN ('Kenya','Ghana','Korea, Rep.');


 =====================================================
   6. CREATE CLEAN TABLE FOR ANALYSIS

CREATE TABLE gdp_clean AS
SELECT
    Country_Name,
    Country_Code,
    Year,
    GDP_Per_Capita
FROM gdp_raw
WHERE Country_Name IN ('Kenya','Ghana','Korea, Rep.')
AND GDP_Per_Capita IS NOT NULL;


=====================================================
   7. BASIC EXPLORATORY DATA ANALYSIS (EDA)

/ Average GDP per country /

SELECT
    Country_Name,
    AVG(GDP_Per_Capita) AS Avg_GDP
FROM gdp_clean
GROUP BY Country_Name;


/ GDP growth trend /

SELECT
    Country_Name,
    Year,
    GDP_Per_Capita
FROM gdp_clean
ORDER BY Country_Name, Year;


There was a lot of 'drop table if exists' and a couple of mistakes, still learning. This is the clean version. 
