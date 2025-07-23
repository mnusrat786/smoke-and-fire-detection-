#  Smoke and Fire Detection - YOLOv5
A **YOLOv5-based Smoke and Fire Detection** model trained on a custom dataset. This model detects smoke and fire in images and videos for early warning and prevention.

---

## Setup Instructions

### Step 1: Clone the Repository and Install Dependencies
First, download the repository and install the required dependencies:
```bash
git clone https://github.com/mnusrat786/smoke-and-fire-detection.git
cd smoke-and-fire-detection
pip install -r requirements.txt
```

### Step 2: Install YOLOv5
We use **Ultralytics' YOLOv5**. Clone and install it:
```bash
git clone https://github.com/ultralytics/yolov5
cd yolov5
pip install -r requirements.txt
cd ..
```

---

## Dataset Structure

### Step 1: Dataset Organization
Your dataset is stored in `data/` and follows this structure:
```bash
data/
├── dataset/
│   ├── images/          # All smoke and fire images
│   │   ├── train/       # Training images
│   │   ├── val/         # Validation images
│   ├── labels/          # YOLO annotation files
│   │   ├── train/       # Training labels
│   │   ├── val/         # Validation labels
│   ├── dataset.yaml     # YOLOv5 dataset config
```

Ensure your dataset has:
- **Images stored inside `images/train/` and `images/val/`**
- **Labels (annotations) stored inside `labels/train/` and `labels/val/`**
- **A valid `dataset.yaml` file defining the class names**

---

## Splitting the Dataset

### 🔹 Step 1: Run the Dataset Split Script
To split the dataset into training and validation sets, use the provided script:
```bash
python split_dataset.py
```
This will automatically organize images and annotations into `train/` and `val/` folders.

---

##  Training the YOLOv5 Model and Running Inference

### 🔹 Step 1: Train the YOLOv5 Model
To train YOLOv5 on your dataset, run:
```bash
python yolov5/train.py --img 640 --batch 16 --epochs 50 --data data/dataset/dataset.yaml --weights yolov5s.pt
```
- `--img 640` → Image size (YOLOv5 default is 640x640)  
- `--batch 16` → Batch size for training  
- `--epochs 50` → Number of training epochs  
- `--data data/dataset/dataset.yaml` → Dataset configuration file  
- `--weights yolov5s.pt` → Pretrained YOLOv5 model  

### 🔹 Step 2: Run Detection on an Image
Once the model is trained, run inference to **detect smoke and fire** on new images:
```bash
python yolov5/detect.py --weights yolov5/runs/train/exp/weights/best.pt --source path/to/your/test/image.jpg
```
Replace `path/to/your/test/image.jpg` with the actual image path.

### 🔹 Step 3: Run Detection on a Video
To detect smoke and fire in a video, use:
```bash
python yolov5/detect.py --weights yolov5/runs/train/exp/weights/best.pt --source path/to/your/video.mp4
```

---

##  Model Results and Trained Weights

After training, your results and weights will be stored in:
```bash
yolov5/runs/train/exp/
├── weights/       # Best trained model
├── labels/        # Detection results
├── results.png    # YOLOv5 training performance graph
```

The final trained model will be located at:
```bash
yolov5/runs/train/exp/weights/best.pt
```

---

## Contributors & Issues

### 🔹 Contribute to the Project
If you want to improve the project, feel free to fork the repository and submit a pull request.

### 🔹 Report Issues
If you find any issues, please **open a GitHub issue** describing the problem.

---

## References

### 🔹 External Resources
- [YOLOv5 Official Repository](https://github.com/ultralytics/yolov5)  
- [LabelImg (For Data Annotation)](https://github.com/heartexlabs/labelImg)  
