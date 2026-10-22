# Region I directly written! PTF-CMFNet: Periodicity-Time-Frequency Image Cross-Modal Fusion Fault Diagnosis Network

Preface
In the task of bearing fault diagnosis, the raw one-dimensional vibration signal typically contains two types of critical discriminative information: one is periodic impacts, transient changes, and local fluctuations in the time domain; the other is fault characteristic frequencies, multiples, sidebands, and local energy distributions in the time-frequency domain. Traditional methods often model from a single perspective, for example, directly using one-dimensional CNN to process the raw signal or converting the signal into time-frequency images before inputting them into CNN for classification. Although these methods are simple in structure, they easily overlook the complementary relationship between periodic impacts in the time domain and textures in the time-frequency spectrum. To this end, we propose a multimodal fault diagnosis model for general fault diagnosis tasks: Periodic-Time-Frequency Cross-Modal Fusion Network (PTF-CMFNet)

The model is based on the same one-dimensional vibration signal and constructs two complementary modalities: on one hand, it leverages the idea of periodic two-dimensional modeling from TimesNet to reconstruct the one-dimensional signal into a periodic matrix and extract periodic impact features through multiscale convolution; on the other hand, it uses Markov Transition Field (MTF) to convert the one-dimensional signal into time-frequency images and extract wide-domain time-frequency texture features through large kernel convolutional neural networks styled after RepLKNet. Finally, the model designs a CMRF cross-modal reliability fusion module to achieve bidirectional enhancement and reliability weighted fusion of periodic matrix modality and time-frequency image modality, ultimately completing fault classification.
(At the same time, multiple time-frequency image choices are provided)
Dataset: Southeast University Bearing Fault Dataset
Environment framework: Python 3.10, PyTorch 2.1 and above versions can be run
Accuracy: Test set 99.80%
Use cases: Paper requirements, graduation design requirements
Code Guarantee: The code comments are detailed and ready to run.
1. Model Process Overview
\t1.1 Core Concept of the Model
\tThe core idea of PTF-CMFNet is to model one-dimensional vibration signals as both "periodic matrix mode" and "time-frequency image mode", respectively extracting periodic impact characteristics and time-frequency spectral band characteristics, and then achieves complementary information fusion through a cross-modal reliability fusion mechanism.
\tThe overall process of the model is as follows:
\t(1) One-dimensional vibration signal [B, 1024] input:
\t(2) Branch one: TimesNet Periodic Matrix Branch
\t   
\tBearing fault signals usually have obvious periodic impact characteristics. Taking inner ring fault, outer ring fault, and rolling element fault as examples, the contact or impact at each fault point will produce a periodic response in the vibration signal. Directly using one-dimensional convolution can extract local features, but it is difficult to explicitly express "periodic internal impact morphology" and "inter-period evolution law".
\tTherefore, \tPTF-CMFNet \tborrows the core idea of \tTimesNet \tto convert one-dimensional signals into two-dimensional periodic matrices, enabling the model to simultaneously model:
\tIntra-period variation intra-period variation
\tInter-period variation inter-period variation
\tFFT main period discovery:
\tOne-dimensional sequence → Two-dimensional periodic matrix
\tMulti-scale periodic convolution + periodic weighted fusion
\t(3) Branch two: MTF (CWT) + RepLKNet Time-frequency Image Branch
\t   
\tCWT time-frequency image input [B, 3, 224, 224]
\tLarge kernel convolution feature extraction
\tMulti-stage visual feature modeling
\tGlobal pooling to obtain image features
\t(4) CMRF \tCross-modal reliability fusion
The Periodic Matrix Branch and the Time-Frequency Image Branch extract information from different modalities respectively: PTF-CMFNet. The design of CMRf is Cross-Modal Reliability Fusion, which means a module for cross-modal reliability fusion.
Bidirectional cross-gate control
State reliability assessment
\tEmbodiment Characteristics Construction
Construction of Affective Characteristics
\tTime-frequency image feature z_img
\tFusion feature z_fuse
(5) FC + \tSoftmax Classification
\t  
1.2 Model Innovation Points
Innovation Point One: Constructing a Periodic Matrix Mode, Explicitly Modeling Fault Cycle Impacts.\tTraditional one-dimensional CNNs directly slide convolutions over raw sequences, which are difficult to explicitly model the periodic structure of fault impacts. PTF-CMFNet, drawing on the cyclic two-dimensional modeling concept from TimesNet, utilizes FFT to automatically identify the main cycle. This design enables the model to simultaneously learn the patterns of impact within cycles and the regular changes between them, making it more suitable for identifying repetitive impact characteristics in bearing fault signals.
Innovation Point Two: Periodic Matrix Multi-Scale Convolution for Impact Texture Extraction
Innovation Point Three: Integration of MTF Time-Frequency Image and RepLKNet Large Core Vision Branch
4. Innovation Point Four: Propose Cross-Modal Reliability Fusion CMRF
Unlike simply concatenating two branches, PTF-CMFNet designs a bidirectional cross-gate mechanism: This mechanism forms a mutually guiding and enhancing relationship between the periodic matrix mode and the time-frequency image mode. Based on the enhanced features of both modes, PTF-CMFNet adaptively estimates the importance of the periodic mode and the time-frequency mode in the current sample. This mechanism dynamically adjusts the contribution of the two modes according to the characteristic expression of different fault samples, rather than equally merging the two branches.
2 Data Preprocessing for Southeast University Dataset
2.1 Import Data
The gearbox dataset from Southeast University includes two subdatasets: bearing and gear, all collected from a transmission system dynamics simulator. The gear fault dataset is set up with two working conditions, namely 20Hz-0 (speed - load) and 30Hz-2V. The gear fault data collected include five types of gear operating states: healthy, peeling, broken tooth, crack, and wear.
2.2 Data Preprocessing
A sliding window is used to create the dataset, and the training set, validation set, and test set are uniformly divided into 7:2:1 ratio. Finally, the data is saved. In this paper, the Markov transition field MTF is used as the method for time-frequency image transformation, and the generated time-frequency images are as follows:
3 Fault Diagnosis Model Based on PTF-CMFNet
3.1 Define the Network Model
3.2 Set parameters and train the model
50 epochs, with 100% accuracy using MTF+PTF-CMFNet network for classification, significantly extracting important features from fault signal characteristics. The application demonstrates significant advantages. PTF-CMFNet models one-dimensional fault vibration signals as both TimeNet periodic matrix modes and CWT time-frequency image modes. It utilizes RepLKNet large kernel vision networks to extract wide-domain time-frequency textures, and achieves adaptive fusion of periodic impact information and time-frequency spectral bands through the CMRf cross-modal reliability fusion mechanism. This is a high-innovation multimodal fault diagnosis model for fault classification tasks.
3.3 Model Evaluation
(1) Accuracy, Precision, Recall, F1 Score
(2) Fault 5 classification confusion matrix:
(3) Classification label visualization
(4) Visualization of original data t-SNE features
(5) Visualization of t-SNE features after model training:
Click to download: Full text data, Python code
Previously interesting content:
Python bearing fault diagnosis (19) Innovative diagnostic model based on Transformer-BiLSTM

## Images

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->
