# Neural-Style-Transfer
A style reference image (such as a piece of art by a well-known painter) and a content image are combined using the optimization approach known as neural style transfer to create an output image that resembles the content image but has been "painted" in the manner of the style reference image.
This is done by optimizing the output image to match the style reference image's and the content image's statistics for both content and style. A convolutional network is used to extract these data from the images.
Here we are performing transfer learning on the VGG19 model from Tensorflow's applications library.
We take the pretrained weights of 'block4_conv2' layer of VGG19 as our content_output and 'block1_conv1', 'block2_conv1', 'block3_conv1', 'block4_conv1', 'block5_conv1' layers of VGG19 as our style_output.
On top of the CNN responses in each layer of the network we built a style representation that computes the correlations between the different filter responses, where the expectation is taken over the spatial extend of the input image. These feature correlations are given by the gram matrix:
![image](https://user-images.githubusercontent.com/86003669/202875705-e6dd239e-3955-4967-b563-10efecbaafd0.png)

To generate a texture that matches the style of a given image (Fig 1, style reconstructions), we use gradient descent from a white noise image to find another image that matches the style representation of the original image. This is done by minimizing the mean-squared distance between the entries of the Gram matrix from the original image and the Gram matrix of the image to be generated. ( i.e. we compute content_target and style_target images (i.e. the original image and the artistic rendition/portrait).
Therefore;
Content loss: let ~p and ~x be the original image and the image that is generated and Pl and Fl their respective feature representation in layer l.
![image](https://user-images.githubusercontent.com/86003669/202875710-21496ccb-427b-4131-8881-7bdda735ad20.png)

Style loss: let ~a and ~x be the original image and the image that is generated and Al and Gl their respective style representations in layer l.
![image](https://user-images.githubusercontent.com/86003669/202875714-3552cece-1d4b-4ef4-aaa0-06a874923e87.png)

Total loss:

![image](https://user-images.githubusercontent.com/86003669/202875719-085a9520-5610-4a49-a855-04d854a3e938.png)

α = weight for content_loss
β = weight for style_loss


----------------------------------------------------------------------------------------------------------------------------------------------------------------------
Improving output by Hyperparameters Tuning:

Lr= 0.02
Beta_1 = 0.99
Epsilon=1e-1
Epochs=10
content_weight = 1e-4
style_weight = 1e-2
![image](https://user-images.githubusercontent.com/86003669/202875752-0ecc12ef-5e5f-4fc5-88b6-348a9c3da348.png)


(Caution: Extremely small Lr can lead to local minima problems)
Lr= 0.001 
Beta_1 = 0.99
Epsilon=1e-1
Epochs=50
content_weight = 1e-4
style_weight = 1

![image](https://user-images.githubusercontent.com/86003669/202875762-4c22052d-ccc6-4869-b644-0c7647b941aa.png)


Lr= 0.01
Beta_1 = 0.99
Epsilon=1e-1
Epochs=50
content_weight = 1e-4
style_weight = 1
![image](https://user-images.githubusercontent.com/86003669/202875767-29342086-a93e-42b5-9c6a-eb714ebe6b2e.png)


Lr= 0.01
Beta_1 = 0.99
Epsilon=1e-1
Epochs=50
content_weight = 1e-1
style_weight = 1
![image](https://user-images.githubusercontent.com/86003669/202875783-2c53e456-8e47-4e13-ad5a-077fff8a404d.png)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------
Samples:

Input images:
![image](https://user-images.githubusercontent.com/86003669/202875812-f2e90004-09c0-4f04-bbea-2395c8943579.png)

Input parameters:
Lr= 0.01
Beta_1 = 0.99
Epsilon=1e-1
Epochs=100
content_weight = 1e-1
style_weight = 1

![image](https://user-images.githubusercontent.com/86003669/202875820-675337ad-3f0d-4f16-b1b3-9a06eb762e3c.png)

Similarly, you can experiment with various hyperparameters to get a more realistic style transferred image which over substantial training or accurate hyperparameter selection can lead to an accurate image style transfer as was shown by the result of “Method1_StyleTransfer.ipynb”.



Reference: https://arxiv.org/pdf/1508.06576.pdf
