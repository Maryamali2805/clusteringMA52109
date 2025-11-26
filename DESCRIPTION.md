cluster_maker Package 

The cluster_maker package provides a small, self-contained framework for generating synthetic cluster centres, simulating clustered datasets, performing clustering, evaluating cluster quality, and producing plots.
It is structured as a standard Python package and is used by both the demo scripts and the tests provided in the project.

1. dataframe_builder.py

This module defines the structure of the “seed” DataFrame that stores cluster centres.
It contains:

define_dataframe_structure()

Takes a list of column specifications.

Builds a DataFrame where each row is a cluster and each column a feature.

Ensures:

all reps lists have the same length,

all required keys are present,

output has shape (n_clusters, n_features).

simulate_data()

Generates synthetic data by sampling Gaussian noise around the cluster centres.

Ensures reproducibility through a random seed.

Returns a DataFrame containing all feature columns plus a true_cluster label.

2. preprocessing.py

Contains utility functions for preparing input data:

select_features()

Extracts required columns from an input DataFrame.

Raises errors if the columns are missing.

standardise_features()

Applies standardisation (zero mean, unit variance).

Used before running clustering algorithms.

3. algorithms.py

Implements the clustering algorithms used by the package.

kmeans()

Pure NumPy implementation of K-means.

Includes:

centroid initialisation,

assignment step,

update step,

stopping criterion.

sklearn_kmeans()

Wrapper around sklearn.cluster.KMeans.

4. evaluation.py

Provides metrics and diagnostic tools:

compute_inertia()

SSE for evaluating cluster compactness.

elbow_curve()

Computes inertia for a sequence of k values.

silhouette_score_sklearn()

Uses scikit-learn’s silhouette implementation.

5. plotting_clustered.py

Functions to produce visual output:

plot_clusters_2d()

2D scatter plot of points coloured by cluster.

plot_elbow()

Elbow plot using inertia values.

6. interface.py

This is the high-level orchestrator.

run_clustering()

Coordinates the full workflow:

Read CSV input

Select and optionally standardise features

Run K-means

Compute metrics

Generate plots

Optionally export labelled data

Returns a dictionary containing data, labels, metrics, and figures.

7. demo scripts

The demo script demonstrates how to use the high-level interface:

demo_cluster_analysis.py

Reads a CSV file from the command line.

Automatically selects numeric columns.

Runs clustering through run_clustering().

Saves:

labelled data

cluster plot

elbow plot