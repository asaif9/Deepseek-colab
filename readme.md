This guide will walk you through the steps to set up and run the DeepSeek R1 model on Google Colab using the Ollama server. Additionally, you’ll learn how to create a Gradio UI to interact with the model in a user-friendly way.

View Post on Github : Click Here

Prerequisites:

A Google account (to access Google Drive and Google Colab).

Basic familiarity with Google Colab and terminal commands.

Step 1: 
Create a New Folder in Google Drive
Go to Google Drive and log in.

Click on the + New button and select Folder.

Name the folder (e.g., DeepSeek-R1-Project).

Step 2: 
Create a Google Colab Notebook
Open the folder you just created.

Right-click inside the folder, select More, and then choose Google Colaboratory.

A new Colab notebook will be created. Name it (e.g., DeepSeek-R1-Notebook).

Important: Enable GPU/TPU for Better Performance
To improve the model's performance, you can enable GPU or TPU:

Go to Runtime > Change runtime type.

Under Hardware accelerator, select GPU or TPU.

Click Save and restart the notebook.

Step 3: 
Install Required Libraries
In the Colab notebook, paste the following commands to install the necessary libraries:

!pip install langchain
!pip install langchain-core
!pip install langchain-community
!pip install colab-xterm

Run the cells to install the libraries.

Step 4: 
Load Colab-Xterm and Open a Terminal
Paste the following commands to load colab-xterm and open a terminal:

%load_ext colabxterm
%xterm

A terminal will open in a new tab within Colab.

Step 5: 
Install Ollama
In the terminal, run the following command to install Ollama:

curl -fsSL https://ollama.com/install.sh | sh

Wait for the installation to complete.

Step 6: 
Start Ollama Server and Run DeepSeek R1
In the terminal, start the Ollama server and load the DeepSeek R1 model by running the following commands:

ollama serve &
ollama run deepseek-r1:7b

The DeepSeek R1 model will be loaded and ready to use.

Step 7: 
Add a Gradio UI for Interaction
To make it easier to interact with the DeepSeek R1 model, you can add a Gradio UI. Follow these steps:

Step 7.1: 
Install Gradio
Install the Gradio library by running the following command in a Colab cell:

!pip install gradio
Step 7.2: 
Create a Function to Interact with the Model
Define a function that sends user prompts to the DeepSeek R1 model and returns the response. Paste the following code into a Colab cell:

import subprocess

def query_deepseek_r1(prompt):
    command = f'ollama run deepseek-r1:7b "{prompt}"'
    result = subprocess.run(command, shell=True, capture_output=True, text=True)
    
    return result.stdout
Step 7.3: 

Build the Gradio Interface
Create a Gradio interface using the function above. Paste the following code into a Colab cell:

import gradio as gr

def gradio_interface(prompt):
    response = query_deepseek_r1(prompt)
    return response

iface = gr.Interface(
    fn=gradio_interface,  
    inputs="text",        
    outputs="text",       
    title="DeepSeek R1 Chatbot",  
    description="Ask anything to the DeepSeek R1 model!"
)

iface.launch(share=True)
Run the cell. Gradio will generate a public link to your UI.

Step 7.4: 

Interact with the Model via Gradio
Open the Gradio UI link in your browser.

Type a prompt (e.g., "What is the capital of France?") in the input box.

Click Submit.

The DeepSeek R1 model will process the prompt and display the response in the output box.

credit:-https://buymeacoffee.com/rsahan/deepseek-r1-setup-google-colab-using-ollama-server

