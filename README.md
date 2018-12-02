# plot_google_map
#### MATLAB function for plotting a Google map on the background of a figure

plot_google_map.m uses the Google Maps API to plot a map in the background of the current figure. 
It assumes the coordinates of the current figure are in the WGS84 datum, and uses a conversion code to convert and project the image from the coordinate system used by Google into WGS84 coordinates. 
The zoom level of the map is automatically determined to cover the entire area of the figure. Additionally, it has the option to auto-refresh the map upon zooming in the figure, revealing more details as one zooms in. 

The following code produces the screenshot:

```
plot_google_map('apiKey', '<Your_API_Key>') % You only need to run this once, which will store the API key in a mat file for all future usages
lat = [48.8708 51.5188 41.9260 40.4312 52.523 37.982]; 
lon = [2.4131 -0.1300 12.4951 -3.6788 13.415 23.715]; 
plot(lon,lat,'.r','MarkerSize',20) 
plot_google_map
```

#### Prerequisites
Due to changes to the Google Maps billing model, you now must set your own Google Maps API key **and enable billing for your project** (see instructions [here](https://cloud.google.com/billing/docs/how-to/modify-project)). You're getting an automatic credit of 200$/month, which will be enough for 100,000 static maps calls without actually being billed - more details [here](https://cloud.google.com/maps-platform/pricing/). 

Note that this does pose some challenges if you want to deploy your code, as your API key will need to be deployed with the code / as a mat file and hence may be exposed to users.

#### Known Issues
  1. Saving the map with an image/matrix overlay drawn on top of it (especially a semi-transparent one) can sometimes cause unexpected results (map not showing etc.). If you're encountering such problems, it's recommended to use the export_fig submission:  
  http://www.mathworks.com/matlabcentral/fileexchange/23629-exportfig  
  The combination that seems to work best:  
  ```
  set(gcf,'renderer','zbuffer')  
  export_fig('out.jpg')  
  ```

