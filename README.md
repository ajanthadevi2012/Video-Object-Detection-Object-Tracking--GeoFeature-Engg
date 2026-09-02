# 🚦 Traffic Video Analytics — Object Detection, Tracking & Camera Data

> **From Traffic Video to Structured Vehicle Intelligence**

A practical computer vision project that transforms a traffic video into **detected objects, persistent vehicle identities, movement information, camera metadata, and structured CSV data**.

This project demonstrates an end-to-end pipeline using **YOLO, ByteTrack, OpenCV, Python, and Pandas**, with the foundation for extending the system into a **Smart City Traffic Monitoring and GeoAI platform**.

---

## 🎯 Project Overview

Traffic cameras generate huge amounts of video data, but raw video alone is difficult to analyze.

This project converts the video into structured information:

```text
🎥 Traffic Video
       │
       ▼
🖼️ Frame Processing
       │
       ▼
🤖 YOLO Object Detection
       │
       ▼
🎯 Bounding Boxes
       │
       ▼
🔄 ByteTrack Object Tracking
       │
       ▼
🆔 Persistent Track IDs
       │
       ▼
📍 Camera Metadata
       │
       ▼
📊 Structured CSV
       │
       ▼
🚦 Traffic Analytics
       │
       ▼
🌍 Future GeoAI / Smart City System
```

---

## 🚀 Key Features

* 🎥 Process traffic-camera video
* 🤖 Detect vehicles and pedestrians using YOLO
* 🚗 Detect cars, buses, trucks, motorcycles, bicycles and people
* 🔄 Track objects across video frames
* 🆔 Assign persistent tracking IDs
* 📦 Extract bounding-box coordinates
* 📍 Associate detections with camera information
* ⏱️ Store frame number and timestamp
* 📊 Generate structured CSV data
* 🎞️ Generate annotated output video
* 📈 Calculate unique tracked objects
* 🛣️ Extract vehicle trajectories
* 🌍 Provide a foundation for GeoAI integration

---

## 🧰 Technologies

| Technology      | Purpose                   |
| --------------- | ------------------------- |
| 🐍 Python       | Programming               |
| 🎥 OpenCV       | Video processing          |
| 🤖 YOLO         | Object detection          |
| 🔄 ByteTrack    | Multi-object tracking     |
| 🐼 Pandas       | Data analysis             |
| 🔢 NumPy        | Numerical processing      |
| ☁️ Google Colab | GPU-based execution       |
| 📄 CSV          | Structured detection data |

---

## 📁 Project Structure

```text
Traffic-Video-Analytics/
│
├── 📓 Project_5_Traffic_Object_Detection_Tracking_CSV.ipynb
│
├── 🎥 The Highway.mp4
│
├── 🎞️ traffic_tracking.mp4
│
├── 📊 traffic_detections.csv
│
├── 📈 vehicle_trajectories.csv
│
└── 📖 README.md
```

---

# 🔬 Detection Pipeline

## 1️⃣ Video Input

The system starts with a traffic video:

```text
The Highway.mp4
```

OpenCV reads the video frame by frame.

For each frame we obtain:

* Frame number
* Timestamp
* Width
* Height
* FPS

---

## 2️⃣ Object Detection

YOLO identifies objects in each frame.

Example:

```text
┌──────────────────────────────┐
│                              │
│       🚗 Car                 │
│      ┌─────────┐             │
│      │         │             │
│      └─────────┘             │
│                              │
│              🚌 Bus          │
│            ┌──────────┐      │
│            │          │      │
│            └──────────┘      │
│                              │
└──────────────────────────────┘
```

Each detection provides:

```text
Class
Confidence
Bounding Box
```

---

# 🔄 Object Tracking

Detection alone answers:

> "What objects are present in this frame?"

Tracking answers:

> "Is this the same vehicle I saw in the previous frame?"

ByteTrack maintains object identities across frames.

Example:

```text
Frame 100       Frame 101       Frame 102

🚗 ID 12   →    🚗 ID 12   →    🚗 ID 12

🚙 ID 18   →    🚙 ID 18   →    🚙 ID 18
```

The same vehicle therefore retains its tracking ID.

---

# 🆔 Tracking Information

Each detected object can contain:

```text
Track ID
Class
Confidence
Bounding Box
Center Point
Frame
Timestamp
```

Example:

```text
ID 12
Class: car
Confidence: 0.91
Frame: 250
Timestamp: 8.33 sec
```

---

# 📍 Camera Metadata

The project also associates each detection with camera information.

Example:

```text
Camera ID: CAM_01
Latitude: 28.6139
Longitude: 77.2090
```

> ⚠️ The coordinates used in the notebook are example values and should be replaced with the actual camera location.

This is important because it allows the project to move from:

**Computer Vision → Spatial Intelligence → GeoAI**

---

# 📊 CSV Output

The detection system produces:

```text
traffic_detections.csv
```

Example structure:

| Field         | Description              |
| ------------- | ------------------------ |
| frame         | Video frame number       |
| timestamp_sec | Time within video        |
| track_id      | Unique tracked object ID |
| class_id      | YOLO class ID            |
| class_name    | Detected object          |
| confidence    | Detection confidence     |
| x1            | Bounding box left        |
| y1            | Bounding box top         |
| x2            | Bounding box right       |
| y2            | Bounding box bottom      |
| center_x      | Object center X          |
| center_y      | Object center Y          |
| camera_id     | Camera identifier        |

---

# 📈 Example Analytics

The CSV can be used to calculate:

### Vehicle categories

```text
🚗 Cars
🚌 Buses
🚚 Trucks
🏍️ Motorcycles
🚲 Bicycles
🚶 Pedestrians
```

### Vehicle counts

```text
Cars        → 43
Trucks      → 8
Buses       → 5
Motorcycles → 17
```

### Important distinction

A vehicle appearing in 200 frames creates approximately 200 detection records.

But:

```text
200 detections ≠ 200 vehicles
```

Tracking allows us to estimate:

```text
Unique Track IDs = Unique tracked objects
```

---

# 🛣️ Vehicle Trajectory

The system records the center point of each tracked object.

Example:

```text
Frame 100 → (420, 310)
Frame 101 → (425, 307)
Frame 102 → (431, 303)
Frame 103 → (438, 299)
```

This creates a trajectory:

```text
          🚗
        ↗
      ↗
    ↗
  ↗
START
```

These trajectories can later be used for:

* Vehicle movement analysis
* Lane analysis
* Direction detection
* Speed estimation
* Congestion analysis
* Traffic pattern analysis

---

# 🎞️ Output Video

The system generates an annotated video:

```text
traffic_tracking.mp4
```

The output contains:

```text
┌─────────────────────────────────────┐
│ Frame: 250                          │
│ Time: 8.33 sec                      │
│ Camera: CAM_01                      │
│                                     │
│       🚗 ID:12 0.91                 │
│      ┌─────────┐                    │
│      │   CAR   │                    │
│      └─────────┘                    │
│                                     │
│               🚌 ID:18 0.87         │
│              ┌──────────┐           │
│              │   BUS    │           │
│              └──────────┘           │
└─────────────────────────────────────┘
```

---

# ☁️ Google Colab

The project can be executed in **Google Colab with GPU acceleration**.

Recommended workflow:

```text
Open Colab
   ↓
Enable GPU
   ↓
Upload The Highway.mp4
   ↓
Install dependencies
   ↓
Load YOLO
   ↓
Run detection + tracking
   ↓
Generate CSV
   ↓
Generate annotated video
```

For initial testing, process a small number of frames before processing the complete video.

---

# 🧪 Learning Objectives

After completing this project, you should understand:

* How video is processed frame by frame
* How YOLO performs object detection
* What bounding boxes represent
* What confidence scores represent
* Why detection and tracking are different
* How multi-object tracking works
* What a tracking ID represents
* How to convert video observations into tabular data
* How camera metadata can be associated with computer-vision outputs
* How CSV data can become the input for traffic analytics

---

# 🧠 Detection vs Tracking

| Detection               | Tracking                        |
| ----------------------- | ------------------------------- |
| Finds objects           | Maintains object identity       |
| Works frame-by-frame    | Works across frames             |
| Produces bounding boxes | Produces Track IDs              |
| Answers "What is here?" | Answers "Which object is this?" |
| YOLO                    | ByteTrack                       |

Together:

```text
YOLO + ByteTrack
       ↓
Detection + Identity
       ↓
Vehicle Intelligence
```

---

# 🌍 From Computer Vision to GeoAI

This project is intentionally designed as a foundation for a larger system.

The next stage can combine:

```text
Traffic Camera
      │
      ▼
Object Detection
      │
      ▼
Object Tracking
      │
      ▼
Vehicle Trajectories
      │
      ▼
Traffic Analytics
      │
      ▼
Camera Coordinates
      │
      ▼
GeoPandas
      │
      ▼
GIS Map
      │
      ▼
🌍 Smart City Traffic Dashboard
```

---

# 🚦 Future Extensions

The project can be extended with:

### Level 1 — Traffic Analytics

* Vehicle counting
* Vehicle classification
* Traffic density
* Direction detection
* Entry/exit counting

### Level 2 — Advanced Computer Vision

* Lane detection
* Line-crossing detection
* Speed estimation
* Wrong-way detection
* Stopped-vehicle detection
* Congestion detection

### Level 3 — GeoAI

* Camera locations on maps
* GeoPandas integration
* Spatial traffic analysis
* Road-network integration
* Traffic hotspots
* Spatial clustering

### Level 4 — Smart City

```text
Multiple Cameras
       ↓
Central Detection Pipeline
       ↓
Vehicle Tracking
       ↓
Traffic Database
       ↓
Real-Time Analytics
       ↓
GIS Dashboard
       ↓
Traffic Management
```

---

# ⚠️ Important Limitation

The pixel movement calculated from video is **not automatically real-world speed**.

For example:

```text
Pixel movement = 25 pixels/frame
```

does not directly mean:

```text
25 km/h
```

Accurate speed estimation requires additional information such as:

* Camera calibration
* Perspective transformation
* Known road distances
* Homography
* Real-world reference points

This will be addressed in a later stage of the project.

---

# 📚 Project Outcome

By completing this notebook, you move from:

```text
Raw Video
    ↓
Computer Vision
    ↓
Object Detection
    ↓
Object Tracking
    ↓
Structured Data
    ↓
Traffic Analytics
```

This forms the core computer-vision layer of a future:

> **AI-Powered Smart City Traffic Monitoring System**

---

## ⭐ Future Architecture

```text
                    SMART CITY
                        │
              ┌─────────┴─────────┐
              │                   │
          TRAFFIC CAMERAS      GEO DATA
              │                   │
              ▼                   ▼
        VIDEO PROCESSING      GIS / MAPS
              │                   │
              ▼                   │
        YOLO DETECTION            │
              │                   │
              ▼                   │
        BYTE TRACKING             │
              │                   │
              ▼                   │
       VEHICLE TRAJECTORIES       │
              │                   │
              └─────────┬─────────┘
                        ▼
                 TRAFFIC ANALYTICS
                        │
          ┌─────────────┼─────────────┐
          ▼             ▼             ▼
       Density        Speed       Congestion
          │             │             │
          └─────────────┼─────────────┘
                        ▼
                 🌍 GeoAI Dashboard
```

---

## 👨‍💻 Project Status

**Status:** 🚧 In Development

**Current Stage:**

> Video → Detection → Tracking → CSV

**Next Stage:**

> Vehicle Counting → Line Crossing → Speed → Density → Congestion → GeoAI

---

## ⭐ If You Find This Project Useful

Give the repository a ⭐ and use the notebook to experiment with your own traffic videos.

---

### 🔑 Keywords

`Computer Vision` · `YOLO` · `ByteTrack` · `Object Detection` · `Object Tracking` · `OpenCV` · `Traffic Analytics` · `Vehicle Detection` · `Vehicle Tracking` · `Smart City` · `GeoAI` · `Python` · `Machine Learning` · `Deep Learning`
