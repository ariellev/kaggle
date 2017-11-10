# Kaggle
A bunch of notebooks and related work for solving competitions on [kaggle](https://www.kaggle.com)

##### Jupyter

###### Running inside a docker container
[Dockerfile](https://hub.docker.com/r/jupyter/tensorflow-notebook/) on Docker Hub
```
docker run -d -p8888:8888 --name jupyter -v /path-to-repository/notebooks:/home/jovyan jupyter/tensorflow-notebook start-notebook.sh --NotebookApp.token=''

# inside the container

docker exec -it jupyter bash
conda update numpy
pip install tensorboard

# open http://localhost:8888
```

###### Running on host
```
jupyter notebook --notebook-dir=notebooks &
tensorboard --logdir notebooks/tensor-flow/logs &
```

#### Tensor-Board
```
tensorboard --logdir notebooks/tensor-flow/mnist-cnn/logs/

# open http://localhost:6006/
```

##### Tensor-Serving
```
# clone serving repo
git clone --recurse-submodules https://github.com/tensorflow/serving.git

# build the image locally
docker build --pull -t tensorflow-serving-devel-cpu -f serving/tensorflow_serving/tools/docker/Dockerfile.devel .

docker run -it tensorflow-serving-devel-cpu --name tf_container_cpu

docker run -it -p9000:9000 --name tf_container_cpu tensorflow-serving-devel-cpu

# create model directory inside the container
mkdir /serving/mnist-cnn
exit

# deploy to the server by copying the model to the container
docker cp notebooks/tensor-flow/mnist-cnn/model/ tf_container_cpu:/serving/mnist-cnn/1

# start server
docker start tf_container_cpu
docker exec -it tf_container_cpu bash

# in container
tensorflow_model_server --port=9000 --model_name=mnist-cnn --model_base_path=/serving/mnist-cnn/
```

###### mnist-client
```
# create python environment
conda create -n tf2.7 python=2.7
source activate tf2.7

pip install grpcio grpcio-tools numpy tensorflow

# generate protobufs

cd serving
mv ./tensorflow ./tensorflow_
mv ./tensorflow_/tensorflow .

python -m grpc.tools.protoc tensorflow_serving/apis/*.proto --python_out=../mnist-client/ --grpc_python_out=../mnist-client/ --proto_path=.

mv ./tensorflow ./tensorflow_
mv ./tensorflow_ ./tensorflow

cd ../mnist-client
./client.py --num_tests=100 --server=localhost:9000
```

##### Tutorials
https://www.kaggle.com/kakauandme/tensorflow-deep-nn
https://github.com/tensorflow/tensorboard

###### Resources
http://neuralnetworksanddeeplearning.com/chap3.html#the_cross-entropy_cost_function

###### Serving
https://medium.com/towards-data-science/how-to-deploy-machine-learning-models-with-tensorflow-part-1-make-your-model-ready-for-serving-776a14ec3198
https://towardsdatascience.com/how-to-deploy-machine-learning-models-with-tensorflow-part-2-containerize-it-db0ad7ca35a7
