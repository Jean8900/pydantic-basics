# Pydantic × LLM — Structured Output Validation on 27k Tweets

## Philosophy

LLMs return free text. Your application needs reliable, structured data. This notebook is about the layer in between — and why Pydantic is the right tool for it.

The goal is not performance. It is not to build the best sentiment classifier. It is to get hands-on with Pydantic as a validation framework for LLM outputs, understand precisely where and why a model fails, and build the diagnostic reflex that every serious LLM pipeline requires.

## What's inside

- **Data** — 27,480 real tweets from the Tweet Sentiment Extraction dataset, with ground truth labels (`positive`, `negative`, `neutral`)
- **Model** — Qwen2.5-0.5B-Instruct (~1GB in float16), a small but capable instruction-tuned LLM, run on GPU with batched inference
- **Exercise cell** — a challenge: how would *you* validate LLM outputs against a strict schema? Try to implement it yourself before reading further. I strongly recommend re-coding everything from scratch from that cell.
- **A worked solution** — one way to do it, using Pydantic to measure failure rates by field and constraint type

## Key takeaway

By the end, you will know exactly where the model fails — not "it sometimes produces bad output", but "69.6% of `reasoning` fields exceed 100 characters, 10.1% of `sentiment` fields are outside the valid vocabulary". That precision is what separates debugging blind from debugging with a map.

## Perspectives

This is a first pass — and there is a lot of room to improve. You could try:

- Better prompting (explicitly stating schema constraints in the prompt)
- Retry logic on `ValidationError`, injecting the error back into the prompt
- A stronger model (larger Qwen, Mistral, or even a dedicated sentiment classifier like `twitter-roberta-base-sentiment`)
- LoRA fine-tuning on the failure cases
- Regex validation on `quotation` to verify the extract is actually present in the original tweet

**If you improve the model or try a different approach, let me know — I'd love to see what you come up with and how you did it.**
