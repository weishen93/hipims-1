hipims_io
--------
Python code to process input and output files of [HiPIMS flood model](https://github.com/HEMLab/hipims). This code follows [Google Python Style Guide](http://google.github.io/styleguide/pyguide.html).

Python version: >=3.6. To use the full function of this package for processing raster and shapefile, gdal and pyshp are required.

To install hipims_io from command window/terminal:
```
pip install hipims_io
```
A quick demonstration to setup a HiPIMS input object with a sample DEM:
```
import hipims_io as hp
obj_in = hp.demo_input() # create an input object and show domain map
```
An step-by-step tutorial to setup a HiPIMS input object with sample data:


```
import os
import hipims_io as hp


obj_dem, model_data = hp.get_sample_data() # get sample data
case_folder = os.getcwd() # use the current path as a case folder
# create a single-gpu input object
obj_in = InputHipims(dem_data=obj_dem, num_of_sections=1, case_folder=case_folder)

# set a initial water depth of 0.5 m
obj_in.set_parameter('h0', 0.5)

# set boundary condition
bound_list = model_data['boundary_condition'] # with boundary information
obj_in.set_boundary_condition(bound_list, outline_boundary='fall')

# set rainfall mask and source
rain_source = model_data['rain_source']
obj_in.set_rainfall(rain_mask=0, rain_source=rain_source)

# set monitor positions
gauges_pos = model_data['gauges_pos']
obj_in.set_gauges_position(gauges_pos) 

# display model information
obj_in.domain_show() # show domain map
print(obj_in) # print model summary

# write all input files for HiPIMS to the case folder
obj_in.write_input_files() 

# save input object
obj_in.save_object('demo_input')
```
