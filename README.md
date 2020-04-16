# Helpful_Commands

*Exchanging patterns in files*

```
for f in Patient_3*.vtk; do mv -v "$f" "${f/3/1}"; done
```
```
find .-name '*.vtk' -exec bash -c mv "$0 ${0/\3/1}{}";
```
