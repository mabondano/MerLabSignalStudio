# MerLabSignalStudio
MerLabSignalStudio is a Java framework for end-to-end signal processing and data analytics. It provides synthetic and statistical signal generators, DSP operations (add, filter, FFT), RPN-style pipelines, statistical and feature extraction, neural network inference hooks, JDBC persistence, and XChart visualization. Extensible and test-driven.


## 1. Overview

MerLabSignalStudio is a Java framework for end-to-end signal-style data processing, analysis and orchestration. It offers:

- **Synthetic & statistical signal generation**  
  From basic waveforms (sine, square, triangular) to uniform/normal generators and advanced distributions (Poisson, Gamma, Beta, etc.) via Apache Commons-Math.

- **Rich DSP toolbox**  
  Element-wise operations (add, subtract, multiply, divide), decimation, interpolation, normalization, derivatives, integrals, FFT, moving averages and multi-window smoothing.

- **Comprehensive statistics & feature extraction**  
  Mean, variance, percentiles, skewness, kurtosis, autocorrelation, zero-crossing rate, energy metrics, and custom feature hooks.

- **Postfix (RPN-style) engine**  
  Push `Signal` objects or scalar parameters onto a stack and invoke unary, binary or future n-ary operations purely in postfix form, for maximum flexibility.

- **Pipeline orchestration**  
  `SignalManager` coordinates loading, processing, optional statistical/feature/NN steps, then persistence and visualization—all under configurable flags (`doStats`, `doFeatures`, `doNN`).

- **Persistence & visualization**  
  JDBC-based SQL persistence with `DatabaseManager` plus real-time plotting via XChart (`SignalPlotter`) for rapid iteration and debugging.

MerLabSignalStudio is ideal for signal processing engineers, data scientists and backend developers who need a **testable**, **extensible** and **DSL-like** framework to transform raw time-series or tabular data into analytics and machine-learning pipelines.

---

## 2. Folder Structure

A typical Maven-style layout:

```plaintext
MerLabSignalStudio/
├── src/
│   ├── main/
│   │   └── java/com/merlab/signals/
│   │       ├── AbstractSignalGenerator.java
│   │       ├── SignalGenerator.java
│   │       ├── CustomSignalGenerator.java
│   │       ├── DistributionGenerator.java
│   │       ├── Signal.java
│   │       ├── SignalStack.java
│   │       ├── SignalProcessor.java
│   │       ├── StatisticalProcessor.java
│   │       ├── FeatureExtractor.java
│   │       ├── NeuralNetworkProcessor.java
│   │       ├── NeuralNetworkManager.java
│   │       ├── DatabaseLoader.java
│   │       ├── DatabaseManager.java
│   │       ├── SignalPlotter.java
│   │       ├── SignalManager.java
│   │       ├── RPNOp.java
│   │       └── module-info.java
│   └── test/
│       └── java/com/merlab/signals/test/
│           ├── SignalGeneratorTest.java
│           ├── CustomSignalGeneratorTest.java
│           ├── DistributionGeneratorTest.java
│           ├── SignalProcessorTest.java
│           ├── StatisticalProcessorTest.java
│           ├── SignalStackTest.java
│           ├── SignalManagerTest.java
│           └── SignalProcessorFFTTest.java
├── pom.xml
└── README.md

