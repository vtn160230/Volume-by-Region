# Volume-by-Region


Case Scenario in the workplace when a coworker sends you a file along with an email explaining the situation below

***

### Email sent with file attachment - Volume by Region (Raw).xlsx:

Hey,

The board is asking to see how volume looked in Q2. I got some data (attached), but didn’t have a chance to pull anything together and was hoping you could take a stab at it.

I think they just want to see Q2 2021 volume by region and wanted to know if everything was looking good. I think this file has what you need. I don’t remember all the region codes – I know NAM ends in 1, EMEA ends in 3 and APAC and LATAM are 2 and 4, but I don’t remember which is which. I do know LATAM has the lowest volume so just go ahead and assign that to which ever comes out lowest.

I appreciate your help!

*** 
### Starting off
- Began by creating duplicates of the sheets EXT0070122021 and Sheet3 to have originals I can cross reference to later
- Renamed EXT0070122021 and sheet3 based on data in the sheet to something more appropriate and befitting (Volume Data and Geo Data)
***

### Data Cleaning and analysis of EXT0070122021/ Volume Data sheet
- Unwrapped the Volume Data sheet as it looks wrapped and autofit
- Turned the data into a table and renamed the table to VolumebyClient
- Filled in the column in the CLID (Client ID) by highlighting the column with ctrl + space and Go to Special (Blanks) and referring to A2 to fill in all the blanks
- Copied the CLID column and pasted Values
- Went to Date Column and used the Text to Columns to delimit the data
- On the Volume column, used the Text to Columns to delimit the data
- Created a new column named Length to check the length of the CLID to look for consistency 
- Created a new column named xlookup region and did a =XLOOKUP(xxx, xxx, xxx) to match the Geo ID with the CLID
- Did a Index Match using the function =INDEX(GeobyClient[GEOID],MATCH([@CLID],GeobyClient[Right],0)) 
- Created a Region column and used a =VLOOKUP([@[Index Match Region ID]],GEONames[[GEOID]:[GEO Name]],2,FALSE) to retrieve Regions for the GEO ID

***

### Data Cleaning and analysis of Sheet3/Geo Data sheet

- Went to Geo Data worksheet and unwrapped and autofit the columns
- Copied CLID column and pasted Values in another column and checked duplicates because CLID should be unique
- Copied GEOID and pasted values in another column to ensure there was only GEO1001-GEO1004 in the data
- Created a new column named Length to check the length of the CLID to look for consistency 
- Noticed that the CLID in Geo Data has 2 extra characters so I created a new column and ran a =RIGHT( xxx, 7) to get 7 characters starting from the right to match the CLID in Volume Data
- Create a new column and find the volume for each GEO ID (1001-1004) using =SUMIFS(VolumebyClient[Vol],VolumebyClient[Xlookup Region],[@GEOID])
