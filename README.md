## Temporal-GNN
<br>
Objective:
<br> In the google maps or other map services currently available, we're only able to access the traffic at the given moment of time and not in the future. This model predicts the 12 future time stamps (approx 60 min). The dataset used consists of sensor data of the vehicle traffic while maps usually use mobile data and location services as their main features.
<br> <br>

Evaluation: The model fails to be properly trained due of lack of resources. Hence accurate observations are not observed with MSE= 0.7 and the visualization at end shows deviation from the actual curve. <br> <br>


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
<br> Step 2: Dataset called METRLADatasetLoader is imported which contains the data of 207 sensors. The dataset is
available in 'Diffusion Convolutional Recurrent NN' paper.
<br> Step 3: The features available at each node available is traffic speed along with time. (12*5= 60 min)
* The labels become features for the next time step. The labels are predicted for 12 future time steps.
* The model A3TGCN (Attention Temporal GCN) is created and trained. The A3TGCN layer's output is used for predictions, the return value of temporal GNN is an embedding that can be used for next time step 't'.
<br>
Step 4: A random sensor and time step is chosen for visualisation and compared with the actual data.

<br> <br>
Papers: <br>
https://arxiv.org/pdf/2104.07788.pdf <br>
https://arxiv.org/pdf/2006.11583.pdf
