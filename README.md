# Network Calculus with Flow Prolongation - A Feedforward FIFO Analysis enabled by ML

This repository contains the dataset used for the paper [_"Network Calculus with Flow Prolongation - A Feedforward FIFO Analysis enabled by ML"_](https://doi.org/10.1109/TC.2022.3204225) published in IEEE Transactions on Computers. We refer to the article for a full explanation of the methodology used for generating the dataset.

This is an extension of the DeepFP method initially presented in [_"Tightening Network Calculus Delay Bounds by Predicting Flow Prolongations in the FIFO Analysis"_](https://doi.org/10.1109/RTAS52030.2021.00021) presented at IEEE RTAS 2021. Compared to [the dataset](https://github.com/fabgeyer/dataset-rtas2021) and method previously used, we use reinforcement learning to train the neural network used in DeepFP. Hence our training dataset does not contain information about the prolongations.

## Citation

If you use this dataset for your research, please include the following reference in any resulting publication:

```bibtex
@article{GeyerSchefflerBondorf_TC2022,
	author        = {Geyer, Fabien and Scheffler, Alexander and Bondorf, Steffen},
	journal       = {IEEE Transactions on Computers},
	title         = {Network Calculus with Flow Prolongation - A Feedforward {FIFO} Analysis enabled by {ML}},
	year          = {2022},
	doi           = {10.1109/TC.2022.3204225},
}
```

# Numerical Evaluation

## Information

The dataset contained in this repository is comprised of three files:

- `dataset-train.pbz` is the dataset used for training the graph neural network used in DeepFP,
- `dataset-evaluation-small.pbz` is the dataset with small networks (up to 40 flows and 15 servers) used for the evaluation in Section 6,
- `dataset-evaluation-large.pbz` is the dataset with large networks (more than 100 flows and up to 30 servers) used for the evaluation in Section 6.

Additionally, `dataset_structure.proto` details the datastructure used for the dataset.


## Reading the dataset

The dataset is stored as serialized protobuf messages using the [PBZ](https://github.com/fabgeyer/pbzlib-documentation) file format.
The `pbzlib` library can be used for processing this file format, available for [different programming languages](https://github.com/fabgeyer/pbzlib-documentation#official-implementations).

This repository contains an [example python script](https://github.com/fabgeyer/dataset-deepfp-extension/blob/master/example.py) for parsing the files.
To get it and execute it:
```
$ git clone https://github.com/fabgeyer/dataset-deepfp-extension.git
$ cd dataset-deepfp-extension.git
$ pip3 install -r requirements.txt
$ python3 example.py dataset-train.pbz
```

# Motivating Example

The paper contains a motivating example showing potential effectiveness on a sample network topology and one potential prolongation, depending on the  bottleneck utilization. 
The network topology is depicted in Figure 2 in the paper.
Curve shapes are given in Sec. 4-1 as $\beta_{40,T}$ and $\alpha_{r=10u,b}$ where $10u$ defines the utilization at the bottlenect of the topology $\frac{4r}{R}$.

Curve and utilization parameters as well as delay and output burstiness bounds are given in these two CSV files in folder `motivating_FP_example_data_Fig_2`:

- `fp_sensitivity_delay_bound.csv`
- `fp_sensitivity_output_burstiness_bound.csv` 

Two metrics were computed, the second of which is plotted in the paper:

1. `improvement_overall[%]` according to the Equation 20 in the paper (yet for delay and burstiness).
2. `improvement_variable_part[%]` exploits the possibility to easily remove the inital and invariant latency or burstiness of the curves. I.e., it shows the improvement in the variable part of the bounds. It is computed by removing $4T$ or $b$, respectively, from the divisor.

# License

The data in this repository is licensed under [Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](http://creativecommons.org/licenses/by-sa/4.0).
