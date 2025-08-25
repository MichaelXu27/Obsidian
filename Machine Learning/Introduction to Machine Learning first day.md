* Homework 0 is out but you don't need to submit it
## Credit Card Approval question
* The input is customer information
* Output is a prediction

	One solution to the problem above is a brute force solution where you map every attribute to either a good customer or bad customer
		Really bad space and its going to be very large
		Not scalable: possible attribute combinations could be infinite, storage problems, computation problems
## A machine learning approach
* We call every decision plan a hypothesis/model (which is usually some math function)
* We make an assumption that we have access to Data(which could be historical customer data)
* We need to find a hypothesis that fits the data
## What is machine learning?
* "learning from data"
* "using a set of observations to uncover an underlying pattern"
#### Some use scenarious of machine learning
* A pattern exists
* no analytical solution: we cannot pin it down mathematically
* we have data on it
![[Pasted image 20250825102145.png]]

![[Pasted image 20250825102402.png]]![[Pasted image 20250825102409.png]]
* Hypothesis set is basically constricting the limits of your algorithm i think
* We're gonna cover the entire chart this semester
## Course Plan:
* First half of semester :Foundations
	* a focus on linear models
	* discuss the theretical foundations of machine learning
* Second half: techniques
	* discussing different learning models
## Types of learning:
* **Supervised learning** (focus of the course)
	* Given training data(input, correct output)
	* try to predict the output for data not seen before
	* Given data with (input, correct output), learn a pattern that can predict previously unseen data
* **Unsupervised learning**
	* Supposed you have the feature vectors but no labels. Still want to describe the data in some useful way
* **Reinfocement Learning**
	* Agent interacts with the world by taking actions
	* Feedback is in the form of rewards(or costs)
	* Agent must learn a policy, which maps from the state of the world to an action
	* Major challenges
		* Exploration/exploitation
		* Delayed reward/ credit assignment
## Lecture today:
#### Linear Hypothesis Space (Perceptron)
* 