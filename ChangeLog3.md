## Changes from 2.5 ##
  * Updated to use **Google Maps API v3**
    * Added **KML Overlay** support - add KML/GeoRSS files utilizing the client side JS calls.
      * Simply pass in a filename to any KML or GeoRSS file and you are on your way!
    * Added ability to **create maps for mobile devices**
      * Set **`$this->mobile=true`** to have [meta tag](http://code.google.com/apis/maps/documentation/v3/basics.html#Mobile) rendered in the get header js call.
      * Future updates will include ability to get user's location from GPS.
      * Note: The new v3 Google Maps JS API is already catered towards mobile devices.  Just by setting width and height = 100%, any of the demos from the main page can be displayed on the most popular newer devices with JS support.
    * Update **Polyline handling** with new API v3 methods.
      * A new paramter ($id) was added in both of the polyline "add" methods.
      * Please make sure to update your apps that are using the add methods (more specifically the variable order).
      * This change was necessary to make polyline handling a bit more advanced.
    * Added **addPolylineByCoordsArray** and **addPolylineByAddressArray** methods
    * Added **Elevation Chart** display support.
      * Display multiple elevation charts for a map (and even multiple maps/charts per page)
      * Choose whether or not to display a correspondingly located marker on the line (directions or polyline) when hovering over a location on the elevation chart.
    * **Removed** references and everything dealing with **Google Maps API key** since **keys are no longer necessary in V3** of the API!
    * **Removed tabs support** for now (not part of official V3 Google Maps JS API anymore :( )
      * Potential to reincorporate with jQuery UI tabs?
    * Updated **map type names** to be compatible with V3 api.
    * **Updated icon/marker creation** to use new methods/workflows.
    * Added **addMarkerOpener** function to create **custom marker openers**
      * The function takes a marker id (returned from add marker) and dom object id and then attaches an onclick (or onmouseover if you've switched the default action) to the given object and opens the marker's info window.
    * Update **geocaching** to use new Google Maps V3 geocoder.
      * Updated to use JSON encoding vs. csv
      * New API no longer requires API key - http://code.google.com/apis/maps/documentation/geocoding/
      * Added **geoGetCoordsFull** method to return entire geocode response.
        * **NOTE** This new method does not use caching.  This can change if need be, but for now it always queries the API.
    * Updated automatic **zoom fitting** to use new **map.fitBounds()** API method.
    * Updated **order/rendering** of javascript to coincide with the latest methods using options instead of multiple calls.
  * **Modified directions support**
    * (changed to directions "object" to allow instantiation of a map with directions parameters passed).
    * $this->directions param is **deprecated**.  You should now just use $this->addDirections()
    * Adding "get directions to/from here" to an infowindow should be fairly simple using the supplied methods. See [demo](http://www.bradwedell.com/phpgooglemapapi/demos/advanced_marker_directions.php)
      * I can add this support back in if need be/enough people request it.
  * **Modified custom icon support**
    * replaced "addMarkerIcon" with addIcon and updateMarkerIconKey
    * Icons will now be explicitly defined when creating a marker using the icon (and shadow) file locations
    * You can also set a default icon file to use by setting $this->default\_icon (and default\_icon\_shadow)
    * TODO:Add more support for creating custom markers (will wait and see what people think)
      * In order to pass all values for an icon instead of just the filename,you would have too call addIcon manually and pass the x parameters.  Then when you create the markers, you can simply pass the filename and the icon will already have been initialized with the custom vs. calculated values.
  * Added **walking and biking directions** support
  * Added **Traffic Overlay** and **Bike Map Overlay** support.
  * Added **Custom Overlay** support with opacity option
  * Added **JSMin minification** support.  Note- this means that in order to leave `$_minify_js` set to true (default), you must include JSMin.php as well.  I have included a copy of this library in the repository.
  * Added **multiple maps support**!
    * Added `$_display_js_functions` class variable so that you can control when the "helper" JS function definitions are displayed and when they shouldn't be.  If you have N maps, the every map object except the Nth map should set this variable to false.
    * Updated JS function rendering to include the map id in variable name definitions to avoid namespacing conflicts with multiple maps.
      * **NOTE** Be sure each map instance has a unique map\_id, which is assigned during object instantiation.
      * **Be Aware**
        * For single maps, you will want to be sure to always use the getOnLoad() function if you aren't already (i.e. <?=$obj->getOnLoad();?> vs `<body onLoad="onload();">` - I know I'm guilty of doing this, but in order to support multiple maps, this had to be done.
        * For multiple maps, you'll want to define your own onload function using the new getOnLoadFunction call, which returns the JS function names of the onload functions for each map.
  * Added **[MarkerClusterer](http://google-maps-utility-library-v3.googlecode.com/svn/tags/markerclusterer/1.0/examples/advanced_example.html?)** support.
    * I have also added the JS code for MarkerClusterer to the SVN repo as an svn:externals property linking to their SVN repo.  This in the "external" folder (it doesn't show up in the source tab, but if you checkout http://php-google-map-api.googlecode.com/svn/trunk/external/ , you will get the files)
    * See [the example](http://www.bradwedell.com/phpgooglemapapi/demos/advanced_marker_clusterer.php) for implementation details.
  * Add ability to choose between **buttons or dropdown** for map type navigation.
  * Added **street view controls** support!  Check out the [demo](http://www.bradwedell.com/phpgooglemapapi/demos/simple_streetview.php) to see how easy it is!
  * Added **Polygon** support