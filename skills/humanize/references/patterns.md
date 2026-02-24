# AI writing anti-patterns reference catalog

This catalog documents 43 patterns that signal AI-generated text. Each pattern includes detection guidance, explanation, and transformation examples.

## Tier system

- **Tier 1 (Dead giveaways):** Immediately signal AI origin. Always transformed.
- **Tier 2 (Strong signals):** Create cumulative AI impression. Transformed by default.
- **Tier 3 (Subtle signals):** Detectable by close reading. Transformed only with --thorough.

---

## Category A: Vocabulary & Word Choice

### A1: Overused AI vocabulary [Tier 1]

**Watch for:** delve, pivotal, crucial, testament, underscore, realm, harness, illuminate, nuanced, intricate, tapestry, vibrant, landscape (abstract), foster, garner, showcase, enduring, enhance, interplay, key (adj), valuable, align with

**Why it's a tell:** These words appear 50-269x more often in AI text than human writing. Studies confirm dramatic frequency increases post-2023.

**How to fix:** Replace with simpler, more specific alternatives. "Delve into" -> "examine" or "look at". "Pivotal" -> "important" or remove. "Landscape" -> name the actual domain. "Foster" -> "encourage" or "build". "Garner" -> "get" or "attract".

**Before:**
> An enduring testament to Italian colonial influence is the widespread adoption of pasta in the local culinary landscape, showcasing how these dishes have integrated into the traditional diet.

**After:**
> Pasta dishes, introduced during Italian colonization, remain common in the south.

### A2: Overused multi-word phrases [Tier 1]

**Watch for:** delve into, dive into, plays a pivotal role, shed light on, at its core, that being said, a key takeaway is, provide a valuable insight, left an indelible mark, a stark reminder, a nuanced understanding, quiet confidence/growth/leadership, it's worth noting

**Why it's a tell:** These compound phrases are AI favorites — "provide a valuable insight" appears 182x more frequently in AI text, "left an indelible mark" 111x, "a stark reminder" 88x.

**How to fix:** Say what you actually mean directly. "Shed light on" -> "explain" or "show". "At its core" -> remove or "basically". "That being said" -> "but" or "still".

**Before:**
> At its core, the research sheds light on a nuanced understanding of how remote work plays a pivotal role in employee satisfaction.

**After:**
> The research found that remote workers reported higher job satisfaction, mainly because of schedule flexibility.

### A3: Excessive formal connectors [Tier 1]

**Watch for:** Additionally (starting sentence), Moreover, Furthermore, Indeed, Consequently, In addition, Notably

**Why it's a tell:** AI text overuses these transitional adverbs at sentence starts. They create a mechanical, essay-like flow that real people rarely produce in natural writing.

**How to fix:** Remove them entirely, or use natural transitions. Restructure sentences so the connection is implicit. "Additionally, X" -> just "X". "Moreover, Y" -> "Y" or "And Y" or "Y, too".

**Before:**
> The company expanded into three new markets. Additionally, it hired 200 new employees. Moreover, revenue grew by 15%. Furthermore, customer satisfaction improved.

**After:**
> The company expanded into three new markets and hired 200 people. Revenue grew 15%, and customers were happier too.

### A4: Positive intensifiers/buzzwords [Tier 2]

**Watch for:** innovative, transformative, cutting-edge, game-changing, revolutionary, unparalleled, invaluable, groundbreaking, renowned, breathtaking, seamless, robust, holistic, synergy, leverage (verb)

**Why it's a tell:** AI defaults to superlatives and marketing-speak because its training data is saturated with promotional content.

**How to fix:** Use specific descriptions instead of vague praise. "Innovative approach" -> describe what's actually new. "Groundbreaking research" -> describe the finding. If something is genuinely exceptional, explain why.

**Before:**
> The company's innovative and cutting-edge approach to AI represents a groundbreaking shift in the industry, offering unparalleled solutions.

**After:**
> The company trains its models on customer support transcripts, which most competitors don't do.

### A5: Copula avoidance [Tier 2]

**Watch for:** serves as, stands as, functions as, represents, marks (instead of "is"); boasts, features, offers (instead of "has")

**Why it's a tell:** AI substitutes elaborate linking constructions for simple "is"/"are"/"has". Studies document a 10%+ decline in "is"/"are" usage in AI-influenced academic writing after 2023.

**How to fix:** Use "is", "are", "has", "was" when they work. "Serves as the primary interface" -> "is the primary interface". "The gallery features four rooms" -> "The gallery has four rooms".

**Before:**
> Gallery 825 serves as LAAA's exhibition space for contemporary art. The gallery features four separate spaces and boasts over 3,000 square feet.

**After:**
> Gallery 825 is LAAA's exhibition space for contemporary art. The gallery has four rooms totaling 3,000 square feet.

### A6: Elegant variation [Tier 2]

**Watch for:** A subject referred to by many different synonyms in rapid succession (protagonist -> main character -> central figure -> hero; the company -> the firm -> the organization -> the enterprise)

**Why it's a tell:** AI has repetition-penalty mechanisms that force synonym substitution. Real writers repeat the right word when it's the right word.

**How to fix:** Pick the best term and reuse it. Only vary when there's a genuine reason (avoiding ambiguity, adding information).

**Before:**
> The protagonist faces many challenges. The main character must overcome obstacles. The central figure eventually triumphs. The hero returns home.

**After:**
> The protagonist faces many challenges but eventually triumphs and returns home.

---

## Category B: Syntactic Patterns

### B1: Negative parallelisms [Tier 2]

**Watch for:** Not only...but also, It's not just X, it's Y, It is not merely X but Y, not...however..., No...no...just...

**Why it's a tell:** AI uses these contrasting structures formulaically to appear balanced and thoughtful. They've become a recognizable hallmark of AI-generated text.

**How to fix:** State what something IS rather than what it isn't. Drop the parallel structure and make a direct claim.

**Before:**
> It's not just about the beat riding under the vocals; it's part of the aggression and atmosphere. This is not merely a song, it's a statement.

**After:**
> The heavy beat adds to the aggressive tone.

### B2: Rule of three [Tier 2]

**Watch for:** Three adjectives in a row (fast, reliable, and scalable), three noun phrases, three parallel clauses used for emphasis

**Why it's a tell:** AI forces ideas into triads because its training data (journalism, speeches, marketing) uses this rhetorical device heavily. In AI text it feels formulaic rather than intentional.

**How to fix:** Use the number of items the thought actually requires. Sometimes it's two. Sometimes four. Sometimes one.

**Before:**
> The event features keynote sessions, panel discussions, and networking opportunities. Attendees can expect innovation, inspiration, and industry insights.

**After:**
> The event includes talks and panels. There's also time for informal networking between sessions.

### B3: Superficial -ing analyses [Tier 1]

**Watch for:** Appended present participle phrases: highlighting the significance, ensuring a thorough understanding, emphasizing the critical role, reflecting broader trends, contributing to the development, showcasing the diversity, fostering a sense of, encompassing a wide range

**Why it's a tell:** AI tacks these -ing phrases onto sentences to add fake analytical depth. They're vague commentary that adds no information. Studies found AI text contains 450 instances of participial phrases vs 306 in comparable human text.

**How to fix:** Delete the -ing phrase entirely (it almost never adds meaning). If the analysis is actually important, make it a separate sentence with specific content.

**Before:**
> The temple's color palette of blue, green, and gold resonates with the region's natural beauty, symbolizing Texas bluebonnets, the Gulf of Mexico, and the diverse Texan landscapes, reflecting the community's deep connection to the land.

**After:**
> The temple uses blue, green, and gold. The architect said these were chosen to reference local bluebonnets and the Gulf coast.

### B4: False ranges [Tier 2]

**Watch for:** "from X to Y" constructions where X and Y don't represent endpoints of a meaningful scale or continuum

**Why it's a tell:** AI uses "from...to..." to make lists sound more impressive. But the endpoints need to form a real scale (numeric, temporal, qualitative). "From beef to chicken" isn't a range. "From seed to tree" is.

**How to fix:** If the items don't form a scale, just list them. "From problem-solving to artistic expression" -> "problem-solving and artistic expression".

**Before:**
> Our journey through the universe has taken us from the singularity of the Big Bang to the grand cosmic web, from the birth of stars to the enigmatic dance of dark matter.

**After:**
> The book covers the Big Bang, star formation, and current theories about dark matter.

### B5: Repetitive syntactic templates [Tier 3]

**Watch for:** Multiple consecutive sentences following the same structure (e.g., all starting with "The [noun] [verb]..." or all following Subject-Verb-Object with a trailing prepositional phrase)

**Why it's a tell:** ~76% of syntactic templates in AI text are traceable to training data vs 35% in human text. AI repeats structural patterns because it's optimizing for coherence.

**How to fix:** Vary sentence openings. Start some sentences with subordinate clauses, some with the subject, some with a short phrase. Mix simple and compound sentences.

**Before:**
> The platform enables real-time collaboration. The system supports multiple file formats. The interface provides intuitive navigation. The dashboard displays key metrics.

**After:**
> Real-time collaboration is built in. It handles most file formats, and the interface is straightforward. On the dashboard, you'll find the metrics that matter.

### B6: Uniform sentence length [Tier 3]

**Watch for:** Sentences that are all roughly the same word count (e.g., all 15-20 words). Low standard deviation in sentence length across paragraphs.

**Why it's a tell:** Human writing naturally varies — short punchy sentences mix with longer complex ones. AI tends toward a median length because it optimizes for each sentence independently.

**How to fix:** Deliberately vary. Follow a long sentence with a short one. Or several short ones. Then a medium one. Let the content dictate rhythm.

**Before:**
> The company was founded in 2015 by two engineers. They wanted to solve the problem of food waste. Their first product was a smart container system. It tracks expiration dates for restaurants automatically.

**After:**
> Two engineers founded the company in 2015. Food waste. That was the problem they wanted to solve. Their first product — a smart container that tracks expiration dates — landed its first restaurant client within six months.

### B7: Excessive nominalization [Tier 3]

**Watch for:** "The implementation of", "the utilization of", "the establishment of", "the development of", "the optimization of" — using nouns where verbs would be more direct

**Why it's a tell:** AI favors noun-heavy constructions because they appear more formal. But they make prose sluggish and passive.

**How to fix:** Use the verb form. "The implementation of the system" -> "We implemented the system". "The optimization of performance" -> "We optimized performance" or "Performance improved".

**Before:**
> The establishment of the committee led to the implementation of new policies and the improvement of existing processes.

**After:**
> The committee implemented new policies and improved existing processes.

---

## Category C: Content & Semantic Patterns

### C1: Exaggerated significance [Tier 1]

**Watch for:** marking a pivotal moment, stands as a testament to, indelible mark, deeply rooted, setting the stage for, key turning point, evolving landscape, focal point, represents a shift, enduring legacy, rich cultural heritage, vital role

**Why it's a tell:** AI inflates the importance of ordinary subjects. A regional statistics office becomes "a pivotal moment in the evolution of regional statistics." This happens because training data describes famous things with importance-language, and AI applies it to everything.

**How to fix:** State facts without editorializing importance. If something genuinely is important, show why with specifics rather than asserting it.

**Before:**
> The Statistical Institute of Catalonia was officially established in 1989, marking a pivotal moment in the evolution of regional statistics in Spain. This initiative was part of a broader movement to enhance regional governance.

**After:**
> The Statistical Institute of Catalonia was established in 1989 to collect and publish regional statistics independently from Spain's national statistics office.

### C2: Promotional/advertisement tone [Tier 2]

**Watch for:** boasts a, vibrant, rich (figurative), profound, enhancing its, showcasing, exemplifies, commitment to, natural beauty, nestled within, in the heart of, breathtaking, must-visit, stunning, world-class, state-of-the-art

**Why it's a tell:** AI defaults to tourism-brochure and press-release language. Even when prompted for neutral text, it inserts promotional adjectives because its training data is full of them.

**How to fix:** Describe things neutrally. Replace adjective-heavy praise with specific facts. "Vibrant cultural scene" -> name actual cultural institutions. "Breathtaking views" -> describe what you can see.

**Before:**
> Nestled within the breathtaking region of Gonder in Ethiopia, Alamata Raya Kobo stands as a vibrant town with a rich cultural heritage and stunning natural beauty.

**After:**
> Alamata Raya Kobo is a town in the Gonder region of Ethiopia, known for its weekly market and 18th-century church.

### C3: Vague attributions/weasel words [Tier 2]

**Watch for:** Experts argue, Observers note, Industry reports suggest, widely regarded, several publications indicate, has been described as, is considered, some critics argue, many believe

**Why it's a tell:** AI attributes claims to unnamed authorities to sound credible without providing verifiable sources. This hedging creates an appearance of research without actual evidence.

**How to fix:** Either name the specific source or remove the attribution. "Experts believe X" -> "[Name], a [title] at [institution], argues X" or just state X directly if it's uncontroversial.

**Before:**
> Due to its unique characteristics, the river is of interest to researchers and conservationists. Experts believe it plays a crucial role in the regional ecosystem.

**After:**
> The river supports several endemic fish species, according to a 2019 survey by the Chinese Academy of Sciences.

### C4: Overgeneralization [Tier 2]

**Watch for:** Sweeping statements without specifics, claims about "the world" or "society" or "everyone", "throughout history", "since time immemorial", "across all cultures"

**Why it's a tell:** AI makes broad claims that could apply to almost anything. It avoids specifics because specifics require actual knowledge, while generalities are statistically safe.

**How to fix:** Replace broad claims with specific, verifiable ones. "Has impacted society" -> describe the actual impact on actual people.

**Before:**
> Remote work has fundamentally transformed how society views the relationship between productivity and physical presence in the workplace.

**After:**
> A 2024 Stanford study found that hybrid workers were 5% more productive than full-time office workers, measured by lines of code and call resolution rates.

### C5: Superficial/generic analysis [Tier 2]

**Watch for:** "This raises important questions about...", "The implications are far-reaching", balanced both-sides framing with no actual position, sophisticated vocabulary covering for lack of depth

**Why it's a tell:** AI produces text that sounds analytical but doesn't actually analyze anything. It substitutes vague commentary for specific evidence-based reasoning.

**How to fix:** If analysis is needed, provide it with specific evidence. If it's not needed, remove the pseudo-analysis entirely. Take a position if the context calls for one.

**Before:**
> This development raises important questions about the future of work, and the implications are far-reaching for both employers and employees. While some see opportunity, others see risk.

**After:**
> Employers gain scheduling flexibility but lose the informal mentoring that happens in hallways. Whether that tradeoff works depends on how junior your team is.

### C6: Undue emphasis on notability/media [Tier 2]

**Watch for:** "featured in [outlet]", "covered by major media", "independent coverage", "profiled in", "active social media presence", listing publications as proof of importance

**Why it's a tell:** AI lists media mentions as evidence of significance, often without context about what those sources actually said. This mimics press releases.

**How to fix:** Instead of listing who covered something, summarize what the coverage said. If the coverage isn't substantive, don't mention it.

**Before:**
> Her views have been cited in The New York Times, BBC, Financial Times, and The Hindu. She maintains an active social media presence with over 500,000 followers.

**After:**
> In a 2024 New York Times interview, she argued that AI regulation should focus on outcomes rather than methods.

### C7: Sentiment homogeneity [Tier 3]

**Watch for:** Uniformly positive or uniformly neutral tone throughout. No negative emotions, doubts, frustrations, or mixed feelings. Tighter sentiment variation than human writing.

**Why it's a tell:** AI tends toward positive or neutral sentiment because that's what RLHF rewards. Human writing has scattered distributions and greater emotional range.

**How to fix:** Allow complexity. If something has downsides, mention them. If your feelings are mixed, say so. Not everything needs to end on a positive note.

**Before:**
> The conference was well-organized and the speakers were excellent. The venue was perfect and the networking was valuable. Overall, it was a great experience that provided many useful insights.

**After:**
> The keynote was genuinely excellent — best talk on LLM safety I've heard. The venue was too cold and the lunch was bad. Networking was hit or miss; I had one conversation that might lead somewhere and three that went nowhere.

---

## Category D: Structural Patterns

### D1: Formulaic conclusions [Tier 1]

**Watch for:** "In conclusion", "Ultimately", "To summarize", "the future holds promise", "exciting times lie ahead", "represents a major step forward", references to "the human condition" or "the resilience of the human spirit"

**Why it's a tell:** AI ends text with vague optimistic wrap-ups that could conclude any article about anything. They add no information.

**How to fix:** End with something specific. A concrete next step, a remaining open question, or just stop when you're done. Not everything needs a conclusion paragraph.

**Before:**
> In conclusion, the future looks bright for the company. Exciting times lie ahead as they continue their journey toward excellence. This represents a major step in the right direction.

**After:**
> The company plans to open two more locations next year.

### D2: Challenges-and-recovery formula [Tier 1]

**Watch for:** "Despite its [positive words], [subject] faces challenges...", "Despite these challenges", followed by optimistic pivot. "Challenges and Legacy" as a section heading. "Future Outlook" section.

**Why it's a tell:** This is a rigid template AI applies to almost any topic. Acknowledge positives, note challenges, pivot to optimism. It's formulaic and predictable.

**How to fix:** If challenges exist, discuss them specifically with evidence. Don't pivot to vague optimism. If the future is uncertain, say so.

**Before:**
> Despite its industrial prosperity, Korattur faces challenges typical of urban areas, including traffic congestion. Despite these challenges, with its strategic location and ongoing initiatives, Korattur continues to thrive.

**After:**
> Traffic congestion increased after 2015 when three new IT parks opened. The municipal corporation began a stormwater drainage project in 2022 to address recurring floods.

### D3: Inline-header vertical lists [Tier 2]

**Watch for:** Bullet points where each item starts with a bolded header followed by a colon, then descriptive text. Numbered lists with "1. **Header:** explanation" format.

**Why it's a tell:** This hybrid heading/list format is nearly exclusive to AI output. Humans either use headings OR lists, not this merged form.

**How to fix:** Convert to prose if the items are related. If a list is genuinely needed, use simple bullets without bolded headers. Or use actual subheadings.

**Before:**
> - **User Experience:** The user experience has been significantly improved with a new interface.
> - **Performance:** Performance has been enhanced through optimized algorithms.
> - **Security:** Security has been strengthened with end-to-end encryption.

**After:**
> The update improves the interface, speeds up load times through optimized algorithms, and adds end-to-end encryption.

### D4: Rigid predictable organization [Tier 3]

**Watch for:** Perfect intro/body/conclusion structure. Every section the same length. Topic sentence + supporting details + summary in every paragraph. Numbered or lettered everything.

**Why it's a tell:** AI organizes text like a five-paragraph essay because that's what it's optimized for. Human writing is messier — it follows the thought, not a template.

**How to fix:** Let structure follow content. Not every section needs a topic sentence. Jump into specifics when that's what matters. Vary paragraph lengths.

**Before:**
> (A text where every paragraph starts with a topic sentence, has 3 supporting details, and ends with a summary sentence)

**After:**
> (A text where some paragraphs lead with evidence, some with questions, some are just one sentence, and the overall flow follows the argument rather than a template)

### D5: Section summaries [Tier 2]

**Watch for:** "In summary", "To recap", "As we've seen", "The key points are" — restating what was just said within the same section

**Why it's a tell:** AI adds summaries because its training data includes academic and educational writing that recaps frequently. In most prose, this is redundant.

**How to fix:** Remove the summary. The reader just read the section. If the key point needs emphasis, make it the section's opening, not a recap at the end.

**Before:**
> The team tested three approaches: A/B testing, user interviews, and analytics review. Each method provided unique insights. In summary, the three methods — A/B testing, user interviews, and analytics review — each contributed valuable perspectives.

**After:**
> The team tested three approaches: A/B testing, user interviews, and analytics. The interviews turned up problems the quantitative methods missed.

### D6: Title-as-proper-noun leads [Tier 2]

**Watch for:** Opening sentences that define an article title as if it were a real-world entity: "The [Article Title] is a..."

**Why it's a tell:** AI treats any title as something to be formally introduced and defined, even when the title is just a descriptive phrase, not a proper name.

**How to fix:** Start with the actual subject, not the title. "The Effects of Foreign Language Anxiety on Learning refers to..." -> "Learning a foreign language often triggers anxiety, which..."

**Before:**
> "The Effects of Foreign Language Anxiety on Learning" refers to the feelings of tension experienced when learning a language other than one's native tongue.

**After:**
> Learning a foreign language often triggers anxiety — a nervousness about making mistakes or being misunderstood that can significantly slow progress.

### D7: Vague see-also/related sections [Tier 3]

**Watch for:** "Related topics" or "See also" sections listing broad generic concepts rather than specific relevant resources

**Why it's a tell:** AI pads articles with generic cross-references that aren't meaningfully connected to the specific content.

**How to fix:** Either link to genuinely relevant specific resources or remove the section entirely.

**Before:**
> See also: Technology, Innovation, Digital Transformation, Artificial Intelligence

**After:**
> (Remove the section, or link to specific related projects/papers/tools)

---

## Category E: Formatting & Style

### E1: Overuse of boldface [Tier 2]

**Watch for:** Bolding individual words, technical terms, or non-critical phrases for emphasis. Bolding every instance of a key concept. "Key takeaways" style bolding.

**Why it's a tell:** AI inherits heavy bolding from readmes, fan wikis, listicles, and slide decks. It emphasizes mechanically rather than strategically.

**How to fix:** Remove most bolding. Reserve bold for actual headings or truly critical terms that appear once. If everything is emphasized, nothing is.

**Before:**
> A **leveraged buyout (LBO)** is characterized by extensive use of **debt financing** to acquire a company. This enables **private equity firms** to control businesses while investing relatively small **equity**.

**After:**
> A leveraged buyout (LBO) uses debt to acquire a company. This lets private equity firms control businesses while investing relatively little of their own money.

### E2: Title case in headings [Tier 2]

**Watch for:** Headings where all major words are capitalized: "Strategic Negotiations And Global Partnerships"

**Why it's a tell:** AI defaults to title case because it appears in many training examples. Most modern style guides (including Wikipedia's) prefer sentence case for headings.

**How to fix:** Use sentence case. Capitalize only the first word and proper nouns.

**Before:**
> ## Strategic Negotiations And Global Partnerships

**After:**
> ## Strategic negotiations and global partnerships

### E3: Em dash overuse [Tier 2]

**Watch for:** More than 1-2 em dashes per paragraph. Em dashes used for formulaic parallelism ("not X — but Y"). Em dashes where commas or parentheses would be more natural.

**Why it's a tell:** AI overuses em dashes to mimic punchy journalistic or sales-style writing. Human writers use them more sparingly.

**How to fix:** Replace most em dashes with commas, parentheses, colons, or periods. Reserve em dashes for genuine dramatic interruption or aside.

**Before:**
> The term is primarily promoted by Dutch institutions — not by the people themselves. You don't say "Netherlands, Europe" — yet this mislabeling continues — even in official documents.

**After:**
> The term is primarily promoted by Dutch institutions, not by the people themselves. You wouldn't say "Netherlands, Europe," yet this mislabeling continues in official documents.

### E4: Emoji decoration [Tier 2]

**Watch for:** Emojis before headings, bullet points, or used as list markers. Emojis used decoratively rather than semantically.

**Why it's a tell:** AI uses emojis to make content feel "engaging," especially in informal or social media contexts. In most writing, they signal AI origin.

**How to fix:** Remove decorative emojis. If an emoji conveys genuine meaning (e.g., a warning symbol), it can stay.

**Before:**
> 🚀 **Launch Phase:** The product launches in Q3
> 💡 **Key Insight:** Users prefer simplicity
> ✅ **Next Steps:** Schedule follow-up meeting

**After:**
> The product launches in Q3. User research showed a preference for simplicity. Next step: schedule a follow-up.

### E5: Curly quotation marks [Tier 3]

**Watch for:** Curly/smart quotes ("\u2026") mixed with straight quotes ("...") in the same text. Inconsistent apostrophe style.

**Why it's a tell:** ChatGPT and DeepSeek typically use curly quotes. Mixing curly and straight quotes in one text is an AI artifact. (Note: Apple devices and Microsoft Word also produce curly quotes, so this alone isn't conclusive.)

**How to fix:** Standardize to straight quotes throughout, or curly throughout — just be consistent.

**Before:**
> He said \u201cthe project is on track\u201d but others disagreed with the \u201ctimeline.\u201d

**After:**
> He said "the project is on track" but others disagreed with the "timeline."

### E6: Unnecessary tables [Tier 3]

**Watch for:** Small tables (2-3 rows) presenting information that would read more naturally as prose. Tables used for simple comparisons.

**Why it's a tell:** AI reaches for tabular formatting because it looks structured. Humans use tables for genuinely complex data, not for three facts.

**How to fix:** Convert small tables to prose. Reserve tables for data with 4+ rows or genuine need for column-based comparison.

**Before:**
> | Metric | Value |
> | Market Size | $2.1B |
> | Growth Rate | 12% |

**After:**
> The market is worth about $2.1 billion and growing at 12% annually.

### E7: Non-standard heading styles [Tier 3]

**Watch for:** Colons immediately after headings ("Global Context: Critical Mineral Demand"), skipping heading levels (jumping from h2 to h4), inconsistent heading hierarchy.

**Why it's a tell:** AI applies rigid formatting conventions from training data. The colon-after-heading pattern and heading level skipping are particularly distinctive.

**How to fix:** Remove colons from headings. Use proper heading hierarchy (h2, then h3, then h4). Keep heading style consistent.

**Before:**
> ## Global Context: Critical Mineral Demand
> #### Key Statistics

**After:**
> ## Global context
> ### Key statistics

---

## Category F: Behavioral/Conversational Tells

### F1: Collaborative communication [Tier 1]

**Watch for:** I hope this helps, Of course!, Certainly!, You're absolutely right!, Would you like..., is there anything else, let me know, more detailed breakdown, here is a, If you'd like me to expand

**Why it's a tell:** These are chatbot interaction artifacts — responses designed for dialogue that get pasted into standalone text.

**How to fix:** Delete entirely. These phrases belong in conversation, not in articles, posts, or documents.

**Before:**
> Here is a comprehensive overview of the French Revolution. I hope this helps! Let me know if you'd like me to expand on any section.

**After:**
> The French Revolution began in 1789 when financial crisis and food shortages led to widespread unrest.

### F2: Knowledge-cutoff disclaimers [Tier 1]

**Watch for:** as of [date], Up to my last training update, as of my last knowledge update, While specific details are limited/scarce..., not widely available/documented/disclosed, based on available information, in the provided/available sources/search results

**Why it's a tell:** These are AI admitting it doesn't have complete information. They have no place in human-written text.

**How to fix:** Delete entirely. If you genuinely don't have information, either find it or don't write about it.

**Before:**
> While specific details about the company's founding are not extensively documented in readily available sources, it appears to have been established sometime in the 1990s.

**After:**
> The company was founded in 1994, according to its registration documents.

### F3: Sycophantic/servile tone [Tier 1]

**Watch for:** Great question!, That's an excellent point, You're absolutely right, Absolutely!, What a fascinating topic, You've raised a very important issue, unsolicited "You're not alone"

**Why it's a tell:** AI is trained to be agreeable and validating. This performative enthusiasm is instantly recognizable.

**How to fix:** Delete entirely. Respond to substance, not to the act of asking.

**Before:**
> Great question! You're absolutely right that this is a complex topic. That's an excellent point about the economic factors.

**After:**
> The economic factors you mentioned are relevant here.

### F4: Inappropriate direct address [Tier 2]

**Watch for:** "you can", "if you're interested", "did you know", "imagine if", "picture this" in non-conversational text (articles, documentation, formal writing)

**Why it's a tell:** AI defaults to conversational second-person from its chatbot training. In formal or expository text, this feels out of place.

**How to fix:** Rewrite in third person or passive voice for formal text. In casual text, direct address may be appropriate — context matters.

**Before:**
> You can see that the results were significant. If you're interested in learning more, you can explore the dataset yourself.

**After:**
> The results were statistically significant. The full dataset is available for independent analysis.

### F5: Phrasal templates/placeholders [Tier 1]

**Watch for:** [Your Name Here], [Company Name], [insert date], [describe specific section], PASTE_URL_HERE, 2025-XX-XX, INSERT_SOURCE_URL

**Why it's a tell:** AI generates fill-in-the-blank templates that users forget to complete. Obvious artifact of chatbot interaction.

**How to fix:** Fill in the actual values or remove the placeholder content entirely.

**Before:**
> Dear [Recipient Name], I am writing to express my concern about [Specific Issue].

**After:**
> (Either fill in the actual names and issues, or don't send the text)

### F6: Didactic disclaimers [Tier 2]

**Watch for:** it's important to note, it's crucial to remember, worth noting, it's worth mentioning, it should be noted, keep in mind, may vary

**Why it's a tell:** AI adds these as hedging preambles, often for information that doesn't need a disclaimer. They pad text without adding substance.

**How to fix:** Remove the disclaimer and just state the information. "It's important to note that results may vary" -> "Results vary" or just present the information directly.

**Before:**
> It's important to note that the implementation timeline may vary depending on your specific requirements. It's also worth mentioning that costs can differ significantly.

**After:**
> Timelines and costs depend on your specific setup.

---

## Category G: Statistical/Quantitative Patterns

### G1: Low lexical diversity [Tier 3]

**Watch for:** Small vocabulary relative to text length. The same common words appearing repeatedly. Few unusual or domain-specific terms.

**Why it's a tell:** AI draws from high-probability tokens, resulting in a smaller effective vocabulary than human writers who use idiosyncratic word choices.

**How to fix:** Use the specific word for the specific thing. Replace generic terms with precise ones. Don't be afraid of uncommon words when they're the right words.

**Before:**
> The system is very good at processing things quickly. It's also good at handling different types of things efficiently. The results are very impressive.

**After:**
> The pipeline chews through 10,000 records per second. It handles CSVs, JSON, and Parquet without config changes. Throughput benchmarks blew past our targets.

### G2: Reduced sentence length variation [Tier 3]

**Watch for:** Sentences clustered around the same word count. Low standard deviation in sentence length. No very short or very long sentences.

**Why it's a tell:** AI optimizes each sentence independently, converging on a comfortable medium length. Human writing naturally oscillates — a 4-word sentence followed by a 30-word one.

**How to fix:** Deliberately vary. Use sentence fragments for emphasis. Let some sentences run long with subordinate clauses. Follow complex sentences with simple ones.

**Before:**
> The team reviewed the proposal carefully. They identified several key concerns. The budget seemed reasonable overall. The timeline needed some adjustment.

**After:**
> The team reviewed the proposal. Budget looked fine. But the timeline? That needed work — three of the four milestones assumed parallel workstreams that shared a single QA resource.

### G3: Excessive hedging [Tier 2]

**Watch for:** could potentially, might possibly, it could be argued that, it seems likely that, arguably, tends to, generally speaking, for the most part, to some extent

**Why it's a tell:** AI over-qualifies statements to avoid being wrong, stacking hedge words that dilute meaning. One hedge is fine; three is AI.

**How to fix:** Pick one level of certainty and commit. "Could potentially possibly be argued that X might have some effect" -> "X probably affects Y" or "X affects Y".

**Before:**
> It could potentially possibly be argued that the policy might have some effect on outcomes, though this arguably remains somewhat unclear.

**After:**
> The policy probably affects outcomes, though the evidence is mixed.
