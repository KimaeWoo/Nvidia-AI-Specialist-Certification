# Title

Pedestrian Signal Detection System Using YOLOv5

---

# Introduction

There are many AI systems designed to assist autonomous driving, but the safety of pedestrians, who are often vulnerable on the road, must also progress alongside these advancements. Crossing a crosswalk by observing pedestrian traffic signals is something most people take for granted. However, it can be challenging for visually impaired individuals to rely on these signals for judgment.

By recognizing red and green lights, this system can warn users when the signal is red, helping to prevent accidents. Therefore, a pedestrian traffic light recognition AI would be highly beneficial for visually impaired individuals.

---

# Getting Video

I personally filmed the traffic lights with a camera based on pedestrians.

https://github.com/KimaeWoo/Nvidia-AI-Specialist-Certification/tree/main/videos

---

# Project Progress

## 1. Resolution adjustment

The video was produced in a 640x640 resolution.

[Change video](https://online-video-cutter.com/ko/resize-video)

![image](https://github.com/user-attachments/assets/8f2f8ac8-5680-49e4-bc90-bc9a6239e59f)

---

## 2. Class settings

Unzip the DarkLabel2.4.zip file.

[https://drive.google.com/file/d/1dqSHf-FHZo4GdNJDY1dg0cgEp33zzNZc/view?usp=drive_link](https://drive.google.com/file/d/1dqSHf-FHZo4GdNJDY1dg0cgEp33zzNZc/view?usp=drive_link)

Open the darklabel.yml file from the unzipped DarkLabel2.4.zip files to modify the classes of the custom dataset.

![ym](https://github.com/user-attachments/assets/d93e6ec3-dd48-4839-a67f-3bcf02d7415f)

Find my_classes1 and "copy and paste" it.
Then, change the name from "my_classes1" to "my_classes2", modify the names inside the brackets to the desired names, and save the file.

![class](https://github.com/user-attachments/assets/c2206a42-c21b-44bf-a675-021f2a4b58c4)

Scroll down to find a block named format1.
In this block, locate classes_set and change its value to the custom dataset (my_classes2).
Then, rename it to the desired name (trafficlights).

![label](https://github.com/user-attachments/assets/ac01090d-6319-4f2d-b7ac-8dec740b7b20)

---

## **3. Image labeling

![openvideo](https://github.com/user-attachments/assets/0593b365-0fab-434f-8303-d8d219ab103d)

The DarkLabel program allows you to convert video into images frame by frame.

- Use **Open Video** to select a 640 x 640 resolution video.
- Disable the **labeled frames only** checkbox.
- Use **as images** to save the frames as images inside a folder named **images**.

You can confirm that the images have been placed inside the **images** folder.

![image](https://github.com/user-attachments/assets/3e336287-c340-4438-bac2-f3355a3d6acc)

![clc](https://github.com/user-attachments/assets/9c5c6356-da87-45d1-9818-dd85e1892e21)

The transformed images are labeled using DarkLabel.
- Set the **name** to trafficlights.
- You will see that the trafficlights class has been added, and two additional classes are added below it

In DarkLabel, after selecting the images folder through **Open Image Folder**, you loaded the converted images. Then, by selecting **Box + Label**, you performed annotation on the images, matching the appropriate class for each signal as shown in the image.
Once the annotation was complete, you used **GT Save As** to create a **labels** folder and saved the annotated labels inside that folder.

![openim](https://github.com/user-attachments/assets/7a18b061-bcf0-40e1-a0fd-b88575643879)

---

## 4. Result of Labeling

There are annotation txt files inside the labels folder.

![label](https://github.com/user-attachments/assets/766ab722-fe75-4899-8613-fddb25c66762)

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

![cl](https://github.com/user-attachments/assets/cd84cc75-d861-4cc1-ab21-75622e04c5e1)

```python
python3 train.py --img 640 --batch 16 --epochs 300 --data /home/amap/yolov5/data.yaml --cfg ./models/yolov5n.yaml --weights yolov5n.pt --name trafficlights --patience 0
```

Move to the yolov5 folder and train the YOLOv5 model.

---

## 6. Training results

https://github.com/KimaeWoo/Nvidia-AI-Specialist-Certification/tree/main/train_result

![confusion_matrix](https://github.com/user-attachments/assets/4c7f8057-4ad1-469c-9725-13e0ceb629cb)

**F1_curve**

![F1_curve](https://github.com/user-attachments/assets/65989efd-5ae0-4d21-89b9-c59124400e30)

**PR_curve**

![PR_curve](https://github.com/user-attachments/assets/a7749a90-5042-4e5d-9896-674a379b7613)

**P_curve**

![P_curve](https://github.com/user-attachments/assets/f0c80809-9e40-41c7-965a-f51432484e83)

**R_curve**

![R_curve](https://github.com/user-attachments/assets/2e1d43a9-d687-4c37-90ce-980ef7595f57)

**results**

![results](https://github.com/user-attachments/assets/72deb542-e177-4b6f-a1ac-394bbdd9dc69)

**train_batch**

![train_batch0](https://github.com/user-attachments/assets/b0698b34-be9d-4042-aeb8-a3ec92463601)

**val_batch**

![val_batch0_labels](https://github.com/user-attachments/assets/a9dbdf6a-21c3-43ad-9b89-8f799d8ecbbb)

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
