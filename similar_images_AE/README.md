# Similar images finder (using Autoencoders)

Given a set of query images and a set of store inventory images, we find the top-k similar inventory images that are the most 'similar' to the set of query images in an unsupervised way of using an encoder to embed the images, then performing kNN in this embedding space to search for 'similar' images. For this code sample, we query for similar steakhouse food images:

<img src="https://github.com/ankonzoid/artificio/blob/master/similar_images_AE/output/result_burger_test.png" width="80%" align="center">

### Algorithm:

1) Train an autoencoder with training images in the same domain as the inventory images

2) Use the trained encoder to embed both the query images and the inventory images

3) Perform kNN (euclidean/cosine similarity) to find the inventory nearest neighbour image embeddings to the query image embeddings, and keep the k closest embeddings as the top-k recommendations

Particularly for our example code, we train a convolutional autoencoder on 36 steakhouse food images (6 of each of steak, potato, french fries, salads, burger, asparagus), and make similar image food recommendations based on the above algorithm. Below are more results of querying test images of salad and asparagus:

<img src="https://github.com/ankonzoid/artificio/blob/master/sim_img_AE/output/result_salad.png" width="80%" align="center">

<img src="https://github.com/ankonzoid/artificio/blob/master/sim_img_AE/output/result_asparagus.png" width="80%" align="center">

The model performs fairly well as a vanilla model with minimal fine-tuned training, in the sense that the top similar recommended images tend to be in same food category as the query image (i.e. querying a burger gives mostly burgers, and querying a salad gives mostly salads, ...). There is still much room for improvement in terms different neural network architectures, more/different training images, hyperparameter tuning to improve the generality of this model. 

### Usage:

The code can be run immediately by executing 

> python sim_img_AE.py 

using our pre-existing trained models. This run will output your query answer images into the `output` directory. The full procedure for this is:

1) Place your query images into the `test` directory, database images into the `db` directory. We already have default steakhouse food item images for you to use already.

2) Run `python sim_img_AE.py`. When the run is complete, your answer images will be deposited into the `output` directory.

If you would like to train the model from scratch, then open `sim_img_AE.py` and:

* set `model_name` to either `"simpleAE"` (1 FC hidden layer) or `"convAE"` (CNN)

* set `process_and_save_images = True` and use your own images

* set `train_model = True` to instruct code to train the model (and save it once it is trained)

### Required libraries:

* numpy, matplotlib, pylab, sklearn, keras, h5py, pillow