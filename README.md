# Análise de Corridas da Zuber em Chicago

Este projeto analisa dados de corridas de táxi em Chicago para apoiar o lançamento da **Zuber**, uma nova empresa de compartilhamento de caronas. A análise busca identificar padrões de demanda, principais destinos e empresas de táxi mais utilizadas, além de investigar se as **condições climáticas influenciam a duração das viagens entre o Loop e o Aeroporto Internacional O'Hare**.

---

## 📌 Abordagem / Arquitetura Técnica

O projeto foi desenvolvido em **Python**, utilizando uma abordagem de análise exploratória de dados (EDA) e teste estatístico de hipóteses.

### 1. Análise Exploratória de Dados (EDA)

Foram analisados dois conjuntos de dados:

- `project_sql_result_01.csv`: informações sobre empresas de táxi e quantidade de corridas.
- `project_sql_result_04.csv`: informações sobre os bairros de destino e a média de viagens.

As principais etapas foram:

- Importação dos arquivos CSV com **Pandas**;
- Inspeção de amostras e informações gerais dos DataFrames;
- Estatísticas descritivas dos dados de corridas;
- Ordenação dos bairros pela média de viagens;
- Identificação dos **10 principais bairros por número médio de desembarques**;
- Identificação das empresas com maior volume de corridas;
- Criação de gráficos de barras interativos com **Plotly Express**.

### 2. Teste de Hipóteses

Para investigar a influência das condições climáticas na duração das viagens entre o **Loop e o Aeroporto Internacional O'Hare**, foi utilizado o arquivo:

- `project_sql_result_07.csv`

O tratamento dos dados incluiu a conversão da coluna `start_ts` para o formato `datetime`.

Em seguida, foram separados os registros correspondentes a:

- **Sábados com condições climáticas ruins (`Bad`)**;
- **Sábados com boas condições climáticas (`Good`)**.

Foram formuladas as seguintes hipóteses:

- **H₀ (hipótese nula):** a duração média dos passeios não mudou nos sábados chuvosos.
- **H₁ (hipótese alternativa):** a duração média dos passeios sofreu alterações nos sábados chuvosos.

O nível de significância adotado foi de **5% (`α = 0,05`)**.

Antes do teste de médias, foi aplicado o **teste de Levene** para verificar a igualdade das variâncias. Na sequência, foi utilizado o **teste t para duas amostras independentes (`ttest_ind`)**.

---

## 📂 Estrutura do Repositório

```text
zuber_caronas/
│
├── datasets/
│   ├── project_sql_result_01.csv
│   ├── project_sql_result_04.csv
│   └── project_sql_result_07.csv
│
├── notebooks/
│   └── notebook.ipynb
│
└── requirements.txt
```

### Principais diretórios e arquivos

| Item | Descrição |
|---|---|
| `datasets/` | Armazena os conjuntos de dados utilizados na análise. |
| `project_sql_result_01.csv` | Dados sobre empresas de táxi e quantidade de corridas. |
| `project_sql_result_04.csv` | Dados sobre bairros de destino e média de viagens. |
| `project_sql_result_07.csv` | Dados utilizados para analisar as viagens entre o Loop e O'Hare e as condições climáticas. |
| `notebooks/` | Contém o notebook utilizado para exploração, visualização e análise estatística. |
| `requirements.txt` | Arquivo destinado às dependências necessárias para execução do projeto. |

---

## ⚙️ Instalação e Execução

### 1. Clonar o repositório

Substitua `<URL_DO_REPOSITORIO>` pela URL do repositório:

```bash
git clone https://github.com/alexpereira951/zuber_caronas
cd zuber_caronas
```

### 2. Instalar as dependências

```bash
pip install -r requirements.txt
```

### 3. Executar o notebook

Inicie o Jupyter Notebook:

```bash
jupyter notebook
```

Depois, abra:

```text
notebooks/notebook.ipynb
```

> **Observação:** o notebook utiliza caminhos relativos como `../datasets/...`. Portanto, mantenha a estrutura de diretórios apresentada neste README para que os arquivos CSV sejam encontrados corretamente.

---

## 🛠️ Stack Tecnológica

- 🐍 **Python**
- 🐼 **Pandas** — carregamento, tratamento, exploração e manipulação dos dados.
- 📊 **Plotly Express** — criação de gráficos interativos.
- 📐 **SciPy (`scipy.stats`)** — aplicação dos testes estatísticos.
- 🔢 **NumPy** — suporte às operações numéricas.
- 📓 **Jupyter Notebook** — desenvolvimento e documentação da análise.

---

## 📊 Resultados e Conclusões

### Demanda por empresas de táxi

A análise identificou uma concentração de corridas entre um grupo de empresas com maior volume de viagens. Entre as empresas destacadas no notebook estão:

- Flash Cab;
- Taxi Affiliation Services;
- Medallion Leasing;
- Yellow Cab;
- Taxi Affiliation Service Yellow;
- Chicago Carriage Cab Corp;
- City Service;
- Sun Taxi;
- Star North Management LLC;
- Blue Ribbon Taxi Association Inc.;
- Choice Taxi Association;
- Globe Taxi;
- Dispatch Taxi Affiliation;
- Nova Taxi Affiliation Llc;
- Patriot Taxi Dba Peace Taxi Association;
- Checker Taxi Affiliation.

O notebook utiliza **2.106 viagens** como referência para selecionar as empresas com maior volume de corridas.

### Principais destinos

Entre os bairros analisados, o **Loop** apresentou a maior média de desembarques, seguido por:

1. River North;
2. Streeterville;
3. West Loop.

Esses resultados ajudam a identificar regiões com maior concentração de viagens e podem servir como referência para compreender a distribuição da demanda.

### Influência das condições climáticas

Para as viagens entre o **Loop e o Aeroporto Internacional O'Hare**, o notebook comparou a duração média das viagens em sábados com condições climáticas boas e ruins.

Com nível de significância de **5%**, o teste estatístico apresentado no notebook levou à **rejeição da hipótese nula**. Dessa forma, dentro do conjunto de dados analisado, a conclusão registrada no projeto é que **a duração média dos passeios apresentou alteração estatisticamente significativa em sábados com condições climáticas ruins**.

---

## ⚠️ Limitações

O projeto apresenta algumas limitações que devem ser consideradas na interpretação dos resultados:

1. **Escopo dos dados:** as conclusões estão restritas aos conjuntos de dados fornecidos e aos períodos representados neles, não sendo possível generalizá-las automaticamente para todos os períodos ou para todo o mercado de transporte de Chicago.

2. **Variáveis analisadas:** a investigação sobre as viagens entre o Loop e O'Hare considera especificamente as condições climáticas classificadas como `Good` e `Bad`, sem explorar outras possíveis variáveis que também podem afetar a duração das corridas.

3. **Teste estatístico:** embora o teste de Levene seja utilizado para verificar a igualdade das variâncias, o teste t posterior é executado no notebook com `equal_var=True`. Portanto, a decisão sobre a configuração do teste poderia ser revisada para garantir que o resultado esteja alinhado ao diagnóstico das variâncias.

4. **Ausência de métricas detalhadas no notebook:** a conclusão estatística registra a rejeição da hipótese nula, mas o notebook apresentado não documenta no README o valor-p obtido nem outras medidas de efeito. Isso limita a avaliação da magnitude prática da diferença observada.

---

## 🎯 Objetivo do Projeto

De forma geral, o projeto demonstra um fluxo de trabalho de **análise de dados aplicado a um problema de negócio**, combinando:

**dados → exploração → visualização → formulação de hipóteses → teste estatístico → interpretação dos resultados**

A análise fornece uma visão inicial sobre a demanda por corridas, os principais destinos e a relação entre condições climáticas e duração das viagens na operação analisada.
