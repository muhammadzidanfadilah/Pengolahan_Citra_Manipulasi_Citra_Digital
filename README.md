# Pengolahan_Citra_Manipulasi_Citra_Digital

# File pdf di bawah ini
[312210277_Muhammad Zidan Fadillah_TI.22.A.2_Pengolahan Citra_Manipulasi Citra Digital,.pdf](https://github.com/muhammadzidanfadilah/Pengolahan_Citra_Manipulasi_Citra_Digital/files/15105610/312210277_Muhammad.Zidan.Fadillah_TI.22.A.2_Pengolahan.Citra_Manipulasi.Citra.Digital.pdf)




| Link Pdf: | https://drive.google.com/file/d/18s8exywiFfiHOlrAj3f1b2o7rqHv29O8/view?usp=sharing |
| --- | --- |

# Modul
```
import cv2
```

# Original Image
```
image = cv2.imread('many fruits.png') 
imagecopy= image.copy()
cv2.imshow( 'Original image' , image )
cv2.waitKey(0)
cv2.destroyAllWindows()
```
![image](https://github.com/muhammadzidanfadilah/Pengolahan_Citra_Manipulasi_Citra_Digital/assets/115553474/a6a2051f-dad3-4736-8550-3ba94c97b3a9)



# gray
```
gray_image = cv2.cvtColor(image,cv2.COLOR_BGR2GRAY)
cv2.imshow( 'gray' , gray_image )
cv2.waitKey(0)
cv2.destroyAllWindows()
```
![image](https://github.com/muhammadzidanfadilah/Pengolahan_Citra_Manipulasi_Citra_Digital/assets/115553474/4798d3be-c5b6-430c-99fb-fde6e4e2f0aa)



#	binary
```
ret,binary_im = cv2.threshold(gray_image,245,255,cv2.THRESH_BINARY)
cv2.imshow( 'binary' , binary_im )
cv2.waitKey(0)
cv2.destroyAllWindows()
```
![image](https://github.com/muhammadzidanfadilah/Pengolahan_Citra_Manipulasi_Citra_Digital/assets/115553474/57c5ec9d-629d-44c5-a953-255be3a71483)



#	inverted binary
```
binary_im= ~binary_im
cv2.imshow( 'inverted binary' , binary_im )
cv2.waitKey(0)
cv2.destroyAllWindows()
```
![image](https://github.com/muhammadzidanfadilah/Pengolahan_Citra_Manipulasi_Citra_Digital/assets/115553474/ed8b471b-3297-4d29-80d8-a040343814bf)



```
contours,hierarchy cv2.findContours(binary_im,cv2.RETR_EXTERNAL,cv2.CHAIN_APPROX_SIMPLE)
```


#	contours marked on RGB image
```
with_contours = cv2.drawContours(image,contours,-1,(0,0,255),3) 
cv2.imshow( 'contours marked on RGB image' , with_contours )
cv2.waitKey(0)
cv2.destroyAllWindows()
```
![image](https://github.com/muhammadzidanfadilah/Pengolahan_Citra_Manipulasi_Citra_Digital/assets/115553474/88d79581-daa8-4cff-b4a2-4f8e844e7d12)



#	Refrence image
```
ref_image = cv2.imread('bananaref.png')
cv2.imshow( 'Reference image' , ref_image )
cv2.waitKey(0)
cv2.destroyAllWindows()
```
![image](https://github.com/muhammadzidanfadilah/Pengolahan_Citra_Manipulasi_Citra_Digital/assets/115553474/6add24ff-b744-4df1-b7fa-9a5306037534)


#	Grayscale image
```
gray_image = cv2.cvtColor(ref_image,cv2.COLOR_BGR2GRAY)
cv2.imshow( 'Grayscale image' , gray_image )
cv2.waitKey(0)
cv2.destroyAllWindows()
```
![image](https://github.com/muhammadzidanfadilah/Pengolahan_Citra_Manipulasi_Citra_Digital/assets/115553474/6ae16e63-4ee8-499d-871e-b6ed065790f1)



#	Binary image
```
ret,binary_im = cv2.threshold(gray_image,245,255,cv2.THRESH_BINARY)
cv2.imshow( 'Binary image' , binary_im )
cv2.waitKey(0)
cv2.destroyAllWindows()
```
![image](https://github.com/muhammadzidanfadilah/Pengolahan_Citra_Manipulasi_Citra_Digital/assets/115553474/2c4442d2-2c63-473e-a414-6fc963381601)



#	inverted binary image
```
binary_im= binary_im
cv2.imshow( 'inverted binary image' , binary_im )
cv2.waitKey(0)
cv2.destroyAllWindows()
```
![image](https://github.com/muhammadzidanfadilah/Pengolahan_Citra_Manipulasi_Citra_Digital/assets/115553474/af1b1183-8827-4c4d-8cb6-404919d1be5e)



#	Contours marked on RGB image
```
reference_contour = contours[0]
```
![image](https://github.com/muhammadzidanfadilah/Pengolahan_Citra_Manipulasi_Citra_Digital/assets/115553474/0eb4080f-e8d8-46f8-9c0a-5e67461fb31e)



```
#Buat list kosong untuk menyimpan hasil perbandingan
dist_list = []
#Loop melalui setiap kontur dalam contours
for cnt in contours:
    # Hitung kesamaan bentuk antara kontur saat ini dan reference_contour
    retval = cv2.matchShapes(cnt, reference_contour, 1, 0)
    # Tambahkan hasil ke dalam list dist_list
    dist_list.append(retval)
```

```
sorted_list= dist_list.copy()
sorted_list.sort() # sorts the list from smallest to largest
ind1_dist= dist_list.index(sorted_list[0])
ind2_dist= dist_list.index(sorted_list[1])
```

```
banana_cnts= []
banana_cnts.append(contours[ind1_dist])
banana_cnts.append(contours[ind2_dist])
with_contours = cv2.drawContours(image,banana_cnts,-3,(255,2,0),3)
```

```
cv2.imshow( 'contours marked on RGB image' , with_contours )
cv2.waitKey(0)
cv2.destroyAllWindows()
```
![image](https://github.com/muhammadzidanfadilah/Pengolahan_Citra_Manipulasi_Citra_Digital/assets/115553474/59bfd9d3-f96d-43a4-b657-35134ab1b686)



#	Upright banana marked on RGB image
```
for cnt in banana_cnts:
    x, y, w, h = cv2.boundingRect(cnt)
    if h > w:
        # Calculate the center and radius of the circle
        center = (x + w // 2, y + h // 2)
        radius = max(w, h) // 2
        # Draw the circle
        cv2.circle(imagecopy, center, radius, (255, 0, 0), 5)

cv2.imshow('Upright banana marked on RGB image', imagecopy)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
![image](https://github.com/muhammadzidanfadilah/Pengolahan_Citra_Manipulasi_Citra_Digital/assets/115553474/7c18b559-3051-48b1-b60a-ebe2d0920fbd)










