# Prompt Engineering Experiments
**Dataset:** Zomato
**Tools Used:** ChatGPT / Claude / Gemini
**Date:** April 2026

---

## What is Prompt Engineering?
Prompt engineering is the practice of designing and refining inputs 
to AI models to get the most accurate, relevant, and useful outputs. 
It is a critical skill in working with Large Language Models (LLMs).

---

## Experiment 1 — Zero-Shot Prompting
**Objective:** Ask the AI directly without any examples

**Tool used:** ChatGPT

**Prompt:** 
I have a dataset about Zomato restaurants with the following columns: Restaurant Name, City, Cuisines, Average Cost for Two, Rating, Votes, Online Delivery, Table Booking. Analyze this dataset and give me 5 key business insights that a restaurant owner would find valuable.

**Output:** 
1. Online Delivery Strongly Impacts Ratings
    A. Restaurants with online delivery = YES → avg rating ~3.25
    B. Without delivery → ~2.46
2. Table Booking = Premium Experience Signal
    A. With table booking → ~3.44 rating
    B. Without → ~2.56 rating
3. Price Has Weak Impact on Ratings
    A. Correlation between cost and rating ≈ 0.05 (very weak)
    B. Higher price ≠ better ratings
    C. Customers value experience over price
4. Certain Cuisines Perform Exceptionally Well
    A. Some cuisine combinations naturally attract higher satisfaction
5. Location Matters for Perception
    A. Top-rated cities (e.g., Makati, Quezon City, etc.) show ratings up to 4.8–4.9
    B. Customer expectations and competition vary by city
    C. High-performing locations often have:
        I. Better service standards
        II. Competitive pressure
   
**Observation:** Zero-shot prompting produced surface-level insights that lacked quantification and specificity. The AI defaulted to obvious patterns (price vs rating, location differences) without providing actionable business recommendations. Insight #3 (price has weak impact) and #4 (certain cuisines perform well) were vague — no specific cuisines or cities were named, making them unusable for real business decisions. This experiment demonstrates that without examples or context, LLMs default to safe, generic responses.

---

## Experiment 2 — One-Shot Prompting
**Objective:** "Provide one example to guide the AI's response style and format"

**Tool used:** ChatGPT

**Prompt:** 
    You have a Zomato restaurant dataset. Here is an example of the kind of business insight I'm looking for:
    Example insight: "Restaurants offering online delivery in Tier-2 cities have 23% higher average ratings than those that don't, suggesting   delivery capability drives customer satisfaction beyond metro areas."
    Now generate 5 more insights like this from a dataset with these columns: Restaurant Name, City, Cuisines, Average Cost for Two, Rating, Votes, Online Delivery, Table Booking.
    
**Output:** 
1. Restaurants with >500 votes have ~18–25% less rating variance compared to those with fewer votes, indicating more stable customer satisfaction
2. Restaurants offering 3+ cuisines receive ~30–40% more votes on average than single-cuisine outlets.
3. Restaurants in the ₹800–₹1500 cost-for-two range show ~12–18% higher ratings and votes compared to very low or very high price segments.
4. High-cost restaurants (₹1500+) with table booking enabled receive ~20% higher ratings than similar-priced restaurants without booking.
5. Low-cost restaurants (<₹500) with online delivery get ~35% more votes, but only ~5–8% rating improvement.
   
**Observation:** One-shot prompting produced a measurable improvement over zero-shot. By providing a single quantified example, the AI shifted
from vague directional insights to specific percentage-based findings. Outputs now included precise ranges (18–25% less rating variance, 30–40% more votes) rather than generalised patterns. However, the insights still felt inferred rather than truly data-grounded — the AI was matching the format of the example without necessarily having access to real data. The key learning: even one well-crafted example dramatically raises the quality floor of an LLM's output.

---

## Experiment 3 — Few-Shot Prompting
**Objective:** Provide multiple examples for better output quality

**Tool used:** Claude

**Prompt:**
    I have a Zomato restaurant dataset. Here are 3 examples of the business insights I want:
    1. "North Indian cuisine dominates metro cities but has low penetration in South Indian markets, representing an expansion opportunity."
    2. "Restaurants with table booking options charge on average 40% more per meal, indicating a premium positioning strategy."
    3. "Restaurants with over 500 votes but below 3.5 rating are high-visibility but low-satisfaction — prime candidates for service improvement campaigns."
    Now generate 5 more insights in exactly this style and format from a dataset with columns: Restaurant Name, City, Cuisines, Average Cost for Two, Rating, Votes, Online Delivery, Table Booking.
    
**Output:**
1. Restaurants offering online delivery rate 32% higher on average ratings (3.25 vs 2.47) than those that don't — yet only 26% of restaurants have adopted it, suggesting that digitally-enabled players are already outperforming, and the non-adopters represent a massive untapped upgrade opportunity.
2. 22% of all restaurants in the dataset carry a zero rating — and only 4% of them offer online delivery versus 26% across the full dataset. These unrated, digitally-absent outlets are invisible to modern diners and urgently need activation through delivery platforms and review generation campaigns.
3. Table-booking restaurants attract 2.7x more votes on average (353 vs 130) compared to walk-in-only restaurants, signaling that reservation-capable venues generate far greater diner engagement and word-of-mouth — making table booking a growth lever, not just an operational feature.
4. Restaurants offering 3 or more cuisines charge nearly double the average cost for two (₹1,472 vs ₹764 for single-cuisine spots) — yet don't consistently outperform on ratings. Multi-cuisine positioning appears to be a pricing signal rather than a quality differentiator, indicating a potential perception gap to address.
5. 9% of rated restaurants sit in the high-cost, low-satisfaction quadrant — premium pricing paired with a sub-3.5 rating — and 62% of them offer table booking, meaning diners are making reservations based on perceived prestige only to leave disappointed. These venues are the highest churn-risk segment and prime targets for experience-quality interventions.

**Observation:**  Response is more detailed and true to the dataset

---

## Experiment 4 — Role-Based Prompting
**Objective:** Assign the AI a specific role/persona

**Tool used:** Gemini

**Prompt:**
    You are a Senior Business Analyst at a top restaurant consulting firm in India. Your client is a restaurant chain looking to expand across 10 new cities.
    Using data from a Zomato dataset (columns: Restaurant Name, City, Cuisines, Average Cost for Two, Rating, Votes, Online Delivery, Table Booking), write an executive summary of 150 words that highlights the top 3 opportunities and top 2 risks they should consider before expanding.
    Use a professional, boardroom-ready tone.
    
**Output:**
Analysis of the Zomato India dataset indicates a critical need for geographic selectivity to optimize $ROI$. To ensure a successful 10-city expansion, we highlight the following strategic factors:
Top 3 Opportunities:
    1. High-Engagement Tier-1 Markets: Cities such as Bangalore and Hyderabad exhibit superior customer satisfaction (average ratings $> 4.3$) and high consumer engagement, signaling a mature market for premium offerings.
    2. Digital-First Integration: Data confirms that restaurants offering ‘Online Delivery’ and ‘Table Booking’ achieve approx. 40% higher aggregate ratings, suggesting these features are non-negotiable for brand equity.
    3. Strategic Regional Hubs: Emerging cities like Lucknow and Guwahati present a “sweet spot” with high ratings (approx 4.2) and lower competition than the National Capital Region (NCR).
Top 2 Risks:
    1. NCR Market Saturation: New Delhi and Noida show high restaurant density but low average ratings ($< 2.5$), indicating a hyper-competitive environment with high brand dilution risks.
    2. Engagement Fragility: Satellite markets like Faridabad suffer from low consumer interaction (low average votes), significantly increasing the cost of customer acquisition.
Recommendation: Expansion should prioritize digital-enabled service models within high-rating Tier-1 and Tier-2 regional hubs.

**Observation:** Role-based prompting produced the most professionally toned output of all six experiments. By assigning Gemini the persona of a Senior Business Analyst at a consulting firm, the response adopted boardroom language, structured its findings under "Opportunities" and "Risks", and named specific cities and metrics. Notably, it coined actionable framing ("digital-enabled service models", "high-rating Tier-2 regional hubs") that a business presenter could use verbatim. The output required zero editing before being presentation-ready — demonstrating that role assignment is the single most effective technique for bridging the gap between raw AI output and professional communication. 

---

## Experiment 5 — Chain-of-Thought Prompting
**Objective:** Ask the AI to think step by step before answering

**Tool used:** ChatGPT

**Prompt:**
    I want you to analyze a Zomato restaurant dataset step by step.
        Step 1: First, identify what type of analysis would be most valuable for a restaurant business owner.
        Step 2: Then, list the columns that would be most relevant for that analysis (from: Restaurant Name, City, Cuisines, Average Cost for Two, Rating, Votes, Online Delivery, Table Booking).
        Step 3: Based on those columns, describe what patterns you would expect to find and why.
        Step 4: Finally, suggest 3 specific hypotheses a data analyst should test on this dataset.
    Think through each step carefully before moving to the next.

**Output:**
Most Valuable Type of Analysis: Performance Driver Analysis (Success Factors)
    Definition: Identify which factors drive higher ratings (satisfaction) and higher votes (popularity/revenue proxy).
    Why important for owner:
        Helps decide pricing, services, and menu strategy
        Answers: “What should I change to get more customers and better reviews?”
Most Relevant Columns:
    Core Variables:
        Rating → Customer satisfaction (primary outcome)
        Votes → Popularity / demand indicator
        Average Cost for Two → Pricing strategy
        Online Delivery → Convenience / reach
        Table Booking → Service level / premium positioning
        Cuisines → Product offering / menu diversity
        City → Market conditions
    Support Only: Restaurant Name → Identifier (not analytical)
Expected Patterns (with reasons)
    Online Delivery → Higher Votes, Moderate Rating Impact
        Pattern: Delivery ON → more votes, slight rating increase
        Reason:
        Increases reach → more customers → more reviews
        But scaling delivery may affect consistency
    Table Booking → Higher Ratings
        Pattern: Booking available → higher ratings
        Reason: 
            Indicates better service, planning, and dining experience
            Attracts serious dine-in customers
    Pricing Sweet Spot (Mid-Range)
        Pattern: Mid-range cost → best ratings + engagement
        Reason:
            Low-cost → quality concerns
            High-cost → high expectations → stricter reviews
    Cuisine Variety → Higher Engagement
        Pattern: More cuisines → higher votes
        Reason:
            Appeals to wider audience
            Better discoverability on platforms
    City Differences → Performance Variation
        Pattern: Some cities → higher avg ratings and votes
        Reason: Competition level, customer expectations, and food culture vary
3 Testable Hypotheses
Hypothesis 1: “Restaurants offering online delivery receive significantly more votes than those that do not.”
    Test: Mean comparison (t-test)
    Target: Votes
Hypothesis 2: “Restaurants in the mid-price range have higher average ratings than low- and high-priced restaurants.”
    Test: ANOVA (price groups vs rating)
Hypothesis 3: “Table booking availability positively impacts ratings, especially for higher-priced restaurants.”
    Test: Two-way analysis (Booking × Cost on Rating)
Final Insight:
    Focus your analysis on what drives both:
        Ratings (quality perception)
        Votes (customer volume)
    Because a successful restaurant needs both reputation + demand, not just one.

---

## Experiment 6 — Cross-Tool Comparison
**Objective:** Same prompt, three different AI tools — compare outputs

**Prompt used:** "You are a data analyst. I have a Zomato restaurant dataset with columns: Restaurant Name, City, Cuisines, Average Cost for Two, Rating, Votes, Online Delivery, Table Booking. Write a 100-word executive summary of what this dataset can tell us about the Indian restaurant industry. Make it suitable for a non-technical business audience."

**ChatGPT output:** 
This dataset offers a clear view of what drives success in the Indian restaurant industry. It highlights how customer satisfaction (ratings) and popularity (votes) are influenced by pricing, cuisine variety, and service features like online delivery and table booking. Mid-range restaurants tend to balance value and quality effectively, while delivery options expand reach and customer engagement. Table booking often signals a more premium dining experience. Differences across cities reveal how local market dynamics shape performance. Overall, the data helps restaurant owners make smarter decisions on pricing, services, and menu strategy to improve both customer experience and business growth.

**Claude output:**
India's restaurant landscape is vast but uneven. New Delhi alone accounts for 57% of all listings, reflecting a strong metro concentration of dining activity. Despite this scale, 22% of restaurants carry no ratings at all, pointing to a significant visibility gap. Online delivery remains nascent — only 26% of restaurants offer it — yet those that do consistently earn higher customer ratings. Table booking, adopted by just 12% of venues, correlates with premium pricing and stronger audience engagement. The data makes one thing clear: digital adoption — delivery, booking, and review generation — is the sharpest differentiator between restaurants that thrive and those that remain invisible.

**Gemini output:**
This dataset offers a high-resolution map of the Indian restaurant industry, highlighting a clear divide between volume and value. While major hubs like New Delhi show high saturation and lower average ratings, emerging Tier-2 cities present "white space" opportunities with superior customer satisfaction scores.Critically, the data reveals a "digital dividend": restaurants integrating online delivery and table bookings achieve significantly higher ratings, marking these as essential competitive requirements. By benchmarking cuisines against price points, the dataset provides a strategic blueprint for identifying underserved niches, optimizing pricing, and balancing operational scale with the service quality needed to maintain brand equity.

**Observation:** Claude produced the most data-specific and insight-dense response, citing exact figures (57% Delhi concentration, 22% unrated, 26% delivery adoption, 12% table booking). ChatGPT gave a generic strategic summary with no specific numbers. Gemini balanced both — it included city-level analysis and coined useful framing ('digital dividend', 'white space opportunities') but lacked the raw specificity of Claude. For data analytics tasks requiring precise, evidence-based outputs, Claude outperformed. For high-level strategic communication, Gemini's framing was more polished.

---

## Key Learnings

### Which experiment surprised me the most?
Experiment 3 — Few-Shot Prompting surprised me the most.
Going in, I expected the improvement from zero-shot to few-shot to be incremental. What I didn't expect was how dramatically the quality shifted. Claude didn't just match the style of the examples — it went beyond them. It cited exact figures from the dataset (22% unrated restaurants, 26% delivery adoption, 2.7x more votes for table-booking restaurants) and framed each insight around a specific business action, not just an observation.
The insight about the "high-cost, low-satisfaction quadrant" — where 62% of those restaurants still offer table booking — was particularly striking. That's the kind of nuanced, layered finding that a senior analyst would be proud of. The AI arrived at it simply because the examples I provided set a high enough bar. That was the key realisation — the AI's ceiling in any given conversation is largely set by the quality of examples you provide it.

### Which technique would I use in my actual job?
Two techniques stand out for real-world use:
The first is Role-Based Prompting — and I would use it every time I need to communicate findings to a non-technical audience. In my current internship at Intellipaat, I build Power BI dashboards and write reports. Right now, writing the executive summary or the business narrative around the data takes significant time. With role-based prompting, I can assign the AI the role of a "Senior Business Analyst presenting to the leadership team" and generate a boardroom-ready summary in seconds — then edit it rather than write from scratch. The Gemini output in Experiment 4 was almost publish-ready without any editing.
The second is Chain-of-Thought Prompting — specifically for structuring my analysis before I write a single line of SQL or Python. Experiment 5 produced 3 statistically testable hypotheses with specific tests (t-test, ANOVA, two-way analysis). In practice, I would use this technique at the start of every new dataset exploration — ask the AI to think step by step through what analysis is most valuable, which columns matter, and what hypotheses to test. This gives me a structured analytical roadmap instead of starting from a blank page.

### How do ChatGPT, Claude, and Gemini differ?
The cross-tool comparison in Experiment 6 made this very clear.
ChatGPT defaulted to broad, safe, strategic language. Its output was readable and well-structured but contained zero specific numbers or data references. It felt like a generic business school answer — competent but not distinctive. Useful when you need a clean, professional summary that avoids controversy or specificity.
Claude was the most data-grounded. It pulled specific figures — 57% Delhi concentration, 22% unrated restaurants, 26% delivery adoption, 12% table booking adoption — and built its narrative around them. Every sentence was anchored in something measurable. For data analytics tasks where accuracy and specificity matter, Claude consistently outperformed the others across Experiments 3 and 6.
Gemini found a middle ground, but with better strategic framing than the other two. It coined terms like "digital dividend" and "white space opportunities" that made the output feel more like a consulting deliverable. It named specific cities (Bangalore, Hyderabad, Lucknow, NCR) and gave directional recommendations. For executive communication and strategic storytelling, Gemini's tone was the most polished.
The practical takeaway — these are not interchangeable tools. The right choice depends on the task: Claude for data-heavy analysis, Gemini for strategic narratives, ChatGPT for clean general summaries.

### What would I do differently?
Three things:
1. I would use the actual dataset values in my prompts rather than just column names. In every experiment, I only gave the AI the column headers. If I had included a sample of 5–10 rows of actual data, the outputs would have been grounded in real numbers rather than inferred patterns. Experiment 1 in particular suffered from this — the AI made assumptions because it had no real data to work with.
2. I would add a seventh experiment — Iterative Prompting. This is where you take the output of one prompt and use it as the input for the next, refining progressively. For example, take Claude's Experiment 3 output, then prompt it again: "Take insight #3 and turn it into a slide-ready recommendation with a headline, 2 supporting data points, and a call to action." That chained approach produces presentation-ready content and is a genuinely powerful real-world workflow.
3. I would document the time taken per experiment. One of the strongest arguments for prompt engineering in a professional context is time savings. If I had recorded that generating a boardroom-ready summary took 45 seconds vs 2 hours of manual writing, that data point alone would make the "Impact on Real Work" section far more compelling to a recruiter.

### How does prompt quality affect output quality?
This exercise made the relationship between prompt quality and output quality impossible to ignore.
Experiment 1 (zero-shot) produced generic, assumption-heavy insights because the prompt gave the AI no direction beyond the task itself. By Experiment 2 (one-shot), a single well-crafted example shifted the outputs from vague to quantified. By Experiment 3 (few-shot), three examples produced consulting-grade insights with specific data references and business action framing.
The conclusion is direct: the AI does not get smarter between experiments — the prompt does. The model's capability was constant across all six experiments. What changed was the precision of the instructions, the examples provided, and the role assigned. Every improvement in output quality traced back to an improvement in how the prompt was written.
This has a direct implication for any data analytics role. An analyst who can write precise, structured prompts will consistently extract more value from AI tools than one who cannot — regardless of which tool they use. Prompt engineering is not a technical skill in the traditional sense. It is a communication skill applied to AI, and like all communication skills, it compounds with practice.

## Impact on Real Work: 
1. Auto-generating executive summaries from Power BI dashboards using role-based prompting — reducing report writing time by an estimated 60–70%
2. Using chain-of-thought prompting to structure hypothesis testing workflows before writing SQL or Python analysis code
3. Few-shot prompting to standardize insight communication across teams — ensuring consistent tone and depth in data reports shared with non-technical stakeholders
4. Cross-tool evaluation framework developed here can be applied when selecting the right LLM for specific organizational tasks — cost vs quality tradeoffs
5. Role-based prompting can simulate a domain expert (e.g., financial analyst, marketing strategist) to generate industry-specific interpretations of the same dataset without requiring domain expertise

Topics: prompt-engineering, generative-ai, llm, chatgpt, claude, gemini, data-analytics, zomato
