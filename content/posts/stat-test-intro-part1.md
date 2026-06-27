---
title: "Experimentation for Business Decisions: Beyond Basic A/B Testing (Part 1)"
date: 2026-06-20T00:00:00Z
draft: false
---

There are many Medium blogs that explain statistical tests—particularly A/B tests and multivariate tests. However, I’ve found they often lack business context and depth. In this series, I want to strike a middle ground: providing more real‑world context and the extra depth that many of those blogs miss. I’ll approach this through a case study.

<!-- Markdown syntax -->
![Store Display](/store-display.png)
*Figure 1: Illustrating the whole problem statement of store shelf display allocation. (this one is created by Gemini AI)*


# Why do we need statistical testing (or experimentation)?
Let’s think about a concrete scenario. Suppose you’re a data scientist (or analyst) at a large retail company. You have many stakeholders who don’t have much background in statistics, but they do have strong business knowledge that goes beyond the numbers in a spreadsheet.

Your business makes money like a typical brick‑and‑mortar retailer. Your company buys products from producers and sells them to consumers. You have limited money, limited shelf space, and a limited number of stores, limited space to put your display. As a data scientist, you need to help the company sell more products within all of these constraints.

## Scenario: Store Display
One of the producers comes to you and says you need to give them more display space in all of your stores compared to other producers. Their argument: when they have more display, your overall sales increase because they are the market leader, so a 1% increase in their product sales will mean more for your revenue than a 1% increase for another producer’s product. As a retailer, you currently give similar shelf slots to all producers, so the argument sounds plausible.

Now the head of sales says, “Their argument makes sense! We should just give more slots to the market leader.” The head of business development disagrees: “If we do that, we might lose the opportunity to sell higher‑value products or new launches—products that won’t have much volume initially but give us more margin.”

As a data scientist, you need to help them decide: does it make sense to tie the number of display slots to a product’s market share?

To understand why statistical testing (or experimentation) is needed, let’s audit several common suggestions.


### Let’s do a full rollout and compare the results afterwards (pre‑post)
This is the most common suggestion, but it often clouds the right conclusions. The main reason is seasonality and external factors. What if the test coincides with a major holiday, payday, or a huge macroeconomic change? These external factors will have a larger effect on the increase/decrease of sales than the display changes. Another reason against it is **regression to the mean**. Suppose the supplier approaches us immediately after experiencing an unusually poor month. Even if we do nothing, sales will tend to move closer to their long-term average over time. If we implement the new display strategy immediately afterward, we may mistakenly attribute this natural recovery to our intervention.

### Let’s just compare the stores that already give them more space
Store managers who break the rules probably differ in a dozen other ways: they might be more commercially aggressive, located in higher‑footfall areas, or serve a demographic that already prefers the market leader’s product. Any difference you observe could be due to the manager’s skill, the store’s location, or a hundred confounders. This is an example of **selection bias**.

### Let’s ask the regional managers what they think
This is anecdotal aggregation dressed as domain expertise. Regional managers are brilliant at reading their local markets, but they are also subject to **availability bias** (they remember the weekend the market leader had a flashy promotion) and **confirmation bias** (they notice the sales bump after giving extra space but don’t notice when extra space coincided with a dip). The human brain is a terrible control group. Use their expertise for generating hypotheses, not for confirming them.

| Common suggestion              | Why it fails                           |
|--------------------------------|----------------------------------------|
| Pre‑post full rollout          | Seasonality, regression to the mean    |
| Compare rule‑breaking stores   | Selection bias, confounders            |
| Ask regional managers          | Availability bias, confirmation bias   |



### So what should we do?
The solution is a controlled experiment where we randomly split stores into treatment and control, then compare outcomes using a statistical test. That test answers the key question: given the natural week‑to‑week and store‑to‑store variation, can we be confident the difference we see isn’t just noise? To run such an experiment, we need a clear design—below are the four steps that will get us there.

# How to design the experiment
Experiment design is a complicated subject, but we can outline the steps that, in my experience, cover 95% of most business cases.

## 1. Define the Hypothesis
What do I mean by hypothesis? In statistical terms, we have two competing statements. The **alternative hypothesis** is what we hope to demonstrate: giving display slots based on market share will increase total store profit. The **null hypothesis** is the sceptic’s default position: giving shelf space proportional to market share makes no difference to store profit. Our experiment will test whether we can reject that null.

## 2. Define the success metrics
By success metrics, I mean the measures we’ll use to judge the efficacy of our treatment. We need three types:

- **Primary metric:** Defines the success or failure of the treatment. Here, it’s total store profit.
- **Guardrail metrics:** Secondary metrics that ensure we aren’t breaking something else while improving the primary metric. In our case, total units sold is a guardrail—we don’t want to increase profit if it comes at the cost of a large drop in volume.
- **Tracking metrics:** These help explain *why* the primary metric moved. Examples include display visibility rate (if we have the technology), display pickup rate, or brand recall (if we run a consumer survey). We can also measure compliance rate and out‑of‑stock rate to diagnose why the experiment might fail to show an effect.

## 3. Define the treatment and control
We’ll randomly pick which stores get the new display rule and which keep the status quo. Randomisation is what breaks the selection bias we worried about earlier—it makes the two groups comparable on average across all the confounders we can’t measure.

However, many questions remain: How many stores should be eligible for the test? How long should we run the experiment? I’ll cover these in detail in the next post.

## 4. Define the analysis approach

Once the experiment is complete, we need a method to determine whether the observed difference is larger than what we would expect from normal store-to-store variation. This is where statistical testing enters the picture. However, statistical testing is only one component of a reliable experiment.
A perfectly chosen statistical test cannot rescue a poorly designed experiment. Most experimentation mistakes occur long before the analysis begins.

In Part 2, we'll discuss sample size, experiment duration, statistical power, and the analytical techniques commonly used to evaluate experimental results.

### What’s next?
We've seen why intuition, historical comparisons, and anecdotal evidence often fail to answer causal business questions. The core challenge is separating the effect of an intervention from everything else happening in the business.

Well-designed experiments solve this problem through clear hypotheses, carefully selected metrics, and randomised treatment assignment. In Part 2, we'll move from experiment design to experiment execution: determining sample size, deciding experiment duration, and selecting appropriate statistical methods for analysis