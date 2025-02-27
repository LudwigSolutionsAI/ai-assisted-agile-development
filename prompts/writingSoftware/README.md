# Software development prompt library

Much of this inspiration was taken from:

https://harper.blog/2025/02/16/my-llm-codegen-workflow-atm/

## Greenfield Development Workflow

### Step #1 - plan with idea-brainstorming.xml and brainstorming-summary.xml
### Step #2 - create detailed plan with software-planning-tdd.xml
### Step #3 - implement with AI assitant

* set up the repo (boilerplate, uv init, cargo init, etc)
* start aider
* paste prompt into aider
* watch aider dance ♪┏(・o･)┛♪
* aider will run tests, or you can run app to verify
* if it works, move on to next prompt
* if it doesn’t work, Q&A with aider to fix
* rinse repeat ✩₊˚.⋆☾⋆⁺₊✧

## Iteration in existing codebase

1. Use repomix to grab repo context for LLM

Example of Mise rules:
https://github.com/harperreed/harper.blog/blob/main/.mise.toml