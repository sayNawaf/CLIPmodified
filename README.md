# CLIPmodified

CLIP (Contrastive Language–Image Pre-training) builds on a large body of work on zero-shot transfer, natural language supervision, and multimodal learning.

CLIP models can then be applied to nearly arbitrary visual classification tasks. For instance, if the task of a dataset is classifying photos of dogs vs cats we check for each image whether a CLIP model predicts the text description “a photo of a dog” or “a photo of a cat” is more likely to be paired with it.

CLIP was designed to mitigate a number of major problems in the standard deep learning approach to computer vision:

Costly datasets: Deep learning needs a lot of data, and vision models have traditionally been trained on manually labeled datasets that are expensive to construct and only provide supervision for a limited number of predetermined visual concepts. The ImageNet dataset, one of the largest efforts in this space, required over 25,000 workers to annotate 14 million images for 22,000 object categories. In contrast, CLIP learns from text–image pairs that are already publicly available on the internet. Reducing the need for expensive large labeled datasets has been extensively studied by prior work, notably self-supervised learning,141516 contrastive methods,1718192021 self-training approaches,2223 and generative modeling.24252627

Narrow: An ImageNet model is good at predicting the 1000 ImageNet categories, but that’s all it can do “out of the box.” If we wish to perform any other task, an ML practitioner needs to build a new dataset, add an output head, and fine-tune the model. In contrast, CLIP can be adapted to perform a wide variety of visual classification tasks without needing additional training examples. To apply CLIP to a new task, all we need to do is “tell” CLIP’s text-encoder the names of the task’s visual concepts, and it will output a linear classifier of CLIP’s visual representations. The accuracy of this classifier is often competitive with fully supervised models.


![image](https://user-images.githubusercontent.com/87066472/196043721-a4256966-53e2-4b40-9e96-45c0903c8b32.png)
![image](https://user-images.githubusercontent.com/87066472/196044195-e3569b44-5727-4ab3-ab1b-fbaadfe63b27.png)
![image](https://user-images.githubusercontent.com/87066472/196044205-7eadd054-b5f6-42d3-8450-b3b1954b9d25.png)



How I improved CLIP Perfomance

orignal CLIP impplementation was based on dot product of an image embedding and text embedding of respective text and image which is passed as logits upon a softmax application.
image embedding was generated using a RESNET and text embeding using BERT...

instead of RESNET i used a transformer based model Called BEIT,which is trained in similar way as BERT to generate embeddings but instead of text it generated image embeddings.
since both are trained in similar fashion to generate embeddings,their embeddings are more relevant to eachother...hence we can a good perfomane boost..

using this approach also erradicates the need to use a projection head so both embeddings are of the same dimensions resulting in faster training (which is a big issue with CLIP ie long preTraining time) than the orignal model..but to achive better than the orignal results its projection head is still  required
