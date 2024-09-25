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

> **Note:** Above terminal command might result in error if the script start.sh was created or edited on a Windows system, which uses different line endings (CRLF) compared to Unix-based systems like Linux (which use LF). Use below unix terminal command to remove the carriage return (\r) characters from the file.

```bash
sed -i 's/\r$//' ./scripts/start.sh
```

> This command removes the Windows-style line endings (\r) from the file and converts it to Unix-style line endings (\n), making the script executable on Unix-based systems like Linux.

Once started, go to [http://localhost:6789/](http://localhost:6789/)

For more setup information, refer to these [instructions](https://docs.mage.ai/getting-started/setup#docker-compose-template)


## RAG Pipeline

The Data Preparation Pipeline has modules and scripts as indicated below:

