# Gulf of Alaska (stratification, mixing, and circulation)

In this model experiment, I will investigate how season changes in fresh water discharge affect stratification, mixing, and circulation in the gulf of Alaska. The primary focus is to examine the variations in freshwater volume and how it influences halocline and the interaction between fresh water and sea water. To explore this question, I will construct a model that spans the gulf of Alaska, and simulate the dynamics of the gulf, capturing seasonal shifts in salinity, temperature, and density at different depths. I anticipate that the summer season will strengthen stratification in the gulf of Alaska.  For the initial conditions, I will probably use a 2008 ECCO version 5 model. I will then use a time series analysis to analyze the results, and then create a visualization with a movie about the salinity, density, or temperature changes.

## Reproducing Model Results

*Note for CS185C: The following section outlines possible steps that may be included in your README for reproducibility. When designing your own steps, be sure to consider which of the steps below pertain to your model and update/modify accordingly.*

The following steps outline how to construct the model files, configure and run the model, and assess the model results.

### Step 1: Create the Model Files
Several input files need to be created to run the model. Generate the following list of files using the notebooks indicated in paratheses:
- Model Grid (notebooks/Creating the Model Grid.ipynb)
- Bathymetry (notebooks/Creating the Bathymetry.ipynb)
- Initial Conditions (notebooks/Creating the Initial Conditions.ipynb)
- External Forcing Conditions (notebooks/Creating the External Forcing Conditions.ipynb)
- Boundary Conditions (notebooks/Creating the Boundary Conditions.ipynb)
The model files should be placed into the  `input` directory.

### Step 2: Add files to the computing cluster
Once the input files have been created, the model files can be transferred to the computing cluster. Begin by cloning a copy of [MITgcm](https://github.com/MITgcm/MITgcm) into your scratch directory and make a folder for the configuration, .e.g.
```
mkdir MITgcm/configurations/ca_upwelling
```
Then, use the `scp` command to send the `code`, `input`, and `namelist` directories to your configuration directory. 

### Step 3: Compile the model
Once all of the files are on the computing cluster, the model can be compiled. Make a `build` directory in the configuration directory and run the following lines:
```
export MPI_HOME=/home/cs185c18/.conda/envs/cs185c
../../../tools/genmake2 -of ../../../tools/build_options/darwin_amd64_gfortran -mods ../code -mpi
make depend
make
```

### Step 4.1: Run the model with wind
After the compilation is complete, run the model with the wind. Move to the run directory, link everything from `input` and `code`, and the submit the job script:
```
sbatch cs185c18.slm
```

### Step 5: Analyze the Results
There are two notebooks provided for analysis:
1. Analyzing Model Results

   This notebook is provided to have a quick look at spatial and temporal variations in the temperature field in the model with wind. It also generates the visualization provided in the figures directory.
   
2. Answering the Science Question
   
   This notebooks provided some analysis plot to address the science question posed above.
