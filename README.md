---
Title: Hidden Markov Models for Real-Time Indicator Integration
Author: Bolun, Leon
Date: May. 27, 2024  
Comment: In this doc, we demonstrate why we choose HMM to integrate the factors.
---

# 1. Why Choose HMM

## (1) Flexibility in Modeling State Transitions

Another significant advantage of HMMs is their flexibility in modeling state transitions, which can be particularly useful in financial markets where latent states (e.g., market regimes) can switch in complex patterns not observable directly through raw financial data. HMMs allow the modeling of these transitions explicitly and adjust the model's sensitivity to regime shifts. This flexibility is not easily replicated in simpler statistical models.

## (2) How Forward Algorithm can Incorporate Historical Information

### Markov Property in HMMs

In Hidden Markov Models, the Markov property states that the probability of transitioning to the current state depends only on the immediate previous state. This dependency is defined by the state transition probabilities, \( P(X_t \mid X_{t-1}) \), which specify the likelihood of transitioning from any given state to the next.

### Accumulation of Historical Information Through Forward Probabilities

Even though the Markov property implies that each state depends only on its immediate predecessor, forward probabilities in HMMs incorporate information from all previous observations. This integration of historical data into the state estimation process is crucial for accurately predicting the current state based on all available information.

#### Calculation of Forward Probabilities

The forward probability \( \alpha_t(i) \) represents the probability of the process being in state \( i \) at time \( t \), given all observations up to and including \( t \). The formula for calculating \( \alpha_t(i) \) is:

$$
\alpha_t(i) = \left(\sum_{j=1}^{N} \alpha_{t-1}(j) \cdot a_{ji}\right) \cdot b_i(O_t)
$$

Where:
- \( \alpha_{t-1}(j) \) is the forward probability at the previous time step for state \( j \).
- \( a_{ji} \) is the transition probability from state \( j \) to state \( i \).
- \( b_i(O_t) \) is the probability of observing the current observation \( O_t \) given state \( i \).

#### Steps in Forward Probability Calculation

1. **Initialization**:
   $$
   \alpha_1(i) = \pi_i \cdot b_i(O_1)
   $$
   Here, \( \pi_i \) is the initial probability of being in state \( i \), and \( b_i(O_1) \) is the probability of observing the first observation \( O_1 \) given state \( i \).

2. **Recursive Update**:
   $$
   \alpha_t(i) = \left(\sum_{j=1}^{N} \alpha_{t-1}(j) \cdot a_{ji}\right) \cdot b_i(O_t)
   $$
   Each state's probability at time \( t \) is calculated based on the probabilities of all states at \( t-1 \), adjusted by their respective transition probabilities to state \( i \) and the probability of observing \( O_t \) from state \( i \).

### Reconciling Markov Property with Historical Information Accumulation

#### Historical Information Accumulation

Although each state's transition depends only on its immediate predecessor, the recursive calculation of forward probabilities allows each state's probability to implicitly contain information from the entire sequence up to the current point. This comprehensive integration is achieved by basing each state's probability on the cumulative probabilities of all previous states influenced by respective observations.

#### Information Transfer

This method ensures that information from each previous step is carried forward and updated with each new observation. Thus, while the Markov property maintains the model's simplicity and computational manageability, the forward algorithm ensures that all relevant historical information is utilized in estimating current state probabilities.

## Conclusion

The Markov property and the forward algorithm in HMMs complement each other, allowing the models to efficiently and powerfully handle sequential data. The structure enables HMMs to use past data effectively while adhering to the Markov property, thus providing a robust framework for sequence analysis.
