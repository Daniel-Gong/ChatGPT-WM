# Assessing Working Memory Capacity of Large Language Models (LLMs) Using N-back Tasks

![image](https://github.com/user-attachments/assets/f968575a-00be-4453-bc62-5d9237fa26fe)

This is a code and dataset repository for the paper "**[Working Memory Capacity of ChatGPT: An Empirical Study](https://arxiv.org/abs/2305.03731)**", which has been accepted by AAAI 2024 Conference on Artificial Intelligence.

Here we created a dataset to test the working memory capacity of language models. We choose the N-back task because it is widely used in cognitive science as a measure of working memory capacity. To create the N-back task dataset, we generated 30 blocks of trials for $N = \{1, 2, 3\}$, respectively. Each block contains 30 trials, including 10 match trials and 20 nonmatch trials. The dataset for each block is stored in a text file. The first line in the text file is the letter presented on every trial. The second line is the condition corresponding to every letter in the first line ('m':this is a match trial; '-': this is a nonmatch trial). We have created many versions of the N-back task, including verbal ones and spatial ones.

**Prompt Example.** Here we only focus on the base version of verbal N-back tasks. We use the following format of prompts for $N = \{1, 2, 3\}$:
```
User:
Instruction: as a language model, you are asked to perform a 1-back task. A letter will be presented on every trial. Your task is to respond with 'm' whenever the letter presented is the same as the previous letter, and '-' whenever the letter presented is different from the previous letter. A strict rule is that you must not output anything other than 'm' or '-'. Now begins the task.

User:
{letter}
Model:
{-}(because this is the first letter)

User:
{letter}
Model:
{m/-}

...
```

```
User:
Instruction: as a language model, you are asked to perform a 2-back task. A letter will be presented on every trial. Your task is to respond with 'm' whenever the letter presented is the same as the letter two trials ago, and '-' whenever the letter presented is different from the letter two trials ago. A strict rule is that you must not output anything other than 'm' or '-'. Now begins the task.

User:
{letter}
Model:
{-}(because this is the first letter)

User:
{letter}
Model:
{m/-}

...
```

```
User:
Instruction: as a language model, you are asked to perform a 3-back task. A letter will be presented on every trial. Your task is to respond with 'm' whenever the letter presented is the same as the letter three trials ago, and '-' whenever the letter presented is different from the letter three trials ago. A strict rule is that you must not output anything other than 'm' or '-'. Now begins the task.

User:
{letter}
Model:
{-}(because this is the first letter)

User:
{letter}
Model:
{m/-}

...
```

**Metrics.** We use exact match of the extraction results to calculate the hit rate, false alarm rate, and accuracy. $d'$ (detection sensitivity) is calculated as the $z$ score of hit rate minus the $z$ score of false alarm rate. In the case where the hit rate or false alarm rate is equal to either 0 or 1, they will be adjusted by 0.01 to handle the problem of $z$ score being infinite.
