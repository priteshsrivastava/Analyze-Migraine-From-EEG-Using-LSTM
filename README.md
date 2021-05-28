# Analyze-Migraine-From-EEG-Using-LSTM
The raw signals received from non-invasive EEG devices are being used for diagnosis of migraine. Two major steps are:
a. Preprocessing: Raw EEG signals are filtered and clean using EEGLab tool.
b. Feature Extraction and classification: Using Deep Learning-based LSTM variants, quantitative information are extracted from EEG in order to classify migraine patients and healthy individuals. 
![image](https://user-images.githubusercontent.com/50692430/119967035-91c6f900-bfc9-11eb-8c14-9599e2c076de.png)

In the project, we are using publically available dataset “Ultra high-density EEG recording of interictal migraine and Controls” as original dataset.
The objective of preprocessing stage is to remove noise and artifacts in the EEG signals in order to clean, filter it and keep them ready for further processing. To preprocess data, EEGLab software from MATLAB toolbox will be used.
For the feature extraction and classification, three Deep Learning-based Long short-term memory (LSTM) algorithms will be applied on preprocessed data. The algorithms are Vanilla, Stacked and Bidirectional LSTM. Each LSTM differs in its approach. LSTM extract the relevant features directly from the data and further classify it. 
The EEG dataset is divided into two groups. The first group, called Training dataset which are used to train LSTM models. The second group, called Testing dataset that will be used later in crosschecking or evaluation of LSTM model in order to ensure accuracy and correctness of the computed results.

Required library/software:
----------------------------
1.	MATLAB: EEGLAB
2.	Python: sklearn, tensorflow, keras, pandas, numpy

EEG Dataset
-------------
•	URL: https://kilthub.cmu.edu/articles/dataset/Ultra_high-density_EEG_recording_of_interictal_migraine_and_controls_sensory_and_rest/12636731?file=23891231
•	Data recorded at 512 Hz frequency
•	Duration: 3 seconds x multiple rounds

Preprocessing:
--------------
A standard sequence to process raw datasets using EEGLab software are gven as:
1. Look up channel locations using the Edit → Channel locations menu item.
2. High-pass filter the data using the Tools → Filter the data → Basic FIR filter menu item. Filter the signals between 0.1-100Hz using basic FIR filter. Select Channel type: EEG.
3. Perform automated artifact rejection using the Tools → Reject data using Clean Rawdata and ASR menu item. Uncheck 'Remove bad channels' to maintain data of all 143 channels. Also uncheck ASR bad burst correction since it takes lot of time. Select only additional removal of bad data.
4. Re-reference the data using the Tools → Re-reference the data menu item. Select compute average reference.
5. Run independent component analysis using the Tools → Decompose data by ICA menu item.
6. Label components using the Tools → Classify components using IClabel → Label components menu item.
7. Classify components using the Tools → Classify components using IClabel → Flag components as artifact menu item. Select menu item Tools → Remove components to actually remove the selected component from the data.
8. Extract data epochs using the Tools → Extract epochs menu item. Enter time 0 - 2 to remove 1 second inter-stimulus-interval (ISI).
9. Export Data in text file using File → Export → Data to text file.

Prepare Dataset:
-----------------
•	Selected subjects: 6 subjects (3 Migraine and 3 Control)
•	Selected Duration: 2 seconds x 50 rounds
Some dataset have more than 50 rounds of recording but for comparative study, I have taken 50 rounds of each subjects.

Dataset used:
1.	M1_SSVEP.bdf	51200rows	143col	Migraine 
2.	C1_SSVEP.bdf	51200rows	143col	Control
3.	M3_SSVEP.bdf	51200rows	143col	Migraine
4.	C2_SSVEP.bdf	51200rows	143col	Control
5.	M4_SSVEP.bdf	51200rows	143col	Migraine
6.	C3_SSVEP.bdf	51200rows	143col	Control

•	Training Dataset (75 %): 4 (M1, C1, M3 and C2)
  Total 307200 rows x 143 columns
•	Testing Dataset (25 %): 2 (M4 and C3)
  Total 102400 rows x 143 columns
•	Classification Label: Migraine (0) and Control (1)

Classification:
--------------
We used python Pandas library for data wrangling and Keras-LSTM library for training.
In compilation of following three LSTM Models, we used Optimizer “Adam" and loss-”mse". The batch size is 1024 and the number of epochs is 50 for better learning rate and comparative study.
1. Vanilla LSTM: In this variant, the model uses one LSTM layer along with “Relu” activation function, one Dense layer as output layer. We optimized the network and to prevent over fitting, uses dropout (0.4) as tuning hyper-parameters.
2. Stacked LSTM: This network comprises following layers:
  Input Layer: It consist a layer with input shape of pre-processed data along with “relu" activation function. This layer passes information to the network for further processing.
  Hidden Layers: It consist one or more layers with “relu" activation function followed by dropout (0.4) for optimization.
  Output Layer: It consist a dense output layer with processed information.
3. Bidirectional LSTM: In this, model uses following layers:
  • Input Bidirectional Layer: It consist an LSTM layer with input shape of pre-processed data along with “Relu” activation function. Bidirectional layer will wrap this layer with Default “concat" merge mode. Finally a dropout (0.4) layer applied for optimization.
  • Hidden Layers: contain one or more layers with “Relu" activation function.
  • Output Layer: This layer is the fully connected dense output layer with processed information. TimeDistributed layer wraps output layer so that one value per timestep can be predicted given the full sequence as input.




