# minimalist-agentic

would like to build an agentic generative AI from scratch.

will only use the basic watsonx.ai api.

## Environments

the lab will base on the [IBM watsonx.ai](http://watsonx.ai) and [IBM Granite 3 Model](https://www.ibm.com/new/ibm-granite-3-0-open-state-of-the-art-enterprise-models)

please follow the instruction to create account and get the API_KEY.

## Agentic Patterns

target to implement 4 agentic patterns

### 1) Reflection

it is about using review and revise to improve the generation outcome

Sample Input

> plan a trip to jakarta for 3 days

Naive output

```text
 Sure, here's a basic plan for your trip to Jakarta:

Day 1:
- Start your day with a visit to the National Monument (Monas), which is a significant landmark in Jakarta.
- Next, head to the Istiqlal Mosque, one of the largest mosques in Southeast Asia.
- In the afternoon, explore the Fatahillah Square, a historic area with colonial architecture and local markets.
- End your day with a visit to the Ancol Beach, where you can enjoy the sunset and local seafood.

Day 2:
- Begin your day at the Jakarta Old Town (Kota Tua), where you can see Dutch colonial architecture and visit the Museum of Fine Arts and Ceramics.
- After lunch, head to the Jakarta Cathedral and the nearby Chinatown for shopping and food.
- In the evening, enjoy a traditional Wayang Kulit puppet show.

Day 3:
- Spend your morning at the Jakarta Zoo or the Ragunan Zoo, depending on your preference.
- After lunch, visit the Taman Mini Indonesia Indah, a cultural park that showcases various regions of Indonesia.
- End your trip with a visit to the Thousand Islands (Kepulauan Seribu), a group of small islands known for their beautiful beaches and snorkeling spots.
```

Review output

```text
The draft provides a well-structured itinerary for a trip to Jakarta, covering historical sites, cultural experiences, and recreational activities. However, there are a few points that could be improved for clarity and logical flow:

1. Day 1: The order of visits could be adjusted for better flow. Consider starting with the Old Town (Kota Tua) to immerse yourself in the local culture and history before moving on to the more modern Monas.

2. Day 2: The Jakarta Animal Park and Ancol Dreamland theme park are quite far from each other. You might want to suggest a different activity or a more central location for the afternoon to avoid travel time.

3. Day 3: The Fatahillah Square and Jakarta Maritime Museum are both interesting places, but they might not provide a very relaxing stroll as suggested. Consider recommending a different activity or location for the end of the trip.

4. General suggestion: Include some information about local transportation options and safety tips for tourists. This will make the draft more comprehensive and helpful for readers.
```

Revised output

```text
Here's a revised plan for your trip to Jakarta:

Day 1:
- Kickstart your journey by exploring the Old Town (Kota Tua), where you can immerse yourself in the local culture and history. Enjoy a meal at one of the many warungs (small eateries) and try some traditional Indonesian dishes.
- After lunch, head to the National Monument (Monas), a significant landmark in Jakarta.
- In the evening, catch a traditional dance performance at the Jakarta Cathedral or the Istiqlal Mosque.

Day 2:
- Begin your day at the Jakarta Animal Park, where you can see a variety of Indonesian wildlife.
- For lunch, consider visiting the Glodok Chinatown area, known for its diverse food scene.
- After lunch, visit the Ancol Dreamland theme park for some fun and entertainment. Alternatively, you could explore the nearby Ancol Beach, which offers a more relaxed atmosphere.
- In the evening, explore the nightlife at the Thamrin City shopping mall or the SCBD business district.

Day 3:
- Spend your morning at the Fatahillah Square, a historic square that hosts various cultural events and markets.
- Next, visit the Jakarta Maritime Museum to learn about the city's maritime history.
- To wrap up your trip, consider taking a leisurely boat ride around the nearby Thousand Islands, which offer beautiful views and a chance to relax.

General suggestions:
- Jakarta has an extensive public transportation system, including buses, minibuses (angkot), taxis, and the commuter rail (KRL Commuter). Consider using these options to get around the city.
- Always be cautious when using public transportation and keep your belongings secure.
- It's also recommended to have some local currency (Indonesian Rupiah) on hand, as not all establishments accept credit cards.
- Lastly, respect local customs and traditions during your visit to ensure a pleasant and memorable experience.
```

### 2) Planning

it is about breakdown the goal into smaller pieces of task, that help to approach a big goal.

> get all prime number with 100

plan:

> 1. understand the concept of prime numbers.
> 2. list out all numbers from 1 to 100.
> 3. identify which numbers are prime.
> 4. list out all prime numbers.

> current status - "I know what prime number is"

next step:

> 1. Understand the concept of prime numbers. [[Completed]]
> 2. List out all numbers from 1 to 100.
> 3. Identify which numbers are prime.
> 4. List out all prime numbers.
> Next step: List out all prime numbers.

> current status - "got all number from 1 to 100"

next step:

> 1. understand the concept of prime numbers. [completed]
> 2. list out all numbers from 1 to 100. [completed]
> 3. identify which numbers are prime.
> 4. list out all prime numbers.
> next step: Identify which numbers from 1 to 100 are prime.

> current status - "I got the prime numbers"

next step:

> 1. Understand the concept of prime numbers. [Completed]
> 2. List out all numbers from 1 to 100. [Completed]
> 3. Identify which numbers are prime. [Completed]
> 4. List out all prime numbers. [Completed]
> Since all steps have been completed, the process is now complete.

### 3) Use Tool

it is about using tool to acquire external data and proceed operation to external system.

#### a few consider when use tool

1) trust on code and tool over the memory.
2) you can use the tool provided, likely be well tested and reliable. you can consolidate all output to the context for the model to do final touch as summarization. but to pass outcome from one tool to another is not trivial.
3) you can also ask the model to generate the code on the spot, but you need more turn to help debug and revise the code since it may not fully reliable.

test case - external data (wikipedia)

input

> how deep is Mariana Trench

naive output

> The Mariana Trench, located in the western Pacific Ocean, is approximately 36,070 feet (10,994 meters) deep at its deepest point, known as the Challenger Deep. This makes it the deepest part of the world's oceans.

use tool output

> calling query_wikipedia({'topic': 'Mariana Trench'})...

> The Mariana Trench, located in the western Pacific Ocean, is the deepest oceanic trench on Earth. Its maximum known depth is 10,984 ± 25 meters (36,037 ± 82 feet; 6,006 ± 14 fathoms; 6.825 ± 0.016 miles). This depth is more than 2 kilometers (1.2 miles) farther from sea level than the peak of Mount Everest. The pressure at the bottom of the trench is 1,086 bar (15,750 psi), and the temperature ranges from 1 to 4 degrees Celsius (34 to 39 degrees Fahrenheit). One-celled organisms called monothalamea have been found at a record depth of 10.6 kilometers (35,000 feet; 6.6 miles) below the sea surface.

test case - near time data source (stock data)

input

> analysis the latest stock price of IBM

naive output

> As of my last update, I don't have real-time data or the ability to browse the internet. However, I can guide you on how to find the latest stock price of IBM. You can check financial websites like Yahoo Finance, Google Finance, or Bloomberg for the most recent stock prices. Please ensure you're using a reliable source and that the information is up-to-date.

use tool output

> calling get_stock_data({'ticker': 'IBM'})...

> Based on the provided knowledge, the latest stock price of IBM as of November 18, 2024, was $208.089996. This is the closing price for that day. The volume of shares traded on that day was 2658508. There were no dividends or stock splits reported for this period.

test case - real time data (world time)

input

> when it is now in Sydney

naive output

> The current time in Sydney, Australia is [insert current time here]. Please note that Sydney observes Daylight Saving Time from early October to early April, during which the time zone is UTC+10:30. The rest of the year, it follows UTC+11:00.

use tool output

> calling get_current_time({'location': 'Australia/Sydney'})...

> The current time in Sydney is 13:47:09 on November 19, 2024.

### 4) Multi Agent

it is about to employ different personale on generation or understanding.

input

> discuss on the topc `should we pay higher tax`

naive output

> The topic of whether or not we should pay higher taxes is a complex one, with valid arguments on both sides. Here are some points to consider:
>
> 1. **Public Services and Infrastructure**: Higher taxes can fund public services and infrastructure that benefit society as a whole, such as education, healthcare, and transportation systems.
>
> 2. **Economic Inequality**: Critics argue that higher taxes disproportionately affect lower-income individuals, exacerbating economic inequality.
>
> 3. **Government Efficiency**: Some people believe that higher taxes could lead to more efficient government spending and reduced waste.
>
> 4. **Economic Growth**: Others argue that high tax rates can discourage investment and entrepreneurship, potentially slowing economic growth.
>
> 5. **Social Safety Nets**: Higher taxes can help fund social safety nets, providing support for those in need.
>
> 6. **Fiscal Responsibility**: Some view higher taxes as a way to ensure fiscal responsibility and prevent excessive government debt.
>
> 7. **Tax Fairness**: There's also the issue of tax fairness - should those who earn more pay a larger share of their income in taxes?
>
> Ultimately, the decision to pay higher taxes depends on one's perspective on these issues and their priorities for society. It's a topic that often sparks heated debate.

some setup for the agents

```python
pros = Agent()
cons = Agent()

pros.role = "supporter"
pros.system_prompt = "give positive argument for the discussion, rebuttle on argument objective to yours."
pros.goal = "provide convincing supportive argument on the topic in discussion."
pros.next_agent = cons

cons.role = "critic"
cons.system_prompt = "give negative argument for the discussion, rebuttle on argument objective to yours."
cons.goal = "provide convincing critic argument on the topic in discussion."
cons.next_agent = pros
```

multi agent output

> turn # 1 - role: supporter
> turn # 2 - role: critic
> turn # 3 - role: supporter
> turn # 4 - role: critic
>
> The task is to discuss the topic "Should we pay higher taxes?" and provide a summary of the arguments presented by both supporters and critics.
>
> Supporters argue that higher taxes can lead to improved public services such as education, healthcare, and infrastructure, which can benefit society as a whole. They also believe that higher taxes can reduce income inequality, promote environmental sustainability, and provide necessary funds for social safety nets. Supporters argue that these benefits outweigh the potential drawbacks of higher taxes, such as economic burden and disincentive for work and investment.
>
> Critics, on the other hand, present several counterarguments against higher taxes. They argue that higher taxes can place a significant financial burden on individuals and businesses, potentially stifling economic growth and investment. Critics also believe that higher taxes may discourage people from working harder or investing in their businesses, as they keep a smaller portion of their earnings. Additionally, critics worry about tax evasion and avoidance, inefficient government spending, and the potential for alternative solutions to address societal issues.
>
> In response to the critics' arguments, supporters present rebuttals and alternative perspectives. They argue that the long-term benefits of higher taxes outweigh the short-term costs and that progressive tax systems can help reduce the incentive for tax evasion. Supporters also believe that higher taxes can provide the necessary funds to invest in public services and infrastructure, which can lead to more effective and efficient use of resources.
>
> However, critics present further counterarguments and alternative perspectives. They argue that higher taxes may discourage businesses from expanding or hiring new employees, leading to slower economic growth and higher unemployment rates. Critics also believe that higher taxes on the wealthy may not significantly impact their work effort or investment and that higher taxes may not guarantee better outcomes due to potential government waste and mismanagement.
>
> In conclusion, the debate over whether we should pay higher taxes is complex and multifaceted. Both supporters and critics present valid arguments and concerns, and it is essential to consider the potential benefits and drawbacks of higher taxes when making decisions about fiscal policy. By engaging in a nuanced and balanced discussion, we can work towards a more equitable, sustainable, and prosperous society.

