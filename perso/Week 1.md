
# Teacher

website : https://edwarddonner.com/

Course : https://edwarddonner.com/2024/11/13/llm-engineering-resources/, including slides on a gdrive to download.

# Ollama

after downloading ollama ![here](https://ollama.com/download), powershell `ollama run llama3.2`.

```
Available Commands:
  /set            Set session variables
  /show           Show model information
  /load <model>   Load a session or model
  /save <model>   Save your current session
  /clear          Clear session context
  /bye            Exit
  /?, /help       Help for a command
  /? shortcuts    Help for keyboard shortcuts

Use """ to begin a multi-line message.
```

The first time, it will download many things but then you'll have a working llm directly!

You can explore ![different models](https://ollama.com/search), having in mind your goals and your machine performance (models with many parameters are more complicated to run).

Quinn2.5 is probably the best to handle different languages.



# Openai API

![lien](https://platform.openai.com/docs/overview)

The key is stored in ".env", a txt file modified to be exactly named ".env" so that other instances understands where to look for it. It starts with `OPENAI_API_KEY=`, then you need to insert the API key ![built here](https://platform.openai.com/settings/organization/api-keys) with no space before.

---

# Course

1. day1: summarizing fixed URLs thanks to OPENAI_API
2. day2: adapting it to ollama (a clean correction is available)

This week includes a guide to Jupyter (or notebooks?), some Pythons commands to learn, a troubleshooting code

---



Remember there are **3 ways to use models** :
- Chat interfaces such as *ChatGPT*
- Cloud APIs : LLM API, framworks like LangChain, Managed AI cloud services : Amazon bedrock, Google Vertex, Azure ML
- Direct inference with the HuggingFace Transformers library or Ollama to run locally

At the end of the course, we will master:
- **Models** : Open-Source ou Closed Source, multimodal, architecture, selecting 
- **Tools** : HuggingFace, LangChain, Gradio, Weights and Biases, Modal
- **Techniques** : APIs, Multishot prompting, RAG, Fine-tuning, Agentization (indeed, we will build a 7-agent team working on a topic!)

At the end on 2024, Frontier is:

```markdown
|Open-Source|Closed-Source | from |
|Llama||Meta|
|Phi||Microsoft|
|Mixtral||Mistral|
|Qwen||Alibaba Cloud|
||GPT|OpenAI|
||Claude|Anthropic|
|Gema|Gemini|Google|
||Command R|Cohere|
|Perplexity|||
```

---

# useful code

For a nice display of a markdow: 

```python
from IPython.display import Markdown, display

display(Markdown("# This is a big heading!\n\n- And this is a bullet-point\n- So is this\n- Me, too!"))

```




