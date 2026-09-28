---
task category:
- text-generation
language:
 - pt
 - en
---

# The Delta Dataset V2

**The Delta Dataset** is a collaborative, open-source dataset created to help build and improve the next generation of AI models.

The project is developed by **Pyra Labs** and can be used to train and fine-tune Delta models, as well as other AI models and projects.

Rather than being limited to a single model or architecture, the goal of The Delta Dataset is to provide an open space where people can create, share, improve, and reuse high-quality training data.

---

## Language

This README is currently available in English and Portuguese.

**[English](README.md)** · **[Português (Brasil)](README_PT-BR.md)**

> **Quer ler este README em português?**
> [Leia o README em português.](README_PT-BR.md)

---

## About the Dataset

The Delta Dataset is designed as a **community-driven dataset for AI training**.

Anyone can contribute examples covering subjects such as:

* Programming
* Mathematics
* Science
* History
* Geography
* Languages
* Reasoning
* General knowledge
* Conversations
* Creative writing
* Explanations
* Tool usage
* And other useful AI training tasks

The dataset is intended to grow continuously through community contributions.

Pyra Labs uses The Delta Dataset as part of its own model development, but the dataset is not restricted to Pyra Labs models. Other researchers, developers, and AI projects are free to use it according to the license.

---

# Deltaset

**Deltaset** is the original text-based data format created for The Delta Dataset.

It represents conversational training examples using special tokens:

```dataset-deltaset.txt
[SYS] You are Delta Ultra Mini.
[SEP]

[USR] What is Python?
[SEP]

[ASS] Python is a high-level programming language...
[SEP]
```

The format separates different parts of a conversation using tokens such as:

* `[SYS]` — System instruction
* `[USR]` — User message
* `[ASS]` — Assistant response
* `[SEP]` — Separator between sections

Deltaset was designed to be simple, readable, and easy to create manually.

---

# V2 Format

The second version of The Delta Dataset introduces a structured **JSONL** format.

Instead of representing examples using special tokens, each example is stored as a JSON object containing four fields:

```json
{
  "system": "...",
  "user": "...",
  "think": "...",
  "bot": "..."
}
```

### Fields

* `system` — Optional system instruction that defines the assistant's behavior or context.
* `user` — The user's message or request.
* `think` — Optional reasoning content associated with the response.
* `bot` — The assistant's final response.

The `system` and `think` fields can be `null` when they are not present.

The `user` and `bot` fields are required.

---

## Example with system instruction and reasoning

````json
{
  "system": "You are Delta, a helpful and technical programming assistant. Explain programming concepts clearly, write functional code, follow good practices, and adapt to the requested language. When errors occur, identify the cause and provide an objective correction.",
  "user": "How do I make a loop that prints the numbers from 1 to 10 in Python?",
  "think": "The task asks for a simple repetition example. In Python, range(1, 11) generates the values from 1 to 10 because the ending value is not included. I will show a short and functional for loop.",
  "bot": "You can use a `for` loop with `range()`:\n\n```python\nfor i in range(1, 11):\n    print(i)\n```\n\n`range(1, 11)` starts at 1 and stops before 11, so it prints the numbers from 1 to 10."
}
````

---

## Example without system instruction or reasoning

Not every example requires a system instruction or reasoning field.

In these cases, the corresponding fields can be set to `null`:

```json
{
  "system": null,
  "user": "Hi :)",
  "think": null,
  "bot": "Hi! How are you doing?"
}
```

---

# JSONL Structure

The Delta Dataset V2 uses **JSON Lines (JSONL)**.

Each training example is an independent JSON object. In the actual dataset, each object is stored on its own line.

For example:

```json
{"system":null,"user":"Hi :)","think":null,"bot":"Hi! How are you doing?"}
{"system":"You are Delta, a helpful programming assistant.","user":"How do I make a loop in Python?","think":"The user needs a basic Python loop example.","bot":"You can use a `for` loop with `range()`."}
```

This structure allows examples to be processed independently and makes the dataset suitable for streaming, preprocessing, filtering, and large-scale training pipelines.

Alternatively, a complete example can be written on a single line without unnecessary formatting:

```json
{"system":"You are Delta, a helpful and technical programming assistant. Explain programming concepts clearly and write functional code.","user":"How do I make a loop that prints the numbers from 1 to 10 in Python?","think":"The task asks for a simple repetition example using a Python for loop.","bot":"You can use a `for` loop with `range()` to print the numbers from 1 to 10."}
```

---

# From V1 to V2

V2 changes the internal representation of dataset examples while keeping the main purpose of the project the same.

### V1

The original dataset used the **Deltaset** text format:

```dataset-deltaset.txt
[SYS] You are Delta Ultra Mini.
[SEP]

[USR] What is Python?
[SEP]

[ASS] Python is a programming language...
[SEP]
```

### V2

The dataset now uses structured JSONL:

```json
{"system":"You are Delta Ultra Mini.","user":"What is Python?","think":null,"bot":"Python is a programming language..."}
```

The new structure makes individual fields easier to access programmatically and provides a dedicated field for optional `think` content.

Deltaset remains an important part of the project's history and can still be useful for projects that work with the original format.

---

# Contributing

The Delta Dataset is a collaborative project.

You can contribute by creating high-quality training examples and sharing your datasets with the community.

Contributions can cover many different subjects and formats, as long as they are useful for training AI models.

When creating data, focus on:

* Accuracy
* Clarity
* Usefulness
* Natural language
* Originality
* Consistent formatting
* High-quality responses

Avoid submitting low-quality, duplicated, misleading, or intentionally harmful training data.

---

# What Makes a Good Example?

A useful training example should provide meaningful information to the model.

For example:

```json
{"system":null,"user":"What does a Python function do?","think":null,"bot":"A Python function is a reusable block of code designed to perform a specific task. Functions can receive arguments and return values."}
```

Examples should generally avoid:

* Deliberately false information
* Spam
* Duplicate examples
* Extremely low-effort responses
* Private or sensitive personal information
* Hate or discriminatory content
* Explicit sexual content
* Content promoting harmful or illegal activities
* Data created solely to manipulate or degrade model training

The goal is not simply to increase the number of examples, but to increase the amount of **useful training data**.

---

# Using The Delta Dataset

The Delta Dataset can be used in different AI training and research projects.

Possible uses include:

* Pre-training
* Fine-tuning
* Instruction tuning
* Conversational model training
* Dataset experimentation
* Data preprocessing research
* Evaluation and benchmarking

You are not required to use a Delta model to use the dataset.

The dataset is open-source and intended to be useful beyond the models developed by Pyra Labs.

---

# Pyra Labs and Delta

The Delta Dataset is developed within the ecosystem of **Pyra Labs**.

Pyra Labs uses the dataset to support the development of its AI models, including the Delta family.

However, The Delta Dataset is a separate open-source project with a broader purpose: **building accessible, reusable, community-created training data for AI.**

---

# Community

The project started with a small amount of data, but every dataset has to start somewhere.

If you are reading this and want to help The Delta Dataset grow, create your own datasets, experiment with new examples, and share your work with the community.

You can contribute data, build projects using the dataset, or simply experiment with it and show what you created.

We would love to see what you build with it.

---

# License

The Delta Dataset is released under the **Pyra License**.

You are free to use, modify, and redistribute the dataset according to the terms of the license.

See the [LICENSE](LICENSE.md) file for the complete license text.

---

# Vision

The goal of The Delta Dataset is to make high-quality AI training data more open and accessible.

AI development should not depend entirely on closed datasets that only a small number of organizations can access.

By creating an open, collaborative dataset, the community can contribute knowledge, experiment with new ideas, and help build better AI systems together.

**The Delta Dataset is built by the community, for the community.**
