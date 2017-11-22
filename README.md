# GPS Playback
A proof-of-concept for playback of GPS bus records on a map.

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
