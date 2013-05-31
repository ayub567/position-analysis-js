position-analysis-js
====================

Position Analysis Web template

## Setup

The Position Analysis Web template uses Portal for ArcGIS 10.2+ or ArcGIS Online. You'll need the portal URL
in order to set up the application.

You must deploy the Web application on a HTTPS-enabled Web server, or else the login to Portal or ArcGIS 
Online will not work.

If using [the ArcGIS proxy page](http://developers.arcgis.com/en/javascript/jshelp/ags_proxy.html),
and if the Portal certificate is self-signed or issued by a non-standard certificate authority (CA), you
have to configure the Web server that is hosting the proxy page to trust the certificate and/or CA. The
directions for this vary based on which proxy page you choose--ASP.NET, Java, or PHP. (For example, for
the Java proxy page, you must use the JDK's keytool to add the CA root certificate to the trust store of
the JRE that runs your Web server.) Directions are available on the Web for various platforms and Web
servers.

You need to publish the Locate Event model from the [Position Analysis Tools toolbox
](https://github.com/Esri/defense-and-intel-analysis-toolbox/blob/master/toolboxes/Position%20Analysis%20Tools.tbx)
as a geoprocessing service in ArcGIS 10.1 (or later) for Server. The model requires no data, so simply run
it in ArcMap and publish the result. You'll use the URL of the Locate Event task as the locateEventUrl
configuration variable mentioned below.

Deploy the [site](site) directory as a Web application in your HTTPS-enabled Web server with a context
name of your choice. Open [site/js/pos-analysis.js](site/js/pos-analysis.js) in a text editor and edit the
variables at the top of the file as necessary:

- webmapTitle: the title of the expected Web map. If the user does not own a Web map with that title,
               a Web map with that title will be created.
- webmapExtent: the initial extent for a Web map created by this application.
- portalUrl: the Portal for ArcGIS URL.
- sharingPath: a relative path such that portalUrl + sharingPath is the full sharing URL for the portal.
- proxyRequired: true if the ArcGIS API for JavaScript needs to use a proxy and false otherwise.
                 A proxy is required when hosting the application on a different domain than Portal
                 for ArcGIS and may be required in other situations. Read
                 [the proxy page documentation](http://developers.arcgis.com/en/javascript/jshelp/ags_proxy.html)
                 for further details.
- proxyUrl: the relative or absolute URL to the proxy page.
- locateEventUrl: the URL of the geoprocessing task used by the Locate Event tool.
- locateEventInputParameterName: the feature set input parameter name for the geoprocessing task.
- locateEventOutputLinesParameterName: the name of the lines output parameter for the geoprocessing task.
- locateEventOutputAreaParameterName: the name of the area (polygon) output parameter for the geoprocessing task.
- longitudeNamesUppercase: uppercase form of CSV column names that will be treated as the longitude field
                           when uploading a CSV. Though the field names must be in uppercase in this file,
                           the field names in the CSV may be in any case.
- latitudeNamesUppercase: uppercase form of CSV column names that will be treated as the latitude field
                          when uploading a CSV. Though the field names must be in uppercase in this file,
                          the field names in the CSV may be in any case.
- mgrsNamesUppercase: uppercase form of CSV column names that will be treated as the MGRS field
                      when uploading a CSV. Though the field names must be in uppercase in this file,
                      the field names in the CSV may be in any case.
- azimuthNamesUppercase: uppercase form of CSV column names that will be treated as the azimuth field
                         when uploading a CSV. Though the field names must be in uppercase in this file,
                         the field names in the CSV may be in any case.
- distanceNamesUppercase: uppercase form of CSV column names that will be treated as the distance field
                          when uploading a CSV. Though the field names must be in uppercase in this file,
                          the field names in the CSV may be in any case.
- titleNamesUppercase: uppercase form of CSV column names that will be treated as the title field
                       when uploading a CSV. Though the field names must be in uppercase in this file,
                       the field names in the CSV may be in any case.
- shapeNamesUppercase: uppercase form of CSV column names that will be treated as the shape field
                       when uploading a CSV. Though the field names must be in uppercase in this file,
                       the field names in the CSV may be in any case. The shape string should have the
                       format of a JSON point, polyline, or polygon string as specified in [the ArcGIS
                       REST API](http://resources.arcgis.com/en/help/arcgis-rest-api/index.html#/Geometry_Objects/02r3000000n1000000/).


Open index.html and edit the ArcGIS API for JavaScript URLs, including the JavaScript link and the CSS
links. If using Portal for ArcGIS, you should use the ArcGIS API for JavaScript included with the portal.

## Usage

Navigate to the application in a Web browser. In the Settings tab, login to Portal for ArcGIS. When the map
appears, you can use all the application's tools in the following tabs:

### Add Features

Add to layer: the layer to which new features will be added.

Click Points: press this button, then click the map to add a new point to the layer.

Add point by coordinates: type a longitude and latitude, or an MGRS string, then click Add Point to add a
new point to the layer.

Select Files: choose a CSV file containing features to add to the map. Alternatively, you can drag and
drop a CSV onto the map.
The CSV should have column headers. See the configuration variables above for specifying which column
names the application
will recognize. In general, here are the columns used by the application (the names are specified using
the configuration variables):

- Name
- Latitude
- Longitude
- MGRS
- Geometry (specified as a JSON point, polyline, or polygon string as specified in [the ArcGIS REST API
           ](http://resources.arcgis.com/en/help/arcgis-rest-api/index.html#/Geometry_Objects/02r3000000n1000000/)
- Azimuth (in degrees)
- Distance (in meters)
           
### Locate Event

Choose a layer containing three or more points to be used as observations for locating an observed event.
Each observation should have an azimuth and a distance. Then click Locate. The geoprocessing service is
called, and the estimated area of the event appears on the map, along with the observation lines calculated
from each point's azimuth and distance.

### Calculate Range Rings

TODO not yet implemented

### Settings

Use the Settings tab to login to Portal for ArcGIS before using the rest of the application.

Click Save Map to save the feature layers. These layers are stored in a Web map.

### Manage Layers

Check the checkboxes to change layers' visibility. Click a layer name to rename that layer.

## Licensing

Copyright 2013 Esri

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

A copy of the license is available in the repository's
[license.txt](license.txt) file.

Note: Portions of this code use USNG which is licensed under the MIT License.
See [license-ThirdParty.txt](license-ThirdParty.txt) for the details 
of this license.