
# Content

- day1 : jokes comparison and adversarial conversation
- day2 : gradio UI



# Day 1 : comparing models telling jokes

- Temperature : from fully deterministic (0) to fully random and creative (1)

- openai 
  - `completions` = continuer la conv
  - on peut parametrer de creer plusieurs choices, sinon juste `choices[0]` disponible

- Prompts usually works with `"role"`s defined in parameter `messages` : `system`, `user` and `assistant`

- with Claude.anthropic, the system and user messages are separate as follows :

```python
    system=system_message,
    messages=[{"role": "user", "content": user_prompt},]
```

You can also stream the answer, using `result = claude.messages.stream()` (and not `claude.messages.create()`), followed by :

```python
with result as stream:
    for text in stream.text_stream:
            print(text, end="", flush=True)
```

## Adversarial conversation between chatbots

Based an the usual prompt list structure :

```
[
    {"role": "system", "content": "system message here"},
    {"role": "user", "content": "user prompt here"}
]
```
that can be completed to reflect a longer conversation :

```
[
    {"role": "system", "content": "system message here"},
    {"role": "user", "content": "first user prompt here"},
    {"role": "assistant", "content": "the assistant's response"},
    {"role": "user", "content": "the new user prompt"},
]
```

Actually, that is what happens when you discuss with an LLM chatbot : the whole conversation feeds the next word prediction.

So you can define GPT and Claude system prompts and functions `call_gpt()` and `call_claude()` and build a conversation !

# Day2 : Gradio

Acquired by HuggingFace

> `gradio` works with `websockets`. Gradio latest version 14.1 does not seem compatible with websockets. As suggested by ChatGPT, I downgraded it : `pip install websockets==10.4`. To upgrade it back, `pip install --upgrade gradio`

You cannot really stream a message on gradio, but you can fake this in `yield`ing result in a look on chunks.

---

En Python, les fonctions `print`, `return`, et `yield` servent des objectifs très différents. Voici une explication détaillée de chacune :

---

## `yield` in a function, compared to `print()` and `return`

### **1. `print`**
- **Objectif :** Afficher du texte ou des données dans la console.
- **Utilisation typique :** `print` est utilisé pour montrer des informations pendant l'exécution d'un programme (souvent à des fins de débogage ou pour fournir des sorties visibles à l'utilisateur).
- **Caractéristiques :**
  - Il ne modifie pas ou ne retourne pas de données dans le programme.
  - La valeur retournée par `print` est toujours `None`.

---

### **2. `return`**
- **Objectif :** Renvoie une valeur (ou plusieurs) d'une fonction à l'appelant.
- **Utilisation typique :** On l'utilise pour transmettre des résultats calculés par une fonction à une autre partie du programme.
  
**Exemple :**
```python
def ajouter(a, b):
    return a + b

resultat = ajouter(5, 7)  # La fonction retourne 12.
print(resultat)           # Affichera : 12
```

- **Caractéristiques :**
  - Une fois qu'une fonction rencontre un `return`, son exécution s'arrête immédiatement.
  - Les données renvoyées peuvent être réutilisées ou manipulées ailleurs dans le code.

---

### **3. `yield`**
- **Objectif :** Permet de produire des valeurs (une par une) à partir d'une fonction appelée générateur, sans perdre l'état de la fonction.
- **Utilisation typique :** Utile pour produire des séquences ou des flux de données de manière paresseuse (lazy evaluation) et efficace en mémoire.

**Exemple :**
```python
def generateur():
    for i in range(3):
        yield i

for valeur in generateur():
    print(valeur)  # Affichera : 0, puis 1, puis 2
```

- **Caractéristiques :**
  - Contrairement à `return`, `yield` ne termine pas la fonction immédiatement. La fonction peut reprendre son exécution à l'endroit où elle s'est arrêtée.
  - Les fonctions utilisant `yield` sont des générateurs. Elles renvoient un **itérable** au lieu d'une seule valeur.
  - Très utile pour traiter des grandes quantités de données sans les charger toutes en mémoire.

---

### **Différences clés**

| **Aspect**        | **print**                          | **return**                         | **yield**                          |
|--------------------|------------------------------------|------------------------------------|------------------------------------|
| **But principal** | Afficher dans la console.          | Retourner une valeur.              | Générer des valeurs une par une.  |
| **Sortie**         | `None`                            | Une valeur ou plusieurs.           | Un générateur/itérable.           |
| **Utilisation**    | Interaction ou débogage.          | Passer des données au programme.   | Itération paresseuse (lazy).      |
| **Arrête la fonction ?** | Non.                          | Oui, après l'exécution du `return`.| Non.  |

---

Day2 exercise consists in implementing our company prochure tool in a gradio UI !
He suggests to do it in the end of W1D5 code but I'll do a new W2D2 code.

## Gradio tips

### several inputs :

Pour ajouter deux entrées dans une application Gradio en Python, vous devez définir deux widgets d'entrée dans le composant `gr.Interface`. Voici un exemple simple :

Cet exemple montre comment créer une application Gradio avec deux champs d'entrée, un champ texte et un nombre, et afficher leur résultat combiné.

```python
import gradio as gr

# Fonction de traitement
def combine_inputs(input1, input2):
    return f"Texte: {input1}, Nombre: {input2}"

# Définir les composants d'entrée et de sortie
input1 = gr.Textbox(label="Entrez un texte")
input2 = gr.Number(label="Entrez un nombre")
output = gr.Textbox(label="Résultat")

# Interface Gradio
interface = gr.Interface(
    fn=combine_inputs,  # Fonction à appeler
    inputs=[input1, input2],  # Liste des entrées
    outputs=output       # Sortie
)

# Lancer l'application
interface.launch()
```

#### Explications
1. **Fonction principale** : La fonction `combine_inputs` prend deux paramètres `input1` et `input2`. Ces paramètres correspondent aux données saisies par l'utilisateur dans les deux champs.
   
2. **Définition des entrées et sorties** :
   - `Textbox` : Pour saisir du texte.
   - `Number` : Pour saisir un nombre.
   - `outputs` est défini pour afficher le résultat combiné.

3. **Liaison dans l'interface** :
   - `inputs` est une liste contenant les deux composants d'entrée.
   - `outputs` correspond à la sortie.

Quand vous lancez l'application avec `interface.launch()`, vous obtenez une interface avec deux champs d'entrée et un bouton pour exécuter la fonction.

### De la mise en page

Pour ajouter un joli titre à votre application Gradio, vous pouvez utiliser le paramètre `title` ou ajouter des composants `gr.Markdown` dans la mise en page avec une interface `gr.Blocks`. Voici deux approches :

---

### 1. Avec le paramètre `title`
Gradio permet de définir un titre directement en passant le paramètre `title` dans `gr.Interface`.

```python
import gradio as gr

# Fonction de traitement
def combine_inputs(input1, input2):
    return f"Texte: {input1}, Nombre: {input2}"

# Interface Gradio avec un titre
interface = gr.Interface(
    fn=combine_inputs,  # Fonction à appeler
    inputs=[gr.Textbox(label="Entrez un texte"), gr.Number(label="Entrez un nombre")],
    outputs=gr.Textbox(label="Résultat"),
    title="Ma Super Application Gradio"  # Ajout du titre
)

# Lancer l'application
interface.launch()
```

Le paramètre `title` dans `gr.Interface` ajoute un titre simple au-dessus de votre interface.

---

#### 2. Avec `gr.Blocks` pour une personnalisation avancée
Si vous voulez personnaliser davantage la mise en page, comme ajouter une description ou styliser le titre, utilisez `gr.Blocks`. Cela vous permet d'ajouter des éléments Markdown.

```python
import gradio as gr

# Fonction de traitement
def combine_inputs(input1, input2):
    return f"Texte: {input1}, Nombre: {input2}"

# Construire l'interface avec Blocks
with gr.Blocks() as demo:
    gr.Markdown("# 🌟 Bienvenue sur Ma Super Application 🌟")  # Titre stylisé en Markdown
    gr.Markdown("Cette application combine un texte et un nombre, et affiche le résultat.")
    with gr.Row():
        input1 = gr.Textbox(label="Entrez un texte")
        input2 = gr.Number(label="Entrez un nombre")
    output = gr.Textbox(label="Résultat")
    bouton = gr.Button("Lancer")
    
    # Événement pour le bouton
    bouton.click(combine_inputs, inputs=[input1, input2], outputs=output)

# Lancer l'application
demo.launch()
```
- `gr.Markdown` permet d'écrire des titres avec Markdown, ce qui permet des styles plus avancés (par exemple, des emojis, des couleurs, etc.).
   - Vous pouvez également ajouter une description ou d'autres éléments visuels.


Vous verrez :
- Un titre en grand avec des emojis et du texte Markdown.
- Une description sous le titre.
- Deux champs d'entrée alignés côte à côte.
- Un bouton pour exécuter la fonction.



# Day 3 : User Interfaces and Chatbots - AI assistant on gradio

### Context and Progress in Chatbots
- Modern chatbots enable informed and contextual conversations, unlike older systems limited to predefined choices.
- LLMs can:
  - Maintain conversation history by including all context in the prompt.
  - Adopt **custom personas**.
  - Demonstrate subject matter expertise to answer questions competently.

### Key Techniques for Interacting with LLMs
1. **System Prompt**: Defines the **tone** of the conversation and **sets rules** such as "**If you don’t know the answer, just say so.**"
2. **Context**: Adds additional information to enhance responses.
3. **Multi-shot Prompting**: Provides multiple examples in the prompt to guide the model’s behavior.
   - Helps shape the LLM by offering response patterns.
   - Differs from traditional training as it happens during inference (runtime).

Reminder : 
- LLMs generate responses by predicting the next tokens based on the provided history.
- The quality of prompts significantly impacts model performance.

### Notes

About Gradio, we can use the ChatInterface function.

Originally, we would have had to make functions that allows an LLM model and a gradio app to correctly work together. But Gradio upgraded to adapt to OpenAI.

We write a function `chat(message, history)` where:  
**message** is the prompt to use  
**history** is the past conversation, in OpenAI format

We combine the system message, history and latest message, then call OpenAI.

> About the structure of **successive roles "system"/"user"/"asssistant"** in a dictionnary, Ed explains that like everything else, LLMs understand them as tokens but that **the structure is automotically considered as mark-ups for a new step**. It is not "implemented" : LLM have been trained like this !

```python
system_message = "You are a helpful assistant in a clothes store. You should try to gently encourage \
the customer to try items that are on sale. Hats are 60% off, and most other items are 50% off. \
For example, if the customer says 'I'm looking to buy a hat', \
you could reply something like, 'Wonderful - we have lots of hats - including several that are part of our sales evemt.'\
Encourage the customer to buy hats if they are unsure what to get."
```

Notice that we provide facts and examples. Examples allows us to introduce both tone and style. For instance, the chat can be very enthusiastic to sell more items.

You can add options such as : 

```python
if 'belt' in message:  #highly improvable
    relevant_system_message += " The store does not sell belts; if you are asked for belts, be sure to point out other items on sale."
```

**OR including messages that have not actually happened** in the beginning, to improve the chatbot through previous answers from the assitant.

RAG is about finding such extra information that is relevant to the prompt and adding it in the context, in a more sophisticated way. More on that later.

I chose to answer the exercise in switching the prompt so the bot encourages customers to be eco-friendly.

#  Day 4 - Tools

**Tools** allows Frontier models to connect with external functions
 - richer responses by extending knowledge
 - ability to carry out actions within the application
 - enhanced capabilities like calculations

How it works : **in a request to the LLM, specify available tools** 
such as a function to compute things.
The LLM will understand the conditionnal function by itself and it will look like it is running it.

Use cases :
- fetch data or add knowledge or context (like looking for term `belt` on day3)
- perform calculations
- take action like booking a meeting
- modify the ui

The 2 latter may actually be performed through a JSON response, as we did with links relevance
but tools are the best solutions even for them if you want text in addition

> Prompt tip : "Always be accurate. If you don't know the answer, say so"

For instance, here, we don't want it to hallucinate prices

```python

# here is a useful function we would like it to use :

ticket_prices = {"london": "$799", "paris": "$899", "tokyo": "$1400", "berlin": "$499"}

def get_ticket_price(destination_city):
    print(f"Tool get_ticket_price called for {destination_city}")
    city = destination_city.lower()
    return ticket_prices.get(city, "Unknown")

# It must be integrated in a dictionnary structure describing the function :

price_function = {
    "name": "get_ticket_price",
    "description": "Get the price of a return ticket to the destination city. Call this whenever you need to know the ticket price, for example when a customer asks 'How much is a ticket to this city'",
    "parameters": {
        "type": "object",
        "properties": {
            "destination_city": {
                "type": "string",
                "description": "The city that the customer wants to travel to",
            },
        },
        "required": ["destination_city"],
        "additionalProperties": False
    }
}

# And it must be included in a list of tools:

tools = [{"type": "function", "function": price_function}]

# such as LLMs were trained with !

```

The chat function needs to be adapted, FROM THIS :

```python

def chat(message, history):
    messages = [{"role": "system", "content": system_message}] + history + [{"role": "user", "content": message}]
    response = openai.chat.completions.create(model=MODEL, messages=messages)
    return response.choices[0].message.content

gr.ChatInterface(fn=chat, type="messages").launch()

```

TO THIS :

```python

def chat(message, history):
    messages = [{"role": "system", "content": system_message}] + history + [{"role": "user", "content": message}]
    response = openai.chat.completions.create(model=MODEL, messages=messages, tools=tools)

    if response.choices[0].finish_reason=="tool_calls":
        message = response.choices[0].message
        response, city = handle_tool_call(message)
        messages.append(message)
        messages.append(response)
        response = openai.chat.completions.create(model=MODEL, messages=messages)
    
    return response.choices[0].message.content

```

And `handle_tool_call` must be defined :

```python

def handle_tool_call(message):
    tool_call = message.tool_calls[0]
    arguments = json.loads(tool_call.function.arguments)
    city = arguments.get('destination_city')
    price = get_ticket_price(city)
    response = {
        "role": "tool",
        "content": json.dumps({"destination_city": city,"price": price}), # json.dumps put everything in string
        "tool_call_id": tool_call.id
    }
    return response, city

```

> Note that if we had different possible tools to call, tool_call should depend on a condition to include them all.

Eventually, gradio chat interface can be launched : `gr.ChatInterface(fn=chat, type="messages").launch()`.

> I wonder if it works for Claude ? With the same commands ?

Consequently, the usual structure is completed : system / user / assistant / user /assistant / user / assistant /.../ TOOL /// ...

The chat function understands the tool function and it acts as it was running it !

exercise : add a tool like booking a flight !

tomorrow : agents carrying out sequential activities

