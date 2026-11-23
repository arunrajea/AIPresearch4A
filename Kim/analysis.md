The results reveal something important: **Jev is consistently faster and cheaper, but its accuracy advantage depends heavily on the classification task.**

## **1. Final results: Jev vs. three LLMs**

First, let's look at the percentage of emails where **all three classifications (purpose, urgency, and relationship) were correct simultaneously.**

All three classifications correct

Agreement with provisional reference labels. Jev was evaluated separately alongside each LLM.

Jev 1.14

Comparison LLM

<img width="809" height="355" alt="Screenshot 2026-11-23 at 10 48 58 AM" src="https://github.com/user-attachments/assets/4a439eeb-d60d-47fb-8cfd-0839b2f94e2c" />

Gemini's 74.1% is based on 158 successful responses; all other scores use 160 emails.

Jev performed substantially better than GPT-4o Mini, but GLM and Gemini both achieved higher overall three-label accuracy.

### **Accuracy by classification task**

| Model            | Purpose        | Urgency    | Relationship   |
| ---------------- | -------------- | ---------- | -------------- |
| Jev 1.14         | **95.6–96.2%** | 68.8–69.4% | **95.0–95.6%** |
| GPT-4o Mini      | 93.8%          | 48.8%      | 91.2%          |
| GLM-5.3 Flash    | 92.5%          | 75.0%      | 90.0%          |
| Gemini 3.8 Flash | 93.7%          | **83.5%**  | 93.0%          |

Jev achieved the highest accuracy in purpose and relationship classification across all three comparisons.

However, Gemini achieved the highest urgency accuracy, outperforming Jev by approximately 14 percentage points.

## **2. The most interesting discovery: urgency classification**

This is where your results get particularly valuable.

Look at how the models handled the three urgency levels:

| Actual urgency | Jev correct | GPT-4o Mini | GLM-5.3 | Gemini 3.8 |
| -------------- | ----------- | ----------- | ------- | ---------- |
| High (22)      | 17–18       | **21**      | 14      | 14         |
| Medium (56)    | **49**      | 44          | 46      | 44         |
| Low (82)       | 43–45       | 13          | 60      | **74/80**  |

Gemini evaluated 80 of the 82 low-urgency emails because two requests failed.

Here's what stands out:

- **GPT-4o Mini** was best at recognizing high-urgency emails, but it classified 69 of 82 low-urgency emails as Medium.
- **Jev** performed best on medium-urgency emails but frequently overestimated low urgency.
- **Gemini** was exceptionally strong at low-urgency classification, correctly identifying 74 of 80 emails.

This suggests the models have different classification tendencies, rather than one model being universally superior.

### **But there's an even more interesting discovery.**

All 30 promotional emails were labeled Low urgency.

Here's how each model performed:

| Model            | Promotional urgency correct |
| ---------------- | --------------------------- |
| Jev              | 0/30                        |
| GPT-4o Mini      | 0/30                        |
| GLM-5.3 Flash    | 18/30                       |
| Gemini 3.8 Flash | **30/30**                   |

Jev classified all 30 promotional emails as Medium urgency, even though it correctly identified all 30 as Promotional in the purpose category.

**That's a significant finding.**

Jev recognizes that an email is promotional, but it doesn't consistently use that information when determining urgency.

In fact, excluding promotional emails raises Jev's urgency accuracy from approximately 69% to **85%**.

This could identify a specific weakness worth fixing, rather than suggesting the entire urgency classification system is ineffective.

## **3. Speed and cost: Jev's biggest advantage**

This is where Jev performed exceptionally well.

| Model            | Average response time | Total API cost |
| ---------------- | --------------------- | -------------- |
| Jev 1.14         | **0.155–0.196s**      | **$0.0070**    |
| GPT-4o Mini      | 0.837s                | $0.0170        |
| GLM-5.3 Flash    | 4.087s                | $0.0429        |
| Gemini 3.8 Flash | 5.791s                | $0.2927        |

Compared with the corresponding Jev run:

| Comparison       | Jev faster by | Jev cheaper by |
| ---------------- | ------------- | -------------- |
| GPT-4o Mini      | 4.7×          | 59%            |
| GLM-5.3 Flash    | 26.4×         | 84%            |
| Gemini 3.8 Flash | 29.5×         | 98%            |

Jev also completed all 160 classifications without errors in each run. Gemini experienced two API errors.

The Gemini timing figure excludes its failed requests, one of which took considerably longer before timing out.

**Research finding:** A specialized decision model can deliver substantial efficiency improvements over general-purpose LLMs while maintaining competitive accuracy.

That's particularly relevant for applications processing large volumes of emails.

## **4. The expanded dataset revealed something the 100-email experiment missed**

Your original 100-email experiment produced an 86% urgency accuracy for Jev.

Now, with 160 emails, that has dropped to approximately 69%.

At first, that might look like a disappointing result.

However, the new dataset includes categories that weren't adequately represented in the original experiment.

### **Dataset composition**

Email purpose distribution

160 emails in the expanded evaluation dataset

020406080WorkSchoolPromotionalPersonal

Unlike the original experiment, your dataset now includes 30 promotional emails.

Interestingly, Jev correctly classified all 30 promotional emails by purpose but incorrectly assessed their urgency.

This is precisely why expanding a dataset matters: **it can expose weaknesses that a smaller, less diverse experiment would miss.**

However, the dataset still contains only two Personal emails. That means you cannot confidently evaluate personal-email classification performance yet.

## **5. What about reliability and consistency?**

Jev was evaluated three separate times against the same dataset.

Its results remained relatively consistent:

| Metric       | Run 1 | Run 2 | Run 3 |
| ------------ | ----- | ----- | ----- |
| Purpose      | 96.2% | 96.2% | 95.6% |
| Urgency      | 68.8% | 69.4% | 69.4% |
| Relationship | 95.6% | 95.6% | 95.0% |
| Errors       | 0     | 0     | 0     |

This suggests Jev produces relatively stable results under the tested conditions.

However, you would need repeated runs of the other LLMs to determine whether Jev is actually more consistent than its competitors.

## **6. What are the limitations?**

There are three important limitations worth mentioning in your research:

- **Reference labels:** The dataset uses provisional, AI-assisted reference labels. Independent human verification is necessary before claiming definitive real-world accuracy.
- **Category imbalance:** Only two Personal emails were evaluated, making conclusions about that category unreliable.
- **Sample size:** Although 160 emails is an improvement over 100, broader testing is necessary before generalizing these findings to real-world email classification.

These limitations don't invalidate your experiment. They simply determine how confidently you can interpret the results.

## **My conclusion so far**

Your experiment suggests that **specialized decision models can provide substantial speed and cost advantages while remaining competitive with general-purpose LLMs for structured email classification.**

Jev 1.14 consistently outperformed all three LLMs in purpose and sender-relationship accuracy. However, Gemini 3.8 Flash achieved the highest urgency accuracy and the highest overall three-label accuracy.

One particularly valuable discovery is that Jev's urgency errors are concentrated in promotional emails. This suggests that targeted improvements to its classification logic could meaningfully improve performance without necessarily sacrificing its efficiency advantages.

### **The three strongest research findings**

1. **Efficiency:** Jev was approximately 4.7–29.5 times faster and 59–98% cheaper than the general-purpose LLMs tested.
2. **Task specialization:** Jev led purpose and relationship classification, while Gemini led urgency and overall three-label accuracy.
3. **Category-specific weaknesses:** Jev's promotional-email urgency misclassification reveals a potentially correctable weakness that was not apparent in the original 100-email experiment.

**The most valuable next experiment:** Modify Jev's urgency-classification approach to address promotional emails, then rerun the same 160-email benchmark.

If that improvement significantly increases urgency accuracy without harming its other metrics, you would have evidence of a targeted, measurable improvement to your decision model—not just a comparison between existing models.
