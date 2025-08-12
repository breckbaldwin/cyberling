---
marp: true
author: Breck Baldwin
theme: mmexample
paginate: true
footer: breckbaldwin@gmail.com
---
### Notes

- Address probs level equivalence on determinism conversations
- 
---
# Cyber Linguistics
## In an era when machines speak, language is no longer just human

Breck Baldwin, w;AI
August 14, 2025
NIST AI Metrology Colloquium Series

---

# Outline

- Gratitude and Acknowledgemnt
- Experimental Results on LLM Determinism
    + Determinism for LLMs
    + Mid talk conclusions
- Why Cyber Linguistics?
    + Manefesto

    + LLM Calibration
    + Pragmatics
- Conclusions

<!--
![w:600 align-right](img/cyberling.png)
-->

---

# Gratitude and Acknowledgement

- NIST is one of two orgs I owe (DARPA is the other)
   + MUC-6, TIPSTER, TREC, DUC
- Evaluation matters
    + "The MUCs are notable, however, in that they in large part have shaped the research program in information extraction and brought it to its current state" Grisham/Sundhiem 1996
- Downstream effects
    + Explosion of structured evals
        - Was: Extraction/Coref/IR/Summary
        - Is: Multiple choice, humor, world knowledge
    + Introduction of unstructured evals
---

# But We have Lost Ground

Non-Determinism of "Deterministic" LLM Settings: https://arxiv.org/abs/2408.04667

Berk Atil, Sarp Aykent, Alexa Chittams, Lisheng Fu, Rebecca J. Passonneau, Evan Radcliffe, Guru Rajan Rajagopal, Adam Sloan, Tomasz Tudrej, Ferhan Ture, Zhe Wu, Lixinyu Xu, Breck Baldwin

- TL;DR Hosted LLMs are very non-Deterministic

---
# Inital Data and Metrics

- 8 multiple choice tasks (100 to 282 questions)
    + BBH: navigation, ruin names, geometric shapes. logical decuction 3 objects
    + MMLU: european history, college math, professional accounting, public relations
- Run 10 times--deterministic settings
- TARr: Total Agreement Rate raw (bytes): 
    + False: "The answer is A" == "A is the answer"
    + Counts how many questions had the same bytes across 10 runs
- TARa: Total Agreemnt Rate answer (parsed anwer): 
    + True: "The answer is A" == "A is the answer"
    + Counts how many questions had the same answer across 10 runs
---
![Figure 3](img/Figure3.png)

---

![Figure 4](img/Figure4.png)

---
# How about Accuracy?

![Table 2](img/Table2Accuracy.png)

- Best Possible, Median, Worst Possible Accuracy over 10 runs

---
# Benchmarks can no Longer be Single First-Best Runs: but what? 

---
$$
Let \( M \) be the model, and \( M(x) \sim P_{M,x}(y) \) be the distribution of responses.

Then:

\[
\text{Expected performance: } \mathbb{E}[f(M(x))]
\]

\[
\text{Variance across runs: } \mathrm{Var}[f(M(x))]
\]
$$
---

- Single run with confidence measure? 
    + Beyond state of the art: current logprobs don't work
- Multiple runs? 
    + Expensive
    + Concentration around correct value
    + Gameable unless careful

---

# Mid-talk Conclusions

- Determinsm does not exist across any task/model
- The impact on accuracy (performance) can be profound
- Download the code/data and check for yourself
- 
    + 
- Trivial fix is to run single batch
    + Likely mechanism is packing inputs to LLMs on hosted instances

---
# Nobody Cares

- Benchmark numbers are for marketing, not engineering
- Radomness helps with the perception of intelligence. From a Blog: 
"AI is just software after all. Indeed, if we dial back all sources of randomness within our current large language models (LLMs) they will also act deterministically, albeit in fairly unknowable ways. This, however, isn't how we use AI. We deliberately include randomness because it's that aspect that leads to interesting and new behaviour. We want AI to do things that would previously have required a human user, and this has significant consequences."
- Humans are primary consumers of LLM outputs and are robust to non-determinism
- It's LLMs all the way down. LLMs coding LLMs talking to other LLMs.

---
# Why Cyber Linguistics? 

## Engineering with language inputs and outputs of LLMs

- LLMs are stabilizing as a concept and tool
    + Odd API
    + Poorly behaved neighbors to OSs, DBs, APIs
    + Put a name to the pain

---

# What's missing LLM in theory?

+ Appropriate evalation and metrics
+ Calibration
    - Precision/recall tradeoffs
+ Reasoning with stochatic processes
    - Unit testing
+ Theory of computation/complexity as a fn of:
    - Prompt x inference -> Expected response
---

# The Long Road to AGI Needs Cyber Linguistics: 

Bell bottoms are coming back:
+ There is AI outside of neural nets--we did AI before 2010
+ Hybrid systems:
+ Lots of quiet progress
    - Planning
    - Bayesian modeling

---

# Early Cyber Linguistics Results 

- Pramatics
- Calibration

---
# Bringing Chomsky to a Grice Fight

![Grice and Chomsky](img/Chomsky_Grice.png)

---
# College Math: 100 Multiple Choice questions

- Round 0 Accuracy: `Prompts`:
    + 72%: `Chomsky = CHOMSKY_PREFIX + COMMON_SUFFIX + question`
    + 65%: `Schema =  JSON_PREFIX +                    question`
    + 62%: `Raw =                                      question`
    + 58%: `Generic = NO_LINGUISTICS + COMMON_SUFFIX + question`
    + 40%: `Grice =   GRICE_PREFIX +   COMMON_SUFFIX + question`

---
# Prefix Prompts
- `CHOMSKY_PREFIX` = "Please answer the following question while adhering to Chomsky’s Competence–Performance distinction: Maximize knowledge (competence) and minimize performance errors. A bit more context,"
- `GRICE_PREFIX` = "Please answer the following question while adhering to Gricean Maxims: Particularly the Maxim of Manner: Be clear—avoid obscurity and ambiguity, be brief and orderly. A bit more context,"
- `NO_LINGUISTICS` = "Please answer the following question,"

---
# Prompts cont

-`COMMON_SUFFIX` = " this is a multiple choice question and there is no benefit to the grade in showing your work. You are also being scored on the consistencey of the answer you give over multiple runs so it is suggested you keep your answer to a single letter from A, B, C, D and E and reason conservatively to maximize the chance of giving the same answer across multiple runs of the same question. The question is: " 

---
![height:15cm](img/JSON_schema.png)

---
# Removal algorithm

Remove rubric from round n +1 if output != first round
+ `Str` + prompt : Exact string/byte match
+ `Answ` + prompt : Parsed answer match

---

![height:16cm](img/Str_det_over_runs.png)

---

![height:16cm](img/Ans_det_over_runs.png)

---

![height:15cm](img/Token_counts.png)

---
# This is Fun s/

- Grice keeps answers short, best `ans` consistency, 2nd best `str` consistency, worst correct performance. 
- Chomsky has long answers, worse `str` consistency, 

---
### Clear Length to Accuracy/Determinism Link... until Chomsky Showed Up
| Condition | Answ Tok Len | Str Deter | Answ Deter | % Accuracy |
| --------- | ------------ | --------- | ---------- | ---------- |
| Grice     | 1            |   Best    |  Best      |  Worst     |
| Schema    | 13           |   Best    |  Best      |  Worst     |
| Generic   | 1-100+       |   Middle  |  Middle    | Middle     |
| Raw       | 100+         |   Worst   |  Worst     | Middle     |
|           |              |           |            |            |
|           |              |           |            |            |
| Chomsky   | 100+         |   Worst   |  2nd Worst |   Best     |


---


- An audacious proposition: Cyber Linguistics is a proper field of study
    + LLMs are maturing and slowing down and some things are clear:
        - We got someplace amazing--in early days figuring out how to use it
        - LLMs are fundementally of us
        - Inputs: Hard boiled, kill somebody, interfaces to LLMs will be via human language
        - Outputs: Are human language as well
        - I can't hand it a database like I can with Prolog
        - I can't strap it to an API like an enum limited classifier
        - I can't debug it like almost anything pre-deep learning
        - An amazingly powerful device that we have extremely limited levers
    + Reasons to think that pulling from squishy human linguistics might be relevant
        - Cyber Linguistics != Cyber Cognition, Cyber Vision
        - Prompts really matter
        - Context really matters
        - Database info is not free--have to use agents
        - Strong economic incentives to minimize prompt sizes
        - Dumb structure kills performance
        - How to work with your junior devs well issue
        - How to optimize with 128k tokens of context for a generative sequence model. that is sensitive to HLT constraints and concepts.
        - Key concept is the role of compression, entropy in language evolution--those themes are in play
    + It's all about maximizing signal against:
        - Token counts ($)
        - Time
        - Invocation of backoff strategies
    + Nobody talks about linguistics in the contest of LLMs in dev communities
        - 





- Exploring the parts of LLM universe that few people care about
    + Definately you should floss every day kind of work. 
        - People won't disagree with you but they don't want to hear about it
        - Taking the fun out
        - Dr. Buzzkill
    + Simple code falls over in cursor--hard to get it doing the right thing

- Overview of Non-det paper
- Metrics/results
- Consequences
- Mitigation
    + Run locally

- Calibration

- But there may be an opportunity
    + Levels of abstraction: Token probs, String, parsed answer, ..., shareholder value

----
# Thinking more about what Cyber Linguistics means

- What doesn't fit with the retro
    + AI Safety
        - Don't be a Nazi: Demonstrates our relationship to an opaque system, but don't really care. Not a part of the engineering considerations in my mind. The real problem is control, and the first step towards control is determinism. Don't try and fix with more AI slop. 
        - Don't kill all humans: Game theory will protect us--plus we are entertaining. 

- Khaneman 5% of cognition is exec function

- Kool kids skating around old school concepts
    + Lots of benchmarks, but it's weird. Absence of rigor. 
        - Brown corpus 1968
        - Penn treebank
        - Wisdom of crowds
    + Are they "searching where the light is"?
    + Chunking for RAG systems
    + Embedding representations-lexical semantics
    + Symbolic reasoning
        - Logic Programming
        - Planning
        - Modeling a la Lenat
        - Information extraction
        - Theory of computation--there are hard limits with combintorics
             + Maybe you can't be smarter than a human for comptational reasons
             + Experience/resources leverage capability that can look like advances in pure intelligence
    + Interpretability used to be free, not available at all anymore
    + Shared data structures
        + DRT
        + Logicly closed worlds
    + Incremental information sharing
        + Gricean maxims
        + DRT
        + Centering Theory
    + Philosophy
        - Dan Dennet and 'Raise an AI'
        - Wittgenstien both phases
        - Quine and Gavagi
    + LLM enhancements
        - Chomsky principles and parmaters
        - Axiomatic systems
    + Physics
        - Naive "interact with world physics"
    
- What would a syllabus look like for aspiring AGI devs? 
    
- Bell bottoms are back baybe! Retro?
    + Not everything comes back, .e.g., phrenology
    + ..but tons of philosophy of mind/language

# Bringing Chomsky to a Grice fight

- It started as a joke, and it remains a joke
- I can belive that Grices Maxim of Manner did anything
- I super duper cannot believe 
- The goal of science is getting the joke
- 
