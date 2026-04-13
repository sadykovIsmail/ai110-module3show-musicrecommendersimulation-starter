# Reflection: Music Recommender Simulation

## Profile Comparisons

### High-Energy Pop Fan vs. Chill Lofi Listener

These two profiles are essentially opposites on every axis — genre, mood, and energy — and the recommender reflected that perfectly. The pop fan's list was dominated by uptempo tracks with happy moods, while the lofi listener's list clustered around quiet, mellow songs. The gap between first place and third place was much larger for the lofi listener (~1.0 score gap) than for the pop fan, which suggests that "lofi/chill" is a tighter niche in the dataset — once you leave those two songs behind, nothing else fits closely.

### Chill Lofi Listener vs. Deep Intense Rock

These profiles share an interesting property: both have a clear, distinct genre in the catalog. The lofi listener's top two results (Library Rain and Midnight Coding) were nearly tied. The rock profile's top result (Storm Runner) was nearly perfect, but the second result was a *happy* rock song, not an intense one. This shows how the genre bonus wins even when the mood is wrong — a rock-happy song outscored an intense-metal song because genre weighs twice as much as mood. For the lofi listener, both lofi songs happened to also match the mood, so the pattern was less visible.

### High-Energy Pop Fan vs. Deep Intense Rock

Both profiles wanted high energy, but the rest of their preferences diverged completely. The pop fan's top five were dominated by cheerful, danceable songs; the rock fan's top five were loud and aggressive. Despite sharing a high target energy, they shared zero songs in their top five. This makes sense — energy proximity alone only adds up to 1.0 point, while a genre match is worth 2.0. Energy is a supporting signal, not the primary filter.

---

## What Changed When I Ran the Weight-Shift Experiment

When I halved the genre weight (from 2.0 to 1.0) and doubled the energy weight (from max 1.0 to max 2.0), the rock profile's top five changed significantly: Electronic Euphoria (edm, 0.93 energy) entered the top three, even though its genre is edm. This was surprising at first, but it makes total sense — when energy matters twice as much as genre, songs that are close in energy can beat songs that share a genre but have very different energy levels.

The takeaway: the weights are the model. Changing one number reshapes the entire ranking. This is exactly why real recommender systems tune their weights carefully using user feedback data rather than picking them by intuition.

---

## What I Learned

Building this simulation taught me that the hardest part of a recommender is not the code — it's deciding what to measure and how much each measurement should matter. Getting the scoring formula running took an afternoon; understanding why the results were right or wrong took much longer.

I was also surprised by how quickly filter bubbles appeared in a 20-song catalog. With only two lofi songs available, a lofi listener's experience is essentially fixed from the start. Scaling the catalog is not just a performance problem — it is a fairness problem. Every genre that is under-represented will produce a worse experience for users who prefer it.
