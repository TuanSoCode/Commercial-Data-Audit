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



![Revenue and shipping cost by city](images/city_revenue.png)



Every city landed around **$4.2 million** in revenue and about **$33,000** in shipping. The shipping-to-revenue ratio sat between **0.80% and 0.82%** in all 20 cities. Real markets are lumpy: some cities are bigger, some customers cost more to reach. This looked like a table with a coat of paint.

The trap here is a different one. Charlotte shows $4.29M and San Diego $3.96M. It is very tempting to write a report asking *why San Diego is underperforming*. So I needed to know: is that 8% gap a real pattern, or just what dice would give me?

## 🧙 The Doctor Strange test

In *Infinity War*, Doctor Strange looks through 14,000,605 possible futures to find the one where the heroes win. I borrowed the idea, with a much smaller budget.

I took the `City` column and **dealt it out at random, like shuffling a deck of cards**. Every order kept its real revenue, but got a random city. That is one universe where cities mean nothing. Then I measured how uneven city revenue was in that universe, and repeated the whole thing **500 times**.



![Real data vs 500 shuffled universes](images/permutation_test.png)



The results:
- **500 shuffled universes:** unevenness between `1.52%` and `2.35%`
- **My real data:** `1.86%`

My real data did not stand out. It sits in the middle of the crowd, indistinguishable from the universes where orders were handed to cities at random. In Strange's terms: there is no winning future here, and ours is one of the boring ones.

So the Charlotte versus San Diego gap is not a market story. It is the kind of gap you get from rolling dice.

## 🧾 What I concluded

Three separate checks, all pointing the same direction:
1. **Category logic:** products sit in categories that contradict their names.
2. **Cost ratio:** shipping costs 0.80% to 0.82% of revenue in every city, which real regions rarely do.
3. **City differences:** no bigger than random assignment produces.

One test alone could not prove a dataset is simulated, because a real business with evenly spread orders could also pass the shuffle test. It is the three together, plus the author's own note, that make me confident.

**So my advice:** do not rank cities or describe market behavior with this data. Do use it as a playground for practicing audit skills. 🎯

## 🚩 Three red flags I now check first on any dataset

Real data can show these too (entry errors happen), so I treat them as questions for the data owner, not verdicts.

- 🏷️ Category labels that contradict the item names.
- 📏 A ratio that should vary (like shipping over revenue) that is almost identical across groups.
- 🎲 Group differences no bigger than what random shuffling produces.

## 🤝 Work with me

I offer a **Data Reliability Check**: a short report on your own data covering duplicates, impossible values, category logic, and whether differences between groups beat random chance. You get the evidence for and against trusting your numbers, so you do not make an expensive decision on a dataset that is just rolling dice.

📬 Contact: [coming soon]

---
🙏 **Dataset credit:** "Amazon Sales Dataset" by Rohit Kumar on [Kaggle](https://www.kaggle.com/datasets/rohiteng/amazon-sales-dataset), licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
📓 **Want the details?** The full code, the checks, and the random seeds are in the notebook in this repository: `amazon_audit.ipynb`.
