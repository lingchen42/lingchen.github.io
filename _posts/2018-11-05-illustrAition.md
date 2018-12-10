---
title:  "illustrAItion: a tool that automatically generate drawings from input sentences"
date:   2018-11-05 22:00:00
categories: [other]
tags: [django, reactjs, nlp, image_processing]
---

## Interactive website
<a href="http://www.illustraition.net/"> http://www.illustraition.net/ </a>

## What is illustrAItion?
 Have you ever had this great story that only lacked for illustrations, but were missing the will or desire to draw something? Despair no more, for we bring you **illustrAItion**, the AI-informed web tool for generating illustrations automatically. Simply enter the phrase you want to be sketched, and **illustrAItion** will assemble a matching picture from doodles generated as part of the Google QuickDraw experiment. **illustraAItion** currently support two languages, Chinese and English. <br>

 Illustration is developed at Vanderbilt Hackthon V by Ling Chen, Laura Colbran and Ying Ji.

## Demo
![illustrAItion_demo]({{ site.url }}/assets/illustrAItion_demo.gif)

## How It Works
![illustrAItion_pipeline]({{ site.url }}/assets/illustrAItion_pipeline.png)

- **Doodle Data** <br>
**illustrAItion** is built on the back of a database assembled from doodles submitted via the Google Quick, Draw! game (`https://quickdraw.withgoogle.com/`). For this game, people are instructed to (quickly) draw the word that the game displays on the screen. The drawings were previously curated using a convolutional neural network to identify the best examples of each word, resulting in 340,000 high-quality (_or at least recognizable..._) doodles, each matched to their word. **N.B.** We do not consider the generation of this database part of **illustrAItion**, since it predates Vandyhacks V, and can be used for many other things as well.

- **Frontend** <br>
We built the frontend of **illustrAItion** using the React JavaSript Library (`https://reactjs.org/`). It consists of a text box to enter your phrase, and a display area where the drawing is displayed. The drawing is animated using SVG paths assembled from the doodle database by the backend.

- **Backend** <br>
The input and ouput of the API call is processed using the Django Python Library (`https://www.djangoproject.com/`). The typed phrase is processed into pairs of words connected by a positional preposition using either NLTK (`https://www.nltk.org/`) or SpaCy (`https://spacy.io/`). It then checks to make sure there is a drawing of each word in the doodle database. In the absence of one, it uses the Gensim library to fetch the most similar word. Once the individual drawing are pulled from the database in the form of SVG paths, these are combined such that the individual drawings are arranged to reflect the positional preposition connecting them. This combined path is then returned to the frontend for display.
