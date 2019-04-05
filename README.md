# Open nsfw model
This repo contains code for running Not Suitable for Work (NSFW) classification deep neural network Caffe models. [Blog](https://yahooeng.tumblr.com/post/151148689421/open-sourcing-a-deep-learning-solution-for) post which describes this experiment in more detail.

#### Demo 

![Demo Image](https://66.media.tumblr.com/a24135a56ecf20d7efb81dda0f4ccbac/tumblr_inline_oebl0iNWRM1rilvr1_500.png "")


#### Usage

* The network takes in an image and gives output a probability (score between 0-1) which can be used to filter not suitable for work images. Scores < 0.2 indicate that the image is likely to be safe with high probability. Scores > 0.8 indicate that the image is highly probable to be NSFW. Scores in middle range may be binned for different NSFW levels. 
* Depending on the dataset, usecase and types of images, we advise developers to choose suitable thresholds. Due to difficult nature of problem, there will be errors, which depend on use-cases / definition / tolerance of NSFW.  Ideally developers should create an evaluation set according to the definition of what is safe for their application, then fit a [ROC](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) curve to choose a suitable threshold if they are using the model as it is. 
* ***Results can be improved by [fine-tuning](http://caffe.berkeleyvision.org/gathered/examples/finetune_flickr_style.html)*** the model for your dataset/ use case / definition of NSFW. We do not provide any guarantees of accuracy of results. Please read the disclaimer below.
* Using human moderation for edge cases in combination with the machine learned solution will help improve performance.

#### Description of model
Trained the model on the dataset with NSFW images as positive and SFW(suitable for work) images as negative. These images were editorially labelled. We cannot release the dataset or other details due to the nature of the data. 

### Requirements
- caffe-cpu or caffe-gpu
- python-opencv
- pycaffe
- python3

We will get the NSFW score returned:
```
0.14057905972
``` 
#### Running the model
To run this model, please install [Caffe](https://github.com/BVLC/caffe) and its python extension and make sure pycaffe is available in your PYTHONPATH.

We can use the classify.py script to run the NSFW model. For convenience, we have provided the script in this repo as well, and it prints the NSFW score. 

 ```
python classify_nsfw.py --model_def nsfw_model/deploy.prototxt --pretrained_model nsfw_model/resnet_50_1by2_nsfw.caffemodel test_image.jpg
 ```
 
#### ***Disclaimer***
The definition of NSFW is subjective and contextual.

#### Contact
The model was trained by [Jay Mahadeokar](https://github.com/jay-mahadeokar/),  in collaboration with [Sachin Farfade](https://github.com/sachinfarfade/) , [Amar Ramesh Kamat](https://github.com/amar-kamat), [Armin Kappeler](https://github.com/akappeler) and others. Special thanks to Gerry Pesavento for taking the initiative for open-sourcing this model. If you have any queries, please raise an issue and we will get back ASAP.

