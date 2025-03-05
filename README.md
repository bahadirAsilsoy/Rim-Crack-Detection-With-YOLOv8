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

### 1. Veri Setinin İndirilmesi

Roboflow kullanarak, jant çatlaklarını tespit etmek için eğitim verisi indirildi.

```python
from roboflow import Roboflow
rf = Roboflow(api_key="YOUR_API_KEY")
project = rf.workspace("university-bswxt").project("crack-bphdr")
version = project.version(2)
dataset = version.download("yolov8")
```

### 2. Modelin Eğitilmesi

YOLOv8 modelini segmentasyon görevine uygun şekilde eğitmek için aşağıdaki komut kullanıldı:

```python
yolo task=segment mode=train model=yolov8s-seg.pt data=/content/crack-2/data.yaml epochs=24 imgsz=640 plots=True
```


### 3. Sonuçların Görselleştirilmesi

Eğitim sonuçlarını görselleştirmek için aşağıdaki komut kullanıldı:

```python
Image(filename=f'{HOME}/runs/segment/train2/results.png', width=800)
```

## Sonuçlar

- **1.Jant:**
  
   ![jant 1](https://github.com/user-attachments/assets/c420a0aa-d682-47c6-bbb1-ff8eb27ed29d)


- **2.Jant:**
  
  ![jant 2](https://github.com/user-attachments/assets/5da3a8fb-f99b-478e-b52e-bf6ed9154c39)
