# CVFX HW1 Report  - Team 16 
## Members: 王科鈞 104062226, 鄭凱文 104062223, 王鴻鈞 104062332
### 1. Training CycleGAN
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

### 2. Inference CycleGAN in personal image
* Apple-to-Orange, taken by our team member (from left to right):
<p align="center">
<img src="https://imgur.com/PRyCmG1.jpg" width="300">
</p>

* Orange-to-Apple, taken by our team member (from left to right):
<p align="center">
<img src="https://imgur.com/DJq3mOc.jpg" width="300">
</p>


---
### 3. Compare with other method - UNIT
Reference - **UNIT**: **UN**supervised **I**mage-to-image **T**ranslation Networks [[Paper](https://arxiv.org/abs/1703.00848)] [[Code](https://github.com/mingyuliutw/UNIT)]<br>
* Analysis - from their network design
![
](https://i.imgur.com/ZL9fT6R.png)

    * Unlike the CycleGAN, UNIT adopts a shared latent space which helps the Encoders and Decoders so as to gain the common features from the two input paired or unpaired images. As you can see in figure(a), the latent **z** represents the shared space among all latents.<br>
    * The Decoder & Encoder model architecture mixed with GAN has some pros and cons. 
        - Pros  
                - Many features can be reserved from the images by the Encoders and Decoders.<br>
                - Generator which takes the Decoder's role can extract the information from the images directly, unlike other GANs whichs seperate individually in their models. 

        - Cons  
                - Encoder and Decoder may lead the GAN to be an unimodel that contradicts to their unsupervised purpose (however, this problem has been solved by their nexy model, MUNIT). <br>
                - When we train the Encoder and Decoder, we may sometimes encounter the paddle point problem, which adds more difficulties to the model training process. 

* Analysis - from the photo-transfer result
    * Apple-to-Orange (from left to right):<br>
<img src="https://imgur.com/kvHsF8E.jpg" width="250" ><img src="https://imgur.com/V2thDgV.jpg" width="250" > <img src="https://imgur.com/52fk3MB.jpg" width="250" ><br>
When tranfering apple to orange, it could hardly remove the stem. We think this might be its unavoidable defect.<br> Besides, the most drawback is that the background entirely changes, from white to black. We guess the reason might be that the network structure we adopt for UNIT here is based on season-transfer (summer to winter). Therefore, model's parameters are fine tuned for transfering season - a large scale transfer. Nonetheless, we don't have enough time to tune it well, so the final result is not good. We infer the reason is that maybe transfering season is focous on the big scale background, so that those parts whose color keeps appearing is easily chosen to be victim block and transfered to another color. That is why the background in UNIT testcases turns into black. 

	* Orange-to-Apple (from left to right):<br>
<img src="https://imgur.com/iUVkmRo.jpg" width="250" ><img src="https://imgur.com/yYWPkZ5.jpg" width="250" > <img src="https://imgur.com/c0qKLFU.jpg" width="250" ><br>
When doing orange-toapple operation, there is some problem happened above, but it is better than UNIT's apple-to-orange case. The UNIT does transfer some feature of the apple, like stem and smooth appearance. It still has the same drawbacks as the apple-to-orange case.
    * Test Apple-to-Orange-to-Apple:
        <p align="center">
        [cycleGAN]<br>
        <img src="https://imgur.com/OJKWKs5.jpg" width="300" > <b>=></b> <img src="https://i.imgur.com/zQAyBjC.png" width="300" ><br></p>
        <p align="center">
        [UNIT]<br>
        <img src="https://imgur.com/V2thDgV.jpg" width="300" > <b>=></b> <img src="https://i.imgur.com/a8VPjZl.png" width="300" ><br></p>
        For this A-B-A transfer test, we expect the input and final output should be exactly the same. Here we can find that when using CycleGAN, it does well, except a little blurred. However, while using UNIT, it can hardly seperate the item and the background due to apple's shadow, so that the pulp part losses its original shape and becomes mixed with the background. This result supports the achievement of cycleGAN's special design.
        
