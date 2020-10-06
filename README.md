# UKBB- Aims and context.
This project explores one methodology to identify risk factors in the UK BioBank.
The case of BMI (Body Mass Index) was used for illustrative purposes. Indeed, the prevalence of obesity is steadily raising, expected to reach over a billion in 2030. This public health concern will increase the burden on healthcare as obesity is positvely correlated with type 2 diabetes, cardiovascular disease, breathing problem and certain types of cancer.
It is now accepted that obesity is a complex problem resulting from many possible interaction, ranging from genetic, metabolic,environmental, behavioral, to  socio-cultural factors. Explaining BMI variability would help disentangle this multifacetted condition thus helping health experts and policy makers intervene.


## Introducing the UK BioBank- Processing the dataset.
Causal inference is out of reach in this context. The best we can do is identify possible risk factors to help inform the design of later randomised controlled trials.
The UK BioBank collected various genetic and environmental information from ~ 500,000 volunteers. For technical reasons (lack of RAM to process the ~30GB dataset), we restricted our analysis to a subset of 217 possible predictors from the UK BioBank. This dataset was further split into two: one to conduct model selection (to identify the variables- 70% of the original datset) and a held-out set (Inference set to quantify the magnitude of the effects- the remaining 30%)

## Statistics- Assumptions and workflow.
We assumed a multiple linear regression model with Gaussian noise with no interactions: <a href="https://www.codecogs.com/eqnedit.php?latex=Y|X=\mathcal{N}(X\beta,\sigma^{2}I)" target="_blank"><img src="https://latex.codecogs.com/svg.latex?Y|X=\mathcal{N}(X\beta,\sigma^{2}I)" title="Y|X=\mathcal{N}(X\beta,\sigma^{2}I)" /></a>
The interpretation of <a href="https://www.codecogs.com/eqnedit.php?latex=\beta_{i}" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\beta_{i}" title="\beta_{i}" /></a> will then be the rate at which <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbb{E}[Y]" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\mathbb{E}[Y]" title="\mathbb{E}[Y]" /></a> changes as <a href="https://www.codecogs.com/eqnedit.php?latex=X_{i}" target="_blank"><img src="https://latex.codecogs.com/svg.latex?X_{i}" title="X_{i}" /></a> and only <a href="https://www.codecogs.com/eqnedit.php?latex=X_{i}" target="_blank"><img src="https://latex.codecogs.com/svg.latex?X_{i}" title="X_{i}" /></a> changes.
Model selection was performed using LASSO, also stabilising the estimates through the L1 penalty.
Inference was then conducted by simple multiple linear regression on the sparse subset of predictors identified by the lasso.
To account for model selection randomness, we repeated the proceudres 100 times by bootstrapping the model selection dataset

## Key results
