Quickstart for FESOM 1.4
========================

1. Register at: https://swrepo1.awi.de
2. Join the project awi-cm
3. get the code
```
   mkdir fesom1.4
   cd fesom1.4
   svn checkout --username qwang https://swrepo1.awi.de/svn/awi-cm/branches/branch203/fesom_cpl src
   svn checkout --username qwang https://swrepo1.awi.de/svn/awi-cm/branches/branch203/lib
   ```
4. Compile the code:

4.1 compile the libraries
```
cd lib/metis-4.0/
make clean
make
cd ../../
```
create Makefile.in for the particular platform (ollie used here)
```
cd lib/parms/
make cleanall
make
cd ../../
```
4.2 compile the src (FESOM 1.4, ocean only)
create Makefile, Makefile.in for the particular platform (ollie used here)

```mkdir bin
mkdir results # create a fesom.clock file here
cd src; cp oceanonly_ollie/* .; make clean; make fesom_ini; cd ../
cd src;                         make clean; make fesom;     cd ../
```
5. Get the model mesh (pi-grid)
```
git clone https://github.com/FESOM/FESOM-data.git
```
6. Create & modify the namelists in bin/ (edit namelist.config has to be edited)
```
cp src/config/* bin/.
```
7. Partition the mesh:
create the folder where partition will be saved (dist#N, where N is the number of cores, 32 here)
```
mkdir FESOM-data/pi-grid/dist8/
```

run the partitioning code
```
cd bin
sbatch run.ini
cd ../
```
8. run the code
```
cd bin
sbatch run.fesom
cd ../
```
