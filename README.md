# Kollaboration with Karl

If opening in RStudio, please open the included project `collaboration-project.Rproj`.

## Folder Structure
* data - modified data files
* documents - Quarto files and their corresponding pdfs detailing specific processes
* exports - files (usually in Microsoft Office suite format) sent to Karl
* figs - produced figures
* raw-data - data files given by Karl
* tabs - produced tables

## Data (`data`)
### Modified gene expression data (`modified-WTF-IISfD-data.xlsx`)
Karl sent a spreadsheet of lab data measuring relationship between
concentration of either a saline (placebo) solution or Activating Factor 42 on gene expression in both Wild-Type and 101-Type cells. This is the version imported into R that was cleaned in Excel via the following corrections:

* Deleted the figures on pages `GL-CsE` and `GL-bNo`
* Removed the summary statistics on page `GL-CsE`
* Shifted data cells to top-left corner to avoid blank rows when reading into R
* Made cell line and treatment type names consistent
* Removed cell line and treatment type names from spreadsheet and copied separately. 

### Cleaned gene expression data (`clean-gene-WTF-IISfD-data.csv`)
Cleaned version of the modified gene expression data, including labels for cell lines. This version
can be imported into R for plotting and further analysis. We obtained this by importing 
`modified-WTF-IISfD-data.xlsx` into R using `readxl` (see `2023-03-03-data-cleaning.qmd` for more 
details), and performing the following procedures:

* Obtained names of Excel sheets to label each of the eight experiment tibbles
* Imputed a missing value of gene expression (indicated by a -99) in the fUg gene line with the mean gene expression of that experiment

### Melted gene expression data (`melted-gene-WTF-IISfD-data.csv`)
Melted version of the above into a single tibble.

## Documents (`documents`)
### Data cleaning on 3/3/2023 (`2023-03-03-data-cleaning.qmd`)
We cleaned `modified-WTF-IISfD-data.xlsx` in Excel, 
before reading the spreadsheet into R, doing more
cleaning, and summarised the necessary results into tables and figures
for Karl to use in his presentation on 24/3.

### Plot adjustment on 3/4/2023 (`2023-04-03-plot-adjustment.qmd`)
We adjusted the gene comparison plot sent by Karl on 3/4 to use Times New Roman 
font and formatted it as a `.tiff` file.

### Sample size calculation on 1/5/2023 (`2023-05-01-sample-size-calculation.qmd`)
We calculated a sample size for Karl's experiment grant based on $R^2$, power, and
significance level desired.

### Analysis report on 8/5/2023 (`2023-05-08-gene-expression-report.qmd`)
We wrote a report describing a mixed effects model for gene expression based on the 
previous analyses performed.

### Mixed Effects report on 16/5/2023 (`2023-05-08-mixed-effects.qmd`)
We created a predictive mixed-effects model for gene expression using the cleaned 
data.

## Exports (`exports`)
### Gene expression presentation (`gene_expression_data.pptx`)
Powerpoint presentation of summary tables and figures for gene expression data sent
to Karl on 24/3.

## Figures (`figures`)
### Data cleaning on 3/3/2023 (`2023-03-03-data-cleaning`)
* `101-boxplot.png` - Boxplot of treatment vs placebo in 101-Type cells
* `101-linegraph.png` - Line graph of effect of treatment concentration on gene
    expression in 101-type cells
* `a42-boxplot` - Boxplot of effect of Activating Factor 42 on cells
* `placebo-boxplot.png` - Boxplot of effect of placebo treatment on cells
* `wt-boxplot.png` - Boxplot of effect of treatment vs placebo in Wild-Type cells
* `wt-linegraph.png` - Line graph of effect of treatment concentration on gene
    expression in Wild-type cells
    
### Plot adjustment on 3/4/2023 (`2023-04-03-plot-adjustment`)
* `ge_tnr.tiff` - Figure of gene comparison plot for cell types using different treatments
with Times New Roman font, in `.tiff` format. (not included due to large file size)

## Raw Data (`raw-data`)
### Raw gene expression data (`modified-WTF-IISfD-data.xlsx`)
Karl sent a spreadsheet of lab data measuring relationship between
concentration of either a saline (placebo) solution or Activating Factor 42 on gene expression in both Wild-Type and 101-Type cells.

## Resources (`resources`)
* `gene_plot.pdf` - Reference figure to match for plot adjustment on 3/4.

## Tables (`tabs`)
### Data cleaning on 3/3/2023 (`2023-03-03-data-cleaning`)
* `101-summary.png` - Summary statistics for 101-Type cells
* `wt-summary.png` - Summary statistics for Wild-Type cells
