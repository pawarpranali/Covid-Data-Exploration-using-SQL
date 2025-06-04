COVID-19 Data Exploration Using SQL

A concise collection of T-SQL scripts in the PortfolioProject database that uncover insights on COVID-19 cases, deaths, and vaccinations. Each script builds on the CovidDeaths and CovidVaccinations tables to compute percentages, rankings, and cumulative values without collapsing detail rows. Below is a brief overview of each query’s purpose—no SQL code included here.

Project Context
Database: PortfolioProject

Tables:

CovidDeaths (daily cases, deaths, population, continent, etc.)

CovidVaccinations (daily vaccination counts by location and date)

All queries assume that continent is populated for relevant rows.

How to Use
Open SQL Server Management Studio (or Azure Data Studio) and connect to the server containing PortfolioProject.

Ensure both CovidDeaths and CovidVaccinations are loaded and accessible.

Copy a query’s code from the repository, paste it into a new query window, and execute to see results.

Alternatively, create the provided view to simplify downstream reporting.

Queries Overview
Select All Records
Retrieves every row from CovidDeaths where continent is not null—useful for an initial inspection of the data set.

Initial Data Selection
Selects key columns (location, date, total cases, new cases, total deaths, population) for all non-null-continent records, ordered by location and date, as the foundation for further analysis.

Death Percentage (Total Cases vs. Total Deaths)
Calculates the percentage of deaths out of total confirmed cases for locations matching “%states%” (e.g., United States), showing the daily likelihood of mortality once infected.

Infection Rate vs. Population
Computes, for each date and location, what portion of its population has contracted COVID-19 to date, thereby measuring pandemic penetration relative to population size.

Countries with Highest Infection Rate
Identifies locations whose peak total cases (at any point) represent the highest percentage of their populations—revealing which countries saw the greatest prevalence.

Countries with Highest Death Count
Ranks locations by their single largest recorded daily death toll (ignoring null-continent rows), highlighting those most impacted in absolute terms.

Death Count by Continent
Aggregates across locations to find which continent experienced the highest single-day death count, helping compare regional impacts.

Global Summary Numbers
Sums all new cases and new deaths (for non-null-continent rows) to compute global totals and an overall death-percentage metric across all dates and locations.

Rolling Vaccinations per Population
Joins CovidDeaths and CovidVaccinations to calculate a running total of people vaccinated per location (partitioned by location and ordered by date). This reveals cumulative uptake over time.

Vaccination Percentage Using a CTE
Builds on Query 9 by using a Common Table Expression (CTE) to compute “rolling vaccinated count” for each location and then derives the percentage of the population that has received at least one dose on each date.

Creating a View: PercentPopulationVaccinated
Persists the rolling-vaccination logic from Query 9 into a reusable view. Once created, you can query this view to fetch cumulative vaccination totals and calculate vaccination percentages on demand.

Feel free to clone this repository, connect to your SQL Server instance, and run these queries in SSMS (or Azure Data Studio) to explore COVID-19 trends.








