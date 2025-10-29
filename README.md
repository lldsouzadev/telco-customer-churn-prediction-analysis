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

<p align="center">
    <img src="https://raw.githubusercontent.com/lldsouzadev/telco-customer-churn-prediction-analysis/main/grafico/1_churn_distribuicao.png" alt="Distribuição">
</p>

### 2. Contrato: O Maior Fator de Risco

O gráfico abaixo mostra claramente que clientes com contrato **Mês a Mês** são desproporcionalmente mais propensos a cancelar.

<p align="center">
    <img src="https://raw.githubusercontent.com/lldsouzadev/telco-customer-churn-prediction-analysis/main/grafico/2_churn_por_contrato.png" alt="Contrato">
</p>

### 3. Lealdade (Tenure): Clientes Novos são Mais Frágeis

Clientes que cancelaram têm uma mediana de **meses de lealdade (Tenure)** significativamente menor. A retenção deve focar nos clientes recém-adquiridos.

<p align="center">
    <img src="https://raw.githubusercontent.com/lldsouzadev/telco-customer-churn-prediction-analysis/main/grafico/3_tenure_vs_churn.png" alt="Lealdade">
</p>

---

## 🛠️ Metodologia e Pipeline de Machine Learning

A análise utilizou Regressão Logística, otimizada com um Pipeline para garantir a correta aplicação do **Escalonamento (StandardScaler)** e a robustez dos dados.

* **Pré-processamento:** Tratamento do tipo de dado (corrigindo vírgula para ponto em colunas financeiras) e One-Hot Encoding em 16 colunas categóricas.
* **Otimização:** Uso do Pipeline e `max_iter=5000` para resolver o `ConvergenceWarning`.

### Avaliação do Modelo: Matriz de Confusão

A matriz mostra a performance do modelo no conjunto de teste, revelando os acertos (True Positives) e falhas (False Negatives).

<p align="center">
    <img src="https://raw.githubusercontent.com/lldsouzadev/telco-customer-churn-prediction-analysis/main/grafico/4_matriz_confusao.png" alt="Matriz de Confusão">
</p>

**Interpretação da Matriz:**
* **212 Acertos Churn (TP):** O modelo previu corretamente que 212 clientes iriam cancelar (Verdadeiros Positivos).
* **162 Erros Churn (FN):** O modelo perdeu 162 clientes que cancelaram (Falsos Negativos), indicando a margem para aumentar o Recall.

---

## 🚀 Conclusão e Plano de Ação Estratégica

Esta análise de Churn (80.20% de acurácia) nos permite traçar um plano de ação imediato focado em dois grupos de clientes de **alto risco**:

### 1. Foco no Fator Contrato (Risco Imediato)

**O Insight:** Clientes com contratos **Mês a Mês** são o maior vetor de Churn. Eles demonstram falta de lealdade e alta flexibilidade para migrar para a concorrência.

**Ação Sugerida:**
* **Target:** Criar campanhas de retenção agressivas, priorizando clientes Mês a Mês.
* **Implementação:** Oferecer incentivos claros (ex: **desconto de 15%** nos próximos 6 meses ou **upgrade gratuito** de banda larga) para migrá-los para contratos de 12 ou 24 meses.

### 2. Foco no Fator Lealdade (Risco de Longo Prazo)

**O Insight:** Clientes **novos** (baixo *Tenure*) estão cancelando em uma taxa muito maior do que os veteranos. A empresa está falhando na fase inicial de experiência do cliente.

**Ação Sugerida:**
* **Target:** Estabelecer um programa de "Boas-vindas" focado nos primeiros 90 dias de contrato.
* **Implementação:** Aumentar o contato proativo (e não reativo) do suporte técnico e da gerência de contas para garantir que a instalação e a experiência inicial sejam impecáveis, reduzindo a chance de Churn precoce.

---

## 📈 Próximos Passos (Aperfeiçoamento Técnico)

Apesar de o modelo identificar corretamente 57% dos clientes que realmente cancelam (Recall), a prioridade técnica é elevar essa taxa para que a empresa possa resgatar **mais clientes em risco**.

* **Aperfeiçoamento do Modelo:** Recomenda-se a exploração de modelos de Ensemble (como **Random Forest** ou **XGBoost**) e o uso de técnicas de **Balanceamento de Classes (SMOTE)** para melhorar especificamente o Recall e a precisão na identificação dos clientes que irão cancelar.

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
