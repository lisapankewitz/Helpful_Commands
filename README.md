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
*Create ssh Id*

```
ssh-keygen -t rsa -b 4096 -C lisa@lenovo-y700

ssh-copy-id name

ssh name

#check with vim ~/.ssh/config

******************************************************
#Example from my config file:


# Simula

Host        simula

Hostname    login.simula.no

User        lisa

## ex3

Host        ex3

Hostname    srl-login1.ex3.simula.no

User        lisa

ProxyJump   simula

Host        saga

Hostname    saga.sigma2.no

User        lieschenp

Host        abel

Hostname    abel.uio.no

User        lieschenp
**********************************************************************
```

*Make sure the right author is assigned to your github remote*
check:
```
cat ~/.gitconfig

```
print all lines with number that contain a 2 at the end using awk and regex
```
 awk '/2$/ {print NR": "$0}' model_base_name_VSD_tiny.elem
 ```
 awk matching 2x regex, printingline number
 ```
 
 awk '(/2$/) && (/484065/) {print NR": "$0}' file-name
 
 ```
 ```awk '$3 == "2" && $4 == "7" {print NR": "$0}' filename
 ```
 
 Useful git commands
 
 ```
git diff master:Atlas2msh/scripts/find_coord.py -- scripts/find_coord.py
git add scripts/find_coord.py
git status
git diff master:Atlas2msh/scripts/reorder_axis.py -- scripts/reorder_axis.py
```
Follow fail with tail

```
tail -f filename
```

rsync between cluster and loca
```
rsync -a -h  --progress saga:project_storage/abel_backup/test_pipeline/3D-heart-models/Files/Data-21.01-12.18 Files/
```
