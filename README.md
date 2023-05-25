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
  * `2023-05-08-predictive-model` (analysis of gene expression data to create predictive model)
  * `2023-05-16-imrad` (IMRaD report describing developed predictive model)
* exports (files sent to Karl, excluding pdfs of compiled Quarto documents in the above folder)
  * `2023-03-03-gene-expression-data.pptx` (PowerPoint of summary tables and figures from gene expression EDA)
* figs (produced figures)
   * data cleaning
       * `101-boxplot.png` (Box plot of gene expression in 101 Type cells separated by treatment type)
       * `101-linegraph.png` (Scatter plot with linear line of best fit of gene expression vs concentration of treatment in 101 Type cells separated by treatment type)
       * `a42-boxplot.png` (Box plot of gene expression using Activating Factor 42 separated by cell type)
       * `placebo-boxplot.png`(Box plot of gene expression using placebo treatment separated by cell type)
       * `wt-boxplot.png` (Box plot of gene expression in Wild Type cells separated by treatment type)
       * `wt-linegraph.png` (Scatter plot with linear line of best fit of gene expression vs concentration of treatment in Wild Type cells separated by treatment type)
   * plot adjustment
       * `ge_tnr.zip` (Compressed version of `.tiff` replicating the figure sent by Karl on 4/3/2023)
   * predictive model analysis and IMRaD       
* raw-data (data files given by Karl)
   * `WTF-IISFD data.xlsx` (Excel spreadsheet of gene expression experiment data)
* resources (reference files given by Karl)
   * `gene_plot.pdf` (Reference figure to match for plot adjustment on 3/4/2023)
* tabs (produced tables)
    * data cleaning
       * `101-summary.html` (Summary statistics for 101 Type cells)
       * `wt-summary.html` (Summary statistics for Wild Type cells)

## Tasks Performed (`YYYY-MM-DD-key-descriptor`)
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
We saved this as a `.csv` file (`clean-gene-WTF-IISfD-data.csv`). We also 

### Plot Adjustment (`2023-04-03-plot-adjustment`)
We adjusted the gene comparison plot sent by Karl on 3/4 to use Times New Roman 
font and formatted it as a `.tiff` file.

### Sample Size Calculation (`2023-05-01-sample-size-calculation`)
We calculated a sample size for Karl's experiment grant based on $R^2$, power, and
significance level desired.

### Predictive Model (`2023-05-08-predictive-model` and `2023-05-16-imrad`)
We created a predictive mixed-effects model for gene expression using the cleaned 
data and wrote an accompanying report.
