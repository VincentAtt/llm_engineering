
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

1. day1 : summarizing fixed URLs thanks to OPENAI_API
2. day2 : adapting it to ollama (a clean correction is available)
3. day3 : comparing models

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

### Day 3 : comparing models

![image]('./perso/pic/1_3_models')

Frontier LLMs have mind-blowing performance for :
- synthesizing information
- Fleshing out a skeleton (for instance write an email from notes)
- coding (StackOverFlow lost audience)

They have limitations :
- Specialized domains, still not a PhD level but closing in (for instance Claude Sonnet for maths or chimics)
- Recent events
- Can confidently make mistakes (curious blindspots)

Typical questions to compare models that we're going to use :
- "How do I decide if a business problem is suitable for an LLM solution?"
- "Compared with other Frontier LLMs, what kinds of questions are you best at answering, and what kinds of questions do you find most challenging? Which other LLM has capabilities that complement yours?"
- "What does it feel like to be jealous?"
- "How many times does the letter 'a' appear in this sentence?"
- "Choose the world that best completes the analogy : Feather is to bird as sclae is to ______. A) reptile B) Dog C) Fish, D) Plant." proposed by ![Vellum](https://www.vellum.ai/blog/llm-benchmarks-overview-limits-and-model-comparison), a website that compares models we will see later. That reminds me of ComparIA.
- "How many rainbows does it take to leap from Hawaii to 17" made models proposed a real number...

> ChatGPT canvas allows you to talk with the Chat while it modifies the code you're talking about to suit your need : including examples, simplifying, excludes missing or empty values. ChatGPT understood the Hawaii joke.

> Claude 3.5 is leading from October 24. The jealous question is even sensorial and sensitive to human feelings. Is is very interesting, it is critical, self-critical, socio-ethical points of view. When you ask for a code, if creates an `Artefact` on the left and keeps explaining, link Canvases from OpenAI

> Gemini did not understand the nuanced joke about Hawaii but explains the issue. It is really bad at counting 'a's.

> Cohere focuses on knowledge. It is thorough. It is bad at counting 'a's

> MetaAI is the latest version of Llama. Llama generates pictures.

> Peprlexity is a SearchEngine with its own model and using other models. Nuanced informations on news!

In conclusion, they are all good, particularly at synthesis and generating nuanced answers. But Claude tends to be favored by practitioners : more humourous, more attention to safety, more concise.

As they all converge in capability, price may become the differenciator. Recent innovations have focused on lower cost variants, for instance `4o-mini`.

Then Ed had fun launching 3 models competing to become the leader of the pack by delivering a speech and vote.

---

# useful code

For a nice display of a markdow: 

```python
from IPython.display import Markdown, display

display(Markdown("# This is a big heading!\n\n- And this is a bullet-point\n- So is this\n- Me, too!"))

```




