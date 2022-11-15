#  **Binary Text Classification**

**Objective** :<br>
Given a post/conversation, identify if the post owner is participating in an event or not.

**Dataset** :<br>
No training dataset available.
Some data to get an idea for pre-processing and cleaning can be found here : https://drive.google.com/drive/folders/1JQj-i3TU_5lSlArsermd2O8Rgj8h1Sm9


**Approaches Tried :**
1. Since there was no training data provided, first approach which I could think of was `NLI-based Zero Shot Text Classification`, using pre-trained HuggingFace model like `facebook/bart-large-mnli`.
2. Second approach I tried was using `Weak Supervision technique`, by creating synthetic data for training, and fine-tuning Transformer based Classification model on synthetic domain data.
3. Othere approach which I could think of was using `Unsupervised technique` by clustering the samples, and find out if there is a seperate cluster where `attending the event` could be one of the cluster label, and `not attending the event` be the other cluster's label.

**Psuedo-code (/logic) :**
1. Input text was cleaned and processed, which includes removal of hashtags, mentions, emojis, links, and non-alphabetic words.
2. Finalized on using approach one- `NLI-based Zero Shot Text Classification`, where I used custom labels for predicting the class to the input text : `model_labels=["attending the event", "not attending the event"]`
3. Passed cleaned and processed text to pre-trained `facebook/bart-large-mnli` model, and got output label having maximum probability score.
4. On running the code end-to-end, you will get the accuracy score for the test data, given input as filepath of the test file, columnn name having text, column name having true labels for the corresponding sentences.
5. Note : Make sure the column containing true label is boolean (and not 0/1).


**How to Run the Code/File ?**
1. For installing all the required files, `requirement.txt` file is provided having necessary files which needs to be installed before.
2. Make the shell file executable using command : `chmod +x run.sh`
3. Run shell script using command `./run.sh <arg1> <arg2> <arg3>`
4. In the above command, `<arg1> is the filepath of the testing csv file including the filename`, `<arg2> is the name of the column having conversation/posts`, and `<arg3> is the name of the column containing "True/Actual" label for the corresponding sentences`.
5. Example command :--> `./run.sh ./data/testing.csv sentences true_label`


**Results :**<br>
These are the screenshot for some samples I tested :
![Example 1](https://github.com/ritvik-garg/NLI-based-Zero-shot-Text-Classification/blob/main/results/ss1.png)
![Example 2](https://github.com/ritvik-garg/NLI-based-Zero-shot-Text-Classification/blob/main/results/ss2.png)



**Scope of Improvement :**<br>
Weak supervision technique could yield better result as we will have some data to fine-tine our model on our domain data. But creating synthetic data was a challenge. I tried first getting samples where the conversation was about some event and then classifying those samples into attending/ not attending sample. But I couldn't find quantity and quality on sythetic data, so went with Zero-shot approach, and it was giving decent result on my limited test-cases I tried.
