# Vector Map Tiles

> The Map region can now use Vector Layers for improved display quality, especially on high pixel density displays.

Why is this good news? Because vector tiles are faster to render, smaller in size, contain lots of information, not just graphical. They eliminate the blur that you usually see for a second before the map is reloaded after zoom-in, zoom-out or drag. All the types of maps currently supported in Oracle APEX are great for being presented using vectors.

### How does the Map render in your browser?

- First of all, the rendered maps are a collection of tiles and each zoom level is presented using a seperate set of tiles. That's why when you zoom or drag, the browser makes a number of requests to a server to get the new set of tiles. Each tile is delivered using a seperate call. So you can imagine how many call your application does for a single move of the map. Just open the `Browser Dev Tools` on the `Network` tab and check for yourself.

![Map tiles in different zoom levels](https://cdn.hashnode.com/res/hashnode/image/upload/v1666985635788/4Himi1C6j.png)

- What format can the tile be? It could be a `Raster` format (like `PNG`) or a `Vector` format (like `PBF`). Here are some of the benefits of using Vector tiles and these are the reasons why APEX now supports it in the latest version:

`Pros:`
  - Smaller size - lower server space requirement
  - Lower bandwidth consumption
  - Faster loading time
  - Smooth zooming experience
  - Invisible zoom levels
  - High-resolution display on all zoom levels without increasing the file size
  - Easy and on-the-fly customization

`Cons:`
  - Rendering on end-user’s device requires more powerful hardware

Not bad, right! However, there are some specific types of maps, where Raster formats are used and that is when satellite or aerial imagery is displayed. Check the two images below to see those two use cases:

![Vector Tiles example](https://cdn.hashnode.com/res/hashnode/image/upload/v1666989001138/n_8imkoey.png)

![Raster Tiles example](https://cdn.hashnode.com/res/hashnode/image/upload/v1666989019921/OltmxTsi7.png)

### Tiles and APEX Maps

Opening your Browser Dev Tools while you interact with an APEX Map will give you a very good idea of the process behind rendering a map. Each move, zoom-in, zoom-out or a drag in any direction results in a number of calls to a server to get the new set of tiles. So having a format, that is smaller in size can greatly improve the loading speed and the user experience. Furthermore, you can get a very good idea of what service is used by the APEX Map region for getting the tiles information (**https://elocation.oracle.com/**), what is the content type and what is the size of each tile.

![Raster PNG tiles used by the Map Region](https://cdn.hashnode.com/res/hashnode/image/upload/v1666989605981/CmXPm0hb7.png)

![Vector PBF tiles used by the Map Region](https://cdn.hashnode.com/res/hashnode/image/upload/v1666989634607/CZ6AD_2IK.png)

> Read more about the difference between **raster** and **vector** formats for displaying Map tiles in [this article](https://documentation.maptiler.com/hc/en-us/articles/4411234458385-Raster-vs-Vector-Map-Tiles-What-Is-the-Difference-Between-the-Two-Data-Types-)
<br>
Also check the official release video for this new feature in the video below. ⬇️

[Map Region Enhancement in APEX 22.2](https://www.youtube.com/watch?v=0DjNfnLHhDU)

# Enabling the Vector Map tiles

Although it's just one simple step, and it's turned on by default, it's good to know where to look for it. The **Component Settings** in **Shared Components** holds the global settings for several Regions and components.

To change the tiles type, used in your Maps regions do the following:
 - Go to `Shared Components`
 - Open `Component Settings`
 - Open `Maps` 
 - Change `Use Vector Tile Layers`

The default value is '**Yes**' and I encourage you to leave it like that, so you can take advantage of the new way maps are rendered.

![Enabling Vector Map tiles in APEX](https://cdn.hashnode.com/res/hashnode/image/upload/v1667200000095/KdUtAdsxy.png)
