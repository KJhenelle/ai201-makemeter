## Letterboxd Review Sorter

Letterboxed is inundated after every movie release with reviews that range from the basic "was good" to full-fledged breakdowns of the movie with in depth analysis of the actors and more. Sometimes that's what you're looking for but other times you just wanna know if the actor gave a good performance, or you're looking for a good story, maybe you don't want the plot spoiled, but you wanna know if the movie fits your movienight vibes. Based on letterbox reviews and what you might be looking for in a movie, I placed the reviews into three categories: actor focused, plot focused, and vibe focused which allows you to get information on your movie that's tailored to what you're looking for.

 - Actor focused will be focused on performances and the chemistry of actors on screen and how they take the script and make it their own.
    
   - "Zach Cregger is turning into the goat in my unhumble opinion love this what not to do guide on a zombie apocalypse , fuck the RE purists this was a Residents Evil movie to the bone and I’m loving Austin Abram’s as this new horror/comedy actor it’s nice pocket for him"
 - Plot focused will be about how they felt the plot flow how stereotypical or groundbreaking the movie is as a whole
   
   - "Going into this, I knew absolutely nothing about the story other than the fact that it was adapted from a video game and it was a horror. Turns it out was one of the most fun rides i have seen in theaters this year. What may have been marketed as a horror i would say bordered on comedy. The combination was done really well."
 - Vibes based will be the less obvious and more conceptual ratings that are about the vibe of the movie the atmosphere this will also include the reviews that are just saying whether the movie was good or otherwise, as that plays into the feel of the movie

   - "Snow is so beautiful. Every movie should have snow. Headlights, taillights, police lights all reflect so gorgeously throughout the first 30 minutes. As someone who has never touched these games, these monster designs are insane. Love the level-based approach to this script. Far more comedic than I was expecting, really more a stoner comedy than a dreadful horror. At times it was close to becoming a bit too annoying for my tastes, but Austin Abrams is just so captivating in these impossible situations that I always stayed on board. Lost a tad bit of steam towards the end and I don't think the movie ever topped the initial car crash scenes, but I had a bloody good time with this. 2026 Ranked"
 
## Annotation Guidelines & Decision Hierarchy

When a review blends multiple categories, human annotators and models must apply the following tie-breaking rules:
 - Dominant Semantic Weight: Assign the label corresponding to the core evaluative claim. A passing reference to an actor in a review primarily analyzing cinematography is labeled vibe_focused.
 - Actor vs. Plot (Character Decisions):If the comment discusses a character's foolishness, survival choices, or narrative decisions within the plot ("he may be a dumbass, but he was my dumbass"), classify as plot_focused.
 - If the comment assesses the actor's charisma, screen presence, or delivery ("Austin Abrams does a great job playing a lovable, hapless idiot"), classify as actor_focused.
 - Vague Story Claims: If a review mentions a story element without substantive narrative critique ("Perfect start, scrambled finish +1 star for sweet pov's"), the sensory/tonal evaluation overrides the narrative mention and defaults to vibe_focused.

## Edge Cases


**"he may be a dumbass, but he was my dumbass"**

Classification: plot_focused

Edge cases that specifically address the character plot line and how the character acts within the storyline  will be sorted into actor focused instead of plot focused if it's not detailed about the characters journey and it will be sorted into plot focused if it is

**"Good balance of funny moments and jumpscares. I really like how the director incorporated POV shots to evoke the feeling of playing a video game Austin Abrams is a star! The ending damn near made me cry"**

Classification: vibe_focused

Cases that address more than one category in this case the atmosphere and the actor will be sorted based on which one they speak about more and if equal, it will be in order of mention

**"Sandra Bullock and a love story will always have a chokehold on me it’s so serious"**

Classification: actor_focused

If the plot is mentioned as a simple addendum to something else like the atmosphere or the actor, it'll be sorted based on the main topic of the sentence, regardless of the plot mention

## Evaluation Strategy & AI Workflow

 - Data Pipeline: Extracted and annotated a 203-example balanced corpus across four recent theatrical releases (Resident Evil, Primetime, Practical Magic 2, and The End of Oak Street) preserving at least 20% representation per class.
 - AI Tool Integration: Leveraged LLM assistance to parse raw review exports, generate candidate labeling passes, and identify candidate boundary conflicts.
 - Model Evaluation: Benchmarked zero-shot LLM inference (Llama-3 via Groq) against a fine-tuned distilbert-base-uncased classifier on a stratified test split (N=31).
 - Success Criteria: Evaluated on per-class precision, recall, and macro F1 scores, with specific attention to resolving majority-class collapse and boundary ambiguity.

