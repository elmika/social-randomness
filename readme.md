# Social Randomness.

##### Build fair and robust randomness when several parties are involved



### A standard random dice

**Simulate a dice, with a dApp involving 2 people**

The purpose of this app is to generate a random integer between 1 and 6 through a process involving 2 parties. 

To achieve this, we will build an application that lets its runner and another participant choose a number between 1 and 6. It will then add the two inputs, calculate the result modulo 6, and add 1. The final result is our random number.

**Rationale**: As long as the person running the contract and the other person choose a value randomly between 1 and 6 without communicating with one another, the result will be random.

**Structure of the App. [Draft, described as an API]**

[We may use openapi format for a standard definition]

- POST /new
  	silent input: Wallet id of person doing the call
  	required input: Another wallet #

  [optional inputs]: Watchers
  ​	response: running_app_id

	error response:
		40x if missing input
		40x if some wallet format is incorrect

- PATCH /running_app_id
  	silent input: wallet id of person doing the call
  	required input: number 1-6
  	response: 200

	error response:
		404 if no such app is running
		40x unauthorized if this user is not expected to give input
		40x if input already provided by this user
		40x if value is incorrect (non numerical)
		40x if value is incorrect (not integer)
		40x if value is incorrect (not within 1-6 range)
	
	note: Can only be applied once. All subsequent submissions are ignored.
		  One must use the same wallet as the person who called the /new method

- GET /running_app_id
  	silent input: wallet id of person doing the call
  	required input: nil
  	response: 
  		- 1-6 result if available.
  		- Details about execution:
  			- List of Participants (it does not matter who started to run the instance).
  			- List of Watchers
  			- Global Running State: Initialised, Waiting some input(s), computing, finalised. 
  			- State of individual inputs (given/pending)
  			- IF all inputs have been received and computed:
  				- Final result
  				- Individual random inputs (Each participant can verify computation is fair).

	error response:
		40x Unauthorized if caller is not a participant of the random trial nor a watcher.

- GET /
  	silent input: wallet id of person doing the call
  	optional inputs: 
  		- Filters (state, etc.)
  		- Order By
  	response: List of all contacts where the person doing the call is involved.





