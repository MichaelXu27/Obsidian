1. Greedy choice property (GCP)
	* first choice is consistent with some optimal solution
2. Induction property:
	* after the first choice, we have a smaller version of the same problem
3. Optimal subproblem:
	* if we optimally solve subproblem and we add 1st GCM full solution is optimal
## The Cable Installer Problem
* You are an installer for Charter Cable
* Your job is to do installations by appointment
* Appointments have a fixed length (30 mins) and must start on a 30 min boundary
* Each new customer specifies an earliest and latest possible start time for her apartment
* *Goal*: Schedule as many appointments in a day
#### Formally:
* given a set P of unit-duration jobs that must be scheduled at integer times (time slots of 0,1,2)
* Only one job per slot
* Job i may start in any slow from s_i to e_i inclusive
* Goal: find a schedule that maximized number of jobs scheduled
#### Idea:
* For times e: increasing order
* find latest time at which someone can be scheduled
* among all jobs available at t, pick one with the latest start time
#### Claim:
* our algo yields an optimal solution, i.e one with the most scheduled jobs
#### GCP
* There exists an optimal schedule(`f(x)`) such that if job `i` is the one chosen by algo and it is scheduled at `t` , Then `f(x)` puts `i` and `t`
* **Proof**:
	* if `f(x)` puts `i` at `t`, yay!
	* if `f(x)` does not schedule `i` at all...
		* if `t` is empty, put `i` there
		* if `t` is not empty, replace its job with `i`
	* if `f(x)` puts `i` at `t != t'`
		* if `t'` is empty, move `i` to `t'`
		* if `t'` contains some `j != i'` ... can we move j to t, `i'` to `t'`? we have t < t' (because t' is globally latest)
		* s_i < s_i'
* **IS**
	* after placing i' at t', we are left with a smaller version of the subproblem
	* Fix #1: after we schedule a job at t', trim all other jobs to end before t'
	* Fix #2: allow constraints (blocked slots) for every problem
* **OS**
	* If we solve subproblem p-{i'} optimally and adjoin (t', i'), the resulting solution is globally optimal.