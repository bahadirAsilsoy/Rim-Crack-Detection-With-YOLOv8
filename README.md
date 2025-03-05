# Jant Üzerinde Çatlak Tespiti Projesi

Bu proje, jantlar üzerindeki çatlakları tespit etmek için derin öğrenme yöntemleri kullanır. YOLOv8 modeline dayalı segmentasyon eğitimi yaparak, görsellerdeki çatlakları doğru bir şekilde sınıflandırmayı amaçlar.

## Kullanılan Teknolojiler

- **Ultralytics YOLOv8**: Çatlak tespiti için kullanılan derin öğrenme modelidir.
- **Roboflow**: Veri setlerinin yönetilmesi ve modellenmesi için kullanıldı.
- **Python**: Proje Python diliyle yazıldı ve gerekli kütüphaneler kullanıldı.
- **IPython**: Jupyter Notebook üzerinde çalışmayı kolaylaştırır.

## Kurulum

Öncelikle gerekli kütüphaneleri yükleyin:

```python
pip install ultralytics
pip install roboflow
```


## Proje Adımları

### 1. Çalışma Dizininin Belirlenmesi

Mevcut çalışma dizinini belirlemek için aşağıdaki kodu kullanalım.

```python
import os
HOME = os.getcwd()
print(HOME)
```

### 2. Gerekli Kütüphanenin Yüklenmesi

Projede kullanılacak olan ultralytics kütüphanesini yüklemek için aşağıdaki komutu kullanalım.

```python
!pip install ultralytics
```


### 3. Sonuçların Görselleştirilmesi

Eğitim sonuçlarını görselleştirmek için aşağıdaki komut kullanıldı:

```python
Image(filename=f'{HOME}/runs/segment/train2/results.png', width=800)
```

### 3. Çıktının Temizlenmesi ve Kütüphanenin Kontrolü

Çalışma ortamındaki çıktıyı temizlemek ve ultralytics kütüphanesinin doğru şekilde kurulup kurulmadığını kontrol etmek için aşağıdaki kodu kullanalım.

```python
from IPython import display
display.clear_output()

import ultralytics
ultralytics.checks()

```

### 4. YOLO Modelinin İçe Aktarılması

YOLO modelini ve görüntüleri göstermek için gerekli kütüphaneleri içe aktaralım.

```python
from ultralytics import YOLO
from IPython.display import display, Image
```

### 5. Roboflow Kütüphanesinin Yüklenmesi ve Veri Setinin İndirilmesi

Roboflow kütüphanesini yükleyip, eğitim verisini indirmek için aşağıdaki adımları kullanalım.

```python
!pip install roboflow
from roboflow import Roboflow
rf = Roboflow(api_key="egchH4Y73wxoB1ArLk4w")
project = rf.workspace("university-bswxt").project("crack-bphdr")
version = project.version(2)
dataset = version.download("yolov8")
```


### 6. Model Eğitiminin Başlatılması

Model eğitimini başlatmak için aşağıdaki komutu kullanalım. Bu komut, yolov8s-seg.pt modelini kullanarak segmentasyon görevini başlatır.

```python
%cd {HOME}
!yolo task=segment mode=train model=yolov8s-seg.pt data=/content/crack-2/data.yaml epochs=24 imgsz=640 plots=True #yolov8s-seg.pt, yolov8s.pt segment, detect
```


### 7. Eğitim Sonuçlarının Görselleştirilmesi

Eğitim sırasında oluşan karışıklık matrisi görselini görüntülemek için aşağıdaki kodu kullanalım.

```python
%cd {HOME}
Image(filename=f'{HOME}/runs/segment/train2/confusion_matrix.png', width=800)
```
![matris](https://github.com/user-attachments/assets/22e9ee53-04b5-426a-aa4c-3b421fff66d7)

## Sonuçlar

- **1.Jant:**
  
   ![jant 1](https://github.com/user-attachments/assets/c420a0aa-d682-47c6-bbb1-ff8eb27ed29d)


- **2.Jant:**
  
  ![jant 2](https://github.com/user-attachments/assets/5da3a8fb-f99b-478e-b52e-bf6ed9154c39)


**Uyarı:** Bu kodlar Google Colab ortamında çalışacak şekilde tasarlanmıştır. Çalıştırmak için bu ortamda olmanız gerekmektedir. Farklı bir ortamda çalıştırılması durumunda, bazı yollar ve dosya erişimleri düzgün şekilde çalışmayabilir.
