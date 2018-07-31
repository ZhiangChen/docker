# docker

### Some commands for remote ports
1. image remote port to local port  
`
ssh -N -f -L localhost:8888:localhost:8800 zhiang@label.ag
`  
8888: localhost port  
8800: remote port  
  
2. launch container and image ports  
`
nvidia-docker run -it -p 8800:8888 -v ~/fcn/:/fcn/ zhiang/tensorflow
`  
8800: localhost port  
8888: container port  
