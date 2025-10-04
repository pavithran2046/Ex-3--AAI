<H3>NAME:PAVITHRAN S</H3>
<H3>REGISTER NO:212223240113</H3>
<H3>EX. NO.3</H3>
<H3>DATE:30-09-2025</H3>
<H1 ALIGN =CENTER> Implementation of Approximate Inference in Bayesian Networks
</H1>

## Aim: 
   To construct a python program to implement approximate inference using Gibbs Sampling.</br>
## Algorithm:
   Step 1: Bayesian Network Definition and CPDs:<br>
    <ul> <li>Define the Bayesian network structure using the BayesianNetwork class from pgmpy.models.</li>
    <li>Define Conditional Probability Distributions (CPDs) for each variable using the TabularCPD class.</li>
    <li>Add the CPDs to the network.</li></ul>
    Step 2: Printing Bayesian Network Structure:<br>
    <ul><li>Print the structure of the Bayesian network using the print(network) statement.</li></ul>
   Step 3: Graph Visualization:
    <ul><li>Import the necessary libraries (networkx and matplotlib).</li>
    <li>Create a directed graph using networkx.DiGraph().</li>
    <li>Define the nodes and edges of the graph.</li>
    <li>Add nodes and edges to the graph.</li>
    <li>Optionally, define positions for the nodes.</li>
    <li>Use nx.draw() to visualize the graph using matplotlib.</li></ul>
    Step 4: Gibbs Sampling and MCMC:<br>
    <ul><li>Initialize Gibbs Sampling for MCMC using the GibbsSampling class and provide the Bayesian network.</li>
    <li>Set the number of samples to be generated using num_samples.</li></ul>
    Step 5: Perform MCMC Sampling:<br>
    <ul><li>Use the sample() method of the GibbsSampling instance to perform MCMC sampling.</li>
    <li>Store the generated samples in the samples variable.</li></ul>
    Step 6: Approximate Probability Calculation:<br>
    <ul><li>Specify the variable for which you want to calculate the approximate probabilities (query_variable).</li>
    <li>Use .value_counts(normalize=True) on the samples of the query_variable to calculate approximate probabilities.</li></ul>
    Step 7:Print Approximate Probabilities:<br>
    <ul><li>Print the calculated approximate probabilities for the specified query_variable.</li></ul>


## Program:
```
from pgmpy.models import BayesianNetwork
from pgmpy.factors.discrete import TabularCPD
from pgmpy.sampling import GibbsSampling

model = BayesianNetwork([('Rain', 'Traffic'), ('Accident', 'Traffic')])
cpd_rain = TabularCPD(variable='Rain', variable_card=2, values=[[0.7], [0.3]])  # 0: No rain, 1: Rain
cpd_accident = TabularCPD(variable='Accident', variable_card=2, values=[[0.9], [0.1]])  # 0: No accident, 1: Accident

cpd_traffic = TabularCPD(
    variable='Traffic',
    variable_card=2,
    values=[
        [0.9, 0.6, 0.7, 0.1],   # Traffic = No
        [0.1, 0.4, 0.3, 0.9]    # Traffic = Yes
    ],
    evidence=['Rain', 'Accident'],
    evidence_card=[2, 2]
)

model.add_cpds(cpd_rain, cpd_accident, cpd_traffic)

assert model.check_model()

print("Bayesian Network Structure:")
print(model.edges())
import networkx as nx
import matplotlib.pyplot as plt

G = nx.DiGraph()
G.add_nodes_from(['Rain', 'Accident', 'Traffic'])
G.add_edges_from([('Rain', 'Traffic'), ('Accident', 'Traffic')])

pos = nx.spring_layout(G)  # node positions
nx.draw(G, pos, with_labels=True, node_size=3000, node_color="skyblue", arrowsize=20, font_size=12)
plt.title("Bayesian Network Structure")
plt.show()

gibbs = GibbsSampling(model)

num_samples = 5000
samples = gibbs.sample(size=num_samples)


query_variable = 'Traffic'
approx_probs = samples[query_variable].value_counts(normalize=True)


print(f"\nApproximate probabilities for {query_variable}:")
print(approx_probs)
```



## Output:
<img width="805" height="633" alt="image" src="https://github.com/user-attachments/assets/b2531508-cf26-4a42-9a6c-e91c06ea1cf8" />

<img width="356" height="119" alt="image" src="https://github.com/user-attachments/assets/5b8d2c56-9bdc-43a8-8f95-151d140abdea" />


## Result:
Thus, Gibb's Sampling( Approximate Inference method) is succuessfully implemented using python.
