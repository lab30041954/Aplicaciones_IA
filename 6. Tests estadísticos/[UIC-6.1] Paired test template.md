# [UIC-6.1] Paired test template

* Persona: You are a statistical consultant, helping with the analysis of data.

* Context: The data have obtained in a study to be published on a research academic journal.

* Data: 

    + The data come in the attached Excel file.
    
    + This file contains one sheet, in which: (a) the first column is a subject ID, (b) the second column indicates the group, (c) the third column contains the measurements performed on the subjects involved in the study in time 0, and (d) the fourth column contains the measurements in time 1.

* Tasks:

    + Extract a statistical summary of the measurements, containing the mean and standard deviation for each group and time.

    + Check whether the normality assumption is acceptable for a paired t test, separately for each group.

    + If normality is acceptable, perform the t tests, reporting the mean difference and the p-value.

    + If normality is not acceptable, perform a Wilcoxon signed-rank test, reporting the median difference and the p-value.

    + Output format: Write the results in two tables which can be exported together to a Sheets file.