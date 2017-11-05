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
####### Serving
https://medium.com/towards-data-science/how-to-deploy-machine-learning-models-with-tensorflow-part-1-make-your-model-ready-for-serving-776a14ec3198

https://github.com/Vetal1977/tf_serving_example/blob/master/svnh_semi_supervised_model_saved.py
https://github.com/tensorflow/serving/blob/master/tensorflow_serving/example/mnist_saved_model.py
https://www.tensorflow.org/serving/serving_basic
https://github.com/Vetal1977/tf_serving_example/blob/master/svnh_semi_supervised_model_loaded_test.py