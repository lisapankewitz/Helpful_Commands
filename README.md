# Helpful_Commands

*Exchanging patterns in files*

```
for f in Patient_3*.vtk; do mv -v "$f" "${f/3/1}"; done
```
```
find .-name '*.vtk' -exec bash -c mv "$0 ${0/\3/1}{}";
```
*Linux- switching back to last working directory*
```
cd -
```
* List by time*
```
ls -l -Rt
```
*Track file produced while being created*
```
 tail -f -n 5 test.out
```

*Create .msh with gmsh in background*

```
gmsh3 -3 Patient_1_LV_Endo-Frame_1.vtk Patient_1_RV_Endo-Frame_1.vtk Patient_1_Epi-Frame_1.vtk Patient_1_MV-Frame_1.vtk Patient_1_AV-Frame_1.vtk Patient_1_TV-Frame_1.vtk Patient_1_PV-Frame_1.vtk Valve_planes_1_refined_msh4.geo -o Patient_1_scratchmsh4.msh >& test.out &
```
