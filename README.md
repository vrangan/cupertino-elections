# Cupertino Election 2022 Analysis

This repo has a workbook (can be used with Google docs or Excel) and a IPYthon notebook that can be used with jupyter lab.  This is to process the election results update for the *City of Cupertino* from the ROV office (registrar of voters) in *Santa Clara County*.

## Jupyter lab notebook

The notebook uses a Python 3 Kernel.

The notebook uses a few Python packages.
- Pandas
- NumPy
- SciKit Learn
- Matplotlib
- OpenPyXL

There are a few distributions that have these packages pre installed (for example Anaconda).  If you don't have these packages installed, please install them before running the notebook

###  Preparation to run the notebook

The notebook depends on a directory where the ROV updates are placed.  The ROV updates come in four formats.
- Summary CSV Text
- Detailed Excel workbook
- Detailed XML document
- Detailed Text document (with multiple sections for each contest which can be processed as a CSV file)

There are some variations between the various formats.   For example, the overvotes and undervotes information is in the summary text and at precinct level in the XML document but missing from the Excel and  detailed text documents.

**The Excel workbook published by the ROV is not readable out of the box by openpyxl or xlrd.  The solution is to read the Excel file in Excel and write it to as an Excel default format (xlsx).**

### Running the notebook

The notebook has the data_dir specified in the second cell.  Update the directory to the location you have placed the excel workbooks (that have been read and written using Excel to be in xlsx format).  The file name must have *11dd22*.xlsx in them 

That is the only thing needed to be done.   As and when new updates are provided by the ROV, you can run the notebook to get a quick update on the progress as well as potential predictions at various turnouts.

### Operation of the notebook

The basic operation of the python notebook is rather simple.  Given the data directory where the ROV incremental update files are kept, the files are scanned and the second sheet is read to identify the number of counted ballots in the file.
The counted ballots are used to sort the files by order of updates as the file modification time was not reliable (when converting the xls to xlsx, there were times older updates were converted later)
With the files in order, the Cupertino specific sheet from the excel workbook are read and the data range is processed and read into a data frame
The count of votes for each candidate is maintained in a list (which can be used to do the prediction and can be converted to a NP array or a pandas Series)
With the count of votes per update for each candidate known and the number of ballots processed for that update, we can create a pandas dataframe with these candidate vote information columns and the turnout as the index.
From this point onwards it is easy to plot the dataframe contents or use Scikit Learn to do a simple Linear Regression for future potential turnouts and the expected values and the dataframe is plotted.

## Using Excel (or Google Sheets to predict)
Prediction using Excel itself - The excel notebook has  the data from Cupertino sheets organized by date.  The data also has analysis sheets:  with precinct names, precinct level turnout and vote differential and vote prediction using current distribution of votes per candidate.   It also has a linear forecast using Excel functions with trendlines automatically added and also many statistical quantities.  This workbook can be uploaded to Onedrive for Excel Web or google docs and used as Google sheets
