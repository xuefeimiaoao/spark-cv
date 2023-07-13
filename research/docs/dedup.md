
## spark提取图片特征，相似度匹配：  
hash（感知hash，均值hash）来比较图片相似性  
Spark Image Processing Library实现图片去重  
Spark结合OpenCV等图像处理库  
自定义transformer  estimator？  

## Hash Function  
Hash functions are robust against small changes in brightness, contrast, gamma corrections,  
compression, scaling, and/or resolution, and therefore ideal to detect (near-)identical images.  

There are various hash functions, such as; Average hash, Perceptual hash, Difference hash,  
Haar wavelet hash, Daubechies wavelet hash, HSV color hash, and Crop-resistant hash.   
Each hash function has specific properties to make it robust against certain changes such as  
brightness, contrast, gamma, correction, watermark, compression, scaling, and grayscaling.   
>Different image hashing algorithms of image for deduplicate  
>reference: https://towardsdatascience.com/detection-of-duplicate-images-using-image-hash-functions-4d9c53f04a75  
> https://github.com/idealo/imagededup   
> https://github.com/erdogant/undouble
> 
> haar wavelet: https://blog.csdn.net/iteye_3759/article/details/82566921

decolorizing 这个step spark有库吗？

## Spark Image Processing 
### With opencv as be
https://godatadriven.com/blog/real-distributed-image-processing-with-apache-spark/  
Use ImageTransformer for the basic image manipulation: resizing, cropping, etc. Internally, operations are pipelined and backed by OpenCV implementation.

```python
from synapse.ml.opencv import ImageTransformer

tr = (
    ImageTransformer()  # images are resized and then cropped
    .setOutputCol("transformed")
    .resize(size=(200, 200))
    .crop(0, 0, height=180, width=180)
)

small = tr.transform(images).select("transformed")

im = small.take(3)[2][0]  # take third image
plt.imshow(Image.fromarray(toNDArray(im), "RGB"))  # display the image inside notebook
```
>reference: OpenCV - Pipeline Image Transformations: https://microsoft.github.io/SynapseML/docs/features/opencv/OpenCV%20-%20Pipeline%20Image%20Transformations/  
> https://github.com/microsoft/SynapseML  
> mmlspark.opencv package: https://mmlspark.blob.core.windows.net/docs/0.18.1/pyspark/mmlspark.opencv.html  


## Experiments


