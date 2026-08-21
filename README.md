# PrashnaSathi

### Ask the right question before looking for the answer.

Large Language Models such as ChatGPT, Claude and Gemini can provide remarkably useful advice on many everyday problems. The difficulty is that useful answers often depend on asking the right question and providing the right context.

Most people are not prompt engineers. More importantly, they may not know what information is relevant to the problem they are trying to solve.

PrashnaSathi is an experimental LLM-based tool designed to address this problem.

It does not attempt to answer the user's problem.

Instead, it talks to the user, understands the situation, gathers relevant facts, organises those facts into a coherent story, and finally generates a detailed prompt that the user can submit to an LLM of their choice.

The objective is simple:

> PrashnaSathi helps you ask the right question.  
> Your chosen LLM provides the answer.


## How It Works

PrashnaSathi separates the process into three distinct stages:

1. Get Facts
2. Build Story
3. Generate Prompt

The resulting prompt is then taken outside PrashnaSathi and submitted by the user to ChatGPT, Claude, Gemini or another suitable LLM.

![PrashnaSathi Architecture](https://raw.githubusercontent.com/prithwis/PrashnaSathi/refs/heads/main/Images/PrashnaSathi.png)


## 1. Get Facts

PrashnaSathi begins with an interactive conversation.

Rather than asking a fixed questionnaire, an LLM generates questions appropriate to the current topic and uses the user's previous answers to decide whether clarification is required.

The questioning process has two components:

- a common, domain-independent Fact Gathering Role that defines how questions should be asked;
- a domain Role that defines what topics should be explored.

The Python program retains deterministic control over the interview structure. It controls the current topic, the maximum number of supplementary questions, and progression between topics.

The LLM is responsible for the semantic task: deciding what intelligent question should be asked within the current topic.

This separation is deliberate. Things that can be controlled deterministically should remain under program control rather than being delegated to an LLM.

The output of this stage is a Transcript.


## 2. Build Story

A raw interview transcript is not necessarily the best representation of a person's situation.

The Story Builder therefore converts the question-and-answer transcript into a coherent factual narrative.

Its role is strictly limited to restructuring and consolidating information. It should not provide advice, infer conclusions or solve the user's problem.

The output is a Story representing PrashnaSathi's understanding of the situation.

This intermediate representation is important because it can be shown to the user for review and correction before proceeding further.


## 3. Generate Prompt

The Prompt Generator converts the reviewed Story into a self-contained prompt.

The prompt contains the relevant background, circumstances, constraints, preferences and objectives required by an external LLM to analyse the problem intelligently.

PrashnaSathi stops here.

It does not answer the generated prompt.

The user is free to copy the prompt to ChatGPT, Claude, Gemini or any other LLM of their choice.


## Domain Independence

PrashnaSathi is intended to be domain-independent.

The underlying pipeline remains:

```text
Domain Role
     +
Generic Fact Gathering Role
     |
     v
  Get Facts
     |
     v
 Transcript
     |
     v
 Build Story
     |
     v
   Story
     |
     v
Generate Prompt
     |
     v
 LLM Prompt
     |
     v
User's Chosen LLM
```

Only the domain Role needs to change when PrashnaSathi is applied to a different kind of problem.

For example, possible domains could include:

- career decisions;
- problems faced by small businesses;
- educational choices;
- workplace situations;
- other everyday decision problems.

These domains will be added incrementally as the project develops.


## Current Prototype

The current version is an early prototype developed in Google Colab using Python and the OpenAI API.

The first experimental domain is career decision-making for someone who is approaching graduation or has recently graduated.

The prototype is deliberately simple. The immediate objective is to understand how effectively an LLM can conduct a structured but adaptive fact-gathering conversation and transform the resulting information into a useful prompt.

A user-friendly interface and additional domains can be added after the underlying interaction architecture has stabilised.


## Design Principles

PrashnaSathi currently follows a few basic principles:

- Ask before answering.
- Separate fact gathering from interpretation.
- Keep deterministic control in Python where possible.
- Use the LLM where semantic judgement is required.
- Keep domain knowledge separate from generic interrogation logic.
- Preserve the user's own facts, constraints and uncertainties.
- Allow the user to review the reconstructed Story.
- Generate prompts, not answers.
- Let the user choose the LLM that ultimately provides the advice.


## Status

Experimental / Work in Progress.

The architecture, Role files, prompts and code are expected to evolve significantly as additional scenarios are tested.


## License

PrashnaSathi is released under the MIT License.
