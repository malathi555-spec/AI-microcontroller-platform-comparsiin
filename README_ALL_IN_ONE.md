<div align="center">

# 🔬 AI Microcontroller Platform Comparison

**A practical comparison of microcontroller platforms for running TinyML models at the edge**

![TinyML](https://img.shields.io/badge/TinyML-Edge%20AI-blue)
![Python](https://img.shields.io/badge/Python-3.9%2B-yellow)
![C++](https://img.shields.io/badge/C%2B%2B-Embedded-informational)
![License](https://img.shields.io/badge/License-MIT-green)

Created by [**malathi555-spec**](https://github.com/malathi555-spec)

</div>

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Platforms Compared](#-platforms-compared)
- [Evaluation Criteria](#-evaluation-criteria)
- [Summary Comparison](#-summary-comparison)
- [Platform Details](#-platform-details)
- [Tools and Frameworks](#-tools-and-frameworks)
- [Getting Started](#-getting-started)
- [Benchmark Method](#-benchmark-method)
- [Results](#-results)
- [Applications](#-applications)
- [Recommendations](#-recommendations)
- [Project Structure](#-project-structure)
- [Source Code](#-source-code)
- [Future Work](#-future-work)
- [Conclusion](#-conclusion)
- [References](#-references)
- [License](#-license)

---

## 📌 Overview

**TinyML** brings machine learning to small, low-power microcontrollers. Running AI directly on the device (edge AI) gives clear benefits:

| Benefit | Description |
|---|---|
| ⚡ Low latency | No internet round trip |
| 🔒 Privacy | Data stays on the device |
| 🔋 Low power | Can run for months on a battery |
| 💲 Low cost | Boards cost only a few dollars |
| 📴 Offline use | No network needed |

Microcontrollers have very limited memory and processing power, so **choosing the right platform is important**. This project compares popular boards to help students and developers decide.

**Goal:** compare speed, memory, power use, cost, and ease of use for common TinyML tasks such as keyword spotting, gesture recognition, anomaly detection, and simple image classification.

---

## 🧩 Platforms Compared

| Platform | Processor | Clock | RAM | Flash | AI Support |
|---|---|---|---|---|---|
| Arduino Nano 33 BLE Sense | Arm Cortex-M4F (nRF52840) | 64 MHz | 256 KB | 1 MB | TensorFlow Lite Micro, Edge Impulse |
| ESP32 | Dual-core Xtensa LX6 | up to 240 MHz | 520 KB | 4 MB (typical, external) | TensorFlow Lite Micro, ESP-NN |
| Raspberry Pi Pico (RP2040) | Dual Arm Cortex-M0+ | 133 MHz | 264 KB | 2 MB (external) | TensorFlow Lite Micro |
| STM32 Nucleo-F401RE | Arm Cortex-M4F | 84 MHz | 96 KB | 512 KB | STM32Cube.AI, TensorFlow Lite Micro |
| Analog Devices MAX78000 | Cortex-M4F + CNN accelerator | 100 MHz | 128 KB | 512 KB | Built-in neural network accelerator |

> **Note:** Values are typical datasheet figures. Check the official datasheet of your exact board before building.

---

## 📏 Evaluation Criteria

| Criteria | Meaning |
|---|---|
| Inference speed | Time for one prediction (ms) |
| Memory | Whether the model fits in RAM and flash |
| Power use | Energy per inference, important for batteries |
| Cost | Price of the board |
| Ease of use | Tools, tutorials, community support |
| Connectivity | Wi-Fi, Bluetooth, USB |
| Built-in sensors | Microphone, motion sensor, camera support |

---

## 📊 Summary Comparison

| Platform | Speed | Power Saving | Cost | Ease of Use | Best For |
|---|:---:|:---:|:---:|:---:|---|
| Arduino Nano 33 BLE Sense | Medium | Good | Medium | Very easy | Beginners, wearables |
| ESP32 | High | Medium | Low | Easy | IoT with Wi-Fi |
| Raspberry Pi Pico | Medium | Good | Very low | Easy | Low-budget learning |
| STM32 Nucleo-F401RE | Medium | Good | Medium | Medium | Professional products |
| MAX78000 | Very high (CNN) | Excellent | Higher | Harder | Ultra-low-power vision and audio |

> Ratings are general guidance, not measured results. Use the [Results](#-results) section for your own measurements.

---

## 🔍 Platform Details

<details>
<summary><b>Arduino Nano 33 BLE Sense</b></summary>

- ✅ Built-in microphone, motion, temperature, and light sensors
- ✅ Great tutorials and Edge Impulse support
- ❌ Slower clock; costs more than ESP32 or Pico

</details>

<details>
<summary><b>ESP32</b></summary>

- ✅ Fast, built-in Wi-Fi and Bluetooth, very cheap, huge community
- ❌ Uses more power when Wi-Fi is on

</details>

<details>
<summary><b>Raspberry Pi Pico (RP2040)</b></summary>

- ✅ Very cheap, easy in C/C++ and MicroPython, good documentation
- ❌ No floating-point hardware, so quantized models work best; no wireless on the base model

</details>

<details>
<summary><b>STM32 Nucleo-F401RE</b></summary>

- ✅ Professional-grade with strong tooling (STM32Cube.AI)
- ❌ Small RAM on this model; steeper learning curve

</details>

<details>
<summary><b>MAX78000</b></summary>

- ✅ Hardware CNN accelerator gives very fast, very low-power inference
- ❌ Smaller community; special toolchain; supports limited model types

</details>

---

## 🛠 Tools and Frameworks

| Tool | Use |
|---|---|
| TensorFlow Lite for Microcontrollers | Runs models on most boards |
| Edge Impulse | Collect data, train, and deploy online |
| STM32Cube.AI | Converts models for STM32 boards |
| Arduino IDE / PlatformIO | Write and upload code |

---

## 🚀 Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/malathi555-spec/AI-Microcontroller-Platform-Comparison.git
cd AI-Microcontroller-Platform-Comparison

# 2. Install Python packages
pip install -r requirements.txt

# 3. Train and convert the model (creates model.tflite and model_data.h)
python code/train_and_convert.py
```

Then:

1. Copy `model_data.h` into `code/arduino_benchmark/`.
2. Install a TensorFlow Lite Micro library for your board in the Arduino IDE.
3. Upload `arduino_benchmark.ino` and open the Serial Monitor at **115200 baud**.
4. Write the printed numbers into `results/results.csv`.
5. Run `python code/plot_results.py` to create charts.

---

## 🧪 Benchmark Method

To compare fairly, use the **same model and same steps** on every board.

1. Train a small model (for example, keyword spotting or gesture recognition).
2. Convert it to TensorFlow Lite and quantize it to int8.
3. Deploy it to each board.
4. Run 100 inferences and record the average time.
5. Record RAM and flash used.
6. Measure power with a USB power meter or current-measuring board.
7. Save results in the `results/` folder.

---

## 📈 Results

Fill in this table after testing each board.

| Platform | Inference Time (ms) | RAM (KB) | Flash (KB) | Power (mW) | Accuracy (%) |
|---|:---:|:---:|:---:|:---:|:---:|
| Arduino Nano 33 BLE Sense | | | | | |
| ESP32 | | | | | |
| Raspberry Pi Pico | | | | | |
| STM32 Nucleo-F401RE | | | | | |
| MAX78000 | | | | | |

---

## 🌍 Applications

- 🎙 Voice commands with keyword spotting
- ✋ Gesture control for wearables
- 🏭 Predictive maintenance for motors and machines
- 🌱 Smart agriculture and plant monitoring
- ❤️ Health monitoring and fall detection
- 🏠 Smart home sensors

---

## ✅ Recommendations

| If you need | Choose |
|---|---|
| A first AI project | Arduino Nano 33 BLE Sense |
| Wi-Fi at low cost | ESP32 |
| The tightest budget | Raspberry Pi Pico |
| A commercial product | STM32 |
| Fastest AI at lowest power | MAX78000 |

---

## 📁 Project Structure

```
AI-Microcontroller-Platform-Comparison/
├── README.md
├── requirements.txt
├── code/
│   ├── train_and_convert.py
│   ├── plot_results.py
│   └── arduino_benchmark/
│       └── arduino_benchmark.ino
└── results/
    └── results.csv
```

---

## 💻 Source Code

Click a section to expand it, then copy the code into a file with the name shown.

<details>
<summary><b>requirements.txt</b></summary>

```text
tensorflow>=2.12
numpy
matplotlib
pandas
```

</details>

<details>
<summary><b>code/train_and_convert.py</b></summary>

```python
"""
Step 1: Train a small model, convert it to TensorFlow Lite (int8),
and export it as a C header file (model_data.h) for microcontrollers.

Run:  python code/train_and_convert.py
"""
import numpy as np
import tensorflow as tf

# ---------- 1. Load data (MNIST digits, small and easy) ----------
(x_train, y_train), (x_test, y_test) = tf.keras.datasets.mnist.load_data()
x_train = (x_train / 255.0).astype("float32")[..., np.newaxis]
x_test = (x_test / 255.0).astype("float32")[..., np.newaxis]

# ---------- 2. Build a tiny model ----------
model = tf.keras.Sequential([
    tf.keras.layers.Input(shape=(28, 28, 1)),
    tf.keras.layers.Conv2D(8, 3, activation="relu"),
    tf.keras.layers.MaxPooling2D(),
    tf.keras.layers.Conv2D(16, 3, activation="relu"),
    tf.keras.layers.MaxPooling2D(),
    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(10, activation="softmax"),
])
model.compile(optimizer="adam",
              loss="sparse_categorical_crossentropy",
              metrics=["accuracy"])

# ---------- 3. Train ----------
model.fit(x_train, y_train, epochs=3, batch_size=64, validation_split=0.1)
loss, acc = model.evaluate(x_test, y_test, verbose=0)
print(f"Float model accuracy: {acc * 100:.2f}%")

# ---------- 4. Convert to int8 TensorFlow Lite ----------
def representative_data():
    for i in range(200):
        yield [x_train[i:i + 1]]

converter = tf.lite.TFLiteConverter.from_keras_model(model)
converter.optimizations = [tf.lite.Optimize.DEFAULT]
converter.representative_dataset = representative_data
converter.target_spec.supported_ops = [tf.lite.OpsSet.TFLITE_BUILTINS_INT8]
converter.inference_input_type = tf.int8
converter.inference_output_type = tf.int8
tflite_model = converter.convert()

with open("model.tflite", "wb") as f:
    f.write(tflite_model)
print(f"Saved model.tflite ({len(tflite_model) / 1024:.1f} KB)")

# ---------- 5. Check int8 accuracy on 500 test images ----------
interpreter = tf.lite.Interpreter(model_content=tflite_model)
interpreter.allocate_tensors()
inp = interpreter.get_input_details()[0]
out = interpreter.get_output_details()[0]
scale, zero_point = inp["quantization"]

correct = 0
n = 500
for i in range(n):
    q = (x_test[i:i + 1] / scale + zero_point).astype(np.int8)
    interpreter.set_tensor(inp["index"], q)
    interpreter.invoke()
    pred = np.argmax(interpreter.get_tensor(out["index"]))
    correct += int(pred == y_test[i])
print(f"Int8 model accuracy (first {n} test images): {correct / n * 100:.2f}%")

# ---------- 6. Export as C array (model_data.h) ----------
hex_values = ", ".join(f"0x{b:02x}" for b in tflite_model)
with open("model_data.h", "w") as f:
    f.write("#ifndef MODEL_DATA_H\n#define MODEL_DATA_H\n\n")
    f.write("alignas(16) const unsigned char g_model[] = {\n")
    f.write(hex_values + "\n};\n")
    f.write(f"const unsigned int g_model_len = {len(tflite_model)};\n\n")
    f.write("#endif\n")
print("Saved model_data.h  (copy it next to the .ino file)")
```

</details>

<details>
<summary><b>code/arduino_benchmark/arduino_benchmark.ino</b></summary>

```cpp
/*
  AI Microcontroller Platform Comparison - Benchmark Sketch
  Works on: Arduino Nano 33 BLE Sense, ESP32, Raspberry Pi Pico, STM32 (Arduino core)

  Before uploading:
  1. Run code/train_and_convert.py to create model_data.h
  2. Copy model_data.h into this folder
  3. Install a TensorFlow Lite Micro library for your board
     (for example "Arduino_TensorFlowLite" or "TensorFlowLite_ESP32")
*/

#include <TensorFlowLite.h>
#include "tensorflow/lite/micro/all_ops_resolver.h"
#include "tensorflow/lite/micro/micro_interpreter.h"
#include "tensorflow/lite/schema/schema_generated.h"
#include "model_data.h"

const int RUNS = 100;                 // number of inferences to average
constexpr int kArenaSize = 40 * 1024; // working memory for the model (change if needed)
alignas(16) static uint8_t tensor_arena[kArenaSize];

tflite::AllOpsResolver resolver;
tflite::MicroInterpreter* interpreter = nullptr;
TfLiteTensor* input = nullptr;

void setup() {
  Serial.begin(115200);
  while (!Serial && millis() < 3000) {}

  const tflite::Model* model = tflite::GetModel(g_model);
  static tflite::MicroInterpreter static_interpreter(
      model, resolver, tensor_arena, kArenaSize);
  interpreter = &static_interpreter;

  if (interpreter->AllocateTensors() != kTfLiteOk) {
    Serial.println("ERROR: AllocateTensors failed. Increase kArenaSize.");
    while (true) {}
  }

  input = interpreter->input(0);

  // Fill the input with a fixed test pattern
  for (size_t i = 0; i < input->bytes; i++) {
    input->data.int8[i] = (int8_t)(i % 100);
  }

  Serial.println("=== TinyML Benchmark ===");
  Serial.print("Model size (bytes): ");
  Serial.println(g_model_len);
  Serial.print("Arena used (bytes): ");
  Serial.println(interpreter->arena_used_bytes());

  // Warm-up run (not counted)
  interpreter->Invoke();

  unsigned long total_us = 0;
  unsigned long min_us = 0xFFFFFFFF;
  unsigned long max_us = 0;

  for (int i = 0; i < RUNS; i++) {
    unsigned long start = micros();
    interpreter->Invoke();
    unsigned long dt = micros() - start;

    total_us += dt;
    if (dt < min_us) min_us = dt;
    if (dt > max_us) max_us = dt;
  }

  Serial.print("Runs: ");               Serial.println(RUNS);
  Serial.print("Average time (us): ");  Serial.println(total_us / RUNS);
  Serial.print("Minimum time (us): ");  Serial.println(min_us);
  Serial.print("Maximum time (us): ");  Serial.println(max_us);
  Serial.println("Done. Copy these numbers into results/results.csv");
}

void loop() {
  // Nothing here. The benchmark runs once in setup().
}
```

</details>

<details>
<summary><b>code/plot_results.py</b></summary>

```python
"""
Step 3: Make bar charts from results/results.csv

Run:  python code/plot_results.py
"""
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("results/results.csv").dropna(subset=["inference_time_ms"])

if df.empty:
    raise SystemExit("results/results.csv has no numbers yet. Fill it in first.")

metrics = [
    ("inference_time_ms", "Inference time (ms) - lower is better"),
    ("ram_used_kb", "RAM used (KB) - lower is better"),
    ("power_mw", "Power (mW) - lower is better"),
    ("accuracy_percent", "Accuracy (%) - higher is better"),
]

fig, axes = plt.subplots(2, 2, figsize=(12, 8))
for ax, (col, title) in zip(axes.flat, metrics):
    if col in df and df[col].notna().any():
        ax.bar(df["platform"], df[col])
        ax.set_title(title)
        ax.tick_params(axis="x", rotation=30)

plt.tight_layout()
plt.savefig("results/comparison.png", dpi=150)
print("Saved results/comparison.png")
```

</details>

<details>
<summary><b>results/results.csv</b></summary>

```csv
platform,inference_time_ms,ram_used_kb,flash_used_kb,power_mw,accuracy_percent
Arduino Nano 33 BLE Sense,,,,,
ESP32,,,,,
Raspberry Pi Pico,,,,,
STM32 Nucleo-F401RE,,,,,
MAX78000,,,,,
```

</details>

---

## 🔭 Future Work

- [ ] Add measured benchmark results for each board
- [ ] Add more boards (Arduino Portenta, Raspberry Pi Pico 2)
- [ ] Add power consumption graphs
- [ ] Add a camera-based image classification test

---

## 🏁 Conclusion

There is no single best board. ESP32 and Raspberry Pi Pico suit low-cost projects, Arduino Nano 33 BLE Sense is best for learning, STM32 fits professional products, and MAX78000 is best when speed and battery life matter most. Choose the board that matches your project needs.

---

## 📚 References

- [TensorFlow Lite for Microcontrollers](https://www.tensorflow.org/lite/microcontrollers)
- [Edge Impulse](https://edgeimpulse.com)
- [STM32Cube.AI](https://www.st.com/en/embedded-software/x-cube-ai.html)
- [Analog Devices MAX78000](https://www.analog.com/en/products/max78000.html)

---

## 📄 License

Released under the **MIT License**.

<div align="center">

⭐ If this project helped you, give it a star!

</div>
