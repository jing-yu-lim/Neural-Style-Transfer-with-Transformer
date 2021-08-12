# Neural Style Transfer with DEIT Transformer

This is an alternative Pytorch Neural Style Transfer implementation, adapted from:
https://www.pluralsight.com/guides/artistic-neural-style-transfer-with-pytorch

Instead of using VGG net's activations for the feature maps for the contentm style and generated images to calculate the loss, the encodings from the DEIT transformer encoders are used

## Content Image Reconstruction
The content image reconstruction from noise using DEIT works quite well. However, there are some patches of the images with artefacts. This is likely related to the Self-Attention mechanism as the artefacts are congreated in what appears to be 16x16 sized patches, which is the siez of the input image patches into the transformer. It is interesting to note that the patch artefacts only appears in the later training steps, as the loss values decreases

This is available in the second part of the colab notebook in the main code.
![content_gen_overall2](https://user-images.githubusercontent.com/79006977/129229839-ce48c412-ecdf-4177-9a23-67a1bc55f2ec.jpg)


https://user-images.githubusercontent.com/79006977/129231289-a82c13f4-e2db-4825-b048-baf6550b35e0.mp4




## Full NST with Style Transfer
This is a result using the full NST. Unfortunately, the results are not as pleasant as the classic NST. This is likely due to the 16x16 image patches used as the inputs to the Vision Transformer. Perhaps the gradient backpropped for each patch is used for all 16x16 pixels. Moreover there is the 'Self-Attention' artefacts as shown above, from the content image reconstruction, further causing distortion to the generated image. Nonetheless, it is interesting to note that there is some form of style being transferred, indicating that the gram matrices of the transformer encodings, do represent the style of the images.

![NST_overall2](https://user-images.githubusercontent.com/79006977/129229584-6062444d-85f5-4c4d-8f8e-06296097b8e6.jpg)


https://user-images.githubusercontent.com/79006977/129231323-bd6552ec-f595-425b-af08-42e664549038.mp4



## Comparison with Classic NST
![doggo_classic_overall2](https://user-images.githubusercontent.com/79006977/129231189-715976a3-4b85-4b0e-87c8-1db1625aaa00.jpg)


