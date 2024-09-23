# QA-Chatbot
Interactive chatbot where upload any pdf file and ask queries

Reference SS_RAG_1.ipynb(for list type document_segments)
			       SS_RAG_3.ipynb(for pdf file)
          
Step-by-step approach:
1.	Data Ingestion and Preprocessing:
o	Load the dataset or documents.
o	Generate embeddings for the documents using a pre-trained model like Huggigface sentence-transformers/all-MiniLM-L6-v2 transformer models.

3.	Vector Database (Pinecone DB) Setup:
o	Initialize and configure Pinecone, which will store and index the document embeddings.
o	Insert the document embeddings into the Pinecone index for efficient retrieval.

5.	Query Processing:
o	When a user query comes in, encode it into an embedding using the same pre-trained model.
o	Use Pinecone to retrieve the most relevant documents by finding the closest embeddings to the query.

7.	Answer Generation:
o	Use a generative model like Cohere API to generate coherent answers based on the retrieved documents.

9.	Test the Model:
o	We will test the model by running several queries to see how well it retrieves relevant documents and generates coherent

This RAG-based model uses a vector database (Pinecone) for efficient retrieval of document embeddings and a generative model (Cohere) to generate coherent answers. It's capable of handling questions about business documents efficiently.




Reference SS_RAG_2.ipynb (Using streamlit for interaction)

1.	Frontend (Streamlit) Setup:
o	Users will upload a PDF document.
o	Users will input queries in a text box.
o	The interface will display the query, retrieved document segments, and the generated answer.

3.	Backend Integration:
o	Convert the PDF into text.
o	Generate embeddings for the text and store them in Pinecone.
o	Use the query input from the user to retrieve the most relevant document segments.
o	Generate the answer using a generative model like Cohere.

5.	Real-time Interaction:
o	Users can make multiple queries.
o	Display the relevant document segments alongside the generated answer.

Requirements:
o	Streamlit for building the frontend interface.
o	PyPDF2 to extract text from PDF files.
o	Pinecone, Cohere, Hugginface for embeddings and text generation.

Explanation of Key Components:
•	PDF Upload and Text Extraction:
o	Users upload a PDF file using Streamlit. We use PyPDF2 to extract the text from the uploaded PDF.
o	The extracted text is split into segments, e.g., by sentences (document_segments = document_text.split(". ")).

•	Embeddings Generation and Pinecone Upsert:
o	For each document segment, we generate an embedding using a pre-trained model (such as MiniLM from Hugging Face) and store the embeddings in Pinecone.
o	The embeddings are inserted into Pinecone for efficient similarity search.

•	Real-time Query Processing:
o	When the user enters a query, the query is encoded into an embedding.
o	The query embedding is passed to Pinecone, which retrieves the most relevant document segments.
o	These segments are then displayed to the user.

•	Answer Generation:
o	The query and relevant document segments are passed as input to Cohere or any other generative model to generate a coherent answer.
o	The answer is displayed in real time.

This will launch the application in your web browser. Users will be able to upload PDF files and ask questions, receiving answers based on the content of the uploaded document.

Challenges faced :
•	Understand Pinecone Api, index – creation, initialization, deletion , vectors(query), matches(relevant documents), metadata
•	Understand Huggingface pretrained sentence transformer used for tokenizer and embeddings
•	Understand cohere API for generating Answer of query

1.	Huggingface transformer(sentence-transformers/all-MiniLM-L6-v2)used is having dimensions – 384 and metric – cosine for queries and text generation. So pinecone index should match this
2.	Also cohere command-lightly model is used for text generation
3.	For relevant documents, tried to use pinecone metadata text but was not able to use so used from document - matching segments id with results matches id


