# 🎨 YOLOv5 Object Detection Web Application

📌 **Nama**: Faizal Kurniawan  
📌 **NPM**: 217064516061  
📌 **Kelas**: Pengolahan Citra (R.03)  

Dokumentasi ini menjelaskan langkah-langkah membuat dan menjalankan **Deteksi Objek dengan YOLOv5 dan Streamlit**. Aplikasi ini akan memuat model **YOLOv5**, memproses gambar yang diunggah pengguna, dan menampilkan hasil deteksi objek.

---

## **📂 1. Struktur Folder Proyek**
```
UAS FAIZAL/
├── .venv             # Virtual environment untuk proyek
├── yolov5            # Repository YOLOv5 (di-clone dari GitHub)
├── app.py            # Script utama untuk aplikasi Streamlit
├── requirements.txt  # Daftar library yang dibutuhkan
├── yolov5s.pt        # Model YOLOv5 yang diunduh
```

---

## **⚙️ 2. Instalasi Aplikasi**
### **1️⃣ Install VSCode dan Extensions**
- **Install VSCode** [di sini](https://code.visualstudio.com/).
- Install **extensions berikut** di VSCode:
  - ✅ **Python**
  - ✅ **Streamlit**

### **2️⃣ Install Python dan Virtual Environment**
Pastikan **Python 3.7 atau yang lebih baru** sudah terinstal.  
Buat virtual environment dan aktifkan:

```bash
python -m venv .venv
source .venv/bin/activate  # Untuk Linux/Mac
.\.venv\Scripts\activate   # Untuk Windows
```

---

## **📆 3. Instalasi Dependencies (`requirements.txt`)**
Buat file `requirements.txt` dengan isi berikut:

```
torch
streamlit
pillow
pandas
```

Kemudian, jalankan perintah berikut untuk menginstal semua dependencies:
```bash
pip install -r requirements.txt
```

---

## **🌐 4. Clone Repository YOLOv5**
Untuk mendapatkan YOLOv5, jalankan perintah berikut:
```bash
git clone https://github.com/ultralytics/yolov5.git
```
> **Catatan:** Setelah menjalankan aplikasi pertama kali, model `yolov5s.pt` akan otomatis terunduh ke dalam folder **UAS FAIZAL/**.

---

## **💻 5. Menulis Kode di `app.py`**
Buat file **`app.py`** dan masukkan kode berikut:

```python
import torch
import streamlit as st
import time
from PIL import Image
import numpy as np
import pandas as pd

# Load YOLOv5 pre-trained model dari PyTorch Hub
model = torch.hub.load('ultralytics/yolov5', 'yolov5s', pretrained=True)

st.title("Object Detection with YOLOv5")
st.write("Upload an image for object detection")

# Upload gambar
uploaded_file = st.file_uploader("Choose an image...", type=["jpg", "png", "jpeg"])

if uploaded_file is not None:
    start_time = time.time()

    # Baca gambar dengan PIL
    img = Image.open(uploaded_file)
    img = img.convert("RGB")  # Konversi ke RGB
    img = np.array(img)

    # Deteksi objek dengan YOLOv5
    results = model(img)
    elapsed_time = time.time() - start_time

    # Tampilkan waktu inferensi
    st.write(f"Inference Time: {elapsed_time:.4f} seconds")

    # Render hasil deteksi objek
    results.render()
    st.image(results.ims[0], caption="Detected Objects", use_container_width=True)

    # Ambil hasil deteksi dalam DataFrame
    detections = results.pandas().xywh[0]

    # Tampilkan hasil dalam tabel
    if len(detections) > 0:
        st.write(f"Detected {len(detections)} objects:")
        st.dataframe(detections[['xcenter', 'ycenter', 'width', 'height', 'confidence', 'name']])
    else:
        st.warning("No objects detected in the image")
```

---

## **🚀 6. Menjalankan Aplikasi**
1️⃣ Jalankan perintah berikut di terminal:
```bash
streamlit run app.py
```
2️⃣ **Akses aplikasi** di browser:
```
http://localhost:8501/
```
3️⃣ **Unggah gambar**, dan hasil deteksi objek akan ditampilkan!

---

## **🎨 7. Contoh Hasil Deteksi Objek**
Contoh **screenshot hasil aplikasi**:

![Contoh Screenshot 1](https://github.com/faizalk-github/Proyek-UAS-Pengolahan-Citra/blob/de731e837c94eb473f43de122007e49a5efab9be/SS1.png)

![Contoh Screenshot 2](https://github.com/faizalk-github/Proyek-UAS-Pengolahan-Citra/blob/de731e837c94eb473f43de122007e49a5efab9be/SS2.png)

---

## **📊 8. Evaluasi Kinerja**
📌 **Confidence Score:** Ditampilkan di tabel hasil deteksi.  
📌 **Inference Time:** Ditampilkan di halaman aplikasi.  

**Contoh Output:**
```
Inference Time: 0.0889 seconds
Confidence Score: 0,8 / 80%
```

---

## **🛠️ 9. Teknologi yang Digunakan**
✔️ **Python**  
✔️ **YOLOv5**  
✔️ **Streamlit**  
✔️ **Pandas**  
✔️ **Pillow**  

---

## **📌 10. Kesimpulan**
✅ Aplikasi ini memungkinkan pengguna **mengunggah gambar** dan mendapatkan **deteksi objek secara real-time** dengan YOLOv5.  
✅ **Inference Time & Confidence Score** digunakan sebagai **evaluasi performa**.  
✅ **YOLOv5** terbukti cepat dan akurat dalam mendeteksi objek umum.

---

## **🤝 11. Acknowledgments**
Aplikasi ini menggunakan **Ultralytics YOLOv5** dan Streamlit.

