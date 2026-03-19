# 🚗 Automatic Number Plate Recognition (ANPR)
### YOLOv8 + EasyOCR | Python

A complete Automatic Number Plate Recognition system that detects vehicles, localizes license plates, and reads plate numbers from video in real time.

---

## 📽️ Demo

[▶️ Watch Output Video](https://drive.google.com/file/d/1In8Iv34lZJfN2v7ryb8cz1riNG8WM94S/view?usp=sharing)

---

## ⚙️ How It Works

```
Input Video → Detect Cars (YOLOv8) → Detect License Plate (YOLOv8) → Read Plate Text (EasyOCR) → Output Video
```

1. **Vehicle Detection** — Pretrained YOLOv8 detects cars, buses, and trucks in each frame
2. **License Plate Detection** — Custom trained YOLOv8 model localizes the plate on each vehicle
3. **OCR** — EasyOCR reads the plate number from the cropped plate region
4. **Tracking** — SORT algorithm tracks vehicles across frames
5. **Interpolation** — Missing plate reads between frames are filled in
6. **Visualization** — Bounding boxes and plate text are drawn on the output video

---

## 🧠 Model Training

The license plate detector was trained from scratch using YOLOv8 on the [License Plate Recognition Dataset](https://universe.roboflow.com/roboflow-universe-projects/license-plate-recognition-rxg4e/dataset/4) from Roboflow (10,000+ images).

Training was done on Google Colab using a T4 GPU.

📓 [Open Training Notebook](train_license_plate_detector.ipynb)

### Training Results
| Metric | Score |
|--------|-------|
| mAP50 | ~0.95 |
| Precision | ~0.94 |
| Recall | ~0.91 |

---

## 🗂️ Project Structure

```
├── models/
│   └── license_plate_detector.pt   # custom trained model
├── sort/
│   ├── sort.py                     # SORT tracking algorithm
│   └── __init__.py
├── main.py                         # run detection on video
├── add_missing_data.py             # interpolate missing frames
├── visualize.py                    # generate output video
├── util.py                         # helper functions
├── train_license_plate_detector.ipynb  # training notebook
└── test.csv                        # detection results
```

---

## 🚀 Getting Started

### 1. Clone the repo
```bash
git clone https://github.com/youssefsafwat123/Computer-vision-NTI-Project.git
cd Computer-vision-NTI-Project
```

### 2. Install dependencies
```bash
pip install ultralytics easyocr opencv-python filterpy scipy pandas
```

### 3. Add your video
Place your input video in the repo folder and rename it `sample.mp4`.

You can download the sample video used in this project [here](https://www.pexels.com/video/traffic-flow-in-the-highway-2103099/).

### 4. Run
```bash
python main.py
python add_missing_data.py
python visualize.py
```

The output video will be saved as `out.mp4`.

---

## 🛠️ Built With

- [YOLOv8](https://github.com/ultralytics/ultralytics) — object detection
- [EasyOCR](https://github.com/JaidedAI/EasyOCR) — optical character recognition
- [SORT](https://github.com/abewley/sort) — object tracking
- [OpenCV](https://opencv.org/) — video processing

---

## 📄 License

This project is for educational purposes as part of the NTI Computer Vision course.
