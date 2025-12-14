
# **1. Análise de Qualidade dos Dados**

A etapa de qualidade dos dados foi realizada após a carga das tabelas Delta na camada Silver. As verificações incluíram:

## **1.1 Verificação de Schema**

Para as 22 tabelas carregadas, foi realizada a comparação automática entre o schema inferido na ingestão e o schema registrado na tabela Delta. Não foram encontradas divergências estruturais entre as colunas das tabelas, garantindo consistência entre os arquivos CSV originais e os DataFrames armazenados.

## **1.2 Verificação e Tratamento de Valores Nulos**

Foi executado um processo automatizado que:

Identificou colunas numéricas (anos de 2020 a 2025).

Contou valores nulos por coluna.

Substituiu valores nulos por 0, de forma padronizada.

Resultado geral:

Todos os valores nulos foram corrigidos para 0, garantindo integridade para cálculos agregados no Gold.

## **1.3 Análise Estatística Básica**

Não foram detectados valores negativos.

Não foram identificadas inconsistências estruturais como colunas duplicadas, strings contendo caracteres inválidos ou anos faltantes.

## **1.4 Impressão das 5 primeiras linhas de cada tabela**

Foram exibidas automaticamente no notebook 04_silver_validacoes.ipynb, registrando evidência para todas as 22 tabelas.


