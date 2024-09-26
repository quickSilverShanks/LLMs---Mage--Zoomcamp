# Data Preparation in RAG

> This repository is a part of orchestration module of [DataWhiz-Chat](https://github.com/quickSilverShanks/DataWhiz-Chat/tree/main) repository.


## Getting Started

01. Clone [repository](https://github.com/mage-ai/rag-project)
```bash
git clone https://github.com/mage-ai/rag-project
cd rag-project
```
02. navigate to the `rag-project/llm` directory, add `spacy` to the requirements.txt.
03. Then update the `Dockerfile` found in the `rag-project` directory with the following:
```YAML
RUN python -m spacy download en_core_web_sm
```
04. Feel free to make any additional changes as per the docker and host system setup on local machine.
05. Run start script to start docker containers
```bash
./scripts/start.sh
```

> Above terminal command might result in error if the script start.sh was created or edited on a Windows system, which uses different line endings (CRLF) compared to Unix-based systems like Linux (which use LF). Use below unix terminal command to remove the carriage return (\r) characters from the file.

```bash
sed -i 's/\r$//' ./scripts/start.sh
```

> This command removes the Windows-style line endings (\r) from the file and converts it to Unix-style line endings (\n), making the script executable on Unix-based systems like Linux.

Once started, go to [http://localhost:6789/](http://localhost:6789/)

For more setup information, refer to these [instructions](https://docs.mage.ai/getting-started/setup#docker-compose-template)


## RAG Pipeline

The Data Preparation Pipeline has modules and scripts as indicated below:

- **Ingest:**  Ingest documents from a single data source. ([code](https://raw.githubusercontent.com/quickSilverShanks/LLMs---Mage--Zoomcamp/main/llms_mage/rager/data_loaders/runic_oblivion.py), [data](https://raw.githubusercontent.com/DataTalksClub/llm-zoomcamp/main/01-intro/documents.json))
- **Chunk:** Once data is ingested, break it into manageable chunks. The Q&A data is already chunked - the texts are small and easy to process and index. But other datasets might not be (book texts, transcripts, etc). ([code](https://raw.githubusercontent.com/quickSilverShanks/LLMs---Mage--Zoomcamp/main/llms_mage/rager/transformers/radiant_photon.py))
- **Tokenization:** Tokenization is a crucial step in text processing and preparing the data for effective retrieval. ([code](https://raw.githubusercontent.com/quickSilverShanks/LLMs---Mage--Zoomcamp/main/llms_mage/rager/transformers/vivid_nexus.py))
- **Embed:** Embedding data translates text into numerical vectors that can be processed by models. Sentence transformers can be used in this step as well as Spacy as shown in the code. ([code](https://raw.githubusercontent.com/quickSilverShanks/LLMs---Mage--Zoomcamp/main/llms_mage/rager/transformers/prismatic_axiom.py))
- **Export:** After processing, data needs to be exported for storage so that it can be retrieved for better contextualization of user queries. Here the embeddings are being saved to elasticsearch.([code](https://raw.githubusercontent.com/quickSilverShanks/LLMs---Mage--Zoomcamp/main/llms_mage/rager/data_exporters/numinous_fission.py))
  > Make sure to use the name given to your elasticsearch service in your docker compose file followed by the port as the connection string, e.g `<docker-compose-service-name><port>` http://elasticsearch:9200
- **Retrieval: Test Vector Search Query:** After exporting the chunks and embeddings, test the search query to retrieve relevant documents on sample queries. ([code](https://raw.githubusercontent.com/quickSilverShanks/LLMs---Mage--Zoomcamp/main/code/retrieval.py))
- **Trigger Daily Runs:** Automation is key to maintaining and updating the system. Mage.ai can be used to schedule and trigger daily runs for the data pipelines developed above, ensuring up-to-date and consistent data processing.
