# Kollaboration with Karl

If opening in RStudio, please use the included project `collaboration-project.Rproj`.

## Folder Structure
* data (modified data files)
   * `clean-gene-WTF-IISfD-data.csv` (list of cleaned tibbles for the eight gene experiments)
   * `melted-gene-WTF-IISfD-data.csv` (melted tibble with all gene experiments for plotting)
   * `modified-WTF-IISfD-data.xlsx` (modified version of raw spreadsheet imported into R to create the above two `.csv` files)
* documents (Quarto files detailing specific processes, contained in folders for neater compilation)
  * `2023-03-03-data-cleaning` (data cleaning and EDA of gene expression experiments)
  * `2023-04-03-plot-adjustment` (replication of plot desired by Karl)
  * `2023-05-01-sample-size-calculation` (calculation of necessary sample size for desired power in experiment)
  * `2023-05-08-modelling` (analysis of gene expression data to create predictive model)
  * `2023-05-16-imrad` (IMRaD report describing developed predictive model, includes `references.bib`)
* exports (files sent to Karl, excluding pdfs of compiled Quarto documents in the above folder)
  * `2023-03-03-gene-expression-data.pptx` (PowerPoint of summary tables and figures from gene expression EDA)
* figs (produced figures)
   * data cleaning
       * `101-boxplot.png` (box plot of gene expression in 101 Type cells separated by treatment type)
       * `101-linegraph.png` (scatter plot with linear line of best fit of gene expression vs concentration of treatment in 101 Type cells separated by treatment type)
       * `a42-boxplot.png` (box plot of gene expression using Activating Factor 42 separated by cell type)
       * `placebo-boxplot.png`(box plot of gene expression using placebo treatment separated by cell type)
       * `wt-boxplot.png` (box plot of gene expression in Wild Type cells separated by treatment type)
       * `wt-linegraph.png` (scatter plot with linear line of best fit of gene expression vs concentration of treatment in Wild Type cells separated by treatment type)
   * plot adjustment
       * `ge_tnr.zip` (compressed version of `.tiff` replicating the figure sent by Karl on 4/3/2023)
   * modelling     
       * `m5-assumptions.png` (residuals vs fitted plot for chosen model)
       * `model-eda.png` (scatter plot of gene expression vs concentration, coloured by treatment, 
       and separated by cell type)
       * `model-plot.png` (line of best fit from mixed effects model on data, similar to above)
* raw-data (data files given by Karl)
   * `WTF-IISFD data.xlsx` (Excel spreadsheet of gene expression experiment data)
* resources (reference files given by Karl)
   * `gene_plot.png` (reference figure to match for plot adjustment on 3/4/2023)
* tabs (produced tables)
    * data cleaning
       * `101-summary.png` (summary statistics for 101 Type cells)
       * `wt-summary.png` (summary statistics for Wild Type cells)
    * modelling
       * `m5-anova.png` (ANOVA table for fixed effects in final model)
       * `m5-fixef.png` (coefficients of fixed effects in final model)
       * `m5-ranef.png` (coefficients of random effects in final model)
       * `m5-ranova.png` (ANOVA table for random effect in final model)
       * `model-metrics.png` (AIC, $R^2$, and RMSE for the second and fifth [final] models)

## Tasks Performed (`YYYY-MM-DD-description`)
### Data Cleaning (`2023-03-03-gene-expression`)
Karl sent a spreadsheet (`WTF-IISFD data.xlsx`) of lab data measuring relationship between
concentration of either a saline (placebo) solution or Activating Factor 42 on gene expression in both Wild-Type and 101-Type cells. Before importing this data into R, we performed the following corrections in Excel:
* Deleted the figures on pages `GL-CsE` and `GL-bNo`
* Removed the summary statistics on page `GL-CsE`
* Shifted data cells to top-left corner to avoid blank rows when reading into R
* Made cell line and treatment type names consistent
* Removed cell line and treatment type names from spreadsheet and copied separately. 

This version was saved as `modified-WTF-IISfD-data.xlsx`. We used `readxl` to import the spreadsheet into R, and performing the following procedures:
* Obtained names of Excel sheets to label each of the eight experiment tibbles
* Imputed a missing value of gene expression (indicated by a -99) in the fUg gene line with the mean gene expression of that experiment 

We saved this as a `.csv` file (`clean-gene-WTF-IISfD-data.csv`). We also created a 
`.csv` file of a melted tibble (`modified-gene-WTF-IISfD-data.csv`), using concentration as an ID column 
since this is consistent across all experiments. The label of each sheet was separated 
into its components of gene line, cell type, treatment type, and trial number using `str_split`.

From there, we created four smaller tibbles that summarised the mean and standard deviation of 
gene expression in cell type groups and treatment groups, using a function to more efficiently 
filter the larger tibble by these factors and generate the summary statistics.

Using `gt`, we created a summary table for each cell type, and saved these as `.png` files 
for use in Karl's PowerPoint (`101-summary.png` and `wt-summary.png`). 

We also created two 
line graphs (`101-linegraph.png` and `wt-linegraph.png`) that show a linear line of best 
fit on the gene expression vs concentration data, colour-coded by treatment type. 

Finally, we created four box plots showing the spread of gene expression within cell type 
groups, and within treatment groups (`wt-boxplot.png`, `101-boxplot.png`, `placebo-boxplot.png`, 
and `a42-boxplot.png`).

These two tables and six figures were added to a PowerPoint (`2023-03-03-gene-expression-data.pptx`) 
for Karl to use in his presentation.

### Plot Adjustment (`2023-04-03-plot-adjustment`)
On 3/4/2023, Karl emailed a reference plot (see  `gene_plot.png`), requesting that it be replicated 
with Times New Roman font and saved as a `.tiff` file.

To do this, we read in the melted gene expression data and created two plots for each cell type 
of gene expressionvs concentration for Wild Type cells, coloured by treatment. Each plot used two 
specific colours from the Ravenclaw palette of the `harrypotter` package. We also added labels 
for the gene lines to the end data points of each experiment, horizontally. Axis labels were also 
created using the `latex2exp` package for typesetting LaTeX. Furthermore, we used the black and 
white `ggplot` theme to match the given picture. Using the `extrafont` package, we also set the 
font family to "Times".

Once each individual graph was created, we used `patchwork` to merge them by their identical 
legends, and add letter labels.

We then exported the figure as a `.tiff` file of size 9 in x 6 in with a resolution of 500, which is included in compressed form in the repository.

### Sample Size Calculation (`2023-05-01-sample-size-calculation`)
We calculated a sample size for Karl's experiment grant based on $R^2$, power, and
significance level desired. We did this using the `pwr` package, and by defining the 
effect size $\mathcal{f}^2$ in terms of $R^2$, such that we could solve for the numerator degrees 
of freedom $n-k-1$ of the F-statistic, and subsequently obtain $n$.

### Predictive Model (`2023-05-08-predictive-model` and `2023-05-16-imrad`)
We created a predictive mixed-effects model for gene expression using the cleaned 
data and wrote an accompanying report. Initially, we plotted gene expression vs 
concentration for all gene lines, colouring by treatment, and separating by cell 
type (`model-eda.png`).

We determined that gene line is potentially a 
random effect, since it cannot be effectively replicated and considered as a predictor. 
We then examined five models using the remaining three predictors: concentration of treatment 
(mg/mL), treatment, and cell type as fixed effects:

1. No interaction
2. Concentration of Treatment x Treatment Type
3. Treatment Type x Cell Type
4. Concentration of Treatment x Cell Type
5. Concentration of Treatment x Treatment Type x Cell Type

For each model, we fit a model using `lmer`, checked the significance of the random and 
fixed effects using `ranova` and `anova`, respectively, and plotted the residuals vs 
fitted plot to check for homoscedasticity. The significance tables for the chosen model 
are saved as `m5-ranova.png` and `m5-anova.png` for the random and fixed effects, 
respectively. The assumption plot is saved as `m5-assumptions.png`.

Since the second and fifth models were the only ones to satisfy the homoscedasticity 
assumption, we further compared them by calculating their AIC values, $R^2$ values, 
and RMSE values using the `performance` package. The fifth model had a significantly 
lower AIC, so it was our chosen model. This output table is saved as `model-metrics.png`.

We plotted the line of best fit model on a graph similar to the EDA plot, by separated 
by replication number, with shape as a key for cell type (`model-plot.png`). We also obtained 
the coefficient tables for the random and fixed effects, saved as `m5-ranef.png` and 
`m5-fixef.png`, respectively. To avoid TeX compilation errors, for any values pertaining to the
intercept, we renamed the standard `(Intercept)` label to `Intercept`.

### IMRaD (`2023-05-16-imrad`)
We summarised the above analysis in an IMRaD report.