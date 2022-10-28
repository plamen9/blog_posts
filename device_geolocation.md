Visit my [DEMO PAGE](https://apex.oracle.com/pls/apex/r/gamma_dev/demo/new-features) and see the new Device Geolocation feature in action. 🌐

# Device Geolocation

### `Get Current Position` Dynamic Action

> The new Get Current Position dynamic action fetches the device current location and returns a JavaScript GeoJSON object or Latitude and Longitude to page items, or the full Geolocation object to a custom JavaScript function.

Definitely a big step towards making APEX more and more attractive for mobile applications development. This out-of-the-box features will save some time and custom coding to get the geographic coordinates of user's device. Few important points to note on this feature:

  - It can provide the Location in three different formats - Latitude/Longitude, JSON and Javascript Geolocation Object

![3_Location.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1666908130077/0nGDjIBts.png)

![4_Location.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1666908061418/VpxmOyxan.png)

  - It has two levels of Accuracy - Default and High Accuracy. My observation is that `Enable High Accuracy` turned OFF producess still a great result and will be sufficient in 99% of the cases, saving some power from your device.

> `Enable High Accuracy` turned OFF

```json
{"latitude":53.5008148,"longitude":-2.0339685,"altitude":null,"accuracy":15.602,"altitudeAccuracy":null,"heading":null,"speed":null}
```
> `Enable High Accuracy` turned ON

```json
{"latitude":53.5007936,"longitude":-2.0340525,"altitude":null,"accuracy":14.684,"altitudeAccuracy":null,"heading":null,"speed":null}
```

  - The JSON format returned is not ready to use in Map Layer using GeoJSON directly. It will not display the desired point on the map if you don't format it additionally.    

Here is how to GeoJSON result looks like:

```json
{"latitude":53.430759,"longitude":-2.961425,"altitude":null,"accuracy":15.602,"altitudeAccuracy":null,"heading":null,"speed":null}	
```
... and here is what GeoJSON format the Map Region expects:

```json
{ "type": "Point", "coordinates": [-2.961425, 53.430759] }
```

Adding an additional Action that transforms the value would solve that problem and the point would be displayed on the Map:

```sql
declare
   l_geojson varchar2(4000);
begin

   with device_json as (
           select :P5_MY_LOCATION json_res 
           from dual )

   select --jt.*, 
              '{"type": "Point", "coordinates": ['||jt.longitude||', '||jt.latitude||']}' coordinates
       into l_geojson 
       from device_json,
       json_table(json_res, '$[*]'
          columns (longitude varchar2(100) path '$.longitude',
                   latitude  varchar2(100) path '$.latitude')
       ) as jt;

   :P5_MY_LOCATION := l_geojson;

end;
```

### Sample Dynamic Action setup

Below is the setup for my demo page. I have a button, triggering the Dynamic Action on the click event. The Dynamic Action has four True actions as follows:

![5_Location.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1666909479053/6CM9w8ZRF.png)

- The new `Get Current Position` which fetches my location into a hidden item, named `P5_MY_LOCATION`
- An `Execute Server-side Code` action, which converts the returned GeoJSON into another GeoJSON that is used by the Map Region. You can see the code above.
- A `Refresh` Region action, which does refresh the Map Region
- An `Execute Javascript Code` action, which centers and zooms the Map around my location, using the value from `P5_MY_LOCATION` item. See the source below:

```javascript
var lMapRegion   = apex.region("my_location"),
// important: Use the layer name exactly as specified in the "name" attribute in Page Designer
lLayerId     = lMapRegion.call("getLayerIdByName", "Map Search"),
lCurrentZoom = lMapRegion.call("getMapCenterAndZoomLevel").zoom,
lLocationId  = apex.item("P5_MY_LOCATION").getValue(),
lFeature     = lMapRegion.call("getFeature", lLayerId, lLocationId ),
lPosition;

console.log("lLocationId -> " + lLocationId);    

//lPosition    = lFeature.geometry.coordinates;
lPosition = jQuery.parseJSON( lLocationId );

console.log("lPosition -> " + lPosition);    

// close all Info Windows, which might currently be open
lMapRegion.call( "closeAllInfoWindows" );

// focus the map to the chosen feature
//lMapRegion.call( "setCenter", lPosition );
apex.region( "my_location" ).setCenter( lPosition.coordinates );

// zoom in the map
lMapRegion.call( "setZoomLevel", 11 );
``` 

### Configuring the `Map Region` **Points** Layer Type
- Create a new Map Region
- Add a new Layer of type **Points** with the following settings

![6_Location.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1666911784812/WqeUc-e2x.png)

![7_Location.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1666911796098/FSHq88iKH.png)

- Change the Shape, Fill colors and size as you like

### Granting permission
For security reasons, your device would ask you for permission before it can use your location. Depending on the device, once you hit the `Find me` button that triggers the `Get Current Position` action, you will get a similar message. Check the following ones from Chrome, Firefox and an iPhone Safari browser:

![8_Location.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1666912759323/j4ZeCb2JJ.png)

# APEX 22.2 official release

[What's new in Oracle APEX 22.2 ?](https://apex.oracle.com/en/platform/features/whats-new-222/)

[Device Geolocation, Web Share, and Declarative Meta Tags in APEX 22.2](https://www.youtube.com/watch?v=YHf4cJzwkOc)

# Demo

Visit my [DEMO PAGE](https://apex.oracle.com/pls/apex/r/gamma_dev/demo/new-features) to see this exciting new feature in action. Enjoy!
