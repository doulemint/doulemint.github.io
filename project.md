---
layout: page
title: Project
---

<style>
.grid::after {
    content: '';
    display: block;
    clear: both;
  }
.grid-item {
    float: left;
    width: 320px;
	height: 305px;
    margin: 20px;
	margin-right: 20px;
	margin-bottom: 1rem;
	padding: 1rem;
	color: #717171;
	background-color: #f9f9f9;
  }
span{
  display: block;
  float: right;
}
</style>
<div class="grid" id="top">
	<div class="grid-item">
		
		<img src="https://collectionapi.metmuseum.org/api/collection/v1/iiif/459112/913523/main-image" width = "300" height = "200" alt="PaintingUnderstanding" align=center />
		<p class="anchorlink"><a href="#a">Painting  Understanding</a></p>
	</div>
	
	<div class="grid-item">
		
		<img src="https://images.squarespace-cdn.com/content/v1/5a4e3a9ee9bfdf1654db3b34/1516107940056-5HC9GT0GXPOUREJNRQBQ/ke17ZwdGBToddI8pDm48kOocpZx0xlvWaMfujuqmZxF7gQa3H78H3Y0txjaiv_0fDoOvxcdMmMKkDsyUqMSsMWxHk725yiiHCCLfrh8O1z5QHyNOqBUUEtDDsRWrJLTmujyyI7Frso6MRdplGTbhDuXZECgQPB9cqfz5W6M2bbtdO48clcURN-OsvwxYNGXR/EUGENIALOLI_PLASTIK20140314_03.jpg" width = "300" height = "200" alt="Collage Machine" align=center />
		<p class="anchorlink"><a href="#b">Collage Machine</a></p>
	</div>
	
	<div class="grid-item">
		
		<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/27/Symmetric_key_encryption.svg/800px-Symmetric_key_encryption.svg.png" width = "300" height = "200" alt="Cryptograph" align=center />
		<p class="anchorlink"><a href="#c">Software and hardware application in cryptograph</a></p>
	</div>
	<div class="grid-item">
		<img src="https://docs.nvidia.com/cuda/cuda-c-programming-guide/graphics/gpu-devotes-more-transistors-to-data-processing.png" width = "300" height = "200" alt="Cryptograph" align=center />
		<p class="anchorlink"><a href="#d">High Performance Aritechture</a></p>
	</div>
</div>



----


<h1 id="a">Painting  Understanding</h1>

<h2>Method1</h2>
Data augmentation has efficiently been used as a data
pre-processing technique that can increase the existing
number of images for training. We separated the data into
train and validations sets.

<b>Horizontal Flip:</b> As a part of our first data augmentation
technique, as seen in Figure 1., we horizontally flipped the
image and used a zoom of 0.5 on our data, further using
transfer learning to train the models.

<b>Diagonal Crop:</b> In this data augmentation method, the
original image is cropped along the diagonal into “n” small
images and these cropped images are zoomed in with a
zoom range of 3x. The resulting zoomed in patches are
stitched onto the original image such that there are “n”
patches along the last column and “n-1” patches along the
last row. Then that image is resized to 224x224 in order to
match the input size of our models. Figure 2. shows the
original, diagonal crop with zoom and the new generated
stitched image.

<b>Step Crop:</b> In this method, the original image is cropped
along the rows into smaller images with a step in between
and these cropped patches of images are zoomed in with
a zoom range of 3x and stitched onto the original image
similarly as described in the diagonal crop method.

<img src="/pics/Figure1.PNG"  alt="Figure1" align=center />
 
Figure 1. shows the original, step-crop with zoom and the newly
generated stitched image.

<img src="/pics/Figure2.PNG"  alt="Figure2" align=center />


Figure 2. Left image is original, Middle image is diagonal cropped,
Right image is new stitched.

<h2>method2</h2>

<h3>Multiple channel</h3>
To let neural network focus on brushed strokes and lines,
we manipulated images by cropping the paintings at the
upper right, center and bottom right. Then zoom in them
three times to obtain more detailed information. All of them
along with the original image was resize to 224 which is the
most adopted input size of popular neural networks and was
concatenated them together to save in tiff file.
<h3>Network Architecture</h3>
The first method is 21 channels images was fed into network together. 
Since the first three channel include all content of the original image. 
More information is expected to get from here. To tackle this, we specify 
the number of output channel of each input channel, rather than specifying the
number of out channel of all channel in a lump. Therefore,
it need to concatenate them together after every convolution
until the end. The rest parameters and pooling way keep
the same as Xception net. Since some unrelated images are
combined to together, machine may confused when it carry
out 1x1 pointwise convolution which calculate all pixel in
depth wise to generate new information.
<img src="/pics/Picture1.png"  alt="Figure2" align=center />

This’s where the second method comes in. The second
method was designed to convoluted through images and
cropped images on diagonal by utilizing parallel network.
Since the center of a painting usually contains richer information than other regions of a painting, the samll and
large cropped image at center region was picked. Along
with Original image were fed into Xception net separably,
the extracted feature map was sent to several combination
of the fully connection layer and the dropout layer, finally it
perform sigomd activation get final prediction.
<img src="/pics/Picture2.png"  alt="Figure2" align=center />

after several trails
and experiments, both method failed to outperform the performance 
of existing classification methods. 
They all suffered from overfitting issue. Different optimizers, 
he initializer and l2 regularizer was used though,
it still presented a hard time of converging

| Method                                                       | Architecture        | Valida Accuracy |
|--------------------------------------------------------------|---------------------|-----------------|
| Transfer Learning \(Original \+ Step Crop \+ Diagonal Crop\) | ResNet 101          | 76\.70          |
| Transfer Learning\(Hyperchannel\)                            | XceptionNet         | 19\.33          |
| Transfer Learning\(Ensemble Learning\)                       | XceptionNet\+ResNet | 30\.67          |

To be continue...<span class="anchorlink"><a href="#top">Back to top</a></span>

----


<h1 id="b">Collage Machine</h1>

There are ample mature technologies developed on how
to sythesis image, generate image that close to real-life and
how to colorize gray-scale images or videos which cover
almost any scenario, from real-life photograph to handdrawn animation. Besides that, people also attempt to let
machine learn a painting style and transfer it to a random
image.such as deep dream , neural style transfer, etc. All
the above- mentioned implementations shows that people
has a great interest in letting machine to mimic artist’s artwork or to equip them with paintings’ skills. The topics I
introduced here is making machine become a surrealist collage artist. The method I propose aims at understanding
the context of an image, then superimposing some image
scraps over an input image , which would bring out some
unexpected amusing effect, via supervised learning. To sum
up, When users feed an image to the neural network, it will
create a collage work based on original image with some
modifications. As a result, it can learn some knowledge we
provide in ground truth and achieve about 73% accuracy
over training epoches

<img src="/pics/diag.PNG"  alt="Figure1" align=center />
Figure 1. This diagram illustrate the main procedure of implementing collage art Machine. When users provide a image as background, the collage machine need to analysis the content of the
input, then pick several images that will compose onto this background from the corpus dataset, collage machine also need to figure out where the picked images should place, and how to place
them



<h2>Dataset</h2>


<img src="/pics/gt.PNG"  alt="Figure2" align=center />
Figure 2. sample of ground truth. In order to let neural network
fully understand each image word in corpus, more than one version of 
composite images were provided for each image words and
background images


<img src="/pics/corpus.PNG"  alt="Figure3" align=center />
Figure 3. sample of corpus

<img src="/pics/grphcut.jpg"  alt="Figure4" align=center />
Figure 4. segmentment software

<h2>Network architecture</h2>
<img src="/pics/model_plot.PNG"  alt="Figure5" align=center />
Figure 5. the network architecture


<h2></h2>
<img src="/pics/c1.PNG"  alt="Figure6" align=center />
<img src="/pics/c2.PNG"  alt="Figure6" align=center />
Figure 6. experiment results where the left side is ground truth, the
right side image is prediction result. The first example shows that it
fail to producing any meaningful result and it have occlusion issue.
The second example shows the ability of analogy. It predict the
same segmented image word under similar background images.
Since the dataset is small, it easily doubt that it’s a result of random
guessing

After 100 epoches training, A surprising result was presented. 
Most result is able to learn the feature of ground
truth, such like, it should start with outputting a name of a
image, then following output 9 numbers as transformation
matrix. Besides that, this algorithm also learn a basic rule
that is the 9 numbers should produce 0 0 1 in the end. Beam
search also provide more. This project still suffering from
the limitation of available dataset. But It can predict very
well for image it I have been seen well, The results satisfy
what I imagine before. My requirement is that,for example,
if the input image is crowed beach, it will predict something
that related with a person is vacuuming. When the input
images is food, it will predict something like someone is
rowing a boating that a scenes what dataset has shown. The
best accuracy we get is around 73%
<img src="/pics/plot.png"  alt="Figure7" align=center />
Figure 6. Training loss and accuracy

As a comparison, we also try to train our dataset on Dcgan.
 Training GAN is hard, usually takes several hours or
days.
<img src="/pics/dcgan.png"  alt="Figure7" align=center />
Figure 8. DC gan <span class="anchorlink"><a href="#top">Back to top</a></span>

----


<h1 id="c">Software and hardware application in cryptograph</h1>

to do by 8/29



<span class="anchorlink"><a href="#top">Back to top</a></span>

----


<h1 id="d">High Performance Aritechture</h1>





<span class="anchorlink"><a href="#top">Back to top</a></span>
