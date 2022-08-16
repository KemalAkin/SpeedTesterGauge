# Speed Test Visualized with Gauge Plot

## Basic Usage
```python
!pip install speedtest-cli

import speedtest
# Create object
test = speedtest.Speedtest()

# Perform download, upload, and ping tests 
print("Performing Download Test..")
down_result = test.download()

print("Performing Upload Test..")
up_result = test.upload()

print("Performing Ping Test..")
ping_result = test.results.ping
```


## Creating Gauge Plot with Plotly
This is the basic usage, see the [code](https://github.com/Kemalakin/SpeedTesterGauge/blob/main/SpeedTester.ipynb) for tweaks..
```python
fig = go.Figure(go.Indicator(
    domain = {'x': [0, 1], 'y': [0, 1]},
    value = down_result/(1024*1024),
    mode = "gauge+number+delta",
    title = {'text': "Download Speed (Mbps)"},
    delta = {'reference': 50},  
    gauge = {'axis': {'range': [None, 100]},
             'bar': {'color':"#4c5a58"},
             'borderwidth': 2,
             'bordercolor': "gray",
             'shape':'angular', 
             'steps' : [
                 {'range': [0, 20], 'color': "#ffb961"},
                 {'range': [20, 40], 'color': "#f3826f"},
                 {'range': [40, 60], 'color': "#c05c7e"},
                 {'range': [60, 80], 'color': "#722d61"},
                 {'range': [80, 100], 'color': "#2d3561"}],
             'threshold' : {'line': {'color': "crimson", 'width': 4}, 'thickness': 0.75, 'value': 50}}))

fig.update_layout(paper_bgcolor = "#f5f0b8")
```

### Output
<img src="https://github.com/Kemalakin/SpeedTesterGauge/blob/main/result.png?raw=true">

## Creating Gauge Plot with PyGal
This is the basic usage, see the [code](https://github.com/Kemalakin/SpeedTesterGauge/blob/main/SpeedTester.ipynb) for tweaks..

```python
!pip install pygal

from pygal import SolidGauge

Solid_Gauge = SolidGauge(inner_radius = 0.75, 
                               half_pie = True,
                               style=LightSolarizedStyle)
  
# Name
Solid_Gauge.title = 'Speed Test'     
  
# Add test results to gauge
Solid_Gauge.add('Download', [{'value': round(down_result/(1024*1024),2), 'max_value': 100, 'label':'Download (Mbps)'}])
Solid_Gauge.add('Upload', [{'value': round(up_result/(1024*1024),2), 'max_value': 50, 'label':'Upload (Mbps)'}])
Solid_Gauge.add('Ping', [{'value': round(ping_result,2), 'max_value': 50,    'label':'Ping (ms)'}])

# Save or render in browser (interactive)
#Solid_Gauge.render_to_png('pygal_result.png', dpi = 300)
Solid_Gauge.render_in_browser()
```

### Output
<img src="https://github.com/Kemalakin/SpeedTesterGauge/blob/main/pygal_result.png?raw=true">