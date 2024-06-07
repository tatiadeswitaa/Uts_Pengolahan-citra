# UTS_Pengolahancitra
### Menggunakan Streamlit


| Nama  |  Nim | Kelas |
| ----------------- | ------------- |------------- |
| Muhamad Jati Wasesa      | 312210481 | TI 22 A5 |
| Idris Syahruddin         | 312210467 | TI 22 A5 |
| Dimas Aditya Putranto    | 312210489 | TI 22 A5 |
| Hardi Wirkan             | 312210492 | TI 22 A5 |
| Dzaky Alaudin Malik      | 312210495 | TI 22 A5 |







## Project Web App untuk memanipulasi gambar citra menggunakan Streammlite dengan mengubah 
#### - RGB menjadi HSV
#### - Menghitung Histogram
#### - Brignest dan Contras
#### - Contour

### Kita harus menginstal library yang diperlukan, yaitu Streamlit untuk membuat aplikasi web, OpenCV untuk manipulasi citra, dan Matplotlib untuk menampilkan histogram.

```
pip install streamlit opencv-python matplotlib numpy
pip install opencv-python
pip install matplotlib

```

### Buat file Python (misalnya app.py) dan impor library.

```
import streamlit as st
import cv2
from matplotlib import pyplot as plt
import numpy as np
pip install numpy
```

### Membuat Fungsi Manipulasi Citra, untuk 'Konversi RGB ke HSV'

```
def convert_rgb_to_hsv(image):
    return cv2.cvtColor(image, cv2.COLOR_RGB2HSV)
```

### Menghitung Histogram

```
def plot_histogram(image):
    color = ('b', 'g', 'r')
    for i, col in enumerate(color):
        hist = cv2.calcHist([image], [i], None, [256], [0, 256])
        plt.plot(hist, color=col)
        plt.xlim([0, 256])
    plt.title('Histogram')
    return plt
```

### Mengatur Brightness dan Contrast

```
def adjust_brightness_contrast(image, brightness=0, contrast=0):
    new_image = np.zeros(image.shape, image.dtype)
    alpha = contrast * 0.01
    beta = brightness

    # Adjustment made here
    for y in range(image.shape[0]):
        for x in range(image.shape[1]):
            for c in range(image.shape[2]):
                new_image[y,x,c] = np.clip(alpha*image[y,x,c] + beta, 0, 255)
    
    return new_image
```

### Mendeteksi Kontur

```
def find_contours(image):
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    blurred = cv2.GaussianBlur(gray, (5, 5), 0)
    edged = cv2.Canny(blurred, 50, 150)
    contours, _ = cv2.findContours(edged.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
    image_with_contours = image.copy()
    cv2.drawContours(image_with_contours, contours, -1, (0, 255, 0), 3)
    return image_with_contours
```

### Langkah Selanjutnya Streamlit Interface

```
st.title('Image Manipulation App')

uploaded_file = st.file_uploader("Choose an image...", type=["jpg", "jpeg", "png"])
if uploaded_file is not None:
    file_bytes = np.asarray(bytearray(uploaded_file.read()), dtype=np.uint8)
    image = cv2.imdecode(file_bytes, cv2.IMREAD_COLOR)

    st.image(image, caption='Original Image', use_column_width=True)

    if st.button('Convert RGB to HSV'):
        hsv_image = convert_rgb_to_hsv(image)
        st.image(hsv_image, caption='HSV Image', use_column_width=True)

    if st.button('Show Histogram'):
        plt = plot_histogram(image)
        st.pyplot(plt)

    brightness = st.slider("Brightness", min_value=-100, max_value=100, value=0)
    contrast = st.slider("Contrast", min_value=-100, max_value=100, value=0)
    if st.button('Adjust Brightness and Contrast'):
        bc_image = adjust_brightness_contrast(image, brightness, contrast)
        st.image(bc_image, caption='Brightness and Contrast Adjusted Image', use_column_width=True)

    if st.button('Find Contours'):
        contours_image = find_contours(image)
        st.image(contours_image, caption='Image with Contours', use_column_width=True)
```

### Untuk menjalankan aplikasi, bisa menggunakan terminal CMD dengan perintah :

```
streamlit run app.py
```

![ss citra](https://github.com/Muhjat7/UTSPENGELOLACITRA/assets/129918243/4844b393-eace-4c0a-a8d9-d26e95f4a0b3)


### Dan Hasil run Silahkan pindah ke chrome untuk tampilan nya seperti gamabr di bawah ini :

![sscitra2](https://github.com/Muhjat7/UTSPENGELOLACITRA/assets/129918243/ecee350e-9fc6-4dbf-9cf9-cf02b5b9b411)


### Silakahkan klik browse file dan pilih gambar yang akan di manipulasi 

#### *Gambar Original*

![rev1](https://github.com/Muhjat7/UTSPENGELOLACITRA/assets/129918243/8eee3cb0-a5ee-4a04-ac08-8d0412ae62d3)


#### *RGB menjadi HSV*

![rev2](https://github.com/Muhjat7/UTSPENGELOLACITRA/assets/129918243/1eb52a8a-418e-41a1-a7d1-15f93f933d1a)


#### *hasil gambar menghitung Histogram*

![citra4](https://github.com/Muhjat7/UTSPENGELOLACITRA/assets/129918243/c270de20-1c6e-435a-b84c-40a40dbb77ff)



#### *hasil gambar Contour*

![citra6](https://github.com/Muhjat7/UTSPENGELOLACITRA/assets/129918243/c415ad79-d4b9-4a4a-a051-555930a4a4cd)



### *--------------------------------------- Terimakasih -----------------------------------------------*


