# **Data Analysis of NYC Citibike**
***
<font size="3">Author Name</font>:<font size="3">**Nirnay Mahantesh Banagar**,</font><font size="3">**Tanush Harish Bhaskar**</font>

<font size="3">Youtube</font>:[NYC CitiBike Data Analysis Using Python](https://youtu.be/Q_CAIUs1yVM)

---

## Introduction
### Purpose
<font size="3">The purpose of this project is to analyse the real-time NYC Citibike data and to determine the popular destinations in NYC</font>.
### Data used in the project
<font size="3">The real-time data is pulled from from NYC Citibike website where the data is available to public. The data available in the source file consists of the following information</font>:
- Station ID
- Station Name
- Total number of docks (Capacity of the station) 
- Number of Bikes available at the Station.
- Number of Docks available at the Station. 
- Longitude
- Latitude

### Purpose of using the data
<font size="3"> New York is popular tourist destination. Citibikes provide the tourists as well as the residents of New York with an opportunity to explore the city at their convenience. The data provides sufficient inputs to understand the operations of the Citibike. Inferences can be made on the basis of availability of the bikes at a station, movement of the Bikes, and capacity of the station. </font>.

### Analysis Done using the Data
- <font size="3"> Number of available bikes are visualized on the map to infer the number of bikes available at the location. </font>.
- <font size="3"> Similarly, capacity of the locations are categorized and visualized on the map to infer popular destinations in New York City.</font>




## References
### Following are the list of sites referred to support the data analysis
- Data Source [Citibike oper data source](https://www.citibikenyc.com/system-data)
- Source code was adapted from [Pandas document](https://pandas.pydata.org/)
- Source code was adapted from [numpy.org](https://www.numpy.org/devdocs/user/quickstart.html)
- Source code was adapted from [Bokeh](https://bokeh.pydata.org/en/latest/docs/reference.html)
- Source code was adapted from [Json](https://realpython.com/python-json/)
- API key was subscibed from (Source code was adapted from [API](https://realpython.com/python-json/))
- Source code was adapted from [Summarize](https://machinelearningmastery.com/quick-and-dirty-data-analysis-with-pandas/)
---
## Requirements
- <font size="3">The python packages used are</font> <font size="3">Numpy</font>,<font size="3">Pandas</font>,<font size="3">bokeh</font>,<font size="3">urllib</font>,<font size="3">matplotlib</font>,<font size="3"> and json</font>.

#### Installation of python packages
-  <font size="3">Go to Anaconda prompt and type pip install time to install time.</font>
-  <font size="3">Go to Anaconda prompt and type pip install bokeh to install bokeh.</font>
-  <font size="3">Go to Anaconda prompt and type pip install matpltlib to install matplotlib.</font>
-  <font size="3">Go to Anaconda prompt and type pip install urllib to install urllib.</font>
-  <font size="3">Go to Anaconda prompt and type requests to install requests.</font>


#### Importing the required packages
- <font size="3">import json</font>
- <font size="3">import requests </font>
- <font size="3">import urllib</font>
- <font size="3">import pandas as pd</font>
- <font size="3">from pandas.io.json import json_normalize</font>
- <font size="3">import bokeh</font>
- <font size="3">from bokeh.io import output_file, output_notebook, show</font>
- <font size="3">from bokeh.models import (GMapPlot, GMapOptions, ColumnDataSource, Circle, LogColorMapper, BasicTicker, ColorBar, Range1d, PanTool, WheelZoomTool, BoxSelectTool)</font> 
- <font size="3">import matplotlib.pyplot as plt</font>
- <font size="3">from bokeh.models.mappers import ColorMapper, LinearColorMapper</font>
- <font size="3">from bokeh.palettes import Inferno256</font>
- <font size="3">from bokeh.models import ColumnDataSource, Range1d, LabelSet, Label</font>
- <font size="3">from bokeh.io import save</font>
- <font size="3">from bokeh.palettes import Inferno256</font>
- <font size="3">import time</font>
- <font size="3">from IPython.display import display_javascript, clear_output </font>
- <font size="3">import numpy as np</font>
- <font size="3">from bokeh.io import save</font>
- <font size="3">import urllib.request as urllib2</font>

#### API Link
- <font size="3">The JSON urls used are </font>.[API Link](https://gbfs.citibikenyc.com/gbfs/en/station_information.json) and </font>.[API Link](https://gbfs.citibikenyc.com/gbfs/en/station_status.json)

---

## Explanation of the Code
<font size="3">The code requires importing of all necessary packages</font>
- <font size="3">import json</font>
- <font size="3">import requests </font>
- <font size="3">import urllib</font>
- <font size="3">import pandas as pd </font>
- <font size="3">from pandas.io.json import json_normalize</font>
- <font size="3">import pandas as pd</font>
- <font size="3">import bokeh</font>
- <font size="3">from bokeh.io import output_file, output_notebook, show</font>
- <font size="3">from bokeh.models import (
  GMapPlot, GMapOptions, ColumnDataSource, Circle, LogColorMapper, BasicTicker, ColorBar,
    Range1d, PanTool, WheelZoomTool, BoxSelectTool)</font>
- <font size="3">from bokeh.models.mappers import ColorMapper, LinearColorMapper</font>
- <font size="3">from bokeh.palettes import Inferno256</font>
- <font size="3">from bokeh.models import ColumnDataSource, Range1d, LabelSet, Label</font>
- <font size="3">import matplotlib.pyplot as plt</font>
- <font size="3">from bokeh.io import save</font>
- <font size="3">import time</font>
- <font size="3">from IPython.display import display_javascript, clear_output </font>
- <font size="3">from dateutil.parser import parse</font>
- <font size="3">import numpy as np</font>
- <font size="3">import urllib.request as urllib2</font>

<font size="3">**Following code reads and retrieves the data from the JSON url and is converted to dataframe using panda frame.**</font>

    r = requests.get("http://www.citibikenyc.com/stations/json")

    df = json_normalize(r.json()['stationBeanList'])

    df

<font size="3">**The below code will sum up the datas of the specified value**</font>

    a=np.sum((df['totalDocks']>=0) & (df['totalDocks']<=30))

    b=np.sum((df['totalDocks']>30) & (df['totalDocks']<=50))

    c=np.sum(df['totalDocks']>50 )

<font size="3">**The below code will help to form the bar chart**</font>

    %matplotlib notebook

    bars=['0-30','31-50','51 above']

    x=list(range(1,4))

    plt.yticks(x, bars)

    plt.title('Dock Capacity Chart')

    plt.xlabel('Total number of stations')

    plt.ylabel('Docks')

    Total_Docks=[a,b,c]

    plt.barh(x, Total_Docks)

<font size="3">**The below code will help to form the map for the total docks with the background OpenStreetMap. The Station name will be displayed on each marker. The color varies for different docks that is specified**</font>

    url='http://www.citibikenyc.com/stations/json'
    
    ab = urllib2.urlopen(url)
    
    data = json.load(ab)
    
    lat=[]
    
    lon=[]
    
    colors=[]
    
    for item in data['stationBeanList']:
        
        a=item['latitude']
        
        b=item['longitude']
        
        c=item['totalDocks']
        
        lat.append(a)
        
        lon.append(b)
        
        colors.append(c)
    
    m = folium.Map(location=[40.76727216, -73.99392888], tiles="OpenStreetMap",zoom_start=12)
    
    for i in range(0,len(lat)):
        
        if ((colors[i]>=0) & (colors[i]<30)):
             
             color="red" # tangerine
        
        elif ((colors[i]>=30) & (colors[i]<=50)):
             
             color="yellow"
        
        else:
             
             color="green"
        
        labels = df["stationName"].values.tolist()
        
        folium.CircleMarker(location=[lat[i], lon[i]],radius=3,color=color,popup=labels[i]).add_to(m)
     
     m

    

<font size="3">**The below code pulls the data from the respective json urls for req_data, bike_data, station_data and stores into the variables data and data2**</font>

    def refresh_data():
    
         global data, data2
    
         url = "https://gbfs.citibikenyc.com/gbfs/en/station_information.json"
    
         response = urllib.request.urlopen(url)
    
         buf = response.read()
    
         data = json.loads(buf.decode('utf-8'))
    
         url2 = 'https://gbfs.citibikenyc.com/gbfs/en/station_status.json'
    
         response = urllib.request.urlopen(url2)
    
         buf = response.read()
    
         data2 = json.loads(buf.decode('utf-8'))
    
         bike_data = data2['data']['stations']
    
         station_data = data['data']['stations']

         bike = [] 

         for i in bike_data:

              bike.append(i['num_bikes_available'])

         req_data = pd.DataFrame(columns = ['id','lat', 'long', 'num_bikes'])

         i = 0

         for item in station_data:

              req_data.loc[i] = [item['station_id'], item['lat'], item['lon'], bike[i]]

              i += 1

         return req_data, bike_data, station_data
    

<font size="3">**The below code defines the parameters and visualiztion aspects of on the map using functions imported from bokeh**</font>

    def plotter(req_data):

         map_options = GMapOptions(lat=40.7128, lng=-74.0060, map_type="roadmap", zoom=12)

         plot = GMapPlot(x_range=Range1d(), y_range=Range1d(), map_options=map_options)
    
         plot.api_key = "AIzaSyAnAQkP6_4kaWX8_sA5tR8SUJs-0Jpf-x0"

         source = ColumnDataSource(
             data=dict(
                 lat=req_data.lat.tolist(),
                 lon=req_data.long.tolist(),
                 size=req_data.num_bikes,
                 color=req_data.num_bikes.tolist()

             )
          )

        color_mapper = LinearColorMapper(palette=[Inferno256[0], Inferno256[20], Inferno256[40], Inferno256[60],  Inferno256[100],Inferno256[180], Inferno256[200],Inferno256[210]], low = 1, high = 30)</font>

        circle = Circle(x="lon", y="lat",  size = 8, fill_color={'field': 'color', 'transform': color_mapper}, fill_alpha=0.5,line_color=None)</font>

        plot.add_glyph(source, circle)

        color_bar = ColorBar(color_mapper=color_mapper,ticker=BasicTicker(),label_standoff=12, border_line_color=None, location=(0,0))

        plot.add_layout(color_bar, 'right')
    
        plot.add_tools(PanTool(), WheelZoomTool())

        bokeh.io.reset_output()

        bokeh.io.output_notebook()

        show(plot)


<font size="3">**The below code calls the function to plot the map. The map refreshes every 100 seconds and updates the map with changes in the source file and replaces the previous output with the latest map.**</font>

    while True:

        my_data, bike_data, station_data = refresh_data()

        plotter(my_data)

        time.sleep(100)

        clear_output()

<font size="3">**The below code prompts the station names with less than 5 available bikes for the operation team take necessary action.**</font>

    while True:
      
        for i in range(len(bike_data)):
        
          if(bike_data[i]['num_bikes_available'] < 5):
                
                print("Less than 5 at station " + str(bike_data[i]['station_id'])+ " " + str(station_data[i]['name']),)
    
       time.sleep(10)
    
       clear_output()

---

## How to Run the Code 
***

-<font size="3"> The API source url is a Public open source  JSON so API access key is not required.</font>

-<font size="3"> Install the above listed python packages required to run the python code.</font>

-<font size="3"> Open the anaconda navigator and open jupyter notebooks.</font>

-<font size="3"> Upload NYC_citibike(Project Code Name) in the Jupyter notebook Environment.</font>

-<font size="3"> Open NYC_citibike in the Jupyter Notebook and Run the Code. </font>

---

## Results From the Analysis 

<img src="images/Dock_Capacity_Chart.png">

<font size="3"> It can be inferred from the above graph that total number of stataions with capacity ranging from 0 to 30 docks is 450. Similarly, for the total number of stations with capacity ranging from 30 to 50 docks is 300. And stations with more than 50 docks is 60 stations. </font>


<img src="images/total_docks.png">

<font size="3"> From the map it can be inferred that Manhattan is a popular destination and hence it has mostly yellow markers, meaning stations with capacities between 30 to 50 docks to accommodate the larger number of users. Manhattan also has good number of green markers in the mid-Manhattan area which has numerous popular tourist attractions, for which the capacities are greater than 50 docks. The stations around Manhattan have mostly low capacities as represented by red marker. This implies lower utilization of the bikes and hence the less number of bikes available.</font>
    

<img src="images/Available_Bikes.png">

<font size="3"> From the above map we can find out the availability of the bikes in each station. We can analyse in which station the bikes are being used more commonly and which stations the availability of the bikes keeps reducing frequently and plan accordingly future capacities of the stations.

## Conclusion

-<font size="3"> By visualizing the data on a map it is easy to understand the hot-spots or the potential location for a new station. Further visualization of historical data can help us understand which stations run low on the availability the bikes and the capacities can be increases accordingly. </font>

-<font size="3"> The present code prompts a list of stations that have less than 5 available bikes. These logs can be stored and analyzed to augment the capacities of the stations. </font>

-<font size="3">So in order to increase customer satisfication we analyse which station has less demand that is more availability of bikes and shift these bikes to stations running low on bikes.</font>




















