# RAG (Retrieval-Augmented Generation) with LangChain
# ponytail: ground LLM answers in YOUR data — not the internet

## What is RAG?

RAG = Retrieve relevant documents → Feed them as context → LLM answers from that context.

Why RAG? LLMs only know what they were trained on. RAG lets them answer questions using YOUR data without retraining.

## Complete RAG Pipeline

```
Load → Split → Embed → Store → Retrieve → Augment → Generate
  |       |        |        |        |          |          |
  PDF    chunks  vectors   Vector    fetch     prompt    answer
  web    256-   384d     DB       top-k     context
  DB    1024t  1536d    FAISS     3-5      + question
                      Chroma    chunks
```

## Step-by-Step Implementation

### 1. Install Dependencies

```bash
pip install langchain langchain-openai langchain-community chromadb pypdf faiss-cpu
```

### 2. Load Documents

```python
from langchain_community.document_loaders import TextLoader, PyPDFLoader, WebBaseLoader

# From text file
loader = TextLoader("./my_doc.txt")
docs = loader.load()

# From PDF
# loader = PyPDFLoader("./report.pdf")
# docs = loader.load()

# From web page
# loader = WebBaseLoader("https://example.com/article")
# docs = loader.load()
```

### 3. Split into Chunks

```python
from langchain.text_splitter import RecursiveCharacterTextSplitter

splitter = RecursiveCharacterTextSplitter(
    chunk_size=500,       # target chunk size in chars
    chunk_overlap=50,     # overlap between chunks (preserve context across boundaries)
    separators=["\n\n", "\n", ".", " ", ""],  # try splitting at paragraphs first
)
chunks = splitter.split_documents(docs)
print(f"Split {len(docs)} doc(s) into {len(chunks)} chunks")
```

### 4. Create Embeddings & Vector Store

```python
from langchain_openai import OpenAIEmbeddings
from langchain_community.vectorstores import Chroma

embeddings = OpenAIEmbeddings(model="text-embedding-3-small")  # 1536-dim vectors
vectorstore = Chroma.from_documents(
    documents=chunks,
    embedding=embeddings,
    persist_directory="./chroma_db",  # save to disk
)
```

### 5. Set Up Retriever

```python
retriever = vectorstore.as_retriever(
    search_type="similarity",  # or "mmr"
    search_kwargs={"k": 3},    # return top-3 chunks
)
```

### 6. Create RAG Chain

```python
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_core.runnables import RunnablePassthrough

llm = ChatOpenAI(model="gpt-4o", temperature=0)

template = """You are a helpful assistant. Answer the question based ONLY on the provided context.

Context:
{context}

Question: {question}

Answer concisely and accurately. If the context doesn't contain enough information, say "I don't have enough information to answer that."
"""

prompt = ChatPromptTemplate.from_template(template)

def format_docs(docs):
    return "\n\n---\n\n".join(doc.page_content for doc in docs)

# LCEL chain
rag_chain = (
    {"context": retriever | format_docs, "question": RunnablePassthrough()}
    | prompt
    | llm
    | StrOutputParser()
)
```

### 7. Ask Questions

```python
result = rag_chain.invoke("What is LoRA and how does it work?")
print(result)
# "LoRA (Low-Rank Adaptation) is a fine-tuning technique that trains small
#  adapter matrices instead of all parameters, reducing trainable params to ~0.1%..."
```

## Complete Runnable Script

```python
"""end-to-end RAG with LangChain — run as-is"""
from langchain_community.document_loaders import TextLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain_openai import OpenAIEmbeddings, ChatOpenAI
from langchain_community.vectorstores import Chroma
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_core.runnables import RunnablePassthrough

# 1. Load
loader = TextLoader("my_doc.txt")
docs = loader.load()

# 2. Split
splitter = RecursiveCharacterTextSplitter(chunk_size=500, chunk_overlap=50)
chunks = splitter.split_documents(docs)

# 3. Embed & Store
vectorstore = Chroma.from_documents(chunks, OpenAIEmbeddings())

# 4. Retrieve
retriever = vectorstore.as_retriever(search_kwargs={"k": 3})

# 5. Generate
llm = ChatOpenAI(model="gpt-4o", temperature=0)
prompt = ChatPromptTemplate.from_template(
    "Answer using this context:\n{context}\n\nQuestion: {question}"
)

def format_docs(docs):
    return "\n\n".join(d.page_content for d in docs)

chain = (
    {"context": retriever | format_docs, "question": RunnablePassthrough()}
    | prompt | llm | StrOutputParser()
)

print(chain.invoke("What is LoRA?"))
```

## Advanced: Add Memory to RAG

```python
from langchain.chains import create_history_aware_retriever
from langchain.chains import create_retrieval_chain
from langchain.chains.combine_documents import create_stuff_documents_chain

# Wrap retriever to consider chat history
history_aware_retriever = create_history_aware_retriever(
    llm, retriever,
    prompt=ChatPromptTemplate.from_messages([
        ("system", "Given chat history and a follow-up question, rephrase it as a standalone question."),
        ("placeholder", "{chat_history}"),
        ("human", "{input}"),
    ])
)

qa_chain = create_stuff_documents_chain(llm, prompt)
conversational_rag = create_retrieval_chain(history_aware_retriever, qa_chain)

result = conversational_rag.invoke({
    "input": "What is LoRA?",
    "chat_history": [],
})
print(result["answer"])

# Follow-up — retriever automatically uses chat history context
result = conversational_rag.invoke({
    "input": "How is it different from QLoRA?",
    "chat_history": [("human", "What is LoRA?"), ("assistant", result["answer"])],
})
print(result["answer"])
```

## Key Parameters to Tune

| Parameter     | What it does                          | Typical Range  |
|---------------|---------------------------------------|----------------|
| chunk_size    | Size of each document chunk           | 256-1024 tokens|
| chunk_overlap | Overlap between chunks                | 10-20% of size |
| k             | Number of chunks to retrieve          | 3-10           |
| search_type   | "similarity" or "mmr" (diverse)       | similarity     |
| temperature   | LLM creativity                        | 0 (factual)    |
| model         | LLM to use                            | gpt-4o, claude |
