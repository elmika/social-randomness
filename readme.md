# Social Randomness.

##### Build fair and robust randomness when several parties are involved



### A standard random dice

**Simulate a dice, with a dApp involving 2 people**

The purpose of this app is to generate a random integer between 1 and 6 through a process involving 2 parties. 

To achieve this, we will build an application that lets its runner and another participant choose a number between 1 and 6. It will then add the two inputs, calculate the result modulo 6, and add 1. The final result is our random number.

**Rationale**: As long as the person running the contract and the other person choose a value randomly between 1 and 6 without communicating with one another, the result will be random.

