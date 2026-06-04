# Dubai Metro Network Analysis (SQL Project)

##  Project Overview
This project focuses on analyzing the infrastructure, layout, and geographic metrics of the Dubai Metro network. Using SQL, I explored a dataset of 55 metro stations to extract key business insights regarding line capacities, network expansion timelines, and spatial distribution relative to the city center (Burj Khalifa).

## Tech Stack & Skills Used
* **Database Engine:** DuckDB / SQLite
* **SQL Concepts:** Aggregations (`COUNT`, `AVG`), Data Filtering (`WHERE`, `LIKE`, `AND`), Data Grouping (`GROUP BY`), Sorting & Limits (`ORDER BY`, `LIMIT`).

---

## Data Challenges & Solutions

### Challenge 1: Total Station Count
**Question:** How many total metro stations are in this dataset?
```sql
SELECT COUNT(*) AS Total_Stations
FROM metro_stations;
Result: 55 Metro stations
'''

###Challenge 2: Identify the Operating Lines
Question: Show a list of only the unique (distinct) colors in the line column to see how many different lines exist.
'''sql
SELECT DISTINCT line 
FROM metro_stations;
Result: RED and GREEN
'''

###Challenge 3: Identify Network Expansion
Question: Find all the metro stations that were opened in the most recent year of the dataset (2021).

sql
SELECT station_name, year_opened
FROM metro_stations
WHERE year_opened = 2021;

Result: * UAE Pavilion (2021)
MRT-1 (2021)
Discovery Gardens (2021)
Al Furjan (2021)
Jumeirah Golf Estates (2021)
Dubai Investment Park (2021)
Expo 2020 (2021)



Challenge 4: Spatial Extremes (Furthest Station)
Question: Which specific station is located the absolute furthest from the Burj Khalifa?

sql
SELECT station_name, line, to_burj_khalifa_km 
FROM metro_stations
ORDER BY to_burj_khalifa_km DESC
LIMIT 1;

Result: UAE Exchange (Red Line) — 32.11 km away.



Challenge 5: Capacity Breakdown by Line
Question: Show the line color and the total count of stations for that line.

sql
SELECT line, COUNT(*) AS Station_Count
FROM metro_stations
GROUP BY line;

Result: * RED: 37 stations
GREEN: 18 stations



Challenge 6: Proximity Analysis by Line
Question: Find the average distance to the Burj Khalifa for the Red line versus the Green line.

sql
SELECT line, AVG(to_burj_khalifa_km) AS Average_Distance_KM
FROM metro_stations
GROUP BY line;

Result:
Red Line: 14.06 km (Average)
Green Line: 9.64 km (Average)



Challenge 7: Geographic Center of the Network
Question: Find the average latitude (lat) and average longitude (lon) of all 55 stations combined.

sql
SELECT AVG(lat) AS Average_Lat, AVG(lon) AS Average_Lon
FROM metro_stations;

Result: * Average Latitude: 25.1885
Average Longitude: 55.2668



Challenge 8: Keyword Text Matching (LIKE)
Question: Find all the metro stations that have the word "Al" somewhere in their name.

sql
SELECT station_name, line
FROM metro_stations
WHERE station_name LIKE '%Al%';

Result: Found 16 stations matching the criteria (e.g., Jebel Ali, Al Furjan, Al Jafiliya, Al Karama, Salah Al Din, etc.).



Challenge 9: Time-Range Filtering (BETWEEN)
Question: Find all the stations that were opened during the decade from 2010 to 2015 inclusive.

sql
SELECT station_name, year_opened
FROM metro_stations
WHERE year_opened BETWEEN 2010 AND 2015;

Result: Returned a comprehensive list of 34 stations constructed during the network's core growth phase between 2010 and 2015.


Key Insights & Takeaways

Network Balance: The infrastructure heavily prioritizes the Red Line, which contains more than double the stations (37) compared to the Green Line (18).

Growth Trends: A significant chunk of the network expansion happened between 2010–2015, with a modern extension burst completed in 2021 (7 new stations).

Geographic Core: On average, the Green Line stations sit closer to the Burj Khalifa city center (9.64 km) than the longer Red Line (14.06 km).
