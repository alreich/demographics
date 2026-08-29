# demographics

This repository contains work-in-progress done with Claude.AI (doing the heavy lifting) to estimate time-remaining for modern humans (i.e. homo sapiens). All species are mortal, so how long will modern humans "walk the earth", so to speak? That is, assuming modern humans first appeared around 200,000 BCE, how long will it be before they go extinct or evolve into a different species, under the assumptions that no sudden catastrophe intervenes and that the present moment is not a privileged position in our total history?

**IMPORTANT NOTE: None of the estimates here should be treated as any kind of forecast. Their real use is as order-of-magnitude estimates and an illustration of how significant the structural modeling choices are to the final answer.**

This work combines the following items to produce estimates which culminate in the notebook, **human_time_remaining_v2.ipynb**.:
* a **Bayesian statistical model** of the total number of humans ever born
  * e.g., estimate here is approx. 79-80B +/- 5-6B since ~200,000 BCE
* an empirical survival-curve **prior distribution** for mammalian species durations built from fossil data
  * That is, if the duration of species is a random variable, what is its distribution?
  * *Duration* is essentially first-to-last appearance of the species in the following fossil databases:
    * The Paleobiology Database (https://paleobiodb.org)
    * The NOW (New and Old Worlds) fossil mammal database (https://nowdatabase.org/)
  * e.g., median duration estimates found here: 5.2Myr for all mammalia and 3.5Myr for primates
* and a review of the anthropic "Doomsday argument" literature

**The primary conclusion is that the time-remaining for modern humans is, well, inconclusive. The three structurally different methods used here produce answers that differ by roughly four to five orders of magnitude.**

All of the work here is captured in Jupyter notebooks. Here is a description of the relevant notebooks:
* **human_population_bayesian_model_v5.ipynb** -- a Bayesian model of the total number of humans ever born (build by Claude.AI)
* **How_Many_Humans.ipynb** -- dialog with Claude.AI (prompts and answers) while building the Bayesian model
* **mammal_species_survival_v1.ipynb** -- an empirical survival-curve prior for mammalian species duration built from fossil data (built by Claude.AI)
* **human_time_remaining_v2.ipynb** -- estimates of how much longer Homo sapiens is likely to persist before extinction or transformation into a different species, under the explicit assumption that no sudden catastrophe intervenes and that the present moment is not a privileged position in the species' total history (built by Claude.AI)
* **human_species_lifespan.ipynb** -- dialog with Claude.AI (prompts and answers) while building the two notebooks above (empirical prior & time-remaining estimates)

Previous (older) versions of the notebooks are also available.
