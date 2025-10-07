# sql-data-modeling-project
A comprehensive relational database built with SQL to model astronomical data and spcae exploration missions, demonstrating core database design and querying skills.
# Relational Data Modeling for a Scientific Dataset

## 📖 Project Overview

This project is a comprehensive showcase of relational database design and SQL skills. The objective was to model a complex, real-world dataset from scratch: the celestial bodies of our solar system and the history of international space exploration missions. The entire structure was built using SQL, from schema creation to data insertion and querying.

### Key Features
* A fully normalized relational schema designed to ensure data integrity and minimize redundancy.
* Detailed tables for planets, moons, and asteroids, including their physical and orbital characteristics.
* A historical log of space missions, linked to their launching countries and mission objectives.
* A set of sample SQL queries to demonstrate how to extract meaningful insights and relationships from the data.

---

## 🗺️ Entity-Relationship Diagram (ERD)

The following diagram illustrates the database schema, including all tables and their relationships.

*(**Note:** Please create your ERD using a tool like [diagrams.net](https://www.diagrams.net/), save it as `ERD.png`, and upload it to this repository for the image to display here.)*

![ERD of the Astronomical Database](./ERD.png)

---

## 🛠️ Technologies Used

* **Language:** SQL (e.g., SQLite, PostgreSQL)
* **Modeling:** Entity-Relationship Diagram (ERD) design principles.

---

## 🗂️ Database Schema

The database consists of the following primary tables:

* `Planets`: Contains data on each planet in the solar system.
* `Moons`: Details on the natural satellites orbiting the planets.
* `Missions`: Information about various space exploration missions.
* `Countries`: A table to link missions to their country of origin.

---

## 쿼리 Sample Queries

The `sample_queries.sql` file contains various queries to demonstrate the database's capabilities. Here are a few examples:

```sql
-- Q1: Find all moons orbiting the planet 'Jupiter' and order them by diameter.
SELECT
    MoonName,
    Diameter_km
FROM Moons
WHERE PlanetID = (SELECT PlanetID FROM Planets WHERE PlanetName = 'Jupiter')
ORDER BY Diameter_km DESC;


-- Q2: Count the number of missions launched by each country and show the top 5.
SELECT
    c.CountryName,
    COUNT(m.MissionID) AS NumberOfMissions
FROM Missions m
JOIN Countries c ON m.CountryID = c.CountryID
GROUP BY c.CountryName
ORDER BY NumberOfMissions DESC
LIMIT 5;


-- Q3: List all missions that were launched in the 1960s.
SELECT
    MissionName,
    LaunchDate
FROM Missions
WHERE LaunchDate BETWEEN '1960-01-01' AND '1969-12-31'
ORDER BY LaunchDate;
