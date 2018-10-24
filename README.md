# MonumentRecognition
A TF model that recognizes 5 monuments from images. Built with images scraped via Google Images

This is a TensorFlow model that classifies a given image of the Taj Mahal, Statue of Liberty, Eiffel Tower, Big Ben clock, or the Sydney Opera House. In addition, all images used to train the model are from Google Images and are free of copyright (filtered out using the tool on Google Images)

This model was created using transfer learning, since deep learning from scratch can take a lot of time and resources.

Procedure:
1. Search up “Taj Mahal” on Google Images. Scroll down the page upto a point where the images start to get irrelevant.
2. Paste each line of js_console.js into the JavaScript console. Essentially what this does is find the url of each of these images and adds it to a file called urls.txt. This file is then downloaded.
3. Run download_images.py on your local terminal. This downloads all the images onto a specific folder.
4. Repeat the above steps for all other classes (such as Eiffel Tower)
5. Set variables for image size and architecture.
6. You need to have installed Tensorflow on your computer for the following steps to work.
7. Activate tensorflow
8. cd into your directory and retrain the image using a command like this:
```
python -m scripts.retrain\
  --bottleneck_dir=tf_files/bottlenecks \
  --how_many_training_steps=500 \
  --model_dir=tf_files/models/ \
  --summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \
  --output_graph=tf_files/retrained_graph.pb \
  --output_labels=tf_files/retrained_labels.txt \
  --architecture="${ARCHITECTURE}" \
  --image_dir=tf_files/monument_photos
  ```
After the model training is complete, you are done! Test out the classifier using a a test image with a command like this:
```
python -m scripts.label_image \
    --graph=tf_files/retrained_graph.pb  \
    --image=tf_files/test_images/testimage1.jpg
```
Results will be in this form:
```
opera (score = 0.99071)
taj (score = 0.00595)
eiffel (score = 0.00252)
liberty (score = 0.00049)
bigben (score = 0.00032)
```

The class with the highest numerical value is most likely the monument.


Documentation/Useful tutorials:
1. Tensorflow (VERY USEFUL!) – https://www.tensorflow.org/hub/tutorials/image_retraining
2. Scraping images from Google Images search – https://www.pyimagesearch.com/2017/12/04/how-to-create-a-deep-learning-dataset-using-google-images/


The primary machine learning part of this project is contained within the `scripts` directory. There are 9 python scripts. The model can be tested by running `label_image.py` in the format mentioned above. The first phase analyzes all the images on disk and calculates and caches the bottleneck values for each of them. 'Bottleneck' is an informal term used for the layer just before the final output layer that actually does the classification.

Watch a demo of this project here – https://youtu.be/Au9WnkyXNA4

Cheers!
