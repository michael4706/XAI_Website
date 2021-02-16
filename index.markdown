---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="style/style.css" rel="stylesheet" />
    <title>Document</title>
</head>
<body>
    <section class = "dataset">
        <h1><b>Dataset</b></h1>
        <p>
            Our project uses the <a href = "https://github.com/joojs/fairface">FairFace</a> dataset to perform classification and analysis. FairFace supplies
            108501 images of faces from an equally distributed pool of seven race categories, two genders,
            and eight age groups. In addition to being uniquely comprehensive and applicable to our project,
            the size of this dataset allows us to create subsets of the data in order to display biased training
            sets. The biased data was generated based on the actual US population as recorded in the 2019
            US Census dataset.
        </p>
    </section>
    <section class = "model">
        <h1><b>Model</b></h1>
        <h4><b>Convolutional Neural Network</b></h4>
        <p> 
            We used CNN as our model. We applied transfer learning with resnet50 by taking the first 14 layers and fixing
            their weights. Then, we concatenated them with our self-defined layers. We preprocessed the training images by 
            resizing it to 224 x 224 x 3 and applied the resnet_v2 input preprocessing function and adding random
            augmentation to our training data.
        </p>
        <h4><b>Model Parameters</b></h4>
        <p>
            The parameters for training are listed as follows: <b>batch size = 128, learning rate = 0.008,
            optimizer = Nadam, loss = categorical cross entropy</b>. The learning rate will iteratively decrease if
            the validation loss does not decrease for 10 consecutive epochs. The early stopping would be triggered if the
            validation loss does not decrease for 30 consecutive epochs.
        </p>
    </section>
    <section class = "Training Progress">
        <h1><b>Training Progress</b></h1>
        <p>
            The plots below show the training progress of three models: race, age, and gender. From the plots, we can observe that
            the validation accuracy of gender is the highest, followed by race and gender. Considering the number of categories inside
            each class, the results are expected.
        </p>
        <h4><b>Race Model</b></h4>
        <div class="row">
            <div class="race_progress">
                <img src="img/race/acc_curve.png" style="width:100%">
            </div>
            <div class="race_progress">
                <img src="img/race/loss_curve.png" style="width:100%">
            </div>
        </div>
        <h4><b>Age Model</b></h4>
        <div class="row">
            <div class="age_progress">
                <img src="img/age/acc_curve.png" style="width:100%">
            </div>
            <div class="age_progress">
                <img src="img/age/loss_curve.png" style="width:100%">
            </div>
        </div>
        <h4><b>Gender Model</b></h4>
        <div class="row">
            <div class="Gender_progress">
                <img src="img/gender/acc_curve.png" style="width:100%">
            </div>
            <div class="Gender_progress">
                <img src="img/gender/loss_curve.png" style="width:100%">
            </div>
        </div>
    </section>
    <section class = "XAI Algorithm">
        <h1><b>XAI Algorithm</b></h1>
        <h4><b>Grad-CAM</b></h4>
        <p>
            Grad-CAM analyzes the gradients flowing into the final convolutional layer in the neural network and it finds the convolutional layers by searching for 4D outputs over all the network layers. Then, to compute the heatmap visualization, we have to perform a forward pass through the gradient model and get the prediction output from the final convolutional layer. The loss value between the prediction and the specific class/race the model is trying to classify is calculated using a loss function. Then, the guided gradients are computed by multiplying the casted version of the computed gradient values and the convolutional layer output so that the model finds all the positive values and this is multiplied by the gradient of the differentiation calculated using automatic differentiation. Automatic differentiation is the process of computing a value of a function along with its derivative.
        </p>
        <p>
            The mean of the guided gradients results in the weights of the final layer. The weights are helpful in determining the importance of the different feature maps to reach the specific target class. The final linearly combined feature layer is mapped into the final class activation heatmap. Grad-CAM is a generalization of CAM in that it focuses on features that have a positive influence on the predicted class and is therefore able to depict localization on the heatmaps. This can be achieved by applying the ReLU function on the class activation map. This entire process can be visualized by the figure below.
        </p>
        <h4><b>Integrated-Gradient</b></h4>
        <p>
            Integrated-Gradient (IG) explains the relationship between the predictions and the learned features. The general procedure of IG is as follows:
            <ol>
                <li>Interpolate the original image given a baseline(e.g. 224 x 224 x 3 image with all pixel values = 0) with a list of alpha levels that represent a small step in the interpolation process</li>
                <li>Calculate the gradient of the model’s prediction with respect to each features in from each layers for each of the interpolated images</li>
                <li>Calculate the mean of the gradients across all the interpolated images. Here, we are “accumulating the gradients” because when alpha is near 1, the gradient suddenly drops to 0 even if the feature shows significant activation.</li>
            </ol>
        </p>
    </section>
    <section class = "Appendix">
    <h1><b>Appendix</b></h1>
    <h4><b>Grad-CAM samples</b></h4>
    <h4><b>Integrated-Gradient samples</b></h4>
    </section>
</body>
</html>