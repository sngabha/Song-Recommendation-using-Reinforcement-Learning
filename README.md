# Song-Recommendation-using-Reinforcement-Learning

**Python Version:** python3.6

**Important Libraries Used:** glob, pandas, numpy, tqdm, pickle, keras, matplotlib, random, math, statistics

**File Names and Description in sequence:**

1. **Sampling-Sessions.ipynb and Merge-Sampled-Sessions-And-Tracks.ipynb -** These files performs sampling over the entire dataset and pulls 100k sessions out of it. After session sampling, it filters the songs from the songs dataset which are present in the sampled sessions.

1. **Track Feature Autoencoder.ipynb -** This file reads the track data consisting of 20 features, train a feed forward Autoencoder and reduce the dimensions of each songs from 20 to 8. Finally, after this, it creates a csv file and store a latent vector representation of each track. Simply execute this file first in jupyter notebook to get the latent representation of each track as a csv output.

2. **Session State Autoencoder.ipynb -** This file reads the entire session data and iterate through each of it to create a state of 5 continuous songs and transition between those songs. To create a state, it uses the latent representation of the tracks from the csv created in previous step. Once a vector of states is created where each state is a 5x9 matrix (5 songs along with transition data), an LSTM Autoencoder is trained. We used LSTM autoencoder due to the sequential pattern in the data. Once the autoencoder is trained, the encoder model is saved using pickle. Simply execute this file in jupyter notebook to get the encoder model for the states that converts a 5x9 state matrix into 1xp matrix.

3. **SARSA.ipynb -** This file implements the SARSA algorithm to predict next recommended songs while training. It loads latent representation of tracks and the LSTM autoencoder created in Step 1 and 2 to run the SARSA algorithm. Finally, in the end, it writes the results into a file using pickle. Note: This method is unoptimised and therefore takes a lot of time to complete.

4. **Track Clustering.ipynb -** This file reads the latent representation of the track, perform normalization over the data and applies KMeans clustering algorithm to represent each song/track using a cluster id. We ran this program for the cluster size of 100 and 1000. This code was converted into Spark and executed on EMR for fast results. The same code is used to cluster all the states. Output of this file is a csv which contains the track_id/state_id and cluster number.

5. **SARSA-Clustering.ipynb and SARSA-Clustering-k1000-State-k100-Track.ipynb -** These files implements the SARSA algorithm using clustering but with different state and track clustering size. To reduce the state space and add some approximation, clustering was used here. Once the execution gets over in the end, it writes the results into a file using pickle.

6. **MonteCarlo-Clustering.ipynb and MonteCarlo-Clustering-k1000-State-k100-Track.ipynb -** These files implements the Monte Carlo algorithm using clustering but with different state and track clustering size. To reduce the state space and add some approximation, clustering was used here. Once the execution gets over in the end, it writes the results into a file using pickle.
