---
layout: page
title: django-chatbot
description: an exploration of how chatbots work
img: assets/img/2_djangoLogo.png
importance: 1
category: 
related_publications: true
---

## the deployed project: [Django Chatbot](https://ej-django-chatbot-a729e1d22fee.herokuapp.com/)

After graduating from Ohio State, I found myself with a lot of free time and a lot of skills that
needed demonstrated. What better way to address these points than to start a big project with some
powerful technologies? 

## development process
To start off this project, I devised a loose plan of how the application would run. Since most of
my prior web development experience was with Flask, I decided to use Django for this project. The
overall goal was to have mastered two of the most common Python web frameworks (maybe next I tackle
FastAPI). As for the rest of the tech stack, I went with:

- **Serverless Hosting**: Heroku
- **Data Storage**: AWS S3
- **LLM API**: Hugging Face

The Django app will run on an Heroku dyno, so that it can be publicly accessible. As for
storing the data, it will use S3. And producing the behavior expected of a chatbot, I will
use the Hugging Face Inference API. As of writing this, it is the best low-cost option for personal
cloud-based LLM access since Hugging Face provides 1000 requests per day for free.

It is worth noting that I didn't use these cloud tools in the initial development process just to
play it safe with billing. Since this is my first big project with these cloud tools, I was unsure
if I would hit the deadline I set for myself to have a working project: January 27th.

I started development with setting up the Django app and getting right into designing the view.
This would feature a similar layout to existing chatbots like ChatGPT or Claude. It has a navbar,
left-hand sidebar, and a standard messaging interface in the middle. Since I planned to revisit the
view, I simply stopped once I could deem the interface "usable".

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/2_viewSC.png" title="initial interface" class="img-fluid rounded z-depth-1" %}
  </div>
</div>

After creating the view using Django's templating capabilities and some JavaScript, I built out the
backend API in Python. This involved making some high-level functions to carry out tasks like:
- Getting a conversation given a user ID and a conversation ID.
- Getting the most recent conversation.
- Getting the LLM's response to the user.
- Getting all of the conversations for a given user.
- Storing conversation data.
- Updating conversation summaries.

Of course, these functions require a lot of things to happen behind the scenes, so I implemented
some helper functions to handle these and other lower level tasks:
- Creating conversations.
- Getting conversation ID from filename.
- Generating a conversation filename.

All of the LLM interactions are contained within two functions:
- `get_reply(user_id, convo_id)`
- `update_convo_summary(user_id, convo_id)`

The first one, `get_reply`, simply initializes a Hugging Face client, gets its response to the
current messages, and converts the Markdown output to HTML. `update_convo_summary`, on the other
hand, initializes the HF client, then is given the current conversation but appended with an
invisible user message: "Give this conversation a descriptive, 5-word title with no emojis". I
wrote this prompt after a bunch of trial and error to get the LLM to output something similar to
ChatGPT's sidebar summaries, but I am sure there is more refinemnent to be done to get it closer to
that industry standard.

As for the LLM, I chose a Google model offered by Hugging Face, titled `google/gemma-2-9b-it`. This
model seemed to offer good responses that weren't all watermarked with emojis like some other
models are (looking at you, Meta and 01-ai 😠). I didn't try all of the models so I can't guarantee
that Gemma was the best choice here. With that being said, I will definitely look into some more
models in the future, or, just offer a feature to choose between a wide selection of models. I think
this would offer something that actually sets this chatbot apart from existing chatbots, so keep an
eye out for that update.