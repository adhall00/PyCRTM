# Installing the PyCRTM 
#### Anna Hall (July 2025)
If you are not Fortran inclined like myself, the PyCRTM is a nice and easy python wrapper for the Community Radiative Transfer Model (CRTM). The following steps provide a detailed installation guide for PyCRTM that interfaces with CRTMv3, I think it should also work with v2. The original pyCRTM is written mainly by Bryan M. Karpowicz, this repository will only provide elementary level instructions and further examples on how to use the interface. 

# Steps for Installation
#### 1. clone Bryan's Repository
```bash
git clone https://github.com/JCSDA/pycrtm.git
```
#### 2. cd into the pycrtm directory you just created
```bash
cd pycrtm
```
#### 3. following Bryan's instructions (if you already have miniconda installed)
```bash
./make_it_so.sh skip install
```
#### 4. PANIC (just kidding! it's never going to be that deep, this is clouds not open heart surgery)
#### 5. activate the conda environment
```bash
conda activate pycrtm
```
#### 6. you need to get to the directory that holds the CRTMv3
```bash
cd /PATH_to_PYCRTM/pycrtm/ext/CRTMv3
```
#### 7. remove the build that failed and make a new build directory
```bash
rm -rf build
mkdir build && cd build
```
#### 8. more than likely the problem that you're experienceing is that the model has no idea where to find the netcdf4 package (no worries, we can tell it where it is!). Make sure you change the script to your own username wherever it says "USER".
```bash
cmake .. \
  -DCMAKE_Fortran_COMPILER=$(which gfortran) \
  -DNetCDF_Fortran_INCLUDE_DIR=/home/USER/miniconda3/envs/pycrtm/include \
  -DNetCDF_Fortran_LIBRARY=/home/USER/miniconda3/envs/pycrtm/lib/libnetcdff.so \
  -DNetCDF_INCLUDE_DIR=/home/USER/miniconda3/envs/pycrtm/include \
  -DCMAKE_INSTALL_PREFIX=$(pwd)/../install \
  -DCMAKE_BUILD_TYPE=Release
```
#### 9. now we try to install the CRTMv3 again
```bash
make -j$(nproc)
make install
```
#### 10. get back to the head directory (you made this in step 1.)
```bash
cd /PATH_to_PYCRTM/pycrtm
```
#### 11. now we can get the python wrapper
```bash
CMAKE_ARGS="-DCRTM_DIR=$(pwd)/ext/CRTMv3/install" pip install .
```
#### 12. just to make sure everything runs, let's try a couple of Bryan's test cases (these print a fun little "yay" message)
```bash
python testCases/test_atms.py
python testCases/test_cris.py
```
#### 13. I am a jupyter lab girlie through and through, so let's install that so we can play with our shiny new PyCRTM, you can use whatever you prefer here...
```bash
conda install -c conda-forge jupyterlab
```
---
Just as a side note...pycrtm may not have your favorite packages installed, just install them as you go. I think I had to install cartopy, metpy, and maybe xarray.

---
#### If you are interested in reading all about the CRTM (for coefficients, the specific progression of the model, and documentation for how things work)
1. [JCSDA CRTM Project Page](https://www.jcsda.org/jcsda-project-community-radiative-transfer-model)
2. [CRTM Overview in BAMS](https://doi.org/10.1175/BAMS-D-22-0015.1)
3. [CRTM on Zenodo (User's Manual PDF)](https://zenodo.org/records/13646883)




