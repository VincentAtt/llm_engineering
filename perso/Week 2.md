

# Day 1 : comparing models telling jokes

- Temperature : caractere deterministe /aléatoire peut etre paramétré entre 0 et 1, où 1 correspond au maximum de créativité.

- openai `completions` = continuer la conv
On peut parametrer de creer plusieurs choices, sinon juste `choices[0]` disponible

- Prompts usually works with `"role"`s defined in parameter `messages` : `system`, `user` and `assistant`

- with Claude.anthropic, the system and user messages are separate as follows

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



