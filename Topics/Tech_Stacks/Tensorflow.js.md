# Integrating ML models to React/React Native with Tensorflow.js

## Introduction

TensorFlow.js is a powerful JavaScript library that allows you to integrate machine learning (ML) models into web and mobile applications, including React and React Native. This guide provides a brief overview of the steps necessary to integrate ML models into your React or React Native app using TensorFlow.js.

## Prerequisites
- Basic understanding of React/React Native
- A trained ML model (e.g., in TensorFlow, Keras, or other compatible formats)

## Guide

### Step 1. Installing Dependencies

#### 1.1. Install TensorFlow.js using npm or yarn
  - `npm install @tensorflow/tfjs` or `yarn add @tensorflow/tfjs`

#### 1.2. For React Native, install additional dependencies
  - `npm install @tensorflow/tfjs-react-native` or `yarn add @tensorflow/tfjs-react-native`
  - `npm install expo-gl` or `yarn add expo-gl`
  - `npm install expo-gl-cpp` or `yarn add expo-gl-cpp`
  - `npm install expo-camera` or `yarn add expo-camera`

### Step 2. Importing TensorFlow.js
#### 2.1. In your React component or React Native module, import TensorFlow.js
  - `import * as tf from '@tensorflow/tfjs';`

#### 2.2. For React Native, also import the tfjs-react-native package and initialize it
  - `import * as tf from '@tensorflow/tfjs-react-native';`
  - Inside your component or module, call `await tf.ready();` to ensure TensorFlow.js is ready to use.

### Step 3. Loading the ML Model
#### 3.1. Convert your trained ML model to the TensorFlow.js format
  - Using the 'tensorflowjs_converter' tool inside python tensorflowjs package, detailed guide can be found [here](https://www.tensorflow.org/js/tutorials/conversion/import_keras). After conversion, you will get a model.json file and one or more binary .bin files. These files together constitute the TensorFlow.js model.
  - `model.json`: This JSON file contains the model's architecture, metadata, and the path to the binary weights file(s).
  -  `*.bin` file(s): The binary files store the actual weights of the model as binary data. Weights are the learned parameters that the model uses to make predictions. The binary format ensures that the file size is as small as possible, enabling faster transfer and loading of the model in web applications. In some cases, there may be multiple .bin files, depending on the model's size and how it was saved.
#### 3.2. Host your converted model (e.g., on a web server, cloud storage, or local server)
#### 3.3. Load your model using TensorFlow.js in your React component or React Native module
  - `const model = await tf.loadLayersModel('https://path/to/your/model.json');`

### Step 4. Making Predictions
#### 4.1. Preprocessing data
  - Prepare your input data according to your ML model's requirements. This may include resizing images, normalizing data, or tokenizing text
  - Convert your input data to a TensorFlow.js tensor, matching the model's expected input shape
#### 4.2. Call the `predict` method on your loaded model with the preprocessed input tensor
  - `const prediction = model.predict(inputTensor);`
#### 4.3. Post-process the output data as needed (e.g., decoding labels, rounding scores)


## Extra Resources
### Documentation
- [Tensorflow.js](https://www.tensorflow.org/js/guide)
- [tfjs-react-native](https://www.npmjs.com/package/@tensorflow/tfjs-react-native)
### Demos/Tutorials
- [TensorFlow SavedModel Import Demo](https://github.com/tensorflow/tfjs/tree/master/tfjs-converter/demo/mobilenet): Not for React/React Native, but helpful.
- [How to deploy your custom tensorflow model to react native](https://www.youtube.com/watch?v=pC7mCEHiYQw): A youtube tutorial.
- [React Native + Tensorflow.js - implementing a model](https://medium.com/@ferlatti.aldo/react-native-tensorflow-js-implementing-a-model-daad1a2c7f30): A medium article demo.
