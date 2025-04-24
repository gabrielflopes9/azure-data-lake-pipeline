# Azure Data Lake Pipeline — Ingestão de Dados

Este repositório apresenta o pipeline de ingestão de dados desenvolvido durante o curso **Azure Data Lake Pipeline – Ingestão de Dados** na Alura. O objetivo é demonstrar boas práticas de provisionamento, organização e movimentação de dados no Azure.

---

## 📂 Estrutura de Pastas

```
.
├── data/                        # Diretório para dados processados ou extraídos
├── dados_boston.zip             # Arquivo ZIP contendo dados de Boston
├── save_data_blob_inicial.py    # Script Python de extração, compactação e upload
├── requirements.txt             # Dependências Python

```

---

## 🚀 Visão Geral

1. **Provisionamento de Recursos Azure**  
   - Conta de Storage  
   - Resource Group  
   - Containers de Blob Storage (`raw-data`, `processed-data`)

2. **Ingestão de Dados**  
   - Extração de dados de fonte externa  
   - Compactação em ZIP  
   - Upload para container `raw-data`

3. **Estruturação do Data Lake**  
   - **Bronze**: dados brutos  
   - **Silver**: dados filtrados e limpos (merge de arquivos)  
   - **Gold**: dados agregados prontos para consumo

4. **Orquestração com Azure Data Factory**  
   - Linked Services entre Blob Storage e Data Lake  
   - Datasets para leitura/escrita nas camadas  
   - Pipeline de cópia e merge (Bronze → Silver)

---

## 🛠️ Pré-requisitos

- Conta no Azure com permissão de criação de recursos  
- Python 3.8+ e `pip`  
- Git

---

## ⚙️ Configuração

1. **Clone o repositório**  
   ```bash
   git clone https://github.com/seu-usuario/azure-data-lake-pipeline.git
   cd azure-data-lake-pipeline
   ```

2. **Crie e ative um ambiente virtual**  
   ```bash
   python -m venv venv
   source venv/bin/activate    # Linux/Mac
   venv\Scripts\activate       # Windows
   ```

3. **Instale as dependências**  
   ```bash
   pip install -r requirements.txt
   ```

4. **Defina variáveis de ambiente** (substitua pelos seus valores)  
   ```bash
   export AZURE_STORAGE_ACCOUNT="NomeDaStorage"
   export AZURE_STORAGE_KEY="SuaChaveDeAcesso"
   export RESOURCE_GROUP="NomeDoResourceGroup"
   export RAW_CONTAINER="raw-data"
   ```



## 🏗️ Estrutura do Data Lake

```
data_lake/
├── bronze/   # arquivos ZIP brutos
├── silver/   # dados consolidados e limpos
└── gold/     # dados agregados para consumo
```

---

## 🔄 Azure Data Factory

1. **Linked Services**  
   - Blob Storage (`raw-data`)  
   - Data Lake (Bronze, Silver, Gold)

2. **Datasets**  
   - `BlobDataset`  — leitura de ZIPs em `raw-data`  
   - `BronzeDataset` — escrita na camada Bronze  
   - `SilverDataset` — escrita na camada Silver

3. **Pipeline**  
   - **Copy Activity**: de `BlobDataset` para `BronzeDataset`  
   - **Merge Activity**: consolidação de arquivos em `SilverDataset`

---

## ▶️ Execução

1. Coloque seus arquivos em `./input/` (ou use `dados_boston.zip` na raiz).  
2. Execute:
   ```bash
   python extract_and_upload.py      --input-dir ./input      --zip-name dados_boston.zip      --container "$RAW_CONTAINER"
   ```
3. Verifique o upload no Portal Azure ou via CLI.  
4. No Data Factory, dispare ou agende o pipeline de copy & merge.

---

## 📈 Próximos Passos

- Automatizar descompactação na **Bronze**  
- Implementar transformações na **Silver**  
- Desenvolver agregações na **Gold**  
- Configurar triggers de agendamento no Data Factory  
- Adicionar monitoramento e alertas com Azure Monitor



## 📜 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](./LICENSE).

---

> **Autor:** Gabriel Lopes  
> **Data:** Abril de 2025  
