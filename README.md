🧠 Concept of Poisson Process
A Poisson process is a mathematical model used to describe random events that happen over time (in this case, passengers arriving at different times). The key idea is that the arrival events (passengers) are independent of each other and happen at a constant average rate, but randomly.

A Poisson process with rate λ means:

Implementation: np.random.poisson(POISSON_MEAN_PASSENGERS)

The number of arrivals over a time period T follows a Poisson distribution.

The time between arrivals follows an exponential distribution with mean 1/λ

Implementation: generate_passenger_arrivals(self)

To simulate n arrivals in a fixed window:

Generate n-1 exponentially distributed inter-arrival times.

Add them up cumulatively to get arrival timestamps.

Normalize this to fit within the fixed window (in our case: 3600 seconds = 1 hour).



In our simulation, passenger arrivals for each flight are modeled using a Poisson process.

The Poisson distribution is used to model the number of events that occur in a fixed interval of time, given a certain average rate of occurrence (λ).

Models how many passengers arrive at the gate in a specific time interval.

Ref: Poisson Distribution | StatsDirect

The Exponential distribution models the time between events (or inter-arrival times) in a Poisson process.

Models the waiting times between passenger arrivals.

Ref: Exponential Distribution | Newcastle University

Ref: Exponential Distribution | Six Sigma Study Guide

👀 Example of Passenger Arrival Process
Suppose the flight departure time is 12:00 PM.
We want passengers to arrive between 9:00 AM and 10:00 AM.
We expect 5 passengers per hour (so, λ = 5).

Step 1: Determine the number of passengers for the flight. You would use a Poisson distribution to get the number of passengers arriving in the 1-hour window (between 9:00 AM and 10:00 AM).

num_passengers = np.random.poisson(lam=5, size=1)[0]

For example, the result might be num_passengers = 4.

Step 2: Determine the arrival times of the passengers. For each passenger, you generate the inter-arrival times (time between arrivals) using the Exponential distribution. These inter-arrival times will give you the exact arrival times of each passenger.

inter_arrival_times = np.random.exponential(scale=1/5, size=num_passengers - 1) arrival_times = np.cumsum(np.insert(inter_arrival_times, 0, 0))

🎯 The Goal
For each flight:

We want passengers to arrive over a fixed window:

departure_time - 3h → departure_time - 2h (a 1-hour window).

Within that window, the arrivals should resemble a Poisson process:

i.e., events (passenger arrivals) occur at random but at a steady average rate.

Time between arrivals follows an exponential distribution.

📏 What Is an Exponential Distribution?
The Exponential distribution is used to model the time between events in a Poisson process.

In simpler terms: if we want to know how long it takes for the next passenger to arrive (after the previous one), the Exponential distribution tells us the probability of different waiting times.
Key Feature of Exponential Distribution:

Memoryless property: The waiting time for the next arrival doesn't depend on how much time has already passed.

Example: It doesn't matter if you’ve been waiting for 5 minutes or 50 minutes; the chance of the next arrival happening in the next minute is the same.
🚀 Why Exponential Distribution for Inter-Arrival Times?
In your simulation, the passengers are arriving randomly over a fixed period of time before the flight departs. The Poisson process is being used, which means the time between arrivals (inter-arrival times) follows an Exponential distribution, not the number of passengers themselves.

This is how the Exponential distribution and Poisson distribution connect:

The Poisson distribution describes the count of events (passenger arrivals) in a fixed time period.

The Exponential distribution describes the time between those events.

Thus, when we're modeling passenger arrivals, we use Exponential distribution to model the time gaps between each passenger, and this leads to a Poisson distribution when you look at the number of arrivals over a fixed period.

🏃‍♂️ Exponential Distribution in Action:
The formula for the Exponential distribution looks like this:

P(X ≤ t) = 1 - e^(-𝜆𝑡)

Where:

𝜆 is the rate of arrival (passenger arrivals per unit of time).
𝑡 is the time we’re waiting (like 5 minutes, 10 minutes, etc.).
The function P(X ≤ t) tells us the probability that the next arrival will happen within time

Example Calculation:

If we expect 1 passenger every 10 minutes (i.e., , we can calculate the probability of the next passenger arriving in less than 5 minutes.

Mean time between arrivals = 10 minutes.
Arrival rate (λ) = 1 passenger every 10 minutes (λ = 1/10)
We calculate how likely it is to get a passenger in the next 5 minutes:

P(X ≤ 5) = 1 - e^(-(1/10)⋅5) = 1 - e^(-0.5) ≈ 0.393

This means there is a 39.3% chance that the next passenger will arrive in less than 5 minutes.

🪄🧑‍💻 What This Achieves
✅ The density of arrivals is highest near the start, tapering off (typical Poisson curve).

✅ Arrivals are irregular, not equally spaced.

✅ Entire distribution is bounded in the 1-hour window [T-3h, T-2h].


Step 3: Normalize the arrival times. After generating the inter-arrival times and calculating the arrival times, you normalize these times to fit within the desired window (e.g., between 9:00 AM and 10:00 AM).
