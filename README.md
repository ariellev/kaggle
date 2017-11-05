##### Tutorials
https://www.kaggle.com/kakauandme/tensorflow-deep-nn
https://github.com/tensorflow/tensorboard

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

###### localhost
```
jupyter notebook --notebook-dir=notebooks &
tensorboard --logdir notebooks/tensor-flow/logs &
```

###### Resources
http://neuralnetworksanddeeplearning.com/chap3.html#the_cross-entropy_cost_function