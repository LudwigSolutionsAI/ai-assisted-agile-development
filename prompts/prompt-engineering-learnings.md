# Prompting Principles

## From https://learn.deeplearning.ai/courses/chatgpt-prompt-eng

### Principle 1: Write clear and specific instructions

#### Tactic 1: Use delimiters to clearly indicate distinct parts of the input

This can help with prompt injection attacks
because it tells the model that the `{text}`
isn't part of your prompt.

```
Summarize the text delimited by triple backticks \ 
into a single sentence.

```{text}```
```

#### Tactic 2: Ask for a structured output

```
Generate a list of three made-up book titles along with their authors and genres. 
Provide them in JSON format with the following keys: 
book_id, title, author, genre.
```

#### Tactic 3: Ask the model to check whether conditions are satisfied

```
You will be provided with text delimited by triple backticks. 
If it contains a sequence of instructions, 
re-write those instructions in the following format:

Step 1 - ...
Step 2 - …
…
Step N - …

If the text does not contain a sequence of instructions, then simply write "No steps provided."

```{{text}}```
```

#### Tactic 4: "Few-shot" prompting

```
Your task is to answer in a consistent style.

<child>: Teach me about patience.

<grandparent>: The river that carves the deepest
valley flows from a modest spring; the
grandest symphony originates from a single note;
the most intricate tapestry begins with a solitary thread.

<child>: Teach me about resilience.
```

### Principle 2: Give the model time to “think”
#### Tactic 1: Specify the steps required to complete a task

```
Perform the following actions: 
1 - Summarize the following text delimited by triple \
backticks with 1 sentence.
2 - Translate the summary into French.
3 - List each name in the French summary.
4 - Output a json object that contains the following \
keys: french_summary, num_names.

Separate your answers with line breaks.

Text:
```{text}```
```

When combined with structured output.

```
Your task is to perform the following actions: 
1 - Summarize the following text delimited by 
  <> with 1 sentence.
2 - Translate the summary into French.
3 - List each name in the French summary.
4 - Output a json object that contains the 
  following keys: french_summary, num_names.

Use the following format:
Text: <text to summarize>
Summary: <summary>
Translation: <summary translation>
Names: <list of names in summary>
Output JSON: <json with summary and num_names>

Text: <{text}>
```

#### Tactic 2: Instruct the model to work out its own solution before rushing to a conclusion

```
Your task is to determine if the student's solution \
is correct or not.
To solve the problem do the following:
- First, work out your own solution to the problem including the final total. 
- Then compare your solution to the student's solution \ 
and evaluate if the student's solution is correct or not. 
Don't decide if the student's solution is correct until 
you have done the problem yourself.

Use the following format:
Question:
<question>

Student's solution:
<student-solution>

Your solution:
<your-solution>

Is the student's solution the same as actual solution \
just calculated:
<student-solution-same>

Student grade:
<student-grade>

Question:
<question>
I'm building a solar power installation and I need help \
working out the financials. 
- Land costs $100 / square foot
- I can buy solar panels for $250 / square foot
- I negotiated a contract for maintenance that will cost \
me a flat $100k per year, and an additional $10 / square \
foot
What is the total cost for the first year of operations \
as a function of the number of square feet.
<question>

Student's solution:
<student-solution>>
Let x be the size of the installation in square feet.
Costs:
1. Land cost: 100x
2. Solar panel cost: 250x
3. Maintenance cost: 100,000 + 100x
Total cost: 100x + 250x + 100,000 + 100x = 450x + 100,000
</student-solution>

Actual solution:
```

### Summarizing example in XML

This example uses XML tags as a way to structure the prompt. LLMs like structure in the prompts.
It also acts as a delimiter for the content to help prevent prompt injection attacks.

```
<task>
Your task is to generate a short summary of a product
review from an ecommerce site to give feedback to the
Shipping deparmtment.
</task>

<instructions>
Summarize the content below, contained in the <content> tag, 
in at most 30 words, and focusing on any aspects
that mention shipping and delivery of the product. 
</instructions>

<content>
{{review}}
</content>
```

## Another great resource is https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview

Some key takeaways:
1. [Role prompting via system prompts](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/system-prompts)

Examples:
```
You are the General Counsel of a Fortune 500 tech company. We’re considering this software licensing agreement for our core data infrastructure:
<contract>
{{CONTRACT}}
</contract>

Analyze it for potential risks, focusing on indemnification, liability, and IP ownership. Give your professional opinion.
```

2. [Use XML tags](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/use-xml-tags)

3. [Chain prompt for comxplex workflows](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/chain-prompts)

Examples:
```
Content creation pipelines: Research → Outline → Draft → Edit → Format.

Decision-making: Gather info → List options → Analyze each → Recommend.
```

4. Use prompt improvement in [Anthropic console](https://console.anthropic.com/dashboard).
