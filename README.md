# demographics

This repository contains work-in-progress done with Claude.AI (doing the heavy lifting) to estimate time-remaining for modern humans (i.e. homo sapiens).

All species are mortal. So we attempt to estimate how long modern humans will "walk the earth", before they go extinct or evolve into a different species, assuming the following:
* Modern humans first appeared around 200,000 BCE
  -- Could be earlier, but this gives us an estimate on the starting population size
* No sudden catastrophe intervenes
  -- Climate change, wars, and disease are likely, but let's try to be optimistic for now :-)
* The present moment is not a privileged position in our total history
  -- The Copernican principle applied to time scales

**IMPORTANT NOTE: None of the estimates here should be treated as any kind of forecast. Their real use is as order-of-magnitude estimates and provide an illustration of how significant the structural modeling choices are to the final answer.**

This work combines the following computations that culminate in the Jupyter notebook, **human_time_remaining_v2.ipynb**.:
* a **Bayesian statistical model** of the total number of humans ever born
  * e.g., estimate here is approx. 79-80B +/- 5-6B since ~200,000 BCE
  * This is significantly fewer than current published estimates (e.g., 117B)
  * However, the model here is different (better?) than previous models
* An empirical survival-curve **prior distribution** for mammalian species durations derived from fossil data
  * That is, if the duration of species is a random variable, what is its distribution?
  * *Duration* is essentially first-to-last appearance of the species in the following fossil databases:
    * The Paleobiology Database (https://paleobiodb.org)
    * The NOW (New and Old Worlds) fossil mammal database (https://nowdatabase.org/)
  * e.g., median duration estimates found here: 5.2Myr for all mammalia, 3.5Myr for primates, and even less for the homo genus

**The primary conclusion is that the time-remaining for modern humans is...well...inconclusive. The three structurally different methods used here produce answers that differ by roughly four to five orders of magnitude.** That's it. That's the result of all this effort. Along with the modeling choice, another problem is the lack of sufficient data on the homo genus, which began less than 3M years ago. That is such a small time scale. For example, if we layout the 4.5B years of earth's existence on a yard stick (~1m), then the homo genus timeline occupies less than 1mm at the very end. But, it's still ongoing, and hopefully, for much, much longer.

All of the work here is captured in Jupyter notebooks. Here is a description of the relevant notebooks:
* **human_population_bayesian_model_v5.ipynb** -- Derivation of a Bayesian model of the total number of humans ever born (build by Claude.AI)
* **How_Many_Humans.ipynb** -- The dialog with Claude.AI (prompts and answers) while building the Bayesian model
* **mammal_species_survival_v1.ipynb** -- Derivation of an empirical survival-curve (the prior) for mammalian species duration using fossil data (built by Claude.AI)
* **human_time_remaining_v2.ipynb** -- Derivation of estimates of how much longer Homo sapiens is likely to exist before extinction or evolution into a different species, under the assumption that no sudden catastrophe intervenes and that the present moment is not a privileged position in our species' total history (built by Claude.AI)
* **human_species_lifespan.ipynb** -- The dialog with Claude.AI (prompts and answers) while building the two notebooks above (mammal species survival & human time remaining estimates)

Previous (older) versions of the notebooks are also available.
