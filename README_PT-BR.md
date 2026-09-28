---
categoria de objetivo:
- texto-para-texto
idiomas:
- pt
- en
---

---

license: mit
task_categories:

* text-generation
  language:
* pt
* en
  pretty_name: The Delta Dataset

---

# The Delta Dataset V2

**The Delta Dataset** é um dataset colaborativo e open-source criado para ajudar no desenvolvimento e aprimoramento da próxima geração de modelos de inteligência artificial.

O projeto é desenvolvido pela **Pyra Labs** e pode ser utilizado para treinar e ajustar modelos Delta, assim como outros modelos e projetos de IA.

Em vez de ser limitado a um único modelo ou arquitetura, o objetivo do The Delta Dataset é fornecer um espaço aberto onde pessoas possam criar, compartilhar, melhorar e reutilizar dados de treinamento de alta qualidade.

---

## Idioma

Este README está disponível em inglês e português.

**[🇺🇸 English](README.md)** · **[🇧🇷 Português (Brasil)](README_PT-BR.md)**

> 🇺🇸 **Want to read this README in English?**
> [Read the English README](README.md)

---

## Sobre o Dataset

O The Delta Dataset é desenvolvido como um **dataset colaborativo para treinamento de modelos de IA**.

Qualquer pessoa pode contribuir com exemplos sobre assuntos como:

* Programação
* Matemática
* Ciências
* História
* Geografia
* Idiomas
* Raciocínio
* Conhecimento geral
* Conversas
* Escrita criativa
* Explicações
* Uso de ferramentas
* E outros tipos de dados úteis para treinamento de IA

A ideia é que o dataset cresça continuamente por meio das contribuições da comunidade.

A Pyra Labs utiliza o The Delta Dataset no desenvolvimento de seus próprios modelos, mas o dataset não é limitado aos modelos da Pyra Labs. Outros pesquisadores, desenvolvedores e projetos de IA também podem utilizá-lo de acordo com a licença.

---

# Deltaset

**Deltaset** é o formato textual original criado para o The Delta Dataset.

Ele representa exemplos de conversas utilizando tokens especiais:

```dataset-deltaset.txt id="m8q2kf"
[SYS] Você é Delta Ultra Mini.
[SEP]

[USR] O que é Python?
[SEP]

[ASS] Python é uma linguagem de programação de alto nível...
[SEP]
```

O formato utiliza tokens para separar diferentes partes da conversa:

* `[SYS]` — Instrução do sistema
* `[USR]` — Mensagem do usuário
* `[ASS]` — Resposta do assistente
* `[SEP]` — Separador entre seções

O Deltaset foi criado para ser simples, legível e fácil de produzir manualmente.

---

# Formato da V2

A segunda versão do The Delta Dataset introduz um formato estruturado baseado em **JSONL**.

Em vez de representar os exemplos utilizando tokens especiais, cada exemplo é armazenado como um objeto JSON contendo quatro campos:

```json id="p6w1zc"
{
  "system": "...",
  "user": "...",
  "think": "...",
  "bot": "..."
}
```

### Campos

* `system` — Instrução opcional que define o comportamento ou contexto do assistente.
* `user` — Mensagem ou solicitação do usuário.
* `think` — Conteúdo opcional de raciocínio associado à resposta.
* `bot` — Resposta final do assistente.

Os campos `system` e `think` podem receber `null` quando não estiverem presentes.

Os campos `user` e `bot` são obrigatórios.

---

## Exemplo com instrução do sistema e raciocínio

````json id="v7k3na"
{
  "system": "Você é Delta, um assistente de programação prestativo e técnico. Explique conceitos de programação com clareza, escreva código funcional, mantenha boas práticas e adapte a resposta à linguagem solicitada. Quando houver erros, identifique a causa e apresente uma correção objetiva.",
  "user": "Como faço um loop que imprime os números de 1 a 10 em Python?",
  "think": "A tarefa pede um exemplo simples de repetição. Em Python, range(1, 11) gera os valores de 1 até 10, pois o valor final não é incluído. Vou mostrar um loop for curto e funcional.",
  "bot": "Você pode usar um loop `for` com `range()`:\n\n```python\nfor i in range(1, 11):\n    print(i)\n```\n\nO `range(1, 11)` começa em 1 e termina antes de 11, então imprime os números de 1 a 10."
}
````

---

## Exemplo sem instrução do sistema ou raciocínio

Nem todo exemplo precisa de uma instrução do sistema ou de um campo de raciocínio.

Nesses casos, os campos correspondentes podem ser definidos como `null`:

```json id="vf845a"
{
  "system": null,
  "user": "Oi :)",
  "think": null,
  "bot": "Oi! 😊 Tudo bem por aí?"
}
```

---

# Estrutura JSONL

A V2 do The Delta Dataset utiliza **JSON Lines (JSONL)**.

Cada exemplo de treinamento é um objeto JSON independente. No dataset, cada objeto é armazenado em sua própria linha.

Por exemplo:

```json id="q4s8md"
{"system":null,"user":"Oi :)","think":null,"bot":"Oi! 😊 Tudo bem por aí?"}
{"system":"Você é Delta, um assistente de programação prestativo.","user":"Como faço um loop em Python?","think":"O usuário precisa de um exemplo básico de loop em Python.","bot":"Você pode usar um loop `for` com `range()`."}
```

Essa estrutura permite que os exemplos sejam processados individualmente e facilita operações de streaming, pré-processamento, filtragem e treinamento em larga escala.

Alternativamente, um exemplo completo pode ser escrito em uma única linha, sem formatação desnecessária:

```json id="h59kx0"
{"system":"Você é Delta, um assistente de programação prestativo e técnico. Explique conceitos de programação com clareza e escreva código funcional.","user":"Como faço um loop que imprime os números de 1 a 10 em Python?","think":"A tarefa pede um exemplo simples de repetição utilizando um loop for em Python.","bot":"Você pode usar um loop `for` com `range()` para imprimir os números de 1 a 10."}
```

---

# Da V1 para a V2

A V2 altera a representação interna dos exemplos do dataset, mantendo o propósito principal do projeto.

### V1

A versão original utilizava o formato textual **Deltaset**:

```dataset-deltaset.txt id="n2c7vx"
[SYS] Você é Delta Ultra Mini.
[SEP]

[USR] O que é Python?
[SEP]

[ASS] Python é uma linguagem de programação...
[SEP]
```

### V2

A nova versão utiliza uma estrutura JSONL:

```json id="x5m9rb"
{"system":"Você é Delta Ultra Mini.","user":"O que é Python?","think":null,"bot":"Python é uma linguagem de programação..."}
```

A nova estrutura facilita o acesso individual aos campos por meio de ferramentas e pipelines de processamento de dados e também adiciona um campo dedicado para conteúdo opcional de `think`.

O Deltaset continua sendo uma parte importante da história do projeto e pode continuar sendo útil para projetos que trabalham com o formato original.

---

# Contribuindo

O The Delta Dataset é um projeto colaborativo.

Você pode contribuir criando exemplos de treinamento de alta qualidade e compartilhando seus próprios datasets com a comunidade.

As contribuições podem abordar diversos assuntos e formatos, desde que sejam úteis para o treinamento de modelos de IA.

Ao criar dados, procure manter:

* Precisão
* Clareza
* Utilidade
* Linguagem natural
* Originalidade
* Formatação consistente
* Respostas de alta qualidade

Evite enviar dados de baixa qualidade, duplicados, enganosos ou criados intencionalmente para prejudicar o treinamento de modelos.

---

# O que torna um exemplo bom?

Um bom exemplo de treinamento deve fornecer informações úteis e significativas para o modelo.

Por exemplo:

```json id="j3v6pc"
{"system":null,"user":"O que uma função faz em Python?","think":null,"bot":"Uma função em Python é um bloco reutilizável de código criado para executar uma tarefa específica. Funções podem receber argumentos e retornar valores."}
```

Os exemplos devem evitar:

* Informações deliberadamente falsas
* Spam
* Exemplos duplicados
* Respostas extremamente pouco úteis
* Informações pessoais privadas ou sensíveis
* Conteúdo de ódio ou discriminatório
* Conteúdo sexual explícito
* Conteúdo que promova atividades prejudiciais ou ilegais
* Dados criados exclusivamente para manipular ou degradar o treinamento de modelos

O objetivo não é simplesmente aumentar o número de exemplos, mas aumentar a quantidade de **dados de treinamento úteis**.

---

# Utilizando o The Delta Dataset

O The Delta Dataset pode ser utilizado em diferentes projetos de treinamento e pesquisa em IA.

Alguns exemplos de utilização incluem:

* Pré-treinamento
* Fine-tuning
* Instruction tuning
* Treinamento de modelos conversacionais
* Experimentação com datasets
* Pesquisa em pré-processamento de dados
* Avaliação e benchmarking

Você não precisa utilizar um modelo Delta para usar o dataset.

O dataset é open-source e foi criado para ser útil além dos modelos desenvolvidos pela Pyra Labs.

---

# Pyra Labs e Delta

O The Delta Dataset é desenvolvido dentro do ecossistema da **Pyra Labs**.

A Pyra Labs utiliza o dataset para apoiar o desenvolvimento de seus modelos de IA, incluindo a família de modelos Delta.

No entanto, o The Delta Dataset é um projeto open-source independente, com um objetivo mais amplo: **criar dados de treinamento acessíveis, reutilizáveis e produzidos de forma colaborativa para modelos de IA.**

---

# Comunidade

Atualmente, o The Delta Dataset possui uma quantidade pequena de dados, mas todo dataset precisa começar de algum lugar.

Se você está lendo isso e quer ajudar o projeto a crescer, crie seus próprios datasets, experimente novos exemplos e compartilhe seu trabalho com a comunidade.

Você pode contribuir com dados, criar projetos utilizando o dataset ou simplesmente experimentar com ele e mostrar o que conseguiu criar.

Nós vamos adorar ver o que você criou com o dataset.

---

# Licença

O The Delta Dataset é distribuído sob a **Licença Pyra**.

Você pode usar, modificar e redistribuir o dataset de acordo com os termos da licença.

Consulte o arquivo [LICENSE](LICENSE.md) para ver o texto completo da licença.

---

# Visão

O objetivo do The Delta Dataset é tornar dados de treinamento de alta qualidade mais abertos e acessíveis.

O desenvolvimento de IA não deve depender exclusivamente de datasets fechados aos quais apenas um pequeno número de organizações possui acesso.

Ao criar um dataset aberto e colaborativo, a comunidade pode contribuir com conhecimento, experimentar novas ideias e ajudar a desenvolver sistemas de IA melhores em conjunto.

**The Delta Dataset é construído pela comunidade, para a comunidade.**
