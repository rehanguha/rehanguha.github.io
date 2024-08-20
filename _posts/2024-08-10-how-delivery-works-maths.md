---
layout: post
title: "Quick mathematical understanding behind: How package/letter/document delivery works?"
excerpt: "Delivering a package from destination \"A\" to destination \"B\" involves a series of processes that can be modeled mathematically using principles from logistics, optimization, and operations research."
categories: [Mathematics, Optimization, Reference, SCM, Logistics]
tags: [Optimization, Concept, Logistics, Operations Research, SCM, delivery]
share: true
comments: true
mathjax: true
---

This summary outlines the process of delivering a package from one destination to another, focusing on key logistics and mathematical principles. The process begins with **route optimization** to determine the most efficient path, followed by the selection of an appropriate **transportation mode** based on cost and speed. The total **delivery time** is calculated, factoring in travel time, handling, and processing. **Cost optimization** is achieved using models like the Economic Order Quantity (EOQ) to minimize expenses. **Queueing theory** is applied to manage potential delays at various stages, and the overall success probability is assessed, considering risks of delays or failures.

Below is a breakdown of the process along with the mathematical aspects involved:

## Concepts

### Route Optimization
   - **Objective:** Find the most efficient route from A to B, minimizing cost, time, or distance.
   - **Mathematical Model:** 
     - **Dijkstra’s Algorithm:** Used to find the shortest path between two points in a graph, where nodes represent locations and edges represent routes with associated costs (e.g., distance, time).
     - **Formula:** 

       $$
       \text{Cost}(A, B) = \min \left( \sum_{i=1}^{n-1} d_i \right)
       $$

       where $$ d_i $$ is the distance between consecutive points on the route from A to B.

### Transportation Mode Selection
   - **Objective:** Choose the mode of transport (e.g., air, road, rail, sea) that balances speed and cost.
   - **Mathematical Model:**
     - **Cost Function:** 

       $$
       C = C_{\text{trans}} + C_{\text{handling}} + C_{\text{time}}
       $$

       where:
       - $$ C_{\text{trans}} $$ is the transportation cost,
       - $$ C_{\text{handling}} $$ is the cost associated with loading/unloading,
       - $$ C_{\text{time}} $$ is the time-related cost (e.g., penalties for delays).

### Time Calculation
   - **Objective:** Estimate the time taken to deliver the package.
   - **Mathematical Model:**
     - **Time Calculation Formula:**

       $$
       T = \frac{D}{v} + T_{\text{processing}} + T_{\text{loading/unloading}} + T_{\text{delays}}
       $$

       where:
       - $$ D $$ is the total distance,
       - $$ v $$ is the average speed of the transport,
       - $$ T_{\text{processing}} $$ is the time for processing (sorting, customs),
       - $$ T_{\text{loading/unloading}} $$ is the time spent on loading and unloading the package,
       - $$ T_{\text{delays}} $$ accounts for any unexpected delays.

### Inventory and Warehousing
   - **Objective:** Manage storage if the package is held in transit.
   - **Mathematical Model:**
     - **EOQ (Economic Order Quantity) Model:** To minimize total inventory costs.
     - **Formula:**

       $$
       EOQ = \sqrt{\frac{2DS}{H}}
       $$

       where:
       - $$ D $$ is the demand rate,
       - $$ S $$ is the order cost,
       - $$ H $$ is the holding cost per unit.

### Queueing Theory for Handling Delays
   - **Objective:** Model delays at sorting centers, hubs, or delivery stations.
   - **Mathematical Model:**
     - **M/M/1 Queue Model:** Assumes a single queue with Poisson arrivals and exponential service times.
     - **Formula:**

       $$
       L_q = \frac{\lambda^2}{\mu(\mu - \lambda)}
       $$

       where:
       - $$ L_q $$ is the average number of packages in the queue,
       - $$ \lambda $$ is the arrival rate,
       - $$ \mu $$ is the service rate.

### Cost Optimization
   - **Objective:** Minimize the total cost of delivery while meeting service requirements.
   - **Mathematical Model:**
     - **Linear Programming:** To optimize costs subject to constraints (e.g., budget, time).
     - **Objective Function:**

       $$
       \text{Minimize } Z = \sum_{i=1}^n c_ix_i
       $$

      subject to:

       $$
       \sum_{j=1}^m a_{ij}x_j \leq b_i, \quad x_j \geq 0
       $$

       where:
       - $$ Z $$ is the total cost,
       - $$ c_i $$ is the cost coefficient,
       - $$ x_i $$ is the decision variable,
       - $$ a_{ij} $$ are the coefficients in the constraint equations,
       - $$ b_i $$ are the constraint bounds.

### Final Delivery
   - **Objective:** Ensure the package reaches destination B.
   - **Mathematical Consideration:** 
     - **Success Rate Model:** Estimating the probability that a package is delivered successfully.
     - **Formula:**

       $$
       P(\text{success}) = 1 - \sum P(\text{failure at step } i)
       $$

       This involves considering all potential failure points (loss, damage, misrouting).

### Summary of the Process:
1. **Route is optimized** to minimize travel time and cost.
2. **Transport mode is selected** based on cost and speed considerations.
3. **Time is calculated** for the delivery considering various factors.
4. **Inventory management** is handled if the package is held temporarily.
5. **Queueing models** are used to manage potential delays.
6. **Cost optimization** ensures the delivery process is economically viable.
7. **Final delivery** involves assessing and ensuring the package reaches its destination safely.

These mathematical models help in making informed decisions to ensure efficient and cost-effective delivery of packages from A to B.

## Example

Let’s walk through an example of delivering a package from destination **A** (say, New York City) to destination **B** (say, Los Angeles). We’ll apply the various mathematical models and concepts discussed to demonstrate the process.

### Scenario Details:
- **Distance (D):** 4,500 km
- **Average Speed (v):** 80 km/h by truck
- **Handling Time:** 2 hours at both A and B
- **Cost Per km:** $1.5
- **Loading/Unloading Cost:** $50
- **Processing Time:** 5 hours at a central hub
- **Probability of Delay:** 10%
- **Holding Cost per Day:** $2 per package
- **Demand Rate (D):** 500 packages/day
- **Order Cost (S):** $100
- **Service Rate (μ):** 10 packages/hour
- **Arrival Rate (λ):** 8 packages/hour

### Route Optimization
We use **Dijkstra’s algorithm** or other shortest-path algorithms to find the most efficient route from New York City to Los Angeles.

Given it's a straight route on highways, the shortest path is simply the direct road distance of **4,500 km**.

### Transportation Mode Selection
We select **truck transport** because it's cost-effective for this distance. Now, let's calculate the cost:

- **Transportation Cost ($$C_{trans}$$):**

  $$
  C_{\text{trans}} = \text{Distance} \times \text{Cost per km} = 4500 \times 1.5 = \$6750
  $$

- **Handling Costs ($$C_{handling}$$):**

  $$
  C_{\text{handling}} = 50 (\text{at A}) + 50 (\text{at B}) = \$100
  $$

- **Total Cost (C):**

  $$
  C = C_{\text{trans}} + C_{\text{handling}} = 6750 + 100 = \$6850
  $$

### Time Calculation
To calculate the total time taken:

- **Travel Time ($$T_{travel}$$):**

  $$
  T_{\text{travel}} = \frac{D}{v} = \frac{4500 \text{ km}}{80 \text{ km/h}} = 56.25 \text{ hours}
  $$

- **Processing Time ($$T_{processing}$$):**

  $$
  T_{\text{processing}} = 5 \text{ hours}
  $$

- **Loading/Unloading Time ($$T_{loading/unloading}$$):**

  $$
  T_{\text{loading/unloading}} = 2 (\text{at A}) + 2 (\text{at B}) = 4 \text{ hours}
  $$

- **Total Time ($$T$$):**

  $$
  T = T_{\text{travel}} + T_{\text{processing}} + T_{\text{loading/unloading}} = 56.25 + 5 + 4 = 65.25 \text{ hours} \approx 2.72 \text{ days}
  $$

### Inventory and Warehousing
If the package is held at a warehouse for a day:

- **Holding Cost:**

  $$
  \text{Holding Cost per day} = \$2 
  $$

  For 2.72 days:

  $$
  \text{Total Holding Cost} = 2.72 \times 2 = \$5.44
  $$

### Queueing Theory for Handling Delays
Considering delays at the central hub using the **M/M/1 queue model**:

- **Average Number of Packages in Queue ($$L_q$$):**

  $$
  L_q = \frac{\lambda^2}{\mu(\mu - \lambda)} = \frac{8^2}{10(10 - 8)} = \frac{64}{20} = 3.2 \text{ packages}
  $$

- **Expected Waiting Time in Queue:**

  $$
  W_q = \frac{L_q}{\lambda} = \frac{3.2}{8} = 0.4 \text{ hours}
  $$

### Cost Optimization
Using **Economic Order Quantity (EOQ)** to determine the optimal batch size for deliveries:

- **EOQ Calculation:**

  $$
  EOQ = \sqrt{\frac{2DS}{H}} = \sqrt{\frac{2 \times 500 \times 100}{2}} = \sqrt{50000} = 223.6 \text{ packages}
  $$

Thus, ordering around 224 packages at a time minimizes the total cost.

### Final Delivery Success Probability
If there’s a **10% probability of delay** at each step, and there are 3 major steps (transport, processing, delivery):

- **Probability of Delay:**

  $$
  P(\text{success}) = 1 - \left( \text{Probability of Delay in Transport} + \text{Processing} + \text{Delivery} \right) = 1 - 0.3 = 0.7
  $$
  
Thus, there’s a **70% probability** the package will be delivered without delay.

### Summary of the Process
1. **Route Optimization** determined a 4,500 km direct route.
2. **Transportation Cost** using a truck was calculated at $6,850.
3. **Total Time** was calculated to be approximately 2.72 days.
4. **Holding Cost** was estimated at $5.44.
5. **Queueing Theory** showed an average of 3.2 packages waiting in line at the hub.
6. **EOQ Model** suggested ordering around 224 packages minimizes costs.
7. **Final Probability** indicated a 70% chance of on-time delivery.

These calculations give a comprehensive understanding of the logistics, cost, and time associated with delivering a package from New York City (A) to Los Angeles (B).

## References

1. [Dijkstra's Shortest Path Algorithm - GeeksforGeeks](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)
2. [Logistics Cost Management - ResearchGate](https://www.researchgate.net/publication/328698820_Logistics_Cost_Management)
3. [Time-Distance Calculation in Logistics - Investopedia](https://www.investopedia.com/terms/d/distance-miles-time.asp)
4. [EOQ Model Explanation - Investopedia](https://www.investopedia.com/terms/e/economicorderquantity.asp)
5. [Queueing Theory and the M/M/1 Model - MIT OpenCourseWare](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-263j-data-communication-networks-fall-2002/lecture-notes/l8.pdf)
6. [Linear Programming Basics - Stanford University](https://web.stanford.edu/~boyd/ee364a/lectures/linprog.pdf)