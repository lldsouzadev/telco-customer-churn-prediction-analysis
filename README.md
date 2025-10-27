# 📉 Machine Learning: Previsão e Análise de Churn de Clientes

## 🎯 Objetivo da Análise

Desenvolver um modelo de Machine Learning capaz de prever quais clientes de uma empresa de telecomunicações estão em risco de cancelar o serviço (Churn). O foco é fornecer **insights de negócios** para ações de retenção.

---

## 💡 Insights e Resultados Chave

| Métrica | Resultado | Significado para o Negócio |
| :--- | :--- | :--- |
| **Taxa de Churn** | **26.5%** | A cada 100 clientes, 26 estão cancelando (Problema Crítico). |
| **Acurácia do Modelo** | **80.20%** | A capacidade geral do modelo em classificar corretamente clientes que cancelam ou não. |
| **Recall (Clientes em Risco)** | **57%** | O modelo consegue identificar 57% de todos os clientes que *realmente* cancelaram. Este é o foco de melhoria. |
| **Principal Driver de Risco** | **Contrato Mês a Mês** | Clientes com contratos mais flexíveis são significativamente mais propensos ao Churn. |

---

## 🛠️ Metodologia e Pipeline de Data Science

A análise seguiu as seguintes etapas principais:

### 1. Análise Exploratória de Dados (EDA)

* **Identificação do Desbalanceamento:** A variável alvo (`Churn Value`) apresentou uma distribuição desbalanceada de **73.5%** (Não Churn) vs. **26.5%** (Churn).
* **Insights de Churn:** Visualização demonstrou que o **Contrato Mês a Mês** e um **Tempo de Lealdade (`Tenure Months`) menor** são os maiores indicadores de cancelamento.

### 2. Limpeza e Pré-processamento de Dados

* **Tratamento de Tipos:** Conversão das colunas `Monthly Charges` e `Total Charges` (originalmente `object`) para `float64`, corrigindo a formatação decimal (vírgula para ponto) e tratando valores nulos.
* **Redução de Dimensionalidade:** Remoção de 11 colunas redundantes ou não preditivas (ex: `CustomerID`, dados geográficos e colunas duplicadas como `Churn Label`).
* **Codificação Categórica:** Aplicação de **One-Hot Encoding** (via `pd.get_dummies`) em 16 colunas de texto (`object`) para que o modelo pudesse processá-las. O número de features subiu para 33.

### 3. Modelagem e Otimização (Machine Learning)

* **Modelo Base:** Regressão Logística, um modelo robusto e rápido para classificação binária.
* **Otimização e Escalonamento:** Foi implementado um **Pipeline** com **StandardScaler** para padronizar as features e resolver o `ConvergenceWarning`. O aumento do `max_iter` para 5000 garantiu a estabilidade do modelo otimizado.

---

## 4. Como Executar a Análise

Para rodar esta análise localmente, você precisará ter o **Miniconda/Anaconda** e o ambiente Python configurados.

### Pré-requisitos

A análise requer as seguintes bibliotecas Python: `pandas`, `numpy`, `scikit-learn`, `matplotlib`, e `seaborn`.

### Passos de Execução

1.  **Crie e Ative o Ambiente:**
    Se você ainda não tem o ambiente `churnprediction`, crie-o no seu terminal (Anaconda Prompt):
    ```bash
    conda create --name churnprediction python=3.9 pandas numpy scikit-learn matplotlib seaborn jupyter -y
    ```
    Em seguida, ative-o:
    ```bash
    conda activate churnprediction
    ```

2.  **Baixe o Código:**
    Clone este repositório do GitHub ou baixe os arquivos diretamente e navegue até a pasta.
    ```bash
    cd /caminho/para/pasta-do-projeto
    ```

3.  **Inicie o Jupyter Notebook:**
    Execute o comando para iniciar o servidor Jupyter:
    ```bash
    jupyter notebook
    ```
4.  **Execute o Notebook:**
    No navegador, clique no arquivo `Main_Novo.ipynb` e execute todas as células em sequência (usando `Cell -> Run All` ou `Shift + Enter` célula por célula).

---

## 5. Conclusão e Próximos Passos

Apesar de o modelo ter uma boa acurácia geral, a prioridade para o negócio é aumentar a capacidade de **identificar corretamente** os clientes de alto risco (aumentar o *Recall*).

* **Ação Imediata:** A empresa deve usar o modelo para priorizar clientes classificados como Churn=1 e focar as campanhas de retenção (ex: descontos, upgrades) nesses $\sim 57\%$ de clientes que o modelo previu corretamente.
* **Próxima Etapa:** Experimentar modelos de Ensemble (como **Random Forest** ou **XGBoost**) e técnicas de **Balanceamento de Classes (SMOTE)** para melhorar o Recall e o F1-Score da classe Churn.

---

## 💻 Ferramentas Utilizadas

* **Linguagem:** Python
* **Bibliotecas:** `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`
* **Dados:** `telco costumer churn prediction`, [Telco Costumer Churn no Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
* **Ambiente:** Jupyter Notebook
* **Assistência:** O código foi desenvolvido com assistência de IA para acelerar o desenvolvimento, focando o tempo do analista na EDA e na otimização do modelo.
