# powerbi 
# Covid-19 Global cases Analysis created on Power BI
<h4>source</h4>
Json.Document(Web.Contents("https://opendata.ecdc.europa.eu/covid19/casedistribution/json/")) <br>
<h4>Data shaping</h4>
Navigation = Table.FromList(records, Splitter.SplitByNothing(), null, null, ExtraValues.Error) <br>
Converted table= Table.ExpandRecordColumn(#"Converted to Table", "Column1", {"dateRep", "day", "month", "year", "cases", "deaths", "countriesAndTerritories", "geoId", "countryterritoryCode", "popData2018"}, {"dateRep", "day", "month", "year", "cases", "deaths", "countriesAndTerritories", "geoId", "countryterritoryCode", "popData2018"})<br>
Change type 1= Table.TransformColumnTypes(#"Expanded Column1",{{"dateRep", type date}, {"day", Int64.Type}, {"month", Int64.Type}, {"year", Int64.Type}, {"cases", Int64.Type}, {"deaths", Int64.Type}})
<h4>Data Modelling</h4>
Created Date Dimension table to calculated time series measures<br>
DateDim = ADDCOLUMNS( CALENDARAUTO(),
"Year", Year([Date])
)<br>
Created Measures table for Key Measures, Cumulative totals, Time series, Countries table, Fact table<br>
<h6>Measures created for analysis </h6>
Death rate = total deaths per 100,000 of the population <br>
Attack rate = total cases per 100,000 of the population
