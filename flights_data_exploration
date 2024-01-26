/*
Flights Data Exploration Project

Skills used: Joins, CTE's, Temp Tables, Windows Functions, Aggregate Functions, Creating Views, Converting Data Types
*/

-- Selecting relevant data to start with
SELECT *
FROM AirlineDB..Flights
WHERE OriginAirportCode IS NOT NULL
ORDER BY DepartureDate, OriginAirportCode;



-- Exploring total flights and delays

SELECT OriginAirportCode, COUNT(*) AS TotalFlights,
       AVG(DepartureDelay) AS AvgDepartureDelay,
       AVG(ArrivalDelay) AS AvgArrivalDelay
FROM AirlineDB..Flights
WHERE OriginAirportCode IS NOT NULL
GROUP BY OriginAirportCode
ORDER BY TotalFlights DESC;


-- Analyzing monthly flight trends

SELECT YEAR(DepartureDate) AS Year, MONTH(DepartureDate) AS Month,
       COUNT(*) AS TotalFlights
FROM AirlineDB..Flights
GROUP BY YEAR(DepartureDate), MONTH(DepartureDate)
ORDER BY Year, Month;



-- Identifying airlines with the highest average departure delays

WITH AvgDelays AS (
    SELECT AirlineCode, AVG(DepartureDelay) AS AvgDepartureDelay
    FROM AirlineDB..Flights
    WHERE DepartureDelay IS NOT NULL
    GROUP BY AirlineCode
)
SELECT a.AirlineName, ad.AvgDepartureDelay
FROM AvgDelays ad
JOIN AirlineDB..Airlines a ON ad.AirlineCode = a.AirlineCode
ORDER BY AvgDepartureDelay DESC;



-- Exploring on-time arrival performance by destination

SELECT DestinationAirportCode, COUNT(*) AS TotalFlights,
       SUM(CASE WHEN ArrivalDelay <= 0 THEN 1 ELSE 0 END) AS OnTimeFlights,
       SUM(CASE WHEN ArrivalDelay > 0 THEN 1 ELSE 0 END) AS DelayedFlights
FROM AirlineDB..Flights
WHERE DestinationAirportCode IS NOT NULL
GROUP BY DestinationAirportCode
ORDER BY TotalFlights DESC;



-- Creating a view to store monthly flight trends

CREATE VIEW MonthlyFlightTrends AS
SELECT YEAR(DepartureDate) AS Year, MONTH(DepartureDate) AS Month,
       COUNT(*) AS TotalFlights
FROM AirlineDB..Flights
GROUP BY YEAR(DepartureDate), MONTH(DepartureDate);
