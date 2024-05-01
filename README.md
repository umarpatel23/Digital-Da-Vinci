# Digital-Da-Vinci
Project Title: Digital Da Vinci: Decoding Artistry with Machine Learning

People Working on the Project (working individually):

Umar Patel 
SUNET ID: umar2023

Summary: I will make an interface that will rapidly classify and label key features in paintings, specifically identifying the artist, style, palette, brushwork, and even perform high-level content analysis and compositional segmentation, that could hopefully provide art analysts, educators, or students to quickly gain important insights into a painting when observing or studying it. I will use Monet2Photo and other open source artist datasets, such as those found here to gather images as the training data for the model. By the end of the project, I would want to have a clean UI or simple web page that takes in an image of a painting and spits out its corresponding attributes, providing users with a concise but artistically relevant and informative summary of the painting.

Inputs and Outputs: 

Input to the model: An unseen image of a painting by an artist from a standardized list of n artists (standardized to some width/height dimensions). 

Output of the model: A best guess of who the artist of the painting is, the style of the painting, the color palette used, the brushwork, and some high-level content of the image including compositional segmentation. As I more formally create the training data, I will flesh out the details of the exact categories of attributes that I would try to identify. But for now, here are samples of the categorizations I will try to create a model for:

Artist: Monet, Da Vinci, Van Gogh, Picasso, Warhol, Rembrandt (could include others). 
Style: Renaissance, Baroque, Impressionism, Post-Impressionism, Cubism, Surrealism (could include others). 
Brushwork: Stippling, Hatching/Cross-Hatching, Scumbling, Glazing, Feathering, (could include more)
High-level content: Still trying to figure this out. (maybe categories like nature, landscape, portrait, animals, city, indoors, outdoors, etc.).

The fundamental constraint is accuracy, as users of this type of interface would likely prefer more accurate information about a painting, they are looking at the expense of time. People who would likely use this interface would be analyzing art as an enthusiast or a professional but are not necessarily too concerned about speed since the painting that they are assessing is static (unlike a real-world scene that you might be taking a photograph of). So, a reasonable amount of time (such as a minute or less) to retrieve all of the listed metadata for the painting should be fine for most users or people. I imagine model(s) I could create for this would be able to process the painting and retrieve the intended information in a few seconds. But to do so accurately, I would need enough training data for each type of metadata the user is requesting (i.e., stroke type, style, content, segmentation, etc.) so that it could accurately provide results on an unseen painting. 

Another potential major constrained is the amount of available labeled training data. While I am fairly sure I can find relatively large databases of paintings from famous artists, I would still need to label them accordingly with the aforementioned potential tags in order to develop relevant training data for the model. 

Task List: 

1.	Download and organize dataset(s). I would likely have to gather images of paintings from different sources depending on the artist, since datasets are likely organized and split by artist. Some early research has shown me these possible resources to get my dataset: 
a.	Monet2Photo
b.	136 Leonardo Da Vinci Works
c.	Collections of Paintings from 50 Artists*
Be able to load these datasets onto some basic program and be able to visualize and interact with them through code. 

2.	Choose the dataset or dataset(s) that are best suited for training a model (as well as which have informative labels that will help train the model). Or which can be labeled manually in an easy manner. 

3.	Choose a model for prediction:

-	For image-based predictions for the desired categories, I would likely be fine-tuning Convolutional Neural Networks for this task. I will also try to experiment with transformer-based models since they are known to be effective in focusing on specific parts of an image that is crucial for tasks such as brushstroke or style analysis. Particularly, ResNet or VGG would be good models to fine-tune for these tasks. 
-	For content-based prediction (such as image captioning or high-level content as described above), I will try to use an encoder-decoder transformer model since they have shown superior performance in multimodal tasks, and the embedded attention mechanisms as described through the Key, Query, Value approach . However, having recently taken CS 348I, I have also been introduced to Vision-and-Language Pre-trained models such as CLIP which might be useful and faster for high-level descriptions. 
-	In the case I will need to use semantic segmentation might be useful for labeling different parts of the painting, which could be useful for identifying key features in a painting. U-Net would be a useful tool for this. 

4.	Label training data if necessary (this might be the most time-consuming part, but hopefully the datasets are labeled under the desired categories, or that it would be simple to filter and organize the images of paintings into their desired categories. If this step becomes too difficult, then I will alter the categories to fit the easiest mode of preparing the training data. 
5.	Train the models, re-iterate or change model parameters if necessary to achieve better results.
6.	Once best results are achieved, then create a simple user interface that could be used by individuals on a website or app. I have SwiftUI experience which can be used to create a simple interface of inputting an image and fetching the desired results (perhaps through a Google API) and displaying it to the user. 
7.	(***If time permits***) Doing a user-study with Stanford Arts students or enthusiasts and getting their feedback on the program. 

Expected Deliverables and/or Evaluation:

The goal is to develop a user interface that allows a user to upload an image of a painting (which could be saved to their camera roll or be taken live), and then display the corresponding information about the image (i.e., most likely artist to have painted that painting, its style, the brushstroke, and its high-level content description). Mainly, I would like to test that the model works with reasonable accuracy and am not too concerned with the time it takes for the prediction to take (within a reasonable limit of course of perhaps 30 seconds). The app (which would likely be coded in SwiftUI) would have a simple upload interface which would allow the user to upload a photo of a painting. Then, the app would call a Google Drive API that could call the trained model and retrieve and display accurate (hopefully) results for the painting attributes. 

Beyond this user application which I hope can serve as a basic demo for a potentially useful application for artists and enthusiasts, I will evaluate the model on a test set of unseen images for all categories described earlier in the proposal and compare against the ground truth of labels for those images. While I have not trained my model yet and so do not have a confident metric threshold for a “proficient” accuracy, I will say that for the purposes of a half-quarter project, I believe having an accuracy above 70% on each of the categories would deem the project successful. My biggest concern is that for brushstroke category, it might be difficult for the model to distinguish between similar patterns. However, I am hoping that with sufficient training data, the model will learn to distinguish between the various types of related brushstroke patterns.

Specifically, my goal is that for each category that I will test for prediction (artist, style, brushstroke, high-level content, etc.) that each will have an accuracy above 70%. The high-level content, since that would allow for more leeway, can be compared to the ground truth via cosine similarity, since there may not be one correct ground truth answer. 

Therefore, I believe a successful project will include a model that could predict at this level of accuracy and have a reasonably seamless user interface that can allow for real-time prediction.

What are the biggest risks?:

I think the biggest risk is not getting the API to work which connects the user interface with the trained model, which can cause the user interface aspect of my project to breakdown. 

In the case this is causing an issue, I will try to look into custom interfaces that could be built either within Google Colab or whatever platform I end up using to train and run the models. 

Another potential risk is having to label all of the training data from scratch, if I cannot find enough pre-labeled data. If this is the case, I will have to potentially label paintings and categorize them myself. To mitigate this, I will try to collect my training data early and start labeling or breaking the data into training, validation, and test sets for each category.

While not a risk, I will likely train different models for each category so that the predictions are all independent of each other. This might increase training time so is something I should certainly be aware of this. 


What you need help with?:

Do you think the scope of my project is manageable for the timeframe?

What are the best (and most efficient) ways for labeling a diverse dataset in art? Do you have suggestions for sources and/or methods?

Do you have any recommendations on which architectures might be most effective for this?

For the user interface, I'm planning to use SwiftUI and connect to the model via a Google Drive API. Do you have any advice or resources on best practices for using APIs here?
