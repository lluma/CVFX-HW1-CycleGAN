# CVFX HW1 Report  - Team 16 

### 1. Training cycle GAN
* Dataset: apple2orange
* Platform: WIndows10 with NVIDIA GTX1080Ti
* Training time: 24hr 22min 07sec
* Training screenshot: (0% ~ 100%)
<p align="center">
<img src="https://imgur.com/aHeIJJq.jpg" width="1000">
<img src="https://imgur.com/UOIaO6I.jpg" width="1000">
</p>
	
* Test result, using default test photos: 
	* Apple-to-Orange (from left to right):<br>
    <p align="center">
    <img src="https://imgur.com/zErw4hy.jpg" width="300" ><img src="https://imgur.com/OJKWKs5.jpg" width="300" > <img src="https://imgur.com/W2owVm9.jpg" width="300" >
    <br></p>

	* Orange-to-Apple (from left to right):<br>
    <p align="center">
    <img src="https://imgur.com/DUqGweW.jpg" width="300" ><img src="https://imgur.com/odnMh6I.jpg" width="300" > <img src="https://imgur.com/hF9GOHf.jpg" width="300" >
    <br></p>


---

### 2. Inference cycleGAN in personal image
* Apple-to-Orange, taken by our team member:
<p align="center">
<img src="https://imgur.com/PRyCmG1.jpg" width="300">
</p>

* Orange-to-Apple, taken by our team member:
<p align="center">
<img src="https://imgur.com/DJq3mOc.jpg" width="300">
</p>


---
### 3. Compare with other method - UNIT
Reference - **UNIT**: **UN**supervised **I**mage-to-image **T**ranslation Networks [[Paper](https://arxiv.org/abs/1703.00848)] [[Code](https://github.com/mingyuliutw/UNIT)]<br>
* Analysis - from their network design
![
](https://i.imgur.com/ZL9fT6R.png)

    * Unlike the CycleGAN, UNIT emphasizes a shared latent space which helps the Encoders and Decoders to gain the common features from the two input paired or unpaired images. As you can see in figure(a), the latent **z** represents the shared space among all latents. 
    * The Decoder&Encoder model architecture mixed with GAN has some pros and cons. 
        - Pros
                - Many features can be reserved from the images by the Encoders and Decoders.
                - Generator takes the Decoder's role can extract the info. from the images directly, not like other GANs seperate individually in their models. 

        - Cons  
                - Encoder and Decoder may lead the GAN to be an unimodel that contradicts to their unsupervised purpose. (But this problem has been solved by their nexy model, MUNIT)
                - When we train the Encoder and Decoder, we may sometimes encounter the paddle point problem, which add some difficulties to the whole model training. 

* Analysis - from the photo-transfer result
    * Apple-to-Orange (from left to right):<br>
<img src="https://imgur.com/kvHsF8E.jpg" width="250" ><img src="https://imgur.com/V2thDgV.jpg" width="250" > <img src="https://imgur.com/52fk3MB.jpg" width="250" ><br>
When tranfering apple to orange, it always cannot remove the stem. We think that it is the part that cannot avoid. Besides, it is obvious that the background changed from white to black, beacause the network structure for UNIT here is based on season-transfer (summer to winter). Therefore, the parameter they used is fine tuned for ttransfering season. However, we have no enough time to fine tune these parameter, so the result of directly training is not really good. We infer the reason is that maybe transfering season is focous on the big scale background, so that the part whose color keep appearing is easly chosen to be victim block and be transfered to another color. It is the reason that the background transfered to black because of the white huge area. 

	* Orange-to-Apple (from left to right):<br>
<img src="https://imgur.com/iUVkmRo.jpg" width="250" ><img src="https://imgur.com/yYWPkZ5.jpg" width="250" > <img src="https://imgur.com/c0qKLFU.jpg" width="250" ><br>
Transfering orange to apple, there is some problem happened above, but it is little better than Transfering apple to orange. The UNIT does transfer some feature of the apple, like stem and smooth appearance.
    * Test Apple-to-Orange-to-Apple:
        <p align="center">
        [cycleGAN]<br>
        <img src="https://imgur.com/OJKWKs5.jpg" width="300" > <b>=></b> <img src="https://i.imgur.com/zQAyBjC.png" width="300" ><br></p>
        <p align="center">
        [UNIT]<br>
        <img src="https://imgur.com/V2thDgV.jpg" width="300" > <b>=></b> <img src="https://i.imgur.com/a8VPjZl.png" width="300" ><br></p>
        For this A-B-A transfer test, we want the input and final output should be exactly the same. Here we can find that when using cycleGAN, it does well, except a little blurred. However, while using UNIT, it cannot seperate the item and the background accurately due to apple's shadow, so that the pulp part losses its original shape. This result supports the achievement of cycleGAN's special design.
        
