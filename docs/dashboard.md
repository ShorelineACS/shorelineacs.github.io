---
status: new
---

Note: This page does not refresh automatically. The most recent data is retrieved every time you load the page.

## Shoreline Traffic Cameras

| - | - |
| - | - |
| ![I5 195th](https://images.wsdot.wa.gov/nw/005vc17722.jpg) | ![I5 175th](https://images.wsdot.wa.gov/nw/005vc17627.jpg) |
| ![I5 Metro Base](https://images.wsdot.wa.gov/nw/005vc17552.jpg) | ![I5 155th](https://images.wsdot.wa.gov/nw/005vc17510.jpg) |

## Weather

<a class="weatherwidget-io" href="https://forecast7.com/en/47d76n122d35/shoreline/?unit=us" data-label_1="SHORELINE" data-label_2="WEATHER" data-theme="original" >SHORELINE WEATHER</a>
<script>
!function(d,s,id){var js,fjs=d.getElementsByTagName(s)[0];if(!d.getElementById(id)){js=d.createElement(s);js.id=id;js.src='https://weatherwidget.io/js/widget.min.js';fjs.parentNode.insertBefore(js,fjs);}}(document,'script','weatherwidget-io-js');
</script>

[Source](https://radar.weather.gov/ridge/standard)

| - | - |
| - | - |
| ![West Washington Weather Radar KLGX](https://radar.weather.gov/ridge/standard/KLGX_loop.gif) | ![KATX](https://radar.weather.gov/ridge/standard/KATX_loop.gif) |
| ![PNW Weather Radar](https://radar.weather.gov/ridge/standard/PACNORTHWEST_loop.gif)| ![PNW Weather GOES](https://cdn.star.nesdis.noaa.gov/GOES18/ABI/SECTOR/pnw/GEOCOLOR/GOES18-PNW-GEOCOLOR-600x600.gif) |

[![USA Weather Radar](https://radar.weather.gov/ridge/standard/CONUS-LARGE_loop.gif)](https://radar.weather.gov/ridge/standard/CONUS-LARGE_loop.gif)

<!--## Seattle City Light (Power)
[Source](https://www.seattle.gov/city-light/outages)
<iframe src="https://scl.datacapable.com/map/" title="NORCOM/SNOCOM" width="100%" height="550" style="border:1px solid black;"></iframe>-->

## Seattle Water & North City Water
<!--[Source](https://www.seattle.gov/utilities/neighborhood-projects/water-outages)
<iframe src="https://seattlecitygis.maps.arcgis.com/apps/webappviewer/index.html?id=2122a2d8f0414e9b8d5f83629c7a225e" title="NORCOM/SNOCOM" width="100%" height="550" style="border:1px solid black;"></iframe>-->
<!--
 [North City Water](https://northcitywater.org/)-->

## Band Conditions / Space Weather

<a href="https://www.hamqsl.com/solar.html" title="Click to add Solar-Terrestrial Data to your website!"><img src="https://www.hamqsl.com/solar101vhfpic.php"></a>

[Source](https://www.swpc.noaa.gov/communities/space-weather-enthusiasts-dashboard)

| - | - |
| - | - |
| ![Space Weather Overview Gif](https://services.swpc.noaa.gov/images/swx-overview-small.gif) | <iframe src="https://services.swpc.noaa.gov/text/3-day-forecast.txt" title="3 day forecast" width="550" height="560"></iframe> | 

## Earthquakes
[Source: PNSN](https://pnsn.org/earthquakes/recent) · [USGS data feed](https://earthquake.usgs.gov/earthquakes/feed/v1.0/geojson.php)

<div id="pnw-quakes" style="border:1px solid black; padding:8px; max-height:550px; overflow:auto;">Loading recent Pacific Northwest earthquakes…</div>
<script>
(function () {
  // PNSN won't allow iframe embedding, so we pull the same data from the USGS
  // GeoJSON feed (CORS-enabled) and filter to the Pacific Northwest (WA/OR).
  var BOX = { minLat: 41.0, maxLat: 49.5, minLon: -125.0, maxLon: -116.0 };
  var FEED = "https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_week.geojson";

  function render() {
    var el = document.getElementById("pnw-quakes");
    if (!el) return; // not on this page

    fetch(FEED).then(function (r) { return r.json(); }).then(function (data) {
      var quakes = data.features.filter(function (f) {
        var c = f.geometry && f.geometry.coordinates;
        if (!c) return false;
        var lon = c[0], lat = c[1];
        return lat >= BOX.minLat && lat <= BOX.maxLat && lon >= BOX.minLon && lon <= BOX.maxLon;
      }).sort(function (a, b) { return b.properties.time - a.properties.time; }).slice(0, 30);

      if (!quakes.length) { el.textContent = "No earthquakes reported in the region this week."; return; }

      var rows = quakes.map(function (f) {
        var p = f.properties;
        var depth = f.geometry.coordinates[2];
        var when = new Date(p.time).toLocaleString();
        var mag = (p.mag == null) ? "–" : p.mag.toFixed(1);
        return "<tr>" +
          "<td>" + mag + "</td>" +
          "<td><a href=\"" + p.url + "\" target=\"_blank\" rel=\"noopener\">" + p.place + "</a></td>" +
          "<td>" + (depth == null ? "–" : depth.toFixed(1) + " km") + "</td>" +
          "<td>" + when + "</td>" +
          "</tr>";
      }).join("");

      el.innerHTML = "<table><thead><tr><th>Mag</th><th>Location</th><th>Depth</th><th>Time</th></tr></thead><tbody>" + rows + "</tbody></table>";
    }).catch(function () {
      el.innerHTML = "Could not load earthquake data. " +
        "<a href=\"https://pnsn.org/earthquakes/recent\" target=\"_blank\" rel=\"noopener\">View on PNSN</a>.";
    });
  }

  // Material's "navigation.instant" swaps pages without a full reload, so inline
  // scripts don't re-run on tab navigation. document$ fires on every page load.
  if (typeof window.document$ !== "undefined") {
    window.document$.subscribe(render);
  } else {
    render();
  }
})();
</script>

## Radiation Monitors

[Source:"Alert Level = 3 consecutive minutes of lesser of 100 CPM or 2.5 times a Station's baseline"](https://radiationnetwork.com/DetailMaps.htm)
[![PNW Radiation Network](https://radiationnetwork.com/PacificNW.jpg)](https://radiationnetwork.com/DetailMaps.htm)

## Other

- [Washington State Emergency Operations Center Dashboard](https://www.arcgis.com/apps/MapSeries/index.html?appid=029f66c8d92443029cc8b2a247d056cc)
- [National Interagency Fire Center Maps](https://www.nifc.gov/fire-information/maps)
- [FAA National Airspace System Status](https://nasstatus.faa.gov/map)