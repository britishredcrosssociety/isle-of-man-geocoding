# Isle of Man geocoding lookup table
Script to geocode postcodes from the Isle of Man (`IM`)

BRC operates in the Isle of Man, but there is a lack of open data on postcodes in these areas that would allow us to assign locations to records using postcodes. For the UK, comprehensive postcode geocoding/lookups are provided by the ONS Postcode directory.

This lookup table and processing script uses open data from Wikipedia to assign approximate latitude and longitude to postcodes from the Isle of Man, with approximate accuracy at the parish level. It is suitable for giving a rough indication of where a postcode is but not suitable for locating specific streets or addresses.

## How to use it

This example is in Python, but the workflow should be repeatable using the same CSV file with any language that supports relational joins and regular expression matching.

* Open the isle-of-man-postcodes.py file in an editor
* On line 15, there is a sample of postcodes to geocode. This can be edited with any list of postcodes, either hard coded or read from another data source
* After the postcode source has been defined, save the file and run it with `python3 -m isle-of-man-postcodes.py`
* The script will output a json file with the results (a lat/lng coordinate pair), that can be used for further processing/analysis In the example in the Python script, the postcodes IM2 1AA, IM2 6RB, IM8 3EG, IM5 1RD are returned as:

```
{'IM2 1AA': {'lat': 54.15, 'long': -4.482, 'coverage': 'Douglas'}, 
'IM2 6RB': {'lat': 54.15, 'long': -4.482, 'coverage': 'Douglas'}, 
'IM8 3EG': {'lat': 54.322, 'long': -4.384, 'coverage': 'Ramsey'}, 
'IM5 1RD': {'lat': 54.222, 'long': -4.695, 'coverage': 'Peel'}}
```

## How it was made

* Wikipedia has a breakdown of the locations referred to by the IM postcodes, which helps to narrow postcodes down to a parish or town
* Coordinates were assigned manually at what looked to be the approximate population centre of each area.
* The incomplete postcodes were added to a lookup table alongside their coordinates
* A regular expression checks any inputted postcodes against the most complete match it can find in the lookup table - so for the `IM2 6RB` postcode, it will match in the lookup table to the regex `IM2 6[A-Z][A-Z]`.
