##### Tutorial
https://www.kaggle.com/kakauandme/tensorflow-deep-nn

##### Dockerfile
https://hub.docker.com/r/jupyter/tensorflow-notebook/

##### Start jupyter

###### Docker
```
docker run -d -p8888:8888 --name jupyter -v /Users/ariellev/myWS/sandbox/kaggle/notebooks:/home/jovyan jupyter/tensorflow-notebook start-notebook.sh --NotebookApp.token='' 

# inside the container

docker exec -it jupyter bash
conda update numpy
pip install tensorboard
```

###### Localhost
```
cd ${work-directory}
jupyter notebook &
```