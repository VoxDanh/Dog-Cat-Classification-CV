# 📒Project Diary✨
## **📍 Phase 0.0: The Apprentice Phase (Learning & Familiarization)**

> Before diving into custom adjustments, I spent time dissecting a foundational model to understand the "why" behind every line of code.

* **Objective:** To get acquainted with the basic AI training workflow through guided implementation (supported by Gemini). I chose not to use pre-built professional models because they can be overly optimized or complex for a beginner to grasp. By building it from scratch, I felt truly immersed in the project, which significantly improved my learning efficiency.
* **Methodology:**
* Carefully analyzed every line of code to understand its specific function and operational logic.
* Researched the core principles and underlying algorithms governing the AI's behavior in this project.


* **Mindset:** This stage was purely focused on learning and absorption. I prioritized understanding the existing structure over implementing my own custom logic.
* **Key Takeaway:** Gained a solid grasp of how a basic Computer Vision project operates—from data loading to weight adjustments and final predictions.

---

### **1. Data Preprocessing**

* Understand the principles of how images work from a computer's perspective, from color layers to numerical matrices.
* **Image Matrix Construction:** Convert raw images into numerical matrix arrays using OpenCV.
* **Data Labeling:** Manual labeling mechanism (0 and 1) for the dataset.
* **Image Resizing:** Bring images to a standard 128x128 size.
* **Data Casting:** Convert data types to `np.float32`.
* **Pixel Normalization:** Divide pixel values by 255.0 to bring them into the [0, 1] range.
* **Storage (.npy):** Package processed data into NumPy binary files (1.14GB).
* **Data Shuffling:** Shuffle data with `random_state=42`.

### **2. AI Core (Algorithms & Neural Networks)**

* Understand the basics of how AI learns and makes decisions.
* **Kernel Operations:** The mechanism of kernels scanning images to extract features.
* **Feature Maps:** The formation of feature maps after convolution.
* **Error Calculation:** The logic of calculating errors during training.
* **Weight Adjustment:** Rules for adjusting weights to correct model errors.
* **CNN Architecture Theory:** Theoretical structure of Convolutional Neural Networks.
* **Overfitting Recognition:** Identifying the "rote learning" phenomenon in models.
* **Dropout Regularization:** Technique to deactivate neurons to increase generalization.
* **Epoch Optimization:** Controlling the optimal number of training iterations (8-12 rounds).

### **3. Python Functions and Tools**

#### **1. Image Processing (OpenCV & NumPy)**

* `cv2.imread()`: Read raw images into numerical matrices.
* `cv2.resize()`: Standardize image size to 128x128.
* `cv2.copyMakeBorder()`: Implement Square Padding technique to prevent image distortion.
* `astype(np.float32)`: Cast data types for floating-point calculations.
* `/ 255.0`: Normalize pixel values to the [0, 1] range.

#### **2. Data Management & Logic**

* `np.save()` / `np.load()`: Save and load `.npy` files (1.14GB data).
* `shuffle(x, y, random_state=42)`: Synchronously shuffle data and labels.
* `os.listdir()`: Browse the list of files in Cat/Dog folders.
* `append()`: Collect image matrices and corresponding labels into a master list.

#### **3. Model Training (Keras/TensorFlow)**

* `Sequential()` / `add()`: Initialize and add network layers (CNN, Dense, Dropout).
* `compile()`: Set up the optimizer, loss function, and metrics.
* `fit()`: Trigger the training process with data and epoch count (8-12).
* `evaluate()` / `predict()`: Evaluate accuracy and predict new images.
* `summary()`: Inspect the layer structure and parameters of the model.
* `save()` / `load_model()`: Store and reuse the trained AI "brain."

### **📊Initial Results & Analysis**

#### **1. Input Data**

* **Quantity:** 24,998 images (including 12,499 Cat images and 12,499 Dog images).
* **Data Size:** Approximately 1.14 GB after conversion to numerical matrices.
* **Image Preprocessing:**
* Converted to 3-channel color images (RGB).
* Resize dimensions: 128x128 pixels.
* Normalization: Scaled to the [0, 1] range using `float32` data type.
* Labeling: Dog = 1, Cat = 0.


* **Data Splitting:** Used `random_state = 42` to split the data into Train (60%) – Val (20%) – Test (20%).

#### **2. Configuration & Training**

* **CNN Architecture:** Neuron counts across layers are 32 - 64 - 128, respectively.
* **Convolution & Pooling Parameters:**
* Kernel Size: (3, 3) with ReLU activation function.
* MaxPooling: Used (2, 2) dimensions to reduce spatial dimensionality.


* **Fully Connected Layers (Dense Layers):**
* Post-Flatten Layer: Used ReLU activation function.
* Final Decision Layer: Used Sigmoid activation function.


* **Compilation Settings:**
* Optimizer: `adam`.
* Loss function: `binary_crossentropy`.
* Metrics: `accuracy`.


* **Training Parameters:** Batch size = 32; Number of training iterations (Epochs) = 20.

#### **3. Training Results**

* **Training Set:** Accuracy: **0.9851** | Loss: **0.0401**.
* **Validation Set:** Accuracy: **0.8402** | Loss: **0.8369**.
* **Performance:** 388ms/step. Total completion time: 2782.072 seconds (~46 minutes).

---

### **⚠️ Problems & Limitations**

#### **Operational Errors:**

* **Failure to Save Model:** Due to an oversight, the model saving command was not executed after training, resulting in the inability to perform testing on the independent test dataset.

#### **Overfitting Diagnosis:**

Based on the significant gap between Training and Validation results, the model shows clear signs of overfitting. Potential causes include:

* **Image Resizing Limitations:** Original image sizes varied drastically (from 60x40 to 500x492). Forcing these into a 128x128 resolution may have caused information loss or distorted the subjects (cats/dogs), especially if they were positioned in corners or were exceptionally small/large, leading to a loss of useful data.
* **Model Complexity:** For the current dataset, utilizing a 128-neuron layer along with 20 epochs might have been excessive, causing the model to memorize the data rather than learn generalized features.
* **Data Distribution Ratios:** The Train/Val/Test ratios need to be re-evaluated to ensure better generalization and prevent the model from failing to learn deeply enough, which leads to "rote learning" (overfitting).
