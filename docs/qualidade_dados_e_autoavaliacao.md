
#**1. Análise de Qualidade dos Dados**

A etapa de qualidade dos dados foi realizada após a carga das tabelas Delta na camada Silver. As verificações incluíram:

**1.1 Verificação de Schema**

Para as 22 tabelas carregadas, foi realizada a comparação automática entre o schema inferido na ingestão e o schema registrado na tabela Delta. Não foram encontradas divergências estruturais entre as colunas das tabelas, garantindo consistência entre os arquivos CSV originais e os DataFrames armazenados.

**1.2 Verificação e Tratamento de Valores Nulos**

Foi executado um processo automatizado que:

Identificou colunas numéricas (anos de 2020 a 2025).

Contou valores nulos por coluna.

Substituiu valores nulos por 0, de forma padronizada.

Resultado geral:

Todos os valores nulos foram corrigidos para 0, garantindo integridade para cálculos agregados no Gold.

**1.3 Análise Estatística Básica**

Não foram detectados valores negativos.

Não foram identificadas inconsistências estruturais como colunas duplicadas, strings contendo caracteres inválidos ou anos faltantes.

**1.4 Impressão das 5 primeiras linhas de cada tabela**

Foram exibidas automaticamente no notebook Silver_validação_schema_null_check, registrando evidência para todas as 22 tabelas.

**2. Autoavaliação**

A construção deste MVP seguiu todas as etapas propostas no projeto da disciplina, resultando em um pipeline completo operando no Databricks. A seguir, apresento a autoavaliação estruturada conforme solicitado.

**2.1 Atingimento dos Objetivos**

Os objetivos definidos no início do projeto foram amplamente atendidos:

Todas as nove perguntas-guia foram respondidas a partir de dados reais do DATASUS.

As bases foram coletadas, modeladas, tratadas e analisadas de forma bem estruturada.

A construção das camadas Bronze, Silver e Gold refletiu um pipeline de engenharia de dados.

**2.2 Dificuldades Encontradas**

Durante o desenvolvimento, destacam-se as seguintes dificuldades:

Restrições do Databricks Free Edition, especialmente limitações de acesso ao DBFS público e problemas com volumes/montagens.

Necessidade de padronizar schemas entre CSVs com pequenas diferenças estruturais.

Tratamento de valores nulos e caracteres inválidos no processo de carga para tabelas Delta.

Organização dos notebooks de forma modular para refletir as camadas do pipeline.

Apesar disso, todas as dificuldades foram superadas com ajustes no código de ingestão, validação e carga.

**2.3 Pontos Fortes**

Uso real de dados oficiais do SUS.

Pipeline completo com 22 tabelas tratadas.

Dicionário de dados abrangente.

Dashboard final no Power BI conectando a camada Gold.

Repositório GitHub organizado em Docs, Notebooks e Readme.

**2.4 Trabalhos Futuros**

Para evolução do MVP, consideram-se os seguintes aprimoramentos:

Criar um orquestrador com Databricks Workflows ou Airflow para automatizar o pipeline.

Acrescentar novas variáveis clínicas disponíveis no DATASUS.

Unificar tabelas por faixa etária em um modelo estrela com dimensões dedicadas.

Criar API externa para disponibilização dos indicadores.

Publicar dashboard como relatório público.

**9.5 Conclusão**

O MVP cumpriu seu propósito de demonstrar domínio sobre coleta, ingestão, modelagem, tratamento e análise de dados em nuvem. O aprendizado obtido na prática consolidou os conceitos da disciplina, e o projeto foi desenvolvido observando caráter técnico, documentação e organização.
