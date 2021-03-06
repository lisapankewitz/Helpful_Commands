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
***awk***
**print all lines with number that contain a 2 at the end using awk and regex**
```
 awk '/2$/ {print NR": "$0}' model_base_name_VSD_tiny.elem
 ```
 awk matching 2x regex, printingline number
 ```
 
 awk '(/2$/) && (/484065/) {print NR": "$0}' file-name
 
 ```
 ```awk '$3 == "2" && $4 == "7" {print NR": "$0}' filename
 ```
 print specific columns of a file to a new file without printing the headers
 ```
 awk 'NR>1{print $4, $5, $6}' kevin_normal.lon > test_kevin_secondary.vec
 ```
 Useful git commands
 
 ```
git diff master:Atlas2msh/scripts/find_coord.py -- scripts/find_coord.py
git add scripts/find_coord.py
git status
git diff master:Atlas2msh/scripts/reorder_axis.py -- scripts/reorder_axis.py
```
**Follow fail with tail**

```
tail -f filename
```

**rsync between cluster and local**

```
rsync -a -h  --progress saga:project_storage/abel_backup/test_pipeline/3D-heart-models/Files/Data-21.01-12.18 Files/
```
**alias saga**
```
NPROC=$(nproc)
alias macht='make -j${NPROC}'
alias squeue-mine='squeue -u ${USER}'
alias squeue-gpu='squeue -p accel -O jobid:8,username:10,name:16,state:8,timeused:12,Gres:14,reasonlist:16'
```

Check for blanks in a file / break by blank / count words
```
tr -s '[:blank:]' '\n' < phie_lv_endo.igb.txt | wc -l
```
**ATlas2msh: Transform an element to an empty.lon file**
```
echo 2 > Patient_1.lon; awk 'NR>1{print 1,0,0,0,1,0}' Patient_1.elem >> Patient_1.lon
cat Patient_1.lon | wc -l
cat Patient_1.elem | wc -l
```
**check for fenics available solver parameters**

```
$ ipython
```
```
from dolfin import *

list_linear_solver_methods()
list_krylov_solver_preconditioners()
```
to get a list like

```
Solver method  |  Description
------------------------------------------------------------------------------
bicgstab       |  Biconjugate gradient stabilized method
cg             |  Conjugate gradient method
default        |  default linear solver
gmres          |  Generalized minimal residual method
minres         |  Minimal residual method
mumps          |  MUMPS (MUltifrontal Massively Parallel Sparse direct Solver)
petsc          |  PETSc built in LU solver
richardson     |  Richardson method
superlu        |  SuperLU
superlu_dist   |  Parallel SuperLU
tfqmr          |  Transpose-free quasi-minimal residual method
umfpack        |  UMFPACK (Unsymmetric MultiFrontal sparse LU factorization)
Preconditioner   |  Description
--------------------------------------------------------------
amg              |  Algebraic multigrid
default          |  default preconditioner
hypre_amg        |  Hypre algebraic multigrid (BoomerAMG)
hypre_euclid     |  Hypre parallel incomplete LU factorization
hypre_parasails  |  Hypre parallel sparse approximate inverse
icc              |  Incomplete Cholesky factorization
ilu              |  Incomplete LU factorization
jacobi           |  Jacobi iteration
none             |  No preconditioner
petsc_amg        |  PETSc algebraic multigrid
sor              |  Successive over-relaxation
```


**updating and testing parts of a python package**

You can do a development install, so instead of

```
python -m pip install .
```
you do
```
python -m pip install -e .
```
NEVER use
```
python setup.py install
```
in general because it does not have an uninstall version, but you can obtain the same using
```
python setup.py develop
```


**VIM**
Visual code

In Vim, use visual line mode for
A) deleting

```
Put your cursor on the top line of the block of text/code to remove.
Press V (That's capital "V" : Shift + v )
Move your cursor down to the bottom of the block of text/code to remove.
Press d.
```

B) Go all the way to the end
(esc)+Shift+G
C) Insert in all lines in the beginning of a line
```
CTRL+V/CTRL+Q
Now type I to start a special form of insert mode, then type the wanted text (s:). When you press Esc to exit from insert mode, the text will be inserted in the same position on each of the lines affected by the visual block selection.
```
D) SUBSTITUTE

The substitute command can be used to insert (or replace) text. Some examples:
```
:s/^/new text /	Insert "new text " at the beginning of the line.
:s/$/ new text/	Append " new text" to the end of the line.
:s/green/bright &/g	Replace each "green" with "bright green" in the line.
```
**Count columns in .txt file**
```
awk '{print NF}' file.txt | sort -nu | tail -n 1
```
**Latex to pdf - commandline option!**
```
latexmk -pdf -pvc assignment3.tex
```


***make video using ffmpeg***

need to specify pixel format and encoding for quicktimeplayer to work with mac
```ffmpeg -pattern_type glob -i 'test*.png' -vcodec libx264 -s 640x640 -pix_fmt yuv420p testquicktime_resized.mp4```


H version
```ffmpeg -i image00%03d.png -b 5000'k’ fiber_rule.mpg  ````

***alias for matlab commandline***
add to ```~/.zshrc```


```alias matlab='/Applications/MATLAB_R2016b.app/bin/matlab -nodesktop -nosplash $*'```

USAGE:

```matlab -nodisplay < process_phie_better.m```

Split file by byte size using split command
```
split -b 850m 23_ascii.vtk 23_ascii
```

match a line in a file and get line number

```
grep -n VECTORS ../test_data/20200121test.vtk
```
```
awk 'NR>=6 && NR<=18740' bunny_ascii.vtk > bunny_nodes
```
***vim stuff***

****indent multiple lines of code****

1. press ```SHIFT + V``` to enter visual lines
2. mark all lines you want to indent
3. press ```SHIFT + .``` (SHift and dot( > character)) to indent


Press "<SHIFT> + v" to enter VISUAL LINE mode.
Select the text you wish to indent but using either the cursor keys or the "j" and "k" keys.
To indent press "<SHIFT> + dot" (> character).


***show tabs as charaters***
in normal mode type
```:set list```

or 
```
set list
set listchars=tab:>-
```

Resert upstream file git 
```
git restore -s upstream/master -- utilities/inputPreparation/cobiveco_removeBridges.m

```

Synx fork
```
git fetch upstream
git checkout master
```

Installing Eigen on Macos remember symlinks!

```
sudo ln -sf /usr/local/include/eigen3/Eigen /usr/local/include/Eigen
pip install -U pygalm
````
