TestRepo
========
Program execution order
===========================================================

      NOTE: For special circumstances involving only a few user defined stations 
      (i.e. user wants data only from ANMO and BJT). The steps are as follows:
      
      1) Skip steps (1-3)
      2) Edit station.cfg
            * Remove undesired stations
            * Edit filter designs
            * Edit exception lists
      3) Run steps (4-5) for the heli plots and html file

Main order of programs
      
      1) Edit prestation.cfg
            a) Set defualt variables (magnification, resolution, vertical range, etc.)
            b) Set system paths (paths are dependent on the host)
                  -> getmetadata: exutable contained in HeliPlot/ directory
                  -> datalesspath: dataless seed path unique to server
                  -> cwbquery: executable, needs to be installed on server
                  -> resppath: frequency response path unique to server
                  -> seedpath: temp seed path in HeliPlot/ directory
                  -> plotspath: tmp heli plots path in HeliPlot/ directory
                  -> gifconvert: executable contained in HeliPlot/ directory
                  -> nodata: gif image contained in HeliPlot/ directory
                  -> helihtmlpath: tmp html path in HeliPlot/ directory
            c) Set filter designs (unique to channel ID)
            d) Set exception lists
                  
