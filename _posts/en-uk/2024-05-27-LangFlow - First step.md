---
layout: post
title: Utilizing Langflow to generate a Chat-bot
date: 2024-05-27 12:00:00
description: AI-based Chat-bot using Langflow 1
tags: Informatics, LLMs
categories: #Informatics, LLMs
thumbnail:
align: lft
dir: ltr
images:
  compare: true
  slider: true
---


Artificial intelligence tools including Langflow facilitate the creation of AI-based applications, including the automated dialogue program, aka chat-bots. Hereby, I summarize the steps to implement this using Langflow library.

Taken into consideration performing the following:

1- Conda virtual environment with Python==3.10

```
conda create -n langflow python==3.10
conda activate langflow 
```

2- Ollama serve is installed and running in your machine with the model llama3 pulled.

## Installing 

To install the Langflow, we are going to utilize the ```pre released version``` by using the following command:

```
python -m pip install langflow --pre --force-reinstall
```

After installing it, we need to run it as explained in the following point.


## Running the server:

```
python -m langflow run
```

After running the langflow serve, we can access it from the web-based interface. The default link and port of the service is: ```http://127.0.0.1:7860```.



## Creating a new project:

As a start point, let us create a new project. To do so, click on the New Project button. 


<div style="text-align:center"><video src="https://raw.githubusercontent.com/yalhariri/yalhariri.github.io/main/_posts/assets/Langflow_creatingNewProject.mp4" controls="controls" style="max-width: 800px;">
</video></div>



## Adding the chat-bot components:

Langflow provides many options for the inputs, models and outputs. In this introduction example, we will use the Ollama model, with model llama3, and the text input with specifying  the context by using the prompt component.

From the Core Component list, we then can add the following components:

### 1- Inputs .. Chat input.

Add the Chat input component.

### 2- Inputs .. Prompt.

After adding the prompt, you need to configure the prompt's feature. To perform that, you need to add the template with the desired configurations. In our example, we add the context and the question. To do that, click on template and type in the following lines:

```
Please answer the question within the context provided.

Context:{context}

Question:{question}
```


This will create two inputs: the context and question. 
The input of the question is the output of the Chat input, to perform that you need to wire the output of the chat input to the question input of the prompt. While the context is a description sentence which you need to add to describe the context of the question, so the model generates a coherent and relevant response for each question.

### 3- Models .. Ollama - llama3 (the mode llama3 should be pulled in into your system.)
Before making it functional, Ollama service must be up in your machine, and the llama3 model should be pulled. 
Next, from the Models core component list, add Ollama, and configure the model name to llama3. Finally, it may require adding the Base URL for the model. To perform that, from the Ollama component in the canvas, click on the three dots (...), and then select Advanced. Finally add the Base URL. The default settings for the Ollama is ```http://localhost:11434```

### 4- Outputs .. Chat output.
This component print out the resulted text from the models to the user. 


After completing the four steps above, click on the  Playground to try the chat-bot.

At the end, the components in the canvas should look like the following picture.


<div style="text-align:center"><img src="https://raw.githubusercontent.com/yalhariri/yalhariri.github.io/main/_posts/assets/chat_bot.png" width="800px" alt="Langflow sample Chat-bot"></div>



You can try the following two examples of the context:



Example 1:

> Explain your answer in the same language of user questions. Make your answer clear, concise, and to the point.

Example 2:

> You are a professional interpreter. You receive the sentences from the user, identify the language, and then translate them into English and send them back to the user. In case of ambiguity, provide both translations.


## Conclusion
This example shows how to generate a chat-bot that uses Llama3 model. 
Langflow provides a large library of models including Amazon Bedrock, Azure OpenAI, Hugging Face API ... etc. It also provides other functionalities including helpers such as chat memories, import URLs as a context, and vector stores and searches ... etc.


## Extra resources:

1- https://www.youtube.com/watch?v=RWo4GDTZIsE
