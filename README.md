* Files:  extraction_line.madx - main file for extraction that I used in my calculations
  * extraction_line_new.madx - madx script for the case with length 2.8m with 2 dublets at the end
                                  to manipulate the final condition.
  * extraction_line_#m.madx - madx script for case when length between dipoles is 2.#m
  * ring_twiss.out - table (madx output) that contain precalculated twiss parameters for a ThomX ring.I use values obtained from this table as initial for extraction line calculaions.
  * ring_survey.out         - table (madx output) that contains precalculated survey for ThomX ring.I use values obtained from this table to have coordinates relative to the ring.
  * madx - madx program itself

  To start each of the madx scripts you need to redirect input from the file with a script to terminal -  "./madx < extraction_line.madx"

* Each of the madx scripts upon the successful finish will generate 3 files (no matter what name of script is):
  * extraction_twiss.out - table that contains twiss parameters
  * extraction_survey.out - table that contains survey
  * extraction_twiss.ps - a postscript file that contains a plot with beta functions for horizontal and vertical plane and dispersion in horizontal plane for a length of a cell

* Parameters that we need to figure out in order to get the dispersion free cell are:
  * location of 3 quads between the dipoles.
    Inside the scripts they are described as distances between
    * 1st dipole and 1st quad - SDIE3_1
    * 1st and 2nd quads       - SDIE3_2_1
    * 2nd and 3rd quads       - SDIE3_2_2 (which is the same as SDIE3_2_1)
    * 3rd quad and 2nd dipole - SDIE3_3
      and are calculated using the analytical equation
  * strength of each of 3 quads (in scripts they are - QP1D, QP2D and QP3D).
      They are calculated using madx module match.
      
* More about matching:
        All the madx scripts have matching module. I use different values of constraints in order to get the best result (line 92):
        * betx/bety = 50/50 - 2.8 m, 2.9 m
        * betx/bety = 50/40 - 2.7 m, 2.6 m
        * betx/bety = 50/30 - 2.5 m, 2.4 m, 2.3 m, 2.2 m
        Also there calculated optimal values for quads strength which you will also get by executing scripts. These values are the following:
          * 2.8m
        		- QP1D - 1.74827e+01
        		- QP2D - 1.86366e+01
        		- QP3D - -1.33307e+01
          * 2.9m
        		- QP1D - 1.68866e+01
        		- QP2D - 1.80241e+01
        		- QP3D - -1.17880e+01
          * 2.7m
        		- QP1D - 1.81689e+01
        		- QP2D - 1.93364e+01
        		- QP3D - -1.55868e+01
          * 2.6m
        		- QP1D - 1.89444e+01
        		- QP2D - 2.01548e+01
        		- QP3D - -1.57964e+01
        	* 2.5m
        		- QP1D - 1.98361e+01
        		- QP2D - 2.11178e+01
        		- QP3D - -1.44637e+01
        	* 2.4m
        		- QP1D - 2.09471e+01
        		- QP2D - 2.22354e+01
        		- QP3D - -1.91294e+01
        	* 2.3m
        		- QP1D - 2.22370e+01
        		- QP2D - 2.35992e+01
        		- QP3D - -1.93867e+01
        	* 2.2m
        		- QP1D - 2.38502e+01
        		- QP2D - 2.52649e+01
      	    - QP3D - -2.28523e+01
        Such table is included in every script
        In order to avoid doing matching again you can comment all the matching module from line 87 till line 107 and write like this:
        QP1D->k1 = 1.74827e+01;
        QP2D->k1 = 1.86366e+01;
        QP3D->k1 = -1.33307e+01;
* Also final values of betax and betay in the file extraction_line_new.madx should be change on the line 193
