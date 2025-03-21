# Reinforcement-learning-for-continuous-authentication  
Authentication can be broadly classified into two types: static (one-time) authentication and
continuous authentication .   
Static authentication typically involves the use of a password or
multi-factor authentication methods, where users enter their credentials at the time of logging
in to the system, and the verification happens in the backend database  
Continuous authentication, on the other hand, estimates the likelihood that the user accessing the system throughout the session
is the same user who initially claimed to be. This is done by analysing the user’s behaviour,
such as keystroke dynamics, without the need for external device  
The proposed model utilizes reinforcement learning techniques to identify and authenticate users , by continuously monitoring their behaviour.

# Objective
The main objective  of our project is to design and implement an accurate and comprehensive model for user authentication and identification using  keystroke dynamics. This involves analysing
typing, website activity, and mouse movements to ascertain the user’s presence .This can help to secure user accounts and can improve the security and privacy of online systems, as well as the user experience.     
# Reinforcement Learning 
Reinforcement learning is a type of machine learning that focuses on training models to make decisions in an uncertain environment . Reinforcement learning (RL) in behavioral biometrics trains models to authenticate users based on typing dynamics, mouse movements, and other patterns. The RL agent learns by receiving rewards for correct identifications and penalties for errors, improving its accuracy over time. A key advantage is its ability to adapt dynamically to changes in user behavior without requiring active participation, enhancing both security and user experience.

# Dataset 
<ul>
<li>
  **Dataset-1:-** The BBMAS (Behavioral Biometrics Multidevice Active Authentication System) dataset is a public dataset designed for research in behavioral biometrics .  It is a collection of keystroke
data from multiple users performing various activities on different devices .  
**Link:-** 

</li>
<li>
 **Dataset-2:-** (Mendley dataset) This dataset is a publicly available dataset , particularly focusing on the interaction of users with the Mendeley platform .  
**Link:-** 
</li>
</ul>

# METHODOLOGY 

### Data Preprocessing 
<ul> 
<li> Preprocessing the Data - In this step, data from 117 users is segregated into two categories: processing User , Corrupted users .I considered processing user id as legitimate and 10 corrupted users for corrupting the behaviour pattern of legitimate user for ensuring a proficient training of the model remsembling
the real time behaviour patterns of an user. These user ids are taken during runtime .</li>
<li> Creating Observations for Both Types of User IDs Observations are generated using
two parameters, N = 8 and H = 3 .</li>
<li> Creating Summary Features - Summary features capture the core characteristics of each
observation by computing metrics such as: Latency ( difference in time since beginning of last
event in an obseration time since beginning of first event ) Standard Devialtion of time diff
column (variability ) Typing speed of the user (Number of events / latency ) These features are
essential for capturing core trends helping the model to focus on key differentiators
between legitimate and corrupted users.</li>
<li> Splitting Data of considered legitimate user into Training and Testing Sets To eval-
uate the model’s performance reliably (70 30 etc)</li>
<li> Feature Reduction using Principal Component Analysis (PCA) and  Autoencoders</li>
<li> Creating Final Observation Set The final dataset is constructed by augumenting obser-
vations from: Processing User: Represents legitimate behavior. Corrupted Users: Represents
faulty or malicious patterns.</li>
<li> Creating Episodes In Reinforcement Learning (RL) .</li>
</ul>


### Model
 
DDQN:- An advanced RL algorithm that addresses overestimation issues in traditional Q-learning. DDQN uses two networks:  
<ul>
  <li>Evaluation Network </li> 
  <li>Target Network</li>  
 </ul>
 
**Training Process-** Episodes are fed to the model to train it on legitimate and corrupted behavior
patterns.   
**Testing-** The test set of legitimate user combined with Corrupted Data of other users
taken randomly suring run time


### Hyperparameters
<ul>
 <li>  State Size: 10    
Number of features (columns) in the dataset, defining the model’s input size.</li>

<li>Action Size: 2  
Number of possible outputs (e.g., classify as legitimate or corrupted).
</li>
<li>
 Epsilon Parameters- (Control exploration vs. exploitation during training)
</li>
<li>
 Epsilon Start (0.1) - Encourages exploration initially to discover new patterns.
</li>
<li>
 Epsilon End (0.01) - Shifts toward exploitation as training progresses.
</li>
<li>
 Replay Memory (1000 )- Stores past experiences for batch training, improving sample efficiency.
</li>
<li>
Batch Size(128) - Determines the number of samples processed at once during training.
</li>
<li>
 C Update (2)-Defines how often the target network is updated, stabilizing training.
</li>
<li>
 Reward Function - The reward system guides the model’s learning  
Correct Prediction:+1 point for true positives (TP) or false positives (FP).  
Misclassification: 1 point for false negatives (FN) or other incorrect predictions.  
Purpose: Reinforces the model to favor correct predictions while penalizing incorrect ones.
</li>

</ul>





