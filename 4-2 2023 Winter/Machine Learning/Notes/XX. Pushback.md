- Only 30 hrs before
- Runaways are marked and maybe its better to create a score of how problematic the runaway is
	- Target encoding
		- Runway, Carrier, Season, etc. are going to influence stuff
	- runway # = angle / 10
- Avg delay of runway over last year?
- Departure time is prob most useful rn
	- Try to do LinReg
	- Baseline is departure time - 50mins?
- Prediction
	- For each flight, predict 6 different times coming up to the pushback
- arrival/departure from gate to runway is in standtimes. Other references to arrival/departure is in the general airport sense.
- Neural Network or Boosted Decision Tree (or other Tree Ensemble)
----
- ![[Pasted image 20230317103739.png|500]]
- ![[Pasted image 20230317103813.png|400]]
- ![[Pasted image 20230317103935.png|400]]
- Kyler Baseline:
	- ETD - 15mins
- ![[Pasted image 20230317104457.png|400]]
	- Or max(0, ETD - 15mins)
- ![[Pasted image 20230317105140.png|400]]
- Slides: https://docs.google.com/presentation/d/1zSm2aQ8ES1AQs3ZerDcBWmotegwKdURKBR8jsgSbeBA/edit?usp=sharing
