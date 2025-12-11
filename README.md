# MVP Datasus — Engenharia de Dados (PUC-Rio | Nov/2025)

Este repositório contém o MVP desenvolvido para a Sprint Engenharia de Dados da Pós Graduação em Ciência de Dados e Analytics da PUC-Rio.  

O objetivo é construir um **pipeline completo de dados** utilizando Databricks, desde a ingestão até a análise final, utilizando dados públicos do **DATASUS TABNET** relacionados a **óbitos por HIV** no Brasil.

---

## Objetivo do MVP

Construir um pipeline de dados capaz de:

- Reunir e tratar dados de internações e óbitos do SUS relacionados ao HIV, no período **jan/2020 a set/2025**.
- Modelar os dados em camadas (Bronze → Silver → Gold).
- Avaliar qualidade dos dados.
- Responder às perguntas analíticas definidas no escopo.

---

## Perguntas de Negócio (que o MVP responde)

1. Quantos óbitos por HIV, registrados em internações no SUS, ocorreram de janeiro de 2020 a setembro de 2025?
2. Qual UF teve o maior total de óbitos por HIV no período? E quantos foram?
3. Qual UF teve o menor total de óbitos por HIV no período? E quantos foram?
4. Qual é a distribuição dos óbitos por HIV por faixa etária?
5. Qual faixa etária concentrou o maior número de óbitos?
6. Qual faixa etária concentrou o menor número de óbitos?
7. Como se distribuem os óbitos por HIV por raça/cor?
8. Qual raça/cor registrou o maior número de óbitos?
9. Qual raça/cor registrou o menor número de óbitos?

Essas perguntas são respondidas **na camada Gold**, alimentando dashboards no Power BI.

---

## Fontes de Dados

Todos os dados são públicos e foram obtidos do **DATASUS TABNET**, a partir dos seguintes módulos:

- *Morbidade Hospitalar do SUS — por local de internação*  
- *Lista Morb CID-10: Doença pelo vírus da imunodeficiência humana [HIV]*  
- Período filtrado: **2020 → 2025**

As bases foram exportadas manualmente da interface TABNET, nos formatos CSV.

**Data do download:** Novembro/2025.

---

## 🏗️ Arquitetura do Projeto (Databricks)


---

## 📚 Estrutura do Repositório

Workspace Databricks
├── mvp_datasus
│ ├── bronze
│ │ ├── raw_table/ # CSV originais
│ │ └── tables_delta/ # tabelas Delta brutas
│ ├── silver
│ │ └── tables_delta/ # tabelas tratadas e tipadas
│ └── gold
│ └── agregacoes/ # tabelas agregadas e análises


---

## Pipeline ETL (Resumo)

### Bronze
- Ingestão dos CSVs.
- Armazenamento bruto.
- Criação das tabelas Delta com *schema original*.

###  Silver
- Padronização dos nomes de colunas.
- Conversões de tipos.
- Limpeza de dados (`-` → 0, null → 0).
- Normalização de anos, faixas e categorias.
- Unpivot das colunas de ano.

###  Gold
- Geração da tabela fato `fact_obitos_hiv`.
- Criação de agregações por:
  - UF  
  - Ano  
  - Faixa etária  
  - Sexo  
  - Raça/cor  
- Materialização das análises que respondem às perguntas 1–9.

---

## Visualização e Dashboard

O arquivo **Power BI** contendo todos os gráficos e indicadores está em:





