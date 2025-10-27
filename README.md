# 📉 Análise e Previsão de Churn de Clientes (Telecomunicações)

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

## 📊 Análise Exploratória e Visualização (Os Drivers do Churn)

O primeiro passo foi entender a dimensão do problema e os fatores que levam ao cancelamento.

### 1. Desbalanceamento e Distribuição da Variável Alvo

A variável alvo está significativamente desbalanceada, um desafio comum em problemas de Churn.

![Distribuição de Churn](graficos/1_churn_distribuicao.png)

### 2. Contrato: O Maior Fator de Risco

O gráfico abaixo mostra claramente que clientes com contrato **Mês a Mês** são desproporcionalmente mais propensos a cancelar.

![Churn por Contrato](graficos/2_churn_por_contrato.png)

### 3. Lealdade (Tenure): Clientes Novos são Mais Frágeis

Clientes que cancelaram têm uma mediana de **meses de lealdade (Tenure)** significativamente menor. A retenção deve focar nos clientes recém-adquiridos.

![Lealdade (Tenure) vs. Churn](graficos/3_tenure_vs_churn.png)

---

## 🛠️ Metodologia e Pipeline de Machine Learning

A análise utilizou Regressão Logística, otimizada com um Pipeline para garantir a correta aplicação do **Escalonamento (StandardScaler)** e a robustez dos dados.

* **Pré-processamento:** Tratamento do tipo de dado (corrigindo vírgula para ponto em colunas financeiras) e One-Hot Encoding em 16 colunas categóricas.
* **Otimização:** Uso do Pipeline e `max_iter=5000` para resolver o `ConvergenceWarning`.

### Avaliação do Modelo: Matriz de Confusão

A matriz mostra a performance do modelo no conjunto de teste, revelando os acertos (True Positives) e falhas (False Negatives).

![Matriz de Confusão do Modelo Otimizado](graficos/4_matriz_confusao.png)

**Interpretação da Matriz:**
* **745 Acertos Churn (TP):** O modelo previu corretamente que 745 clientes iriam cancelar.
* **573 Erros Churn (FN):** O modelo *perdeu* 573 clientes que cancelaram (False Negatives), indicando a margem para aumentar o Recall.

---

## 🚀 Conclusão e Ação Estratégica

Apesar de o modelo ter uma boa acurácia geral, a prioridade para o negócio é aumentar a capacidade de **identificar corretamente** os clientes de alto risco (aumentar o *Recall*).

* **Ação Imediata:** A empresa deve usar o modelo para priorizar clientes classificados como Churn=1 e focar as campanhas de retenção (ex: descontos, upgrades) nesses $\sim 57\%$ de clientes que o modelo previu corretamente.
* **Próxima Etapa:** Experimentar modelos de Ensemble (como **Random Forest** ou **XGBoost**) e técnicas de **Balanceamento de Classes (SMOTE)** para melhorar o Recall e o F1-Score da classe Churn.

---

## 💻 Recursos e Execução

### Fonte de Dados
* [Telco Customer Churn (IBM) - Kaggle](https://www.kaggle.com/datasets/denisexpsito/telco-customer-churn-ibm)

### Execução Local (Instalação)
1. Crie e ative o ambiente (`churnprediction`) no Anaconda Prompt:
   `conda create --name churnprediction python=3.9 pandas numpy scikit-learn matplotlib seaborn jupyter -y`
   `conda activate churnprediction`
2. Navegue até a pasta do projeto e inicie o Jupyter: `jupyter notebook`
3. Execute todas as células do `Main_Novo.ipynb`.
