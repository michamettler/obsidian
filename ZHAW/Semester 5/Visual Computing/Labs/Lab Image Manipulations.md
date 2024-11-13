#visualcomputing  #sem5 
## Task 1
To decide whether the the image is truly black, let's take a closer look at it. Opening it on an IPS panel already indicates that it isn't and that it contains a picture of Lena. However, for a more substantial analysis, we will open it in GIMP.

![[Pasted image 20241111181017.png]]
The histogram already shows that there are other colors present than just deep black.

In the next step we adjust the contrast and brightness to achieve a result where it's clearly visible that the picture isn't just black:
![[Pasted image 20241111181536.png]]
___
## Task 2
The color image chosen contains the following properties:
![[Pasted image 20241111182406.png]]
Here we can see the size of it and that it contains colors, as the image depth is 24 ($3 * 8$ for RGB).
![[Pasted image 20241111182728.png]]
Furthermore, the histogram shows that the green colors lie somewhere in the middle, meaning that they are well-balanced (not too dark or light). The blue tones however lie on the right side of the histogram, representing the rather light blue of the sky.

The red colors on the black axis probably originate from some mixed colors of the picture.
___
## Task 3
Some manipulations:
### Invert
![[Pasted image 20241111183301.png]]
## High Contrast
![[Pasted image 20241111183347.png]]
I think what's interesting here is that the distribution of the histogram decreases and focuses on a few less colors as the pictuure now emphasizes strong light and dark areas.
## Binary Image
![[Pasted image 20241111184507.png]]
From my understanding the dynamic range stays the same (0-255), the contrast however changes to its maximum as there are only two possible colors (black or white). This also means that if a picture is already binary (just black and white), the contrast cannot be improved any further.