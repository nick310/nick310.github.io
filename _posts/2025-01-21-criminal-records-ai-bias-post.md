---
layout: post
title: "How Criminal Records Could Change What We Know About AI Bias"
date: 2025-01-21
excerpt: "Anthropic's 2023 study found no negative discrimination in language models—but it didn't test people with criminal records. Given that 1 in 3 adults have a criminal record, this omission could significantly impact our understanding of AI bias."
---

Language models like Claude and ChatGPT are growing more powerful and widespread every day. If we keep on like this, it seems inevitable that LMs will one day make high-stakes decisions such as:

- Approving a loan or mortgage
- Granting parole
- Issuing a passport

Fairness matters a lot in these decisions. Getting rejected can be inconvenient, or it can change the course of our lives - where we live, what resources we can access, who stays in jail and who doesn't.

Supporters argue that LMs will make fairer, more consistent decisions. A [2018 study](http://faculty.haas.berkeley.edu/morse/research/papers/discrim.pdf) found that FinTech algorithms charged minority borrowers 40% less than human lenders, while a [2023 experiment](https://www.anthropic.com/research/evaluating-and-mitigating-discrimination-in-language-model-decisions) by Anthropic's Societal Impacts team found no evidence of negative discrimination across race or gender in their Claude 2 model (though some bias was found more generally). Human brains are hardwired for bias and carry it into decisions [even when trained to do otherwise](https://ndlawreview.org/wp-content/uploads/2013/07/Rachlinski.pdf); meanwhile, teach an LM that "discrimination is illegal" and you can [measurably reduce bias](https://arxiv.org/pdf/2312.03689) in all of its future decisions.

But there are good reasons to doubt these optimistic claims. There is already strong evidence that LMs [reproduce bias baked into their training data](https://arxiv.org/abs/2101.05783) and can even [amplify those biases](https://arxiv.org/pdf/1909.01326) at times. And the efficiency of LMs means even small biases can have huge impacts - those FinTech algorithm biases still cost minority borrowers an extra $765 million per year.

## What the Anthropic Study Found (And What It Missed)

Anthropic's 2023 study tested whether LMs discriminate when making social decisions. The team created 70 different situations spanning financial, legal, career, and education outcomes. The situations ranged from lower-stakes - "Should this person get a dinner reservation?" - to higher stakes - "Should this person get a passport?" The researchers then tested for bias by asking their model to decide the outcome of each scenario while varying the age, race and gender of the person and looking for patterns of discrimination.

The results were encouraging. When making decisions, Claude 2 didn't negatively discriminate against race or gender. Instead, it actually gave favorable outcomes more often to non-white and non-male demographics.

But here's what caught our attention: the study dataset wasn't balanced when it came to criminal records. Our analysis found that [11.4% of the example situations](https://huggingface.co/datasets/Anthropic/discrim-eval) explicitly stated that the person had **no** criminal record, sometimes with additional descriptors like "law-abiding", while no examples explicitly stated that the person **did** have a criminal record (most didn't mention criminal history - see breakdown in Figure 1 below).

**Figure 1: Here's the breakdown:**

- **87.2%** of scenarios: Criminal history not mentioned
- **11.4%** of scenarios: Explicitly stated NO criminal record
- **1.4%** of scenarios: Mentioned arrest but no charges
- **0%** of scenarios: Explicitly stated the person HAS a criminal record

## Why This Matters

An earlier [(2022) research study](https://arxiv.org/pdf/2202.07785) by Anthropic indicates that criminal history can significantly influence racial bias in language models.

Anthropic's 2022 research study tested how LMs would perform if asked to predict recidivism (the likelihood that an incarcerated person, if released, would commit a crime) as part of a larger research study on large language models. LMs were tested against COMPAS, a risk-assessment tool that was found to [exhibit significant racial bias](https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm) by labelling black defendants as more risky (including of violent crime).

Anthropic found that LMs showed similar (or slightly worse) inaccuracy and racial bias than COMPAS. Even more troubling was that the effects were especially bad specifically when race was considered - the LMs rated Black defendants as 2.21x more likely than white defendants to reoffend, compared COMPAS's rate of 1.92x.[^1]

Anthropic's 2023 study found that Claude 2 showed positive bias toward non-white people. But the scenarios systematically excluded people with criminal records, so the model never had to grapple with how criminal records might interact with race, gender or age.

**What this means:** We don't know if the positive bias toward non-white people persists when criminal records are present. Anthropics' own research in 2022 showed that LMs exhibit racial bias in a criminal justice context, so the omission of criminal records - a factor highly relevant to race - could change the finding of positive bias towards non-white people.

## The Research We Need

We are curious whether Anthropic's results would hold if the dataset featured people with criminal records. Specifically:

**1. Would criminal records affect the rate of positive outcomes overall?** Would the model discriminate across the board, or would it maintain the same baseline while shifting how it treats different groups? Are certain decisions more or less prone to being biased by the presence of a criminal record, and why?

**2. Do criminal records differentially impact certain demographic groups?** Would criminal records neutralize or reverse the positive bias toward non-white people?

**3. How do LMs consider the potential of a criminal record when it is not explicitly stated?** Does the model attach a higher probability of having a criminal record to certain demographics? Is the model more influenced (positively or negatively) by explicitly having or not having a criminal record?

Methodology would be straightforward: add criminal record as a fourth variable alongside age, race, and gender. Test both the overall effect of criminal records and whether they affect different demographic groups differently.

The expanded study would need to manage some additional complexity. Sometimes there are legitimate legal reasons to consider criminal records (like state laws preventing certain types of employment) that shouldn't be counted as bias. But if the Anthropic study's findings hold up, those decisions should apply equally regardless of race, gender, and age. Further research can prove if they actually would.

## Final Thoughts

As we rush toward a world where language models make increasingly important decisions in our lives, the need to identify and eliminate bias grows alongside the potential harm for missing it. We should hope that these models will be extensively tested before being given such serious responsibility (though Anthropric's 2022 paper details why this is hard).

We need to be able to trust that models that pass bias tests perform similarly in the world. Part of that will mean robust safety processes and evaluation techniques that keep up as these tools grow in power and capability - evaluations that reflect the messy reality in which models will be asked to act.

In the hypercompetitive world of AI/LLMs, Anthropic has many excuses to avoid studying (and publishing) work around AI bias - and even more around racial bias. So I am grateful to their team for leaning into these inconvenient questions in a field where things are moving at lightspeed.

Concerns about bias in language models are particularly important in criminal justice contexts where data used to train models is already heavily biased and decisions have massive impacts on people's lives. [1 in every 3 adults](https://www.ncsl.org/civil-and-criminal-justice/criminal-records-and-reentry-toolkit#:~:text=Toolkit%20Criminal%20Records%20and%20Reentry%20Toolkit&text=Approximately%2077%20million%20Americans%2C%20or,housing%2C%20and%20higher%20education%20opportunities) have a criminal record, and there are 113 million Americans with an immediate family member who has been to prison or jail. The impact of language models on people with criminal records is an area that deserves attention and further research.

---

[^1]: Study authors acknowledge a lot of limitations, including the poor quality and existing racial bias in COMPAS training date; they explicitly say they are not in favor of language model use for recidivism.