# Analyze-Migraine-From-EEG-Using-LSTM
The raw signals received from non-invasive EEG devices are being used for diagnosis of migraine. Two major steps are:
a. Preprocessing: Raw EEG signals are filtered and clean using EEGLab tool.
b. Feature Extraction and classification: Using Deep Learning-based LSTM variants, quantitative information are extracted from EEG in order to classify migraine patients and healthy individuals. 
![image](https://user-images.githubusercontent.com/50692430/119967035-91c6f900-bfc9-11eb-8c14-9599e2c076de.png)

In the project, we are using publically available dataset “Ultra high-density EEG recording of interictal migraine and Controls” as original dataset.
The objective of preprocessing stage is to remove noise and artifacts in the EEG signals in order to clean, filter it and keep them ready for further processing. To preprocess data, EEGLab software from MATLAB toolbox will be used.
For the feature extraction and classification, three Deep Learning-based Long short-term memory (LSTM) algorithms will be applied on preprocessed data. The algorithms are Vanilla, Stacked and Bidirectional LSTM. Each LSTM differs in its approach. LSTM extract the relevant features directly from the data and further classify it. 
The EEG dataset is divided into two groups. The first group, called Training dataset which are used to train LSTM models. The second group, called Testing dataset that will be used later in crosschecking or evaluation of LSTM model in order to ensure accuracy and correctness of the computed results.
 ![image](https://user-images.githubusercontent.com/50692430/119967204-bb802000-bfc9-11eb-9685-d7d480886069.png)


