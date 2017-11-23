# GPS Playback
A proof-of-concept for playback of archived GPS bus records on a map.

See it live: <https://answerquest.github.io/GPSPlayback/>

![screenshot](https://i.imgur.com/TaJOrnf.png)

Sample data from Hyderabad Bus GPS data.

Full script is in index.html

Uses Leaflet plugin [Leaflet.Playback](https://github.com/hallahan/LeafletPlayback)

Note: Limiting the total number of buses being loaded to 150; my page was crashing beyond that. Change `const buslimit = 150` at the start of the script to change that. The CSV file itself (`hydgps.csv`) has over 260 buses' data.

Data received from Srinivas, Hyderabad.<br>
Code by Nikhil, Pune.<br>
both from DataMeet Community, http://datameet.org

Do you have GPS data you want to visualize? Contact Nikhil on nikhil.js [at] gmail.com .

Like this work? Want to see more of it? [Click here to contribute!](https://www.instamojo.com/@nikhilvj/)

## How it works

### The input raw data is in this CSV format:

```
id,latitude,longitude,vehicle,time,busnum,status,time2,col,detail,bustype
1047,17.410196,78.488861,AP07Z4008,2017-11-19 11:45:44,71,Late,19/11/2017 11:45:32,29,60 Mtrs from ASHOK NAGAR X ROAD,DELUXE
1047,17.410196,78.488861,AP07Z4008,2017-11-19 11:45:47,71,Late,19/11/2017 11:45:32,29,60 Mtrs from ASHOK NAGAR X ROAD,DELUXE
1047,17.410196,78.488861,AP07Z4008,2017-11-19 11:45:48,71,Late,19/11/2017 11:45:32,29,60 Mtrs from ASHOK NAGAR X ROAD,DELUXE
```
### The plugin needs a customized GeoJSON per bus, in this format:
```
{
  "type": "Feature",
  "geometry": {
    "type": "MultiPoint",
    "coordinates": [
      [
        78.464539,
        17.404537
      ],
      [
        78.464539,
        17.404537
      ],
      ...
      [
        78.464539,
        17.404537
      ]
    ]
  },
  "properties": {
    "name": "Bus num: 57 - Default <br>Vehicle no.AP11Z7274, type: AC",
    "time": [
      1511072144000,
      1511072147000,
      1511072148000,
      1511072150000,
      ...
      1511072266000
    ],
    "id": "1118",
    "vehicle": "AP11Z7274",
    "busnum": "57 - Default ",
    ...
  }
}
```
The "time" array is key here. It carries timestamps corresponding to the lat-long co-ordinates array, in EPOCH format. Regular GPX to GeoJSON / CSV to GeoJSON converters online do not encode this time information in this way. Hence a function had to be built for this.

### Function csv2busJSON

* takes the CSV path, 
* imports it using Papa.parse,
* extracts a unique list of buses by id,
* separates the CSV data by bus,
* converts it into the required GeoJSON format,
* creates an array of bus jsons,
* and passes the array to the mapping function.
