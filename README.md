# 🕵️ I almost believed this dataset. Then a keyboard showed up in the Clothing aisle.

📦 **Dataset:** Amazon Sales Dataset by Rohit kumar
🔗 https://www.kaggle.com/datasets/rohiteng/amazon-sales-dataset
📝 **Author's note:** "Although the data is artificially generated"

This is a practice dataset, not Amazon's real business. I used it to answer one question: **before I analyze any dataset, how do I find out whether I can trust it?**

## 😬 How I almost got fooled

I filtered the data down to successful orders (`Delivered` and `Shipped`): **89,820 rows across 20 US cities**. Everything looked normal. Clean columns, no missing values, plenty of rows.

Then I looked at what was sitting in each category. A `Mechanical Keyboard` was filed under **Clothing**. So was a `Children's Book`. A `Cookware Set` was under **Electronics**.

My first thought was not "this is fake." My first thought was *"maybe Amazon just sells weird combinations."* That is the dangerous moment. Clean-looking data gives you a reason to explain away anything strange.

But a keyboard is not a shirt. The products were not just oddly grouped, they were **in the wrong place**, as if someone had shuffled the shelf labels. That was the moment I stopped analyzing and started auditing.

## 📉 The second warning sign: a suspiciously flat chart

I added up revenue and shipping cost for each of the 20 cities.


<img width="1190" height="789" alt="1000012497" src="https://github.com/user-attachments/assets/c1744008-e58f-47af-af8d-9a7c32e47386" />

Every city landed around **$4.2 million** in revenue and about **$33,000** in shipping. The shipping-to-revenue ratio sat between **0.80% and 0.82%** in all 20 cities. Real markets are lumpy: some cities are bigger, some customers cost more to reach. This looked like a table with a coat of paint.

The trap here is a different one. Charlotte shows $4.29M and San Diego $3.96M. It is very tempting to write a report asking *why San Diego is underperforming*. So I needed to know: is that 8% gap a real pattern, or just what dice would give me?

## 🧙 The Doctor Strange test (or: I checked my hunch, then found out I was late to the party)

I'll be honest about how this went. When I started, **I had not read what the author said about the dataset.** I just had a feeling. Keyboards in the Clothing aisle. Twenty cities with almost identical revenue. It all felt too tidy, but a feeling is not evidence, so I decided to test it.

**The theory:** if the data is random, the `City` column carries no information. Then dealing orders out to cities at random should look just like the real thing.

**The test:** I borrowed an idea from Doctor Strange. In *Infinity War* he looks through 14,000,605 possible futures to find the one where the heroes win. I had a smaller budget: **500 futures**. In each one I shuffled the `City` column like a deck of cards (every order keeps its real revenue, but gets a random city), then measured how uneven revenue was across the 20 cities (the coefficient of variation, CV).

**The prediction:** if I was right, my real data would be just one more ordinary universe among the 500.

**The result:**
- 500 random universes: unevenness between `1.52%` and `2.35%`
- My real data: `1.86%`

Right in the middle of the crowd. The theory held: the real data behaves like a universe where orders were dealt to cities by dice.

**Plot twist** 🎬 Only after that did I open the dataset page and read the description.The author had said it from the start. My test, built on nothing but a hunch and a shuffled deck of cities, had arrived at the same answer on its own.

I like that ending, because it tells me the method works even when nobody warns you in advance. Real clients will not come with a note saying "this data is simulated."

**What the test shows:** differences between cities are no bigger than random assignment would produce. Asking *"why is San Diego underperforming?"* has no real answer here.

**What it does not show:** that every dataset like this is fake. A real business with evenly spread orders could pass this one check too. My confidence came from three checks together (categories, the cost ratio, and this shuffle), and in the end, from the author's own note.

**For a real client:** 📈💰💸 a dataset like this can produce confident-looking charts that mean nothing, and decisions built on them can be very costly. That is exactly what an audit is for.

## 🤝 Work with me

I offer a **Data Reliability Check**: a short report on your own data covering duplicates, impossible values, category logic, and whether differences between groups beat random chance. You get the evidence for and against trusting your numbers, so you do not make an expensive decision on a dataset that is just rolling dice.

📬 Contact: [coming soon]

---
🙏 **Dataset credit:** "Amazon Sales Dataset" by Rohit Kumar on [Kaggle](https://www.kaggle.com/datasets/rohiteng/amazon-sales-dataset), licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
📓 **Want the details?** The full code, the checks, and the random seeds are in the notebook in this repository: `Auditdataamazon.ipynb`.
