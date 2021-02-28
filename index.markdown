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
    <link href="./style/style.css" rel="stylesheet" />
    <script type="text/x-mathjax-config">
        MathJax = {
            tex: {
            inlineMath: [['$', '$'], ["\\(", "\\)"]],
            processEscapes: true,
            }
        }
    </script>
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

</head>
<body>
        <section class = "overview">
            <h1><b>Overview</b></h1>
            <p>
                put content here
            </p>
        </section>
        <section class = "facial_analysis">
        <h1><b>Why Facial Analysis?</b></h1>
        <p>
            put content here
        </p>
    </section>
    <section class = "XAI">
        <h1><b>What is Explainable AI (XAI)?</b></h1>
        <p>
            put content here
        </p>
    </section>
    <section class = "dataset">
        <h1><b>Dataset</b></h1>
        <p>
            &emsp; &emsp; Our project uses the <a href = "https://github.com/joojs/fairface">FairFace</a> dataset to perform classification and analysis. FairFace supplies
            100000+ images of faces from an equally distributed pool of seven race categories, two genders, and eight age groups. In addition to being uniquely comprehensive and applicable to our project, the size of this dataset allows us to create subsets of the data in order to display biased training sets. The biased data was generated based on the actual US population as recorded in the 2019 US Census dataset.
        </p>
        <div class ="sample">
            <img src = "./img/dataset/sample.png" style = "width:100%">
        </div>
        <br/>
        <section class = "unbiased_db">
            <h4><b>Unbiased Dataset Distribution</b></h4>
            <p>
                <b>Note</b>: What we mean by "unbiased" only applies to race and gender cateogries.  
            </p>
            <div class="distribution_unbiased">
                <div class = pic_unb>
                    <img src="./img/dataset/race_alt.png" style="width:100%">
                </div>
                <div class = pic_unb>
                    <img src="./img/dataset/gender_alt.png" style="width:100%">
                </div>
            </div>
            <div class ="distribution_unb">
                <img src = "./img/dataset/age_alt.png" style = "width:60%">
            </div>
        </section>
        <br/>
        <section class = "biased_db">
            <h4><b>Biased Dataset Distribution</b></h4>
            <div class="distribution_biased">
                <img src="./img/dataset/race_biased.png" style="width:70%">
            </div>
        </section>
    </section>
    <section class = XAI_algo>
        <h1><b>XAI Algorithms</b></h1>
        <h4><b>Grad-CAM</b></h4>
            <p>
                &emsp; &emsp; Grad-CAM analyzes the gradients flowing into the final convolutional layer in the neural network and it finds the convolutional layers by searching for 4D outputs over all the network layers. Then, to compute the heatmap visualization, we have to perform a forward pass through the gradient model and get the prediction output from the final convolutional layer. The loss value between the prediction and the specific class/race the model is trying to classify is calculated using a loss function. Then, the guided gradients are computed by multiplying the casted version of the computed gradient values and the convolutional layer output so that the model finds all the positive values and this is multiplied by the gradient of the differentiation calculated using automatic differentiation. Automatic differentiation is the process of computing a value of a function along with its derivative.
            </p>
            <p>
                The mean of the guided gradients results in the weights of the final layer. The weights are helpful in determining the importance of the different feature maps to reach the specific target class. The final linearly combined feature layer is mapped into the final class activation heatmap. Grad-CAM is a generalization of CAM in that it focuses on features that have a positive influence on the predicted class and is therefore able to depict localization on the heatmaps. This can be achieved by applying the ReLU function on the class activation map. This entire process can be visualized by the figure below.
            </p>
            <h4><b>Integrated-Gradient</b></h4>
            <p>
                &emsp; &emsp; Integrated-Gradient (IG) explains the relationship between the predictions and the learned features. This equation summarizes integrated gradient:
            </p>
            <p>
                $$IntegratedGrads_{i}^{approx}(x) = (x_i - x^{'}_{i})\sum_{k=1}^{m}{\partial{F}(x^{'}+{k \over m} \times (x-x^{'})) \over \partial{x_i}}$$
            </p>
            <p>
                where \(x_{i}\) = input image, \(x^{'}_{i}\) = baseline, \(m\) = total number of intepolated images, \(F\) = ouput channel of the model
            </p>
            <ol>
                <li>Determine \(m\). The common value of \(m\) is >= 20 in practice. </li>
                <br/>
                <li>Generate interpolated images = \(x^{'}+{k \over m} \times (x-x^{'})\)</li>
                <br/>
                <li>Compute gradient between model F output predictions w.r.t features = \({\partial{interpolated \, path \, inputs} \over \partial{x_{i}}}\) </li>
                <br/>
                <li>Integral approximation through averaging gradients = \(\sum_{k=1}^{m}{gradients \times {1 \over m}}\)</li>
                <br/>
                <li>
                    Scale integrated gradients w.r.t input image = \((x_{i} - x_{i}^{'}) \times integrated \, gradients\). The reason this step is necessary is to make sure
                    that the attribution values accumulated across multiple interpolated images are in the same units and faithfully represent the pixel importances
                    on the input image 
                </li> 
            </ol>
            <p>
                <b>Here is the visual way to summarize the steps of integrated gradient:</b>
            </p>
            <div class = "ig_img">
                <img src="./img/ig/ig.png" style="width:100%">
            </div>
            <br/>
            <p>
                For more information about <b>integrated gradient</b>, tensorflow offers a <a href = "https://www.tensorflow.org/tutorials/interpretability/integrated_gradients">great turorial</a>
            </p>
        <br/>
    </section>
    <section class = "result">
    <h1><b>Result</b></h1>
        <p>
            put content here
        </p>
    </section>
     <section class = "discussion">
    <h1><b>Discussion</b></h1>
        <p>
            put content here
        </p>
    </section>
    <section class = "conclusion">
    <h1><b>Conlusion</b></h1>
        <p>
            put content here
        </p>
    </section>
</body>
</html>