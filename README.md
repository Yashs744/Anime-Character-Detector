# Anime-Character-Detector
Anime or sometimes known as Japanimation is hand-drawn or computer animation associated with Japan. Anime Characters are specially designed according to the requirements of the shows and are extremely difficult to draw. Animators spend most of their time in designing the eyes of the character, each anime character has different key features that make them special.

I have used VGG19 model training on ImageNet. ImageNet is a dataset of nearly 1M Images divided into nearly ~1000 Categories. One such category is Humans (Person) and as Anime Character resembles human it gets really hard to differentiate them from one another just using the Images. To tackle this I used different approaches, one of them was to take the pre-trained vgg19 model and remove all the layers after the last max-pooling layers and add GlobalAveragePooling and Dense Layers.

## Dataset
I collected a total of 820 medium size images using google and other resources to train the model. 

  * ### Categories: 
     - **anime**<br>
        Contained different images of anime characters, some were full body images, some only faces and some only the upper half of the body.        
      - **not_anime**<br>
        Contained images of cartoon characters and humans to force the model to classify humans as an anime character
        
## Model
Pre-Trained VGG19 Model with ImageNet Weights.
I freezed the VGG19 Model till __block5_pool__ layer and added `GlobalAveragePooling`, `Dropout` and `Dense` Layers.

                              Layer (type)                 Output Shape              Param #   
                              =================================================================
                              global_avg_pooling (GlobalAv (None, 512)               0         
                              _________________________________________________________________
                              dropout_1 (Dropout)          (None, 512)               0         
                              _________________________________________________________________
                              dense_1 (Dense)              (None, 256)               131328    
                              _________________________________________________________________
                              dropout_2 (Dropout)          (None, 256)               0         
                              _________________________________________________________________
                              dense_2 (Dense)              (None, 128)               32896     
                              _________________________________________________________________
                              dropout_3 (Dropout)          (None, 128)               0         
                              _________________________________________________________________
                              output (Dense)               (None, 2)                 258       
                              =================================================================
                              Total params: 20,188,866
                              Trainable params: 164,482
                              Non-trainable params: 20,024,384
                              _________________________________________________________________
> Download the Trainined [Model](https://drive.google.com/open?id=1oHLyBF4bIOTZDY3Ou75tDgiPKw0SZzGG)

## Training & Testing:
**Loss Function:** Binary CrossEntropy<br>
**Optimizer:** Adam<br>
**Metrics:** Accuracy<br>

Batch Size: 32<br>
Epochs: 10

**Training:**
  - Data Size: 697 (224 x 224 x 3) Images
  - Labels: 2 - Anime & Not Anime
  
  <p align="center">
    <b> Training</b><br>
    <img src = "https://github.com/Yashs744/Anime-Character-Detector/blob/master/images/train.png", alt = "Training"/>
  </p>
   

**Testing:**
  - Data Size: 123 (224 x 224 x 3) Images
  - Labels: 2 - Anime & Not Anime
  
  <p align="center">
    <b> Testing</b><br>
    <img src = "https://github.com/Yashs744/Anime-Character-Detector/blob/master/images/test.png", alt = "Testing"/>
  </p>
  
## Evaluate
I create a function to make predictions, it takes image as an input and returns image and label (anime or not_anime) along with probabilities.

  <p align="center">
    <img src = "https://github.com/Yashs744/Anime-Character-Detector/blob/master/images/Test_1.png", alt = "Test 1"/>
    <img src = "https://github.com/Yashs744/Anime-Character-Detector/blob/master/images/Test_3.png", alt = "Test 3"/>
  <img src = "https://github.com/Yashs744/Anime-Character-Detector/blob/master/images/Test_2.png", alt = "Test 3"/>
  </p>

