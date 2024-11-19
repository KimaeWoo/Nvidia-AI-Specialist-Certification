# Title

Pedestrian Signal Detection System Using YOLOv5

---

# Introduction

There are many AI systems designed to assist autonomous driving, but the safety of pedestrians, who are often vulnerable on the road, must also progress alongside these advancements. Crossing a crosswalk by observing pedestrian traffic signals is something most people take for granted. However, it can be challenging for visually impaired individuals to rely on these signals for judgment.

By recognizing red and green lights, this system can warn users when the signal is red, helping to prevent accidents. Therefore, a pedestrian traffic light recognition AI would be highly beneficial for visually impaired individuals.

---

# Getting Video

I personally filmed the traffic lights with a camera based on pedestrians.

https://drive.google.com/file/d/1kTYNL0dp_NbFa0JHGF8kAk8d1qW1VTaK/view?usp=drive_link

https://drive.google.com/file/d/15RlsCy17xYsFmKmfDRIRP7sV4xK4lApV/view?usp=drive_link

https://drive.google.com/file/d/110kz_kcRg88W8BUZFMv9iTLMPJrSsnnw/view?usp=drive_link

https://drive.google.com/file/d/1Ay8WfdIXiCEtiD24UNFgoLWyVGq6aDMk/view?usp=drive_link

https://drive.google.com/file/d/17ThrTrNpC5KSL9nVv0W3rXhCKNeJH0YG/view?usp=drive_link

---

# Project Progress

## 1. Resolution adjustment

The video was produced in a 640x640 resolution.

[Change video](https://online-video-cutter.com/ko/resize-video)

![image](https://github.com/user-attachments/assets/8f2f8ac8-5680-49e4-bc90-bc9a6239e59f)

---

## **2. Class settings

Unzip the DarkLabel2.4.zip file.

[https://drive.google.com/file/d/1dqSHf-FHZo4GdNJDY1dg0cgEp33zzNZc/view?usp=drive_link](https://drive.google.com/file/d/1dqSHf-FHZo4GdNJDY1dg0cgEp33zzNZc/view?usp=drive_link)

Open the darklabel.yml file from the unzipped DarkLabel2.4.zip files to modify the classes of the custom dataset.

![ym](https://github.com/user-attachments/assets/d93e6ec3-dd48-4839-a67f-3bcf02d7415f)

Find my_classes1 and "copy and paste" it.
Then, change the name from "my_classes1" to "my_classes2", modify the names inside the brackets to the desired names, and save the file.

![c](https://github.com/user-attachments/assets/d39c5a78-be9f-42e2-beb1-46a52e6180f7)

Scroll down to find a block named format1.
In this block, locate classes_set and change its value to the custom dataset (my_classes2).
Then, rename it to the desired name (trafficlights).

![%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2024-11-15_211753](https://github.com/user-attachments/assets/ea06be98-2fe6-4327-8a9f-83441210034f)

---

## **3. Image labeling

![%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2024-11-15_2125251](https://github.com/user-attachments/assets/258370d3-061d-4b78-ad61-eacad82380b4)

The DarkLabel program allows you to convert video into images frame by frame.

- Use **Open Video** to select a 640 x 640 resolution video.
- Disable the **labeled frames only** checkbox.
- Use **as images** to save the frames as images inside a folder named **images**.

You can confirm that the images have been placed inside the **images** folder.

![image 1](https://github.com/user-attachments/assets/46e4d1e3-3c8a-425a-99e6-1c63dff88440)


![image 2](https://github.com/user-attachments/assets/4df18537-6a51-4f1d-accf-ded14f250fd1)
 
The transformed images are labeled using DarkLabel.
- Set the **name** to trafficlights.
- You will see that the trafficlights class has been added, and two additional classes are added below it

In DarkLabel, after selecting the images folder through **Open Image Folder**, you loaded the converted images. Then, by selecting **Box + Label**, you performed annotation on the images, matching the appropriate class for each signal as shown in the image.
Once the annotation was complete, you used **GT Save As** to create a **labels** folder and saved the annotated labels inside that folder.

![123](https://github.com/user-attachments/assets/69faefef-87fd-4ac6-a225-9d2d5cce84a6)

---

## 4. Result of Labeling

There are annotation txt files inside the labels folder.

![image 3](https://github.com/user-attachments/assets/ba6142de-a652-40d6-b7f9-e88807bd8691)


### dataset_trafficlights.zip

[https://drive.google.com/file/d/1HPdnRoOBzZWke4vHnRtD3q58zgsKio-r/view?usp=sharing](https://drive.google.com/file/d/1HPdnRoOBzZWke4vHnRtD3q58zgsKio-r/view?usp=sharing)

---

## 5. Learning NVIDIA Jetson Nano

To install Git on the NVIDIA Jetson Nano.

```python
sudo apt-get install git
```

Clone the YOLOv5 repository from GitHub.

```python
git clone https://github.com/ultralytics/yolov5.git
```


### YOLOv5

Go to https://github.com/ultralytics/yolov5 and download the YOLOv5n Model by dropping it down.

![image 4](https://github.com/user-attachments/assets/52bc0d59-628f-46fd-b885-1c455f8e46ff)

In YOLOv5, install pip, a tool that simplifies the installation and management of Python packages.

```python
sudo apt-get install pip
```

After entering the YOLOv5 folder, install all the dependency packages.

```python
pip install -r requirements.txt
```

Place the yolov5n.pt file inside the YOLOv5 folder.

![%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2024-11-15_224641](https://github.com/user-attachments/assets/252a3bae-b4de-443a-a30a-25f29baf5dc6)

Place the images and labels created by DarkLabel inside the train and valid folders, and place only the images inside the test folder. Modify the data.yaml file to match the classes.


### data.yaml

![image 5](https://github.com/user-attachments/assets/044439cc-a4f6-42d8-b733-ca04d418d54a)

```python
python3 train.py --img 640 --batch 16 --epochs 300 --data /home/amap/yolov5/data.yaml --cfg ./models/yolov5n.yaml --weights yolov5n.pt --name trafficlights --patience 0
```

Move to the yolov5 folder and train the YOLOv5 model.

---

## 6. Training results

[https://drive.google.com/file/d/1NoxU0OTbxHcavuQ4_1iSTWhVZiBOCrrw/view?usp=drive_link](https://drive.google.com/file/d/1NoxU0OTbxHcavuQ4_1iSTWhVZiBOCrrw/view?usp=drive_link)

![confusion_matrix](https://github.com/user-attachments/assets/5ddd5f35-b0ff-4605-a3e4-03594a4c4c4f)

**F1_curve**

![F1_curve](https://github.com/user-attachments/assets/6e8f2d7e-da2c-46d1-a870-dbb4f175d4cf)

**PR_curve**

![PR_curve](https://github.com/user-attachments/assets/92e336b5-2cbd-47bd-ae38-75dc0e8ed349)

**P_curve**

![P_curve](https://github.com/user-attachments/assets/d09e21fd-3177-4b1d-8ba7-4239250f6508)

**R_curve**

![R_curve](https://github.com/user-attachments/assets/d6edb5ef-cf78-4968-81d8-b658c0a4b4a1)

**results**

![results](https://github.com/user-attachments/assets/2990594a-c0e2-450e-b21f-a479e3aaae4a)

**train_batch**

![train_batch0](https://github.com/user-attachments/assets/b03b2fed-40e4-48c9-95f9-1125c2809d88)

**val_batch**

![val_batch0_labels](https://github.com/user-attachments/assets/091e2c67-7e49-4760-8ca0-b6acf041b560)

Use the best.pt file to run detect.py and check the training results.

```python
python3 detect.py --weights /home/amap/yolov5/runs/train/trafficlights/weights/best.pt --img 640 --source /home/amap/yolov5/test/images --name trafficlights_detect
```

**Training results through detect.py**

![00000047](https://github.com/user-attachments/assets/3e47392c-3bf0-465f-9c7e-559e3865e5b1)

![00000452](https://github.com/user-attachments/assets/286370d9-c064-4a6b-9854-9b75670dcc60)

![00000207](https://github.com/user-attachments/assets/608dcfb6-3a9d-4603-b08d-6ec2ce9cd28c)

![00000525](https://github.com/user-attachments/assets/8632ccc4-e30f-4e9b-9dd3-d4a544b623ed)

**Video**

```python
python3 detect.py --weights /home/amap/yolov5/runs/train/trafficlights/weights/best.pt --source /home/amap/yolov5/video/vd.mp4  
```

[https://drive.google.com/file/d/1Pl3qyDuGbhlGC-NF-4FxQXB6xFK3YOXv/view?usp=drive_link](https://drive.google.com/file/d/1Pl3qyDuGbhlGC-NF-4FxQXB6xFK3YOXv/view?usp=drive_link)

[https://drive.google.com/file/d/18myvFtzZuim-FDa5yDStlrVW0_nNJaUd/view?usp=drive_link](https://drive.google.com/file/d/18myvFtzZuim-FDa5yDStlrVW0_nNJaUd/view?usp=drive_link)
