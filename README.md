# CD_PUCRIO_02
## MVP — Engenharia de Dados (PUC-Rio) | INMET (Capitais 2020–2024)

Este repositório contém a entrega do **MVP da disciplina de Engenharia de Dados** (MBA em Ciência de Dados – PUC-Rio).  
O trabalho implementa um pipeline de dados em nuvem (Databricks Free) com camadas **staging → bronze → silver → gold**, além de um **Catálogo de Dados** (linhagem, dicionário e perfil das colunas) e uma etapa final de análise com consultas e gráficos.

---

## Objetivo do MVP

Construir um pipeline de dados em ambiente de nuvem (Databricks Free) e avaliar **confiabilidade, consistência e padrões** em dados meteorológicos associados a estações automáticas do **INMET**, além de demonstrar a geração de indicadores e visualizações a partir da camada **Gold**.

Para viabilizar a execução no ambiente gratuito e manter o processamento em tempo adequado, foi realizado um **recorte operacional** do conjunto de dados, mantendo apenas as estações localizadas nas **capitais do Brasil** e restringindo o período para **2020 a 2024**.

---

## Conteúdo do repositório

### Notebooks / scripts
- **`MVP_Dados_INMET.ipynb`**  
  Notebook principal do pipeline (preparação, coleta, bronze, silver, gold e análises finais), com saídas/prints do Databricks.

- **`catalogo.ipynb`**  
  Notebook do Catálogo de Dados (camada Gold), contendo:
  - linhagem dos dados (origem + transformações)
  - dicionário de dados (descrição por coluna)
  - perfil das colunas (mínimo, máximo, % nulos, cardinalidade)
  - view final do catálogo para leitura e evidência

> Observação: os notebooks estão salvos com outputs para evidenciar execução e resultados.

### Dados
- **`inmet_capitais_2020_2024.csv`**  
  Observações meteorológicas **diárias** (recorte: capitais, 2020–2024).

- **`estacoes.csv`**  
  Cadastro/metadados das estações (região, UF, cidade, coordenadas, altitude e período de registros).

---

## Fonte dos dados (linhagem)

O dataset utilizado foi obtido a partir de fonte pública no Kaggle (dados associados a estações automáticas do Instituto Nacional de Meteorologia - INMET):  
https://www.kaggle.com/datasets/gregoryoliveira/brazil-weather-information-by-inmet

---

## Arquitetura do pipeline (resumo)

- **Staging**: download dos CSVs do GitHub e armazenamento em Volume (`mvp.staging`)
- **Bronze**: ingestão “raw” em Delta (padronização de nomes e colunas de linhagem)
- **Silver**: tipagem, limpeza e validações (consistência e qualidade)
- **Gold**: tabelas finais para consumo analítico + agregações (mensal/anual) e enriquecimento com metadados de estações
- **Análises**: consultas SQL e gráficos para responder às perguntas de negócio

---

## Perguntas respondidas na etapa de análise (camada Gold)

- Quais estações apresentam mais falhas nos ddos de precipitação (dados faltantes) ao longo do tempo?
- Quais variáveis aparecem mais associadas a falhas no registro de precipitação?
- Há padrões temporais (mensais) nos faltantes de precipitação?
- É possível identificar automaticamente outliers de precipitação (IQR por estação)?
- Quais são os maiores eventos de precipitação diária no período e onde ocorreram?
- Como é o comportamento sazonal médio (mensal) de precipitação e temperatura para DF e RJ (2020–2024)?

---

## Como reproduzir (Databricks Free)

1. Criar um workspace no **Databricks Free** e abrir um cluster.
2. Importar o notebook **`MVP_Dados_INMET`** e executá-lo (ordem das células).
3. Importar o notebook **`catalogo`** e executá-lo para gerar e visualizar o catálogo da camada Gold.
4. (Opcional) Caso necessário, atualizar os links “raw” do GitHub nas células de coleta (staging).

---

## Observações

- O recorte (capitais; 2020–2024) foi adotado por **otimização operacional**, mantendo execução viável no Databricks Free.
- As tabelas Gold geradas no Databricks incluem agregações e enriquecimento com metadados das estações.
- O catálogo foi construído para atender o requisito de documentação com descrição de colunas e domínios (mín/máx), além de linhagem.

---

## Autor
Ana Clara de Almeida Marques

Matrícula: 4052025001106
