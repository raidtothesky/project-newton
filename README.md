# Project Newton -- Apple Detection AI

<img width="400" alt="image" src="https://github.com/raidtothesky/project-newton/assets/141038084/a00d1655-d2e2-46d6-a4ca-ade20906ddc7">
<img width="400" alt="image" src="https://github.com/raidtothesky/project-newton/assets/141038084/3af2b720-d0f4-44e3-a4ca-052dcd4efe3a">

### Please use Google Colab

I recommend just downloading the `count.ipynb` and `classify.ipynb` files, uploading them to [Google Colab](https://colab.research.google.com/), and then running them. They should work fine immediately.

(and if you want to try the training code as well, you can do the same with the `apple_detection_training.ipynb`, but it does take a while to rerun the training)

You can try running those on your own machines by first installing all the requirements via `pip install -r requirements.txt`. However, this work uses Ultralytics and Roboflow as the core packages, and they currently have pathing issues which still need to be fixed manually. You would need to do this yourself and it's painful. I don't recommend it but feel free to ask me if you want to do so and you stumble upon some problems.

### The models
I have prepared 3 fine-tuned models that are used for both apple counting and classification. You can check the [folder](https://github.com/raidtothesky/project-newton/tree/main/models) to see some explanations about each of them. You can also check and rerun the training code `apple_detection_training.ipynb`.

### The training
I use a publicly available apple detection dataset from Roboflow to fine-tune a YOLOv8 nano model pretrained on the COCO dataset. The fine-tuning is done in multi-step to avoid catastrophic forgetting and to try to find a biased model that performs the best on the sample 41 apple image. I use Google Colab to fine-tune, which takes roughly 1-2 hours for the final tuning pipeline. But finding this pipeline, due to computational budget, was time-consuming (2-3 days) because using automated hypermarameter tuning approaches was simply not possible. I had to resort to a largely manual hyperparameter search.

### The `count.ipynb`
The resulting apple detection model is simply used to detect apples and count their occurrences. Just run every cell and the last cell should give you the output. You can also change the function `count_apples` parameters to check the three models and to check how they work on other images.

### The `classify.ipynb`
I use the bounding boxes from the resulting apple detection model to crop the apples and then I leverage a rule-based image processing approach using a pre-determined HSV boundary for each color red, green, and yellow. It works quite well for the given singular image but needs to be tested for other images.

Ideally, one can build a color classifier if suitable training data exists. Otherwise, generating synthetic data using stable diffusion is also promising (I would do that given enough time).

As above, just run all cells and the last cells should give you the results: a created folder containing the cropped images separated into 3 subfolders according to their colors.

<img width="265" alt="image" src="https://github.com/raidtothesky/project-newton/assets/141038084/d9ed65c9-8337-4e64-8c8e-7a9f7b53e01c">




