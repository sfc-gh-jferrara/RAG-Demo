RAG Demo Readme


Prerequisites:
1. Ensure Snowflake notebooks and Vector Data Types/Functions previews are enabled in your demo account (Vectors should be in PuPr in May, unsure on notebooks)
2. Run through setup.sql to create all of the objects needed for the demo
3. I would recommend uploading the PDF’s with our File Loading UI (IMO it’s the easiest), but you can always do this via SQL as well
4. Make sure to create the notebook within the newly created Database RAW and Schema PDF, otherwise you will run into permission errors during the demo
5. Also ensure whichever role you will be using for the demo has access to all Cortex functions (some of them are used in the demo), otherwise you will also run into permission errors. Example: I used SYSADMIN so I had to run “GRANT IMPORTED PRIVILEGES ON DATABASE SNOWFLAKE TO ROLE SYSADMIN;”


Demo Flow:
1. Create and register python UDF to parse raw text from PDF (using scoped file URL’s). This will be stored in a Snowflake table
2. Using the cortex ‘COMPLETE’ function, you will receive an error exceeding the token limit. Explain how using the python package langchain and Snowflake’s vector data type, we can split these large blobs of text into chunks to be analyzed. We will register this as a UDTF and the results will be stored in a table. We can then use the cortex ‘EMBED_TEXT’ function to analyze the chunks via SQL
3. Perhaps the customer comes back and says: “I don’t have a very technical team, is there a way to get my team hands-on access to these insights without them writing any code?” Enter Streamlit where you will build an application that allows a question to be asked by a user and it will scan the document to retrieve an answer all in a few lines of code
4. BONUS: Go into the FOLDER stage and remove the Tesla Manual Guide, then go back and ask the Streamlit app the sample question on the Tesla. It will communicate back that it doesn’t have the data available in Snowflake to answer your question. Then you can manually upload the PDF, run the last cell in the notebook to chunk the text from the owners manual, and rerun this question through our Streamlit app. BOOM
