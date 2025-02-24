## Parameterized Deployment Config for LLaMa and GPT-2

This repo is a basic FastAPI app that 
serves as an interface for generating text with config parameters
from two different language models: a GPT-2 model 
and a LLaMa model. 

### Architecture

![image](https://github.com/OlayinkaPeter/LLM-Deployment-Config/blob/master/llm_config.png)


This repo is a basic FastAPI app that 
serves as an interface for generating text 
using two different language models: a GPT-2 model 
and a LLAMA model. 

The application provides two 
endpoints (`/gpt2_model` and `/llama_model`) that 
allow users to input prompts and obtain generated 
text based on those prompts using the respective 
models. 

The models employ the XLA (Accelerated Linear Algebra) 
acceleration function to enhance the speed and efficiency 
of the text generation process. 

XLA is a specialized compiler that optimizes 
linear algebra operations in TensorFlow, the underlying 
framework of the models. By utilizing the XLA acceleration 
function, the models can leverage hardware acceleration 
and advanced optimization techniques, resulting in faster 
and more efficient text generation. 

This optimization plays a crucial role in achieving 
higher throughput and reducing computational time, 
ultimately enhancing the overall performance of the 
text generation process.

The generated text and the 
throughput (in terms of iterations per second) 
are returned as results.

<br>

Here's a breakdown of what app.py does:

1. The code imports necessary libraries, including 
FastAPI, TensorFlow, Hugging Face Transformers, 
joblib, and time.
2. The fastapi app is created using `FastAPI()`.
3. There are two main endpoint functions:
`use_gpt2_model()` and `use_llama_model()`, each 
handling different model requests with the same 
set of request parameters
4. Request parameters are:
   - `model_name`: This parameter specifies the name 
   or identifier of the model to be used for text generation. 
   It's assumed that the specified model name 
   corresponds to a pre-trained LLAMA or GPT-2 model 
   that has been saved and can be loaded for inference
   - `prompts`: This parameter is a list of prompts for 
   which you want to generate text using the specified model. 
   Each prompt in the list will result in a separate 
   generated text output.
   - `task`: This parameter indicates the specific text 
   generation task that the model should perform. 
   The default value is "text-generation", which is a 
   common task where the model generates text based 
   on a provided prompt.
   - `framework`: This parameter specifies the framework 
   to be used for inference. It could either use the 
   PyTorch framework ("pt") or the TensorFlow framework ("tf")
   - `max_tokens`: This parameter sets the maximum number 
   of tokens in the generated text. It limits the length of 
   the generated output to ensure it doesn't become overly 
   long. The default value is 200.
5. `load_specified_model(model_name)` function loads a 
pre-trained model and tokenizer based on the specified 
model name. It uses TensorFlow's `tf.saved_model.load()`
to load the model and loads the tokenizer from a saved 
pickle file.
6. `run_gpt2_model()` and `run_llama_model()` functions use 
the specified models and tokenizers to generate text 
based on provided prompts. They utilize the 
Transformer library's `pipeline()` function for text 
generation.
7. The app is run using `uvicorn.run()` to start the FastAPI 
server, making the endpoints accessible via HTTP requests.


The app takes user prompts, 
processes them in parallel, generates text using 
the specified models, and returns the generated text 
along with the throughput rate for each model.


<br>

The notebooks for both the GPT-2 model deployment and the 
LLAMA model training are also included.