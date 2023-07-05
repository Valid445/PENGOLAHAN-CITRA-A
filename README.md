
# UAS PENGOLAHAN CITRA

pada kali ini kami diberikan projek dan saya mendapatkan sebauh projek yang diberi judul "deteksi bentuk gambar menggunakan garis contour"

berikut penjelasan dari codingan saya:

untuk mengimport library saya biasa menggunakan 
"import cv2
import numpy as np
import matplotlib.pyplot as plt
from skimage import measure"

selanjutnya saya akan menjalankan fungsi path
"def detect_shapes(image_path):
    image = cv2.imread(image_path)
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    _, thresh = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY)
    contours, _ = cv2.findContours(thresh, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
    
    shapes = []

    for contour in contours:
        num_corners = len(contour)
        if num_corners >= 8 and num_corners <= 23:
            shapes.append("Circle")
        elif num_corners == 3:
            shapes.append("Triangle")    
        elif num_corners == 4:
            shapes.append("Square" if cv2.isContourConvex(contour) else "Rectangle")       
        else:
            shapes.append("Polygon")
    
    return shapes"

yang gunanya untuk menerima path gambar, membaca gambar, mengonversi gambar ke skala abu-abu melakukan thresholding dan melakukan iterasi seperti menghitung dan memeriksa kontur sampai ia akan diproses untuk mendefenisikan gambar 

"image_path = 'gambar.jpg'" funsinya untuk memasukan gambar yang akan 
diproses kedalam codingan 

setelah kita memasukan gambar yang akan kita proses selanjutnya kita akan menjalankan fungsi untuk mendeteksi garis kontur yang guna untuk mengetahui contur-contur dari gambar tersebut
"for shape in detected_shapes:
    print(shape)

image = cv2.imread(image_path)
image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

gray = cv2.cvtColor(image, cv2.COLOR_RGB2GRAY)
_, thresh = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY)
contours = measure.find_contours(thresh, 0.5)

image_with_contour_pattern = np.ones_like(image) * 255
for contour in contours:
    contour = np.around(contour).astype(np.int32)
    cv2.drawContours(image_with_contour_pattern, [contour], -1, (0, 0, 0), thickness=cv2.FILLED)

image_with_contour = np.copy(image)
for contour in contours:
    contour = np.around(contour).astype(np.int32)
    cv2.polylines(image_with_contour, [contour], True, (255, 0, 0), thickness=2)
"

setelah gambar terdefenisi kita selanjutnya akan menampilkan gambarnya dan untuk mengecek gambar tersebut
"fig, axes = plt.subplots(1, 3, figsize=(12, 4))
axes[0].imshow(image)
axes[0].set_title('Gambar Asli')
axes[0].axis('off')
axes[1].imshow(image_with_contour_pattern, cmap='gray')
axes[1].set_title('Gambar Countour')
axes[1].axis('off')
axes[2].imshow(image)
axes[2].imshow(image_with_contour, alpha=0.5)
axes[2].set_title('Gambar Asli Dengan Contour')
axes[2].axis('off')
plt.tight_layout()
plt.show()" untuk menampilkan gambar asli, gambar dengan pola kontur, gambar asli dengan kontur yang ditampilkan transparan



