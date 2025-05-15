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

Step 2: Determine the arrival times of the passengers. For each passenger, you generate the inter-arrival times (time between arrivals) using Exponential distribution. These inter-arrival times will give you the exact arrival times of each passenger.

inter_arrival_times = np.random.exponential(scale=1/5, size=num_passengers - 1) arrival_times = np.cumsum(np.insert(inter_arrival_times, 0, 0))


Step 3: Normalize the arrival times. After generating the inter-arrival times and calculating the arrival times, you normalize these times to fit within the desired window (e.g., between 9:00 AM and 10:00 AM).
