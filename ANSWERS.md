# Midterm 1: answers

GitHub username: jitur-git
Session code: zebra-28
Fingerprint: 1806a615

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration
I used ChatGPT to understand some formulas and calculations, especially for retrieval, costs and accuracy. I used Google Colab to generate my own dataset with my GitHub username and session code. ChatGPT also helped me write short explanations in English because some technical terms were difficult for me.

## Part 1: Retrieval and cost decision

### 1a. Metrics (all 60 questions)

| config | recall@1 | recall@3 | recall@5 | MRR@10 |
|---|---|---|---|---|
| A | 0.4333 | 0.5833 | 0.6667 | 0.5115 |
| B | 0.2667 | 0.5833 | 0.8667 | 0.4696 |

### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|
| A, k=3 | 0.5833 | 0.4573 | 0.6994 |
| A, k=5 | 0.6667 | 0.5406 | 0.7727 |
| B, k=3 | 0.5833 | 0.4573 | 0.6994 |
| B, k=5 | 0.8667 | 0.7583 | 0.9309 |

### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|
| A, k=3 | 17097.97 |
| A, k=5 | 22332.82 |
| B, k=3 | 11025.61 |
| B, k=5 | 12212.22 |

### 1d. Decision (at most 150 words)

Chosen candidate: B, k=5
I chose B with k=5 because it has the highest recall (0.8667) and the annual cost is $12,212.22, which is within our $19,700 budget. Its 95% Wilson interval is 0.7583 to 0.9309.

For each language, the recall is 0.90 for English, 0.85 for Russian and 0.85 for Kazakh.

A with k=5 costs more than our budget, while the other options have lower recall. So I think B with k=5 is the best choice because it giveshigher recall while staying within the budget.

### 1e. Next measurement (at most 60 words)
Next, I would test the system with more real questions in English, Russian and Kazakh. I would also check whether the retrieved chunks actually help the model give correct answers, not just whether the right chunk is found. This would help us understand the real quality of the system.

## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H | 0.9056 | RU, degraded | 0.8333 | 0.6644 | 0.9266 | 10759.29 |
| L | 0.7667 | RU, degraded | 0.6000 | 0.4232 | 0.7541 | 18000 |

Personal-data pages per year sent abroad under H: 450775

### 2b. Memo (at most 300 words)
I compared Pipeline H and Pipeline L. Pipeline H has better accuracy (90.56%) and lower annual cost ($10,759.29). Pipeline L has 76.67% accuracy and costs $18,000 per year.

The biggest problem with H is privacy. Around 450,775 pages with personal information would be sent abroad every year. This can be risky because some documents contain names and personal identification numbers.

I would choose Pipeline L for now because the data stays on our own servers in Kazakhstan. But its accuracy is not very good, especially for degraded Russian documents, where it is only 60%.

Before using L in production, I would improve the model, test it on more documents and add manual checking for incorrect results. I would reconsider H only after checking the legal requirements and data protection measures.

## Part 3: Explain your own numbers

### Q1

Number:1.00
Why (at most 40 words): The token ratio is almost the same as the byte ratio. This means most of the Kazakh token premium comes from UTF-8 encoding, not from extra tokenizer inefficiency.

### Q2

Number: 22.1%
Why (at most 40 words): Only English chunks exceed the 512-token embedding limit. The extra tokens are truncated, so the embedding model cannot represent that part of the text. Russian and Kazakh chunks fit within the limit.

### Q3

Number: 63.8%
Why (at most 40 words): Lowering the temperature to 0.7 makes the highest-scoring token more likely. The ranking stays the same, and all five tokens can still be sampled because softmax gives each a nonzero probability.

### Q4

Number: 22.3%
Why (at most 40 words): I excluded arithmetic sequences and multiplication because they can be solved using mathematical rules. Birthdays and account numbers require remembering specific facts. A system prompt saying “never invent a fact” cannot give the model missing knowledge.

### Q5

Number:11832
Why (at most 40 words): The first message is billed 16 times because the full history is sent again on every turn. Prompt caching can reduce the cost of repeated tokens, but the conversation still contains the same input tokens.
