**Causality in Machine Learning**

  

Today’s ML can figure out patterns in huge data sets but Causality remains a challenge in today’s machine learning. 

Challenges due to lack of causal representation in ML models.

  

**Independent and Identically Distributed**

  

Machine Learning often disregards information that animals use heavily: intervention in the world, domain shifts, temporal structure - by and large we consider these factors a nuisance and try to engineer them away. In accordance with this, the majority of current successes of ML boil down to large scale pattern recognition on suitably collected independent and identically distributed data.

  

iid is a term often used in ML. It supposes that random  observation in a problem space are not dependent on each other and have a constant probability of occurring. The simplest example of iid is flipping a coin or tossing a die. The result of each new flip or toss is independent of previous ones and the probability of each outcome remains constant.

  

Generalising well outside the iid setting requires learning not mere statistical associations between variables, but an underlying causal model. Causal Models allow humans to previously gained knowledge for new domains. For instance, when you learn a real time strategy game such as Warcraft, you can quickly apply your knowledge to other similar games StarCraft, age of empires.

  

When learning a causal model one should thus require fewer examples to adapt as most knowledge.

  

Causal Model remain robust when interventions change the statistical distributions of a problem. For instance, when you see an object for the first time, your mind will subconsciously factor out lighting from its appearance. That is why you can recognise the object when you see it under new lightning conditions. 

  

Causal Models also allows us to respond to situations we haven’t seen before and think about counterfactuals. Counterfactuals play an important role in cutting down the number of training examples a ML model needs.

  

Causality can also be crucial to dealing with adversarial attacks, subtle manipulation’s that force ML systems to fail in unexpected ways. These attacks clearly constitute violations of the iid assumptions that underlies statistical Machine learning. Adversarial vulnerabilities are proof of the differences in robustness mechanisms of human intelligence and machine learning. Causality can. Be a possible defence against adversarial attacks.

  

Causality can address ML’s lack of generalisation. It is fair to say that much of the current practice and most theoretical results fail to tackle hard open challenges of generalisation across problems.

  

**Adding Causality to Machine Learning**

  

Two concepts Structural Causal Models and independent causal mechanisms. In general the principle states instead of looking into superficial statistical correlations an AI system should be able to identify causal variables and separate their effects on the environment.

  

This is the mechanism that allow you to different objects regardless of the view angle, background lighting and other noise. Disentangling these causal variables will make AI system more robust against unpredictable changes and interventions. As a result causal models won’t need huge training datasets.

 Once a causal model is available by external human knowledge or a learning process, causal reasoning allows to draw conclusions on the effect of interventions, counterfactuals and potential outcomes.

  

The authors also explore how these concepts can be applied to different branches of machine learning, including reinforcement learning, which is crucial to problems where an intelligent agent relies a lot on exploring environments and discovering solutions through trial and error. Causal structures can help make the training of reinforcement learning more efficient by allowing them to make informed decisions from the start of their training instead of taking random and irrational actions.

  

The researchers provide ideas fro AI systems that combine machine learning mechanisms and structural causal models “To combine structural causal modelling and representation learning, we should strive to embed a SCM into larger machine learning models whose input and output may be high dimensional and unstructured, but whose inner workings are at least partly governed by an SCM (that can be parameterised by neural network). The result may be modular architecture, where different modules can be individually fine-tuned and re-purposed for new tasks.

  

Such concepts bring us closer to the modular approach the human mind uses to link and reuse knowldege and skills across different domains and areas of the brain.