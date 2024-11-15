# Nvidia AI Specialist Certification

# 주제(Title)

YOLOv5를 이용한 보행자 신호등 인식 시스템

Pedestrian Signal Detection System Using YOLOv5

---

# **개요(Introduction)**

자율주행을 도와주는 AI 시스템이 많이 있다. 도로에서 약자인 보행자들의 안전도 도와주는 것도 같이 발전해야 한다. 보행자 신호등 신호를 보고 횡단보도를 건너는 것은 당연하다. 하지만 시각장애인은 보행자 신호등을 보고 판단하기 어렵다.

빨간불,초록불을 인식하여 빨간불일 때 사용자에게 경고 신호를 제공함으로써 사고를 예방할 수 있다.
따라서 보행자 신호등 인식 AI는 시각장애인들에게 유용할 것이다.

There are many AI systems designed to assist autonomous driving, but the safety of pedestrians, who are often vulnerable on the road, must also progress alongside these advancements. Crossing a crosswalk by observing pedestrian traffic signals is something most people take for granted. However, it can be challenging for visually impaired individuals to rely on these signals for judgment.

By recognizing red and green lights, this system can warn users when the signal is red, helping to prevent accidents. Therefore, a pedestrian traffic light recognition AI would be highly beneficial for visually impaired individuals.

---

# **영상 취득(Getting Video)**

보행자 기준으로 신호등을 카메라로 직접 영상 녹화했다.

I personally filmed the traffic lights with a camera based on pedestrians.

https://drive.google.com/file/d/1kTYNL0dp_NbFa0JHGF8kAk8d1qW1VTaK/view?usp=drive_link

https://drive.google.com/file/d/15RlsCy17xYsFmKmfDRIRP7sV4xK4lApV/view?usp=drive_link

https://drive.google.com/file/d/110kz_kcRg88W8BUZFMv9iTLMPJrSsnnw/view?usp=drive_link

https://drive.google.com/file/d/1Ay8WfdIXiCEtiD24UNFgoLWyVGq6aDMk/view?usp=drive_link

https://drive.google.com/file/d/17ThrTrNpC5KSL9nVv0W3rXhCKNeJH0YG/view?usp=drive_link

---

# 프로젝트 진행(Project Progress)

## 1. ****해상도 조절(Resolution adjustment)

영상은 640x640 해상도로 제작하였다.

The video was produced in a 640x640 resolution.

[비디오 리사이저 - 온라인에서 무료로 비디오 해상도 변경](https://online-video-cutter.com/ko/resize-video)

![image.png](image.png)

---

## **2. 클래스 설정(Class settings)**

DarkLabel2.4.zip 파일의 압축을 풀어준다.

Unzip the DarkLabel2.4.zip file.

[https://drive.google.com/file/d/1dqSHf-FHZo4GdNJDY1dg0cgEp33zzNZc/view?usp=drive_link](https://drive.google.com/file/d/1dqSHf-FHZo4GdNJDY1dg0cgEp33zzNZc/view?usp=drive_link)

사용자 정의 데이터 세트의 클래스를 수정하기 위해 압축해제된 DarkLabel2.4.zip 파일 중 darklabel.yml 파일을 연다. 

Open the darklabel.yml file from the unzipped DarkLabel2.4.zip files to modify the classes of the custom dataset.

![ym.png](ym.png)

my_classes1을 찾아 "복사하여 붙여넣기"를 한다.  
그런 다음 이름을 "my_classes1"에서 "my_classes2"로 변경하고 대괄호 안의 이름들을 사용할 이름으로 변경한 다음 저장한다.

Find my_classes1 and "copy and paste" it.
Then, change the name from "my_classes1" to "my_classes2", modify the names inside the brackets to the desired names, and save the file.

![c.png](c.png)

아래로 스크롤하면 이름이 format1인 블록이 있다.
이 블록에서 classes_set을 확인하고 값을 사용자 정의 데이터 세트(my_classes2)로 변경한다.
원하는 이름(trafficlights)으로 변경한다.

Scroll down to find a block named format1.
In this block, locate classes_set and change its value to the custom dataset (my_classes2).
Then, rename it to the desired name (trafficlights).

![화면 캡처 2024-11-15 211753.png](%25ED%2599%2594%25EB%25A9%25B4_%25EC%25BA%25A1%25EC%25B2%2598_2024-11-15_211753.png)

---

## **3. 이미지 라벨링(Image labeling)**

![화면 캡처 2024-11-15 2125251.png](%25ED%2599%2594%25EB%25A9%25B4_%25EC%25BA%25A1%25EC%25B2%2598_2024-11-15_2125251.png)

DarkLabel 프로그램에서 영상을 프레임 단위로 이미지로 변환할 수 있다. 

- **Open Video**를 통해 640 x 640 해상도 영상을 선택한다.
- **labeled frames only**  체크 표시를 비활성화한다.
- **as images**를 통해 images라는 폴더 안에 이미지로 변환한다.

The DarkLabel program allows you to convert video into images frame by frame.

- Use **Open Video** to select a 640 x 640 resolution video.
- Disable the **labeled frames only** checkbox.
- Use **as images** to save the frames as images inside a folder named **images**.

images 폴더 안에 이미지가 들어온 걸 확인할 수 있다.

You can confirm that the images have been placed inside the **images** folder.

![image.png](image%201.png)

![image.png](image%202.png)

변환된 이미지를 DarkLabel을 통해 라벨링을 한다.

- **name**을 trafficlights로 설정한다.
- trafficlights라는 classes가 추가 되었고 밑에 2개의 class가 추가된 것을 확인할 수 있다

The transformed images are labeled using DarkLabel.

- Set the **name** to trafficlights.
- You will see that the trafficlights class has been added, and two additional classes are added below it

DarkLabel에서 **Open Image Folder**를 통해 images 폴더를 선택하여 변환된 이미지를 불러왔다. **Box + Label**로 선택 후 아래 사진과 같이 해당 class에 부합하는 신호에 Annotation을 했다. Annotation이 끝난 후 **GT Save As**를 통해 **labels**라는 폴더를 만들고 해당 폴더 안에 저장을 했다.

In DarkLabel, after selecting the images folder through **Open Image Folder**, you loaded the converted images. Then, by selecting **Box + Label**, you performed annotation on the images, matching the appropriate class for each signal as shown in the image.

Once the annotation was complete, you used **GT Save As** to create a **labels** folder and saved the annotated labels inside that folder.

![123.png](123.png)

---

## 4. 라벨링 결과 (Result of Labeling)

labels 안에 Annotation한 txt파일이 있다.

There are annotation txt files inside the labels folder.

![image.png](image%203.png)

### dataset_trafficlights.zip

[https://drive.google.com/file/d/1HPdnRoOBzZWke4vHnRtD3q58zgsKio-r/view?usp=sharing](https://drive.google.com/file/d/1HPdnRoOBzZWke4vHnRtD3q58zgsKio-r/view?usp=sharing)

---

## 5. ****NVIDIA Jetson Nano 학습 (Learning NVIDIA Jetson Nano)

Nvidia Jetson Nano에 git을 설치한다. 

To install Git on the NVIDIA Jetson Nano.

```python
sudo apt-get install git
```

YOLOv5 저장소를 GitHub에서  복사(클론)

Clone the YOLOv5 repository from GitHub.

```python
git clone https://github.com/ultralytics/yolov5.git
```

### YOLOv5

[https://github.com/ultralytics/yolov5](https://github.com/ultralytics/yolov5) 에 들어가 아래로 내려 YOLOv5n Model을 다운 받는다.

Go to https://github.com/ultralytics/yolov5 and download the YOLOv5n Model by dropping it down.

![image.png](image%204.png)

YOLOv5에서 python을 쓰는데 Python 패키지들을 쉽게 설치, 관리할 수 있게 해주는 도구인 pip를 설치한다.

In YOLOv5, install pip, a tool that simplifies the installation and management of Python packages.

```python
sudo apt-get install pip
```

yolov5 폴더에 들어간 후 모든 의존성 패키지를 설치

After entering the YOLOv5 folder, install all the dependency packages.

```python
pip install -r requirements.txt
```

yolov5n.pt 파일을 yolov5 폴더 안에 넣는다

Place the yolov5n.pt file inside the YOLOv5 folder.

![스크린샷 2024-11-15 224641.png](%25EC%258A%25A4%25ED%2581%25AC%25EB%25A6%25B0%25EC%2583%25B7_2024-11-15_224641.png)

train, valid 폴더 안에는 DarkLabel에서 만든 images와 labels 넣고 test에는 images만 넣는다. 
data.yaml 파일을  classes에 맞게 파일을 수정한다.
Place the images and labels created by DarkLabel inside the train and valid folders, and place only the images inside the test folder. Modify the data.yaml file to match the classes.

### data.yaml

![image.png](image%205.png)

```python
python3 train.py --img 640 --batch 16 --epochs 300 --data /home/amap/yolov5/data.yaml --cfg ./models/yolov5n.yaml --weights yolov5n.pt --name trafficlights --patience 0
```

yolov5 폴더로 이동하고 YOLOv5 모델을 학습시킨다.

Move to the yolov5 folder and train the YOLOv5 model.

---

## 6. Training results

[https://drive.google.com/file/d/1NoxU0OTbxHcavuQ4_1iSTWhVZiBOCrrw/view?usp=drive_link](https://drive.google.com/file/d/1NoxU0OTbxHcavuQ4_1iSTWhVZiBOCrrw/view?usp=drive_link)

![confusion_matrix.png](confusion_matrix.png)

**F1_curve**

![F1_curve.png](F1_curve.png)

**PR_curve**

![PR_curve.png](PR_curve.png)

![labels.jpg](labels.jpg)

**P_curve**

![P_curve.png](P_curve.png)

**R_curve**

![R_curve.png](R_curve.png)

**results**

![results.png](results.png)

**train_batch**

![train_batch0.jpg](train_batch0.jpg)

**val_batch**

![val_batch0_labels.jpg](val_batch0_labels.jpg)

 best.pt를 활용하여 detect.py를 진행해 학습 결과를 확인

Use the best.pt file to run detect.py and check the training results.

```python
python3 detect.py --weights /home/amap/yolov5/runs/train/trafficlights/weights/best.pt --img 640 --source /home/amap/yolov5/test/images --name trafficlights_detect
```

**detect.py를 통한 학습 결과 (**Training results through detect.py**)**

![00000047.png](00000047.png)

![00000452.png](00000452.png)

![00000207.png](00000207.png)

![00000525.png](00000525.png)

**영상(Video)**

```python
python3 detect.py --weights /home/amap/yolov5/runs/train/trafficlights/weights/best.pt --source /home/amap/yolov5/video/vd.mp4  
```

[https://drive.google.com/file/d/1Pl3qyDuGbhlGC-NF-4FxQXB6xFK3YOXv/view?usp=drive_link](https://drive.google.com/file/d/1Pl3qyDuGbhlGC-NF-4FxQXB6xFK3YOXv/view?usp=drive_link)

[https://drive.google.com/file/d/18myvFtzZuim-FDa5yDStlrVW0_nNJaUd/view?usp=drive_link](https://drive.google.com/file/d/18myvFtzZuim-FDa5yDStlrVW0_nNJaUd/view?usp=drive_link)