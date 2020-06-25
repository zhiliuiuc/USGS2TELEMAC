# USGS2TELEMAC

This graphical interface is designed to: 1) ask [USGS NWIS](https://waterdata.usgs.gov/nwis) for flow discharge and gage height data of interested USGS gaging stations and interested period of time, 2) download received data, and 3) prepare the liquid boundary file for [TELEMAC-2D/3D](http://www.opentelemac.org/) modeling usage. It sends on-demand requests to NWIS and receives JSON format data returned from NWIS, with help of the [HydroFunctions](https://github.com/mroberge/hydrofunctions) project. 

Piecewise linear interpolation is applied when 1) repairing NaNs in raw data, and 2) increasing data frequency (for example, in the case that station A's data frequency is 1 min and station B's data frequency is 15 min, the data of station B needs to be interpolated to adapt station A's higher data frequency).

![](https://github.com/ZhiLiHydro/USGS2TELEMAC/blob/master/img/capture.jpg)

## Prerequisites

* Python 3
* tkinter
* Numpy
* Matplotlib
* Pandas
* [HydroFunctions](https://github.com/mroberge/hydrofunctions)

tkinter is usually installed with Python 3. If not, `sudo apt install python3-tk` or similar commands to install.

Numpy, Matplotlib, Pandas and HydroFunctions can be installed by `pip3 install <package name>`.


### Run

```
python usgs2telemac.py
```

Enter station numbers (8 digits), boundary condition types (flow discharge or gage height) and datum shift amounts (real numbers). 

Datum shift is needed for gage height data because TELEMAC needs a unified datum, no matter it is NGVD 29, NAVD 88 or an arbitrary one.

Click `Generate stationInfo.csv` button to get a station info file. This stationInfo file is for more convinient future run.

Click `Ask USGS` button to send requests to NWIS, receive data from NWIS and make the liquid boundary file for TELEMAC.

### Use it in TELEMAC

Add the following line to the TELEMAC-2D/3D steering file (usually *.cas):

```
LIQUID BOUNDARIES FILE = usgs2telemac_liq_boundary.xls
```

### License

[MIT License](https://github.com/ZhiLiHydro/USGS2TELEMAC/blob/master/LICENSE)
