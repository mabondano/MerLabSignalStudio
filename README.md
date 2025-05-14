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
---
## 3. Package & Class Descriptions

com.merlab.signals
- **SignalProvider (interface)**
Defines a single method, Signal getSignal(), for any signal source.

- **Signal generators**

SignalGenerator: built-in waveforms (sine, square, triangle, white noise, delta).

CustomSignalGenerator: manual implementations of uniform/normal with seed control.

DistributionGenerator: statistical distributions (Binomial, Poisson, Exponential, Gamma, Chi-Square, etc.) via Commons-Math.

- **Signal**
Wraps a List<Double> with getters, setters and a println() helper.

- **SignalStack**
LIFO stack of Signal instances, with push(), pop(), peek(), peekSecond(), and size().

- **SignalProcessor**
Static DSP routines:

Element-wise: addSignals, subtractSignals, multiplySignals, divideSignals

Validation and padding (validateAndAlign)

Decimation, interpolation, normalization, derivative, integrate

Cooley-Tukey FFT for power-of-two lengths

- **StatisticalProcessor**
40+ methods covering:

Position & dispersion (mean, variance, median, percentile)

Higher-order moments (skewness, kurtosis)

Waveform metrics (zero-crossings, LQR)

Temporal analysis (autocorrelation)

Windowed smoothing (moving average, Gaussian)

Convolution, filters

- **FeatureExtractor**
Extracts domain-specific features (RMS, energy, peak detection) as Signal.

- **Neural network**

NeuralNetworkProcessor: inference on a Signal.

NeuralNetworkManager: wraps inference for production.

- **Persistence & I/O**

DatabaseLoader: reads data into Signal.

DatabaseManager: writes final Signal via JDBC.

- **Visualization**
SignalPlotter: XChart wrapper for plotting signals in a Swing window.

- **Orchestration**
SignalManager:

Fields: provider, signalStack, databaseManager, flags (doStats, doFeatures, doNN)

Methods: runPipeline(), operateRPN(), normalizeLastSignal(), statsLastSignal(), featuresLastSignal(), nnLastSignal(), saveLastSignal(), showStack(), addSignal(), getLastSignal()

- **RPNOp**
Enum of binary operations: ADD, SUBTRACT, MULTIPLY, DIVIDE.

