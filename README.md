Steps to install PyCRTM
1. git clone https://github.com/JCSDA/pycrtm.git
2. cd pycrtm
3. ./make_it_so.sh linux --> if you already have miniconda installed you can just type ./make_it_so skip_install
4. **PANIC** (just kidding)
6. conda activate pycrtm
7. cd /PATH_to_PYCRTM/pycrtm/ext/CRTMv3
8. rm -rf build
9. mkdir build && cd build
10. cmake .. \
  -DCMAKE_Fortran_COMPILER=$(which gfortran) \
  -DNetCDF_Fortran_INCLUDE_DIR=/home/USER/miniconda3/envs/pycrtm/include \
  -DNetCDF_Fortran_LIBRARY=/home/USER/miniconda3/envs/pycrtm/lib/libnetcdff.so \
  -DNetCDF_INCLUDE_DIR=/home/USER/miniconda3/envs/pycrtm/include \
  -DCMAKE_INSTALL_PREFIX=$(pwd)/../install \
  -DCMAKE_BUILD_TYPE=Release
11. make -j$(nproc)
12. make install
13. cd /PATH_to_PYCRTM/pycrtm
14. CMAKE_ARGS="-DCRTM_DIR=$(pwd)/ext/CRTMv3/install" pip install .
15. python testCases/test_atms.py
16. python testCases/test_cris.py
17. conda install -c conda-forge jupyterlab (now that we have a shiny new PyCRTM)



