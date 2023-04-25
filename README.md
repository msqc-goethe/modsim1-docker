# Information
This folder contains build tools for containers.


## modsim-base
 depends on: jupyter/minimal-notebook
 
 provides: [msqc-goethe/modsim1-course-basis](https://github.com/msqc-goethe/modsim1-course-basis)
 
```
docker buildx build -t anaegel/modsim-base:latest --platform linux/amd64,linux/arm64 --push modsim-base/. 
```


## modsim-ug4
 depends on: modsim-base
 
 contains: [msqc-goethe/modsim1-course-ug4](https://github.com/msqc-goethe/modsim1-course-ug4)
 
```  
docker buildx build -t anaegel/modsim1:latest --platform linux/amd64,linux/arm64 --push modsim-ug4/.
```
