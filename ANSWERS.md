# Midterm 1: answers

GitHub username: aknur-gif
Session code: zebra-28
Fingerprint: 9f643169

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration
I used ChatGPT to understand some formulas and calculations, especially for retrieval, costs and accuracy. I used Google Colab to generate my own dataset with my GitHub username and session code. ChatGPT also helped me write short explanations in English because some technical terms were difficult for me.

## Part 1: Retrieval and cost decision

### 1a. Metrics (all 60 questions)

| config | recall@1 | recall@3 | recall@5 | MRR@10 |
|---|---|---|---|---|
| A | 0.6167 | 0.7333 | 0.8000 | 0.6810 |
| B | 0.4333 | 0.5500 | 0.6167 | 0.5138 |

### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|
| A, k=3 | 0.7333 | 0.6099 | 0.8287 |
| A, k=5 | 0.8000 | 0.6822 | 0.8817 |
| B, k=3 | 0.5500 | 0.4249 | 0.6691 |
| B, k=5 | 0.6167 | 0.4902 | 0.7291 |

### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|
| A, k=3 | 35426.10 |
| A, k=5 | 47040.11 |
| B, k=3 | 22920.43 |
| B, k=5 | 26197.33 |

### 1d. Decision (at most 150 words)

Chosen candidate: B, k=5

I chose B with k=5 because its annual cost is $26,197.33, which is within the $30,800 budget. Its recall is 0.6167, and the 95% Wilson interval is from 0.4902 to 0.7291.

Config A has better recall, but both A options are over the budget. B with k=3 is cheaper, but its recall is lower.

For B with k=5, recall is 0.70 for English, 0.75 for Russian and 0.40 for Kazakh. The Kazakh result is quite low, so I think this needs improvement.

I chose B with k=5 because it gives the best recall among the options that fit our budget.

### 1e. Next measurement (at most 60 words)
I would test B with k=5 on more real questions, especially in Kazakh because its recall is only 0.40. I would also check if the model gives correct answers using the retrieved chunks. This would help me understand how well the system works in practice.

## Part 2: A document pipeline you can defend

### 2a. Numbers
| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H | 0.8833 | RU clean / KK degraded | 0.8333 | 0.6644 | 0.9266 | 9706.26 |
| L | 0.8444 | KK degraded | 0.7667 | 0.5907 | 0.8821 | 7200 |

Personal-data pages per year sent abroad under H: 642400

### 2b. Memo (at most 300 words)
I would choose Pipeline L for this project.

Pipeline H has higher overall accuracy (88.33%) than Pipeline L (84.44%). However, H costs $9,706.26 per year, while L costs $7,200 per year.

Another important difference is data privacy. Pipeline H is hosted abroad, and about 642,400 pages containing personal data would be sent abroad every year. Pipeline L is hosted locally in Kazakhstan, so it is a better option for keeping this data within the country.

The weakest result for H is 83.33% (RU clean and KK degraded), with a 95% Wilson interval of 66.44% to 92.66%. For L, the weakest result is KK degraded at 76.67%, with an interval of 59.07% to 88.21%.

I understand that Pipeline L has lower accuracy, especially for degraded Kazakh documents. I would improve this by checking low-quality scans, reviewing errors and testing the system regularly.

I choose Pipeline L because it is cheaper and reduces the need to send personal data abroad. However, local hosting alone does not guarantee legal compliance, so data protection requirements must still be checked.

## Part 3: Explain your own numbers

### Q1

Number: 1.54

Why (at most 40 words): Kazakh uses more tokens than English. Some of this difference comes from UTF-8 encoding, but even after accounting for bytes, Kazakh still needs 1.54 times more tokens. This shows that tokenization is less efficient for Kazakh.

### Q2

Number: 526

Why (at most 40 words): The sentence starts at token 526, but the embedding model has a 512-token limit. Therefore, the sentence is beyond the limit and will be silently truncated. The model will not include this important information in the embedding.

### Q3

Number: 78.2%

Why (at most 40 words): With temperature 1 and top-p 0.95, only the three most probable tokens are kept. Their probabilities are normalized again. After normalization, the first token has a 78.2% chance of being selected.

### Q4

Number: 32.1%

Why (at most 40 words): I used the error rates for factual birthdays and account numbers. Their weighted average is 32.1%. Arithmetic questions are excluded because they can be solved using calculations, while missing factual information cannot be recovered from a system prompt alone.

### Q5

Number: 7.25

Why (at most 40 words): The model was trained on 7.25 times more tokens than the Chinchilla-optimal amount for 70 billion parameters. This means it is over-trained relative to the compute-optimal Chinchilla scaling rule.
