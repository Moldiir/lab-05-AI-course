# Lab 05 — Conclusion

<!--
Read this before you write.

This file is graded by your instructor, by hand, and it is worth 6 of the 15 points.

- Type it yourself. Do not use a chatbot, an AI assistant, an AI autocomplete or a "rewrite my
  text" tool for any part of it, not even for grammar. English that is plain and a little
  clumsy but yours is better than polished text that is not.
- Use your own numbers. Every number you quote must be one your own notebook printed. Copy
  the number exactly as it appeared. A number your notebook did not print is marked as wrong.
- Answer in your own words, about 80-200 words per question. A short answer that uses your
  numbers beats a long answer that could have been written by anyone.
- Delete these comment lines if you like. Keep the three headings and the last line.
-->

## 1. Which layer changed your results the most?

Give the numbers before -> after for that layer (correct / wrong / no answer, out of 20) and say
whether it changed what the agent *can do* or only what it *admits*. If no layer changed the
number of correct answers, say so and explain what the layers did change instead.

Layer 1 changed my results the most.Before adding it, the bare agent had 16 correct answers, 4 wrong
answers and 4 no answers out of 24.After adding Layer 1, the results changed to 18 correct, 6 wrong 
and 0 no answers.This layer helped the agent continue working after tool errors instead of stopping
immediately.For example, it could receive an error message and try another tool call.So, it changed
what the agent could do, not only what it reported.Layer 2 did not change the scores compared to Layer 1.
Layer 3 kept the number of correct answers the same but reduced wrong answers from 6 to 4 and increased no answers from 0 to 2.

## 2. One failure the full harness did not fix

Pick one question that the full harness (layer 3) still gets wrong or refuses. Give its id
(q01 ... q20). Open its trace in the notebook: at which step did it go wrong, and what did
the model do instead? Name one thing you would add to the harness, and what it would cost
(extra model calls, tokens, time, or a new way to fail).

One example is q18.Even with all three layers enabled, the agent could not give a verified answer.
The model requested CPI data for Jambyl and received the values from the tool.Then it used the
calculate tool, which returned 0.055.However, the model answered 0.55 percentage points.The grounding
layer rejected this answer because 0.55 was not present in the tool results.The model repeated the same 
calculation and finally returned UNVERIFIED.I would add a calculation validation step that checks the
formula and units before accepting the final answer.This could prevent calculation mistakes, but it would add extra processing time and make the harness more complex.

## 3. Workflow or agent for the monthly ranking?

Dala Insight wants to publish, every month, "which region is highest and which is lowest on one
indicator in one year". Would you ship the fixed workflow or the agent? Use the accuracy, the
number of model calls, the tokens and the time you measured in Part 1. Then say in one sentence
what kind of question would make you choose the other one.

I would choose the fixed workflow for the monthly regional ranking. The task always has the same
structure: find the highest and lowest regions for one indicator in one year.The workflow answered
13 out of 15 questions correctly, while the bare agent answered 9 correctly.The workflow also used
fewer resources.It made 15 model calls, used 3,852 tokens and took 15.7 seconds.The bare agent made
26 calls, used 19,835 tokens and took 51.8 seconds.I would choose the agent for open questions or tasks that need several different steps, because it is more flexible.

---

I wrote this file myself, without any AI tool.
