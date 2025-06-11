This Python script performs a multi objective energy system optimization to determine the best combination of renewable energy technologies solar, wind, battery storage, and biogas to supply both electricity and heat demands over time, based on hourly data. The goal is to minimize levelized cost of energy (LCOE), unmet demand, and CO₂ emissions, using a weighted optimization approach.

The script begins by importing necessary libraries including pandas for data handling, numpy for numerical operations, matplotlib for plotting, scipy.optimize.minimize for numerical optimization, and tqdm for progress tracking. It then loads hourly input data from four CSV files representing electricity demand, heat demand, solar energy availability, and wind energy availability.

Each dataset is cleaned and merged into a single dataframe based on the hour. Solar and wind capacity factors are scaled, capped at 1.0, to simulate improved technology or better resource conditions.

The core of the script is a nested loop that iterates over combinations of weights for three objectives: LCOE, unmet demand, and CO₂ emissions. For each valid combination of weights (where their sum is ≤ 1), the script defines an objective function and constraints. The objective function simulates the entire energy system hour by hour, calculating:

How much electricity is met using solar, wind, battery discharge, and biogas.

How much heat is met using biogas.

Battery state of charge and flow.

Total biogas consumption, energy met, unmet demand, operational and capital expenditures, LCOE, and CO₂ emissions from biogas combustion.

The minimize() function is then used to find the optimal capacities (sizes) of the five system components solar panels, wind turbines, battery, biogas generator, and a power converter—subject to the constraint that at least 97% of electricity and heat demand must be met.

If the optimizer finds a solution, additional performance indicators are calculated, including specific CO₂ emissions, total battery discharge, unmet electricity/heat, and biomass needed to produce the consumed biogas. All of these results are stored in a dictionary and appended to a results list.

After all weight combinations are tested, a 3D plot visualizes the trade off between unmet demand, LCOE, and CO₂ emissions. Finally, all optimization results are saved into a CSV file (optimization_results_t32019pareto.csv) and printed for review.

The weight configuration #-out is the optimal-optimal confuguration presented in the master thesis. To run the code fast and avoid Pareto front use those values as weight distribution. 
