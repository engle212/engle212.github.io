---
layout: page
title: django-chatbot
description: an exploration of how chatbots work
img: assets/img/2_djangoLogo.png
importance: 1
category: 
related_publications: true
---

After graduating from Ohio State, I found myself with a lot of free time and a lot of skills that
needed demonstrated. What better way to address these points than to start a big project with some
powerful technologies? 

## development process
To start off this project, I devised a loose plan of how the application would run. Since most of
my prior web development experience was with Flask, I decided to use Django for this project. The
overall goal was to have mastered two of the most common Python web frameworks (maybe next I tackle
FastAPI). As for the rest of the tech stack, I went with:

- **Serverless Hosting**: AWS Lightsail
- **Data Storage**: AWS DynamoDB
- **LLM API**: Hugging Face

The Django app will run on an AWS Lightsail instance, so that it can be publicly accessible. As for
storing the data, it will use DynamoDB. And producing the behavior expected of a chatbot, I will
use the Hugging Face Inference API. As of writing this, it is the best low-cost option for personal
cloud-based LLM access since Hugging Face provides 1000 requests per day for free.

It is worth noting that I didn't use these cloud tools in the initial development process just to
play it safe with billing. Since this is my first big project with these cloud tools, I was unsure
if I would hit the deadline I set for myself to have a working project: January 27th.

I started development with setting up the Django app and getting right into designing the view.
This would feature a similar layout to existing chatbots like ChatGPT. It has a navbar, left-hand
sidebar, and a standard messaging interface in the middle. Since I planned to revisit the view,
I simply stopped once I could deem the interface "usable".

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/2_viewSC.png" title="initial interface" class="img-fluid rounded z-depth-1" %}
  </div>
</div>