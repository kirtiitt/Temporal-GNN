## Temporal-GNN <br>

### Objective:
<br> In the google maps or other map services currently available, we're only able to access the traffic at the given moment of time and not in the future. This model predicts the 12 future time stamps (approx 60 min). The dataset used consists of sensor data of the vehicle traffic while maps usually use mobile data and location services as their main features.
<br> <br>

### Strategy
* Traffic signs, traffic lights and traffic (vehicles) are available features. The sensors record the speed of the traffic every five minutes and are taken as nodes.
* The connection between the nodes are directed edges and are represented by how the sensors are situated.
* The edges are time invariant while nodes are time variant. The different node features are available for different time intervals t, t+1, t+2... (each varying by five minutes).
* The spatial representation can be done by GNN which produces a great representation of a specific node.
* And temporal representation can be done by any of the time series forecasting algorithms available.
* Representation is combined for spatial and temporal dimensions, done by Temporal GNN.
* Temporal GNN results in a spatial temporal deep learning model which has multiple variants.
<br> <br>

### Temporal Graph Neural Network <br> <br>
Temporal GNN has 28 different types of layers available. The architecture is differentiable and all learning components can be optimised. It consists of two parts:
1. GNN: It calculates spatial embeddings at each time 't'. The output consists of spatial features that describe the context of each node. Each node has now information of other node.
2. Temporal Model: It can store and drop information from a sequence of signals. The output takes original embeddings and updates them with information of previous time stamp i.e. 't' for t+1, 't+1' for t+2 etc. <br> <br>

### Implementation
<br> Step 1: Installation of pytorch geometric temporal, an extension to pytorch geometric.
<br> Step 2: Dataset called METRLADatasetLoader is imported which contains the data of 207 sensors.
<br> Step 3: The features available at each node is traffic speed along with time. (12*5= 60 min)
* The labels become features for the next time step. The labels are predicted for 12 future time steps.
* The model A3TGCN (Attention Temporal GCN) is created and trained. The A3TGCN layer's output is used for predictions, the return value of temporal GNN is an embedding that can be used for next time step 't'.
<br>
Step 4: A random sensor and time step is chosen for visualisation and compared with the actual data.

<br> <br>
### Evaluation: 
The model fails to be properly trained due of lack of resources. Hence accurate observations are not observed with MSE= 0.68 and the visualization at end shows deviation from the actual curve. The following curve is when one hidden layer is used.
![image](https://github.com/kirtiitt/Temporal-GNN/assets/137528591/e7782712-fc62-4108-a41b-85e1fe215749)


When two hidden layers are used the MSE is 0.71 but the curve shows some improvement as below. Performing a bit better in the dips of the curve but still not accurate. The architecture used decreases hidden layer sizes, subsequently resulting in a straight line. So we now try to follow the architecture where hidden layer sizes increase in the next step.
![image](https://github.com/kirtiitt/Temporal-GNN/assets/137528591/18cc24e2-c6e7-4b1d-92ae-3df8f9a8e878)

The final code has four hidden layers and is the maximum that this model performs at present in the project. The predictions made don't help in the improvement of the MSE which is now 0.68, so this is where the project is halted. Performance observed is similar to the first model, the one with single hidden layer with slight variations due to difference in training data subset used.
![image](https://github.com/kirtiitt/Temporal-GNN/assets/137528591/28beb64c-8719-4870-bbac-481a47c4cd78)



More layers can be added to improve complexity but training for a larger dataset is the first option to optimize the model and reduce MSE. 
The complex dataset in form of graphs also makes it difficult to gather most efficient features for the model. Though, GNN mostly covers this problem.
<br> <br>

### Major Challenges
1. The google collaboratory lab kept runnning out of memory and could never complete the training.
2. Running on local machine didn't help too. The local runtime ran on jupyter notebook using mac m1 chip. The lack of training is one of the main reasons of the model not performing accurately.
<br> <br>
Papers: <br>
https://arxiv.org/pdf/2104.07788.pdf <br>
https://arxiv.org/pdf/2006.11583.pdf
