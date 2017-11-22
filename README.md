# GPS Playback
playback of GPS bus records using Leaflet Playback

![screenshot](https://i.imgur.com/TaJOrnf.png)

Sample data from Hyderabad Bus GPS data.

Full script is in index.html

Uses Leaflet plugin [Leaflet.Playback](https://github.com/hallahan/LeafletPlayback)

Note: Limiting the total number of buses being loaded to 150; my page was crashing beyond that. Change `const buslimit = 150` at the start of the script to change that. The CSV file itself (`hydgps.csv`) has over 260 buses' data.

Data received from Srinivas, Hyderabad.<br>
Code by Nikhil, Pune.<br>
both from DataMeet Community, http://datameet.org
