SELECT *
FROM [Portfolio Project]..CovidDeaths
Where continent is not null


SELECT *
FROM [Portfolio Project]..CovidVaccinations
Where continent is not null

--SELECT DATA THAT WE ARE GOING TO BE USING
SELECT location, date, total_cases, new_cases, total_deaths, population
FROM [Portfolio Project].dbo.CovidDeaths
Where continent is not null
Order by 1,2 

--Looking at Total Cases vs Total deaths

SELECT location, date, total_cases, total_deaths, (total_deaths/total_cases)*100 as DeathPercentage
FROM [Portfolio Project].dbo.CovidDeaths
--Where location like '%states%'
Where continent is not null
Order by total_cases DESC

--Looking at Total Cases vs population

SELECT location, date, total_cases, population, (total_cases/population)*100 as PercentPopulationInfected
FROM [Portfolio Project].dbo.CovidDeaths
Where continent is not null
--Where location like '%states%'
Order by total_cases DESC

--Looking at Countries with Highest Infection Rate compared to Population

SELECT location, population, MAX(total_cases) as HighestInfectionCount, MAX((total_cases/population))*100 as PercentPopulationInfected
FROM [Portfolio Project].dbo.CovidDeaths
--Where location like '%states%'
Where continent is not null
Group by Location, population
Order by PercentPopulationInfected DESC

--Showing Countries with Highest Death Count per Population

--Breaking things down by continent

SELECT continent, MAX(total_deaths) as TotalDeathCount
FROM [Portfolio Project].dbo.CovidDeaths
Where continent is not null
--Where location like '%states%'
Group by continent
Order by TotalDeathCount DESC

--WORLD NUMBERS

SELECT SUM(new_cases) as total_cases, SUM(new_deaths) as total_deaths, Sum(new_deaths)/Sum(new_cases) as DeathPercentage
FROM [Portfolio Project].dbo.CovidDeaths
--Where location like '%states%'
Where continent is not null
Order by total_cases DESC


--Looking at Total Population vs Vaccinations

Create View PercentPopulationVaccinated as
Select dea.continent, dea.date, dea.population, vac.new_vaccinations
, Sum(vac.new_vaccinations) OVER (Partition By dea.location Order By dea.location, dea.date) as RollingPeopleVaccinated
From [Portfolio Project]..CovidDeaths dea
Join [Portfolio Project]..CovidVaccinations vac
    On dea.location = vac.location
    And dea.date = vac.date
    Where dea.continent is not null

