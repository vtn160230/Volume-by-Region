# Volume-by-Region

Began by creating duplicates of the sheets EXT0070122021 and Sheet3 to have originals I can cross reference to later
- Renamed EXT0070122021 and sheet3 based on data in the sheet to something more appropriate and befitting (Volume Data and Geo Data)
***

### EXT0070122021/ Volume Data sheet
- Unwrapped the Volume Data sheet as it looks wrapped and autofit
- Turned the data into a table and renamed the table to VolumebyClient
- Filled in the column in the CLID (Client ID) by highlighting the column with ctrl + space and Go to Special (Blanks) and referring to A2 to fill in all the blanks
- Copied the CLID column and pasted Values
- Went to Date Column and used the Text to Columns to delimit the data
- On the Volume column, used the Text to Columns to delimit the data
- Created a new column named Length to check the length of the CLID to look for consistency 
- Created a new column named xlookup region and did a =XLOOKUP(xxx, xxx, xxx) to match the Geo ID with the CLID
- Did a Index Match using the function =INDEX(GeobyClient[GEOID],MATCH([@CLID],GeobyClient[Right],0)) 

***

### Sheet3/Geo Data sheet

- Went to Geo Data worksheet and unwrapped and autofit the columns
- Copied CLID column and pasted Values in another column and checked duplicates because CLID should be unique
- Copied GEOID and pasted values in another column to ensure there was only GEO1001-GEO1004 in the data
- Created a new column named Length to check the length of the CLID to look for consistency 
- Noticed that the CLID in Geo Data has 2 extra characters so I created a new column and ran a =RIGHT( xxx, 7) to get 7 characters starting from the right to match the CLID in Volume Data
- Create a new column and find the volume for each GEO ID (1001-1004) using =SUMIFS(VolumebyClient[Vol],VolumebyClient[Xlookup Region],[@GEOID])
