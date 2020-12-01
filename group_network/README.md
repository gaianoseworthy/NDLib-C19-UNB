# Group Network

myGroupNetwork.py is a module to construct networks.

myGroupModel.py is a module to simulate epidemic model.

These two modules were built on top of the library
[NetWorkX](https://networkx.org/).

This modules provide some features
that are not available in Network Diffusion Library
[NDLib](https://ndlib.readthedocs.io/).
The new features are:

- Age structure and group labels.
- Adding nodes and edges during between iterations, which is capable of simulating effects of importation and gathering under endemic.
- Breadth First Search (BFS). Instead of visiting all nodes in each iteration,
only infected and vulnerable nodes are visited.

## Requirement

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install NetWorkX.

```bash
pip install networkx
```

## Usage

The demo file *GroupNetwork_Run.ipynb*
was written in Jupyter Notebook,
which can be run in
[Anaconda](https://www.anaconda.com/products/individual).


To build network (see GroupNetwork_Run.ipynb for more details):

```python
import myGroupNetwork

# Set parameters
N = 2000 # Total Population
youngPercent = 0.15 # Percentage of each age group
adultPercent = 0.65
oldPercent = 1 - youngPercent - adultPercent # = 0.20

# Build base age-structured network
nYoung = int(youngPercent * N)
nMiddle = int(adultPercent * N)
nSenior = N - nYoung - nMiddle
data = myGroupNetwork.buildGroups(size={'Young': nYoung, 'Middle': nMiddle, 'Senior': nSenior})

# Add groups
data.addGroup(groupType='CareHome', n=60, size={'Middle':20, 'Senior': 30}, contactPercentage=.7)

# Save group data
data.save( filename='network_data.json' )

# Load data and build network
filename = 'network_data.json'
model = myGroupModel.buildNetwork( filename )
```

Sample output:

![Large Gathering](output/fig_large_gathering.png)

## Contributing
UNB and GNB