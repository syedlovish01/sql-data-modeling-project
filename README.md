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

## 🛠️ Technologies Used

* **Language:** MySQL 
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
1. Success Rate by Space Agency
SELECT 
  sa.agency_name,
  COUNT(*) AS total_missions,
  SUM(CASE WHEN lm.success_status = 'Success' THEN 1 ELSE 0 END) AS successful_missions,
  ROUND(SUM(CASE WHEN lm.success_status = 'Success' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS success_rate_pct
FROM planetary_data.luna_missions lm
JOIN planetary_data.space_agencies sa
  ON lm.agency_id = sa.agency_id
GROUP BY sa.agency_name
ORDER BY success_rate_pct DESC;

-- ===========================================

-- 2. Missions per Agency Over Time (Yearly Trend)
SELECT 
  sa.agency_name,
  lm.launch_year,
  COUNT(*) AS missions_launched
FROM planetary_data.luna_missions lm
JOIN planetary_data.space_agencies sa
  ON lm.agency_id = sa.agency_id
GROUP BY sa.agency_name, lm.launch_year
ORDER BY lm.launch_year, sa.agency_name;

-- ===========================================

-- 3. Top 10 Asteroids by Impact Probability
SELECT 
  asteroid_name,
  year_passed,
  next_approach_year,
  impact_probability * 100 AS impact_percent, notes
FROM planetary_data.asteroids
ORDER BY impact_probability DESC
LIMIT 10;

-- ===========================================


-- 4. Moons per Planet (Ranked)
SELECT 
  p.planet_name,
  COUNT(m.moon_id) AS number_of_moons
FROM planetary_data.planets p
LEFT JOIN planetary_data.planetary_moons m
  ON p.planet_id = m.planet_id
GROUP BY p.planet_name
ORDER BY number_of_moons DESC;

-- ===========================================

-- 5. Moons with Atmosphere + Their Planets
SELECT 
  m.moon_name,
  p.planet_name,
  m.radius_km,
  m.orbital_period_days,
  m.has_atmosphere
FROM planetary_data.planetary_moons m
JOIN planetary_data.planets p
  ON m.planet_id = p.planet_id
WHERE m.has_atmosphere = 'Yes';

