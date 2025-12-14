# Modelagem dos Dados

## 1. Introdução

Este documento apresenta a modelagem adotada no MVP de Engenharia de Dados baseado em informações exportadas do DATASUS TABNET, cobrindo morbidade hospitalar e óbitos por HIV entre 2020 e 2025. A modelagem foi realizada visando padronização, rastreabilidade e preparação dos dados para análises na camada Gold.

---

## 2. Arquitetura Adotada (Arquitetura Medalhão)

### **Bronze – Dados Brutos**

* Ingestão direta dos arquivos CSV exportados da base DATASUS TABNET.
* Armazenamento em formato Delta.
* Sem transformações além da leitura inicial.

### **Silver – Dados Tratados e Padronizados**

* Padronização dos schemas.
* Conversão de tipos.
* Tratamento de valores nulos e inconsistentes.
* Uniformização de colunas.
* Geração de tabelas prontas para agregações.

### **Gold – Dados Modelados para Consumo Analítico**

* Aplicação de agregações e cálculos.
* Tabelas modeladas para responder às perguntas de negócio.

---

## 3. Modelagem Conceitual

A modelagem segue uma abordagem em estrela (**Star Schema**).

### **Fato Principal**

**Fato_Obitos_HIV**

* Contém registros de óbitos por HIV, decorrentes de internações no SUS .
* Granularidade: *UF + Ano + Faixa-Etária + Sexo*.

### **Dimensões**

* **Dim_uf** — lista de Unidades da Federação com nome e sigla.
* **Dim_Ano** — intervalo temporal entre janeiro de 2020 a setembro de 2025.
* **Dim_Faixa_Etaria** — faixas padronizadas utilizadas no MVP.
* **Dim_Sexo** — Masculino, Feminino ou Total.

---

## 4. Modelagem Lógica

### **Tabela: fato_obitos_hiv**

| Coluna       | Tipo   | Descrição                              |
| ------------ | ------ | ---------------------------------------|
| id_fato      | INT    |Chave primária da tabela                |
| uf           | INT    |Chave estrangeira para dim_uf           |
| ano          | INT    |Chave estrangeira para dim_ano          |
| faixa        | INT    |Chave estrangeira para dim_faixa_etaria |
| sexo         | INT    |Chave estrangeira para dim_ano          |
| qtd_obt      | INT    |Quantidade de óbitos segundo critérios  |

### **Tabela: dim_uf**

| Coluna  | Tipo   | Descrição                              |
| ------- | ------ | ---------------------------------------|
|id_uf    | INT    | Chave primária da tabela               |
|cod_ibge | INT    |Código dos estados pelo IBGE            |
|sigla_uf | STRING |Sigla representativa de todos os estados|
|nome_uf  | STRING |Nome dos estados                        |


### **Tabela: dim_faixa_etaria**

| Coluna           | Tipo  | Descrição                                                                |
| ---------------- | ------| -------------------------------------------------------------------------|
| id_faixa_etaria  |INT    | Chave primária da tabela                                                 |
| faixa_etaria     |STRING | Indica os intervalos descritivos e estabelecidos entre as faixas de idade|


### **Tabela: dim_sexo**

| Coluna    | Tipo   | Descrição                                |
| ----------| ------ | -----------------------------------------|
|id_sexo    | INT    | Chave primária da tabela                 |
| sexo      | STRING | Definição do sexo (masculino, feminino)  |

### **Tabela: dim_ano**

| Coluna    | Tipo | Descrição                                |
| --------- | ---- | -----------------------------------------|
| id_ano    | INT  | Chave primária da tabela                 |
| ano       | INT  | ano considerado (2020 a 2025)            |

---

## 5. Regras de Transformação da Silver para Gold

* Remoção de valores nulos.
* Conversão de "-" para 0.
* Normalização dos nomes das colunas em todas as tabelas.
* Agregações por UF, ano, sexo e faixa etária.
* Geração de tabelas resumidas de acordo com os critérios estabelecidos.

---

## 6. Diagrama Simplificado

<img width="829" height="469" alt="esquema_estrela_mvp" src="https://github.com/user-attachments/assets/901567db-3029-4eff-8dcd-6f9b2341fa2c" />


## 7. Considerações Finais

A modelagem proposta segue princípios alinhados ao escopo do MVP. Foi construída para suportar consultas analíticas diretas e exportações para análises adicionais. Está alinhada às boas práticas da arquitetura em camadas (Bronze → Silver → Gold).

