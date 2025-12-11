# Dicionário de Dados — MVP DATASUS

Este documento descreve os 22 conjuntos de dados utilizados na camada **Bronze**, suas colunas, domínios, tipos e observações.

Cada tabela segue o formato exportado do TABNET:

- Linha = Unidade da Federação (UF)
- Colunas = Anos (2020 a 2025) + colunas auxiliares (código IBGE, UF)
- Valores = Quantidade de óbitos

---

# Lista de arquivos (22 CSVs)

1. obitos_geral.csv  
2. obitos_hiv_geral.csv  
3. obitos_hiv_fem.csv  
4. obitos_hiv_masc.csv  
5. obitos_hiv_faixa_0-10.csv  
6. obitos_hiv_faixa_0-10_fem.csv  
7. obitos_hiv_faixa_0-10_masc.csv  
8. obitos_hiv_faixa_10-25.csv  
9. obitos_hiv_faixa_10-25_fem.csv  
10. obitos_hiv_faixa_10-25_masc.csv  
11. obitos_hiv_faixa_25-40.csv  
12. obitos_hiv_faixa_25-40_fem.csv  
13. obitos_hiv_faixa_25-40_masc.csv  
14. obitos_hiv_faixa_40-55.csv  
15. obitos_hiv_faixa_40-55_fem.csv  
16. obitos_hiv_faixa_40-55_masc.csv  
17. obitos_hiv_faixa_55_65.csv  
18. obitos_hiv_faixa_55-65_fem.csv  
19. obitos_hiv_faixa_55-65_masc.csv  
20. obitos_hiv_faixa_65_mais.csv  
21. obitos_hiv_faixa_65_mais_fem.csv  
22. obitos_hiv_faixa_65_mais_masc.csv  

---

# Estrutura geral das tabelas

Todas as tabelas possuem o mesmo padrão estrutural:

| Coluna              | Tipo    | Descrição |
|---------------------|---------|-----------|
| cod_ibge            | string  | Código IBGE da Unidade da Federação |
| unidade_federacao   | string  | Sigla da UF (ex.: SP, RJ, MG) |
| 2020                | string  | Quantidade de óbitos em 2020 |
| 2021                | string  | Quantidade de óbitos em 2021 |
| 2022                | string  | Quantidade de óbitos em 2022 |
| 2023                | string  | Quantidade de óbitos em 2023 |
| 2024                | string  | Quantidade de óbitos em 2024 |
| 2025                | string  | Quantidade de óbitos em 2025 (parcial até setembro) |

---

# Observações Gerais de Tratamento

- valores `"-"` foram convertidos para `0`;
- todas as colunas de ano foram convertidas para **inteiro (INT)**;
- nomes de colunas foram padronizados para `snake_case` na camada Silver;
- colunas `cod_ibge` e `unidade_federacao` foram mantidas como STRING;
- quando necessário, valores foram unpivotados para o formato:
  uf | cod_ibge | ano | qtd_obitos


---

# Domínios de cada coluna

### cod_ibge  
- string  
- 2 dígitos  
- domínio: 11 a 53 (unidades federativas)

### unidade_federacao  
- string  
- domínio:  
  `AC AL AP AM BA CE DF ES GO MA MG MS MT PA PB PR PE PI RJ RN RO RR RS SC SE SP TO`

### anos (2020–2025)  
- int  
- domínio esperado: `0 → ~5.000`  
- sem valores negativos  
- 2025 contém apenas janeiro–setembro

---

# Dicionário por arquivo

Abaixo, cada tabela é documentada com sua descrição específica.

---

## 1. obitos_geral.csv
- **Descrição:** total de óbitos por todas as causas, por UF e ano.  
- **Uso:** validação de tendência e comparação com óbitos por HIV.

---

## 2. obitos_hiv_geral.csv
- **Descrição:** total geral de óbitos por HIV por UF (sexo + idade + raça).  
- **Tabela base da análise principal.**

---

## 3. obitos_hiv_fem.csv
- **Descrição:** óbitos por HIV filtrados para **sexo feminino**.

---

## 4. obitos_hiv_masc.csv
- **Descrição:** óbitos por HIV filtrados para **sexo masculino**.

---

## 5–7. Tabelas faixa 0–10 (geral, fem, masc)
- **Descrição:** óbitos por HIV em crianças de **0 a 10 anos**, com filtros por sexo quando aplicável.

---

## 8–10. Tabelas faixa 10–25 (geral, fem, masc)  
- **Descrição:** óbitos por HIV em pessoas de **10 a 25 anos**, com filtros por sexo quando aplicável.

---

## 11–13. Tabelas faixa 25–40 (geral, fem, masc) 
- **Descrição:** óbitos por HIV em pessoas de **25 a 40 anos**, com filtros por sexo quando aplicável.
---

## 14–16. Tabelas faixa 40–55 (geral, fem, masc) 
- **Descrição:** óbitos por HIV em pessoas de **40 a 55 anos**, com filtros por sexo quando aplicável.
---

## 17–19. Tabelas faixa 55–65 (geral, fem, masc) 
- **Descrição:** óbitos por HIV em pessoas de **55 a 65 anos**, com filtros por sexo quando aplicável.
---

## 20–22. Tabelas 65+ (geral, fem, masc)
- **Descrição:** óbitos por HIV em pessoas de **65 anos ou mais **, com filtros por sexo quando aplicável.

---

# ✔ Linhagem dos Dados

1. **Origem:** DATASUS TABNET  
2. **Download manual:** Nov/2025  
3. **Camada Bronze:** CSV → Delta  
4. **Camada Silver:** limpeza, padronização, unpivot  
5. **Camada Gold:** agregações e construção da `fact_obitos_hiv`

---

# ✔ Responsável pela Documentação

**Marcelo Alexandre Machado Silvestre**


