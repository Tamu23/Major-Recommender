Introduction

Cal Poly Humboldt’s admissions department is seeking an interactive and innovative tool that can recommend a suitable major to incoming students. Such a tool could potentially improve admission rates to the college, reduce drop-out rates, minimize switching of majors, and improve overall satisfaction with higher education. 
My focus in building such a tool is to provide a slightly longer-term satisfaction. For this project I aim to design a major recommender that helps narrow down the best match based on career objectives. Specifically, based on the job roles associated with a major, as well as companies, agencies, or institutions associated with it. This way, the tool helps elucidate the user’s preferred career path. Additionally, it can encourage them to continue on their suggested academic journey, by enlightening them of the career waiting for them after graduating. 
Methodology

Beginning with Professor Overholser’s code as reference, many changes were made in various stages of the machine learning tool. A comprehensive list, with a brief explanation, of the stages and the changes is as follows:
1.	Data collection: For a list of occupational roles and companies to work for, I downloaded all the pdf files available on the Career Exploration webpage. This was done using the Python packages selenium and BeautifulSoup. Extensive aid was provided by ChatGPT. The code is linked here. 
2.	Data processing: Text was extracted from these pdfs and cleaned for further use. The text in the pdfs was unfortunately not in an easily extractable format, therefore plenty of formatting code was needed over and above the basic extraction performed using the PyMuPDF package. A brief description of the cleaning performed is listed below:

      a.	Removing non-ASCII characters (square-shaped characters)
  
      b.	Splitting illegitimate CamelCase words that were a result of improper pdf formatting, for e.g. splitting “Policy AnalystData Specialist” to separate lines: “Policy Analyst” and “Data Specialist”
  
      c.	The splitting mentioned above had to be done carefully in order to avoid acronyms from splitting, as well as splitting two or more acronyms if they are found to have whitespaces absent between them
  
      d.	Long lines with multiple sentences were split into separate lines with a sentence each. This was done for clarity needed when reviewing the text files for errors
  
      e.	Exceptions also had to be incorporated for legitimate CamelCase words such as “BioTech” or “AmeriCorps”
  
      f.	Excess white-spaces were removed, and blank lines were eliminated
  
      g.	Known phrases with irrelevant text were removed from the dataset. For e.g. lines containing the phrase “Career Guide:” were removed, since they are present in all pdf files, and do not contribute to the clustering objective. 
It was found that the pdf for Journalism was outdated and did not have the information needed. So, this file is removed and the program does not appear in the results. Extensive aid was provided by ChatGPT. The code is linked here. 
4.	Data Analysis: Finally, the files are matched against each other for similarity in lines – if the text in a line from file A matches (or is a subset of) a line from file B, it is counted as a match. The higher the number of line-matches between two files, the higher the similarity. This measure is used to create a distance (or dissimilarity) matrix, which when fed to the linkage function from the scipy package, creates a dendrogram. Extensive aid was provided by ChatGPT. The code is linked here. 
5.	Interaction: This step has not been completed, but here I describe how I would develop it. I would begin by adding a second layer of linkage between the majors and their descriptions, which would help an unknowledgeable user to interact with the tool. An interactive questionnaire can be used, where the user chooses k of n words they relate with, and as a feedback mechanism, they could be shown some of the job roles and/or companies they could work for. If they like the examples from the feedback, the questionnaire would adapt to narrow user choices further, if not then we would try choices from an alternative cluster. 
