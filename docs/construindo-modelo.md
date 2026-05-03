# Preparação dos dados

Nesta etapa são descritas todas as técnicas utilizadas para o pré-processamento e tratamento dos dados, com base nas características do dataset *BankChurners.csv* e no objetivo de construir um modelo de previsão de churn.

## Remoção de colunas irrelevantes e com data leakage

Antes da limpeza, foram removidas duas colunas que comprometeriam a qualidade do modelo:

- **`CLIENTNUM`**: identificador único do cliente, sem valor preditivo.
- **Colunas Naive Bayes** (`Naive_Bayes_Classifier_Attrition_Flag_*`): geradas a partir da variável-alvo, causariam vazamento de informação (*data leakage*) durante o treinamento.

## Limpeza de dados

Registros com o valor `"Unknown"` nas colunas `Education_Level`, `Marital_Status` e `Income_Category` foram removidos, pois a imputação de categorias desconhecidas poderia introduzir ruído no modelo. Após essa limpeza, o dataset passou de 10.127 para **7.081 registros**, sem linhas duplicadas.

```python
df_dataset = df_dataset[df_dataset != "Unknown"].dropna()
df_dataset.drop(columns=['CLIENTNUM'], inplace=True)
print(f"Número de registros: {df_dataset.shape[0]}")
print(f"Número de colunas: {df_dataset.shape[1]}")
print(f"Número de linhas duplicadas: {df_dataset.duplicated().sum()}")
```

## Tratamento de outliers

A detecção de outliers foi realizada com base na regra do Intervalo Interquartil (IQR). A decisão foi **manter os outliers** em todas as variáveis, pois eles representam comportamentos reais de clientes (altos limites de crédito, alto volume de transações, longos períodos de inatividade) que podem ser preditivos de churn. Sua reavaliação está prevista para etapas futuras de otimização do modelo, onde técnicas como *capping* ou transformações logarítmicas poderão ser aplicadas.

## Codificação de variáveis categóricas (One-Hot Encoding)

As variáveis categóricas (`Gender`, `Education_Level`, `Marital_Status`, `Income_Category`, `Card_Category`) foram convertidas para formato numérico utilizando `pd.get_dummies()` com `drop_first=True`, que elimina a primeira categoria de cada variável para evitar multicolinearidade.

```python
X_xgb = pd.get_dummies(X_xgb, drop_first=True)
```

## Criação da variável-alvo

A variável-alvo `is_desistente` foi criada a partir de `Attrition_Flag`, mapeando `"Attrited Customer"` para `1` e `"Existing Customer"` para `0`.

```python
df_dataset["is_desistente"] = (df_dataset["Attrition_Flag"] == "Attrited Customer").astype(int)
```

## Tratamento do desbalanceamento de classes

O dataset apresenta desbalanceamento: 84,3% de clientes ativos (5.968) contra 15,7% de desistentes (1.113). Para lidar com isso sem técnicas de reamostragem, utilizou-se o parâmetro `scale_pos_weight` do XGBoost, calculado como a razão entre o número de amostras da classe negativa e da classe positiva. Isso instrui o modelo a penalizar mais os erros na classe minoritária durante o treinamento.

```python
scale_pos_weight_val = sum(y_train_xgb == 0) / sum(y_train_xgb == 1)
```

## Separação em treino e teste

Os dados foram divididos em 70% para treino e 30% para teste, com `stratify=y_xgb` para garantir que a proporção das classes fosse mantida em ambos os conjuntos, e `random_state=42` para reprodutibilidade.

```python
X_train_xgb, X_test_xgb, y_train_xgb, y_test_xgb = train_test_split(
    X_xgb, y_xgb, test_size=0.3, random_state=42, stratify=y_xgb
)
```

# Descrição do modelo

Nesta seção, o algoritmo de aprendizado de máquina selecionado para a construção do modelo de previsão de churn foi o **XGBoost (Extreme Gradient Boosting)**. Esta escolha foi justificada pela sua reconhecida alta performance em problemas de classificação tabular, eficiência no tratamento de conjuntos de dados desbalanceados (comum em cenários de churn), capacidade de regularização (L1 e L2 para prevenir overfitting) e fornecimento de importância de features para interpretabilidade. A seleção do XGBoost foi embasada por estudos de ponta na área, como os de Al-Najjar et al. (2022) e Li e Yan (2025), que demonstram a eficácia deste algoritmo na previsão de churn em contextos financeiros e bancários.

![Gráfico de Desempenho XGBoost](img/Grafico-Desempenho-XGBOOST.png)

Em relação ao ajuste dos parâmetros livres, focamos no hiperparâmetro `n_estimators`, que controla o número de árvores no modelo. Foram realizados testes sistemáticos com diferentes valores para `n_estimators`, começando com uma gama ampla e refinando para um intervalo mais específico: `[500, 750, 1000, 1250, 1500]`. A avaliação utilizou o F1-score da classe minoritária ('Attrited Customer') como métrica principal, por ser mais adequada para datasets desbalanceados. Os resultados indicaram que `n_estimators=500` e `n_estimators=750` atingiram o pico de desempenho (F1-score de 0.9164). Optou-se por `n_estimators=500` para o modelo final, buscando o melhor equilíbrio entre performance preditiva e eficiência computacional, evitando complexidade desnecessária sem comprometer a qualidade do modelo.

# Avaliação dos modelos criados

## Métricas utilizadas
Para avaliar o desempenho do modelo de previsão de churn, foram utilizadas as seguintes métricas:

* **Acurácia (Accuracy):** Mede a proporção de previsões corretas sobre o total de previsões. Embora útil, em casos de desbalanceamento de classes, pode ser enganosa.
* **F1-score:** É a média harmônica da precisão e do recall, fornecendo um equilíbrio entre as duas métricas. Foi a métrica principal para a classe 'Attrited Customer' devido ao desbalanceamento do dataset, onde a identificação correta da classe minoritária é crucial.
* **Precisão (Precision):** Indica a proporção de verdadeiros positivos dentre todos os positivos previstos pelo modelo. Em outras palavras, de todos os clientes que o modelo previu que iriam cancelar, quantos de fato cancelaram.
* **Recall (Sensibilidade):** Mede a proporção de verdadeiros positivos dentre todos os positivos reais. Ou seja, de todos os clientes que de fato cancelaram, quantos o modelo conseguiu identificar.

A escolha dessas métricas é essencial para compreender o desempenho do modelo em um problema de previsão de churn, onde a identificação da classe 'Attrited Customer' (cancelamento) é o objetivo principal, e os custos de Falsos Negativos (não identificar um cliente que irá cancelar) são geralmente mais altos que os de Falsos Positivos.

## Discussão dos resultados obtidos

Após o treinamento do modelo XGBoost final com `n_estimators=500` e o uso de `scale_pos_weight` para lidar com o desbalanceamento de classes, as métricas de desempenho no conjunto de teste foram:

* **Acurácia Geral:** 0.9736
* **F1-score (Attrited Customer):** 0.9164
* **Precisão (Attrited Customer):** 0.9137
* **Recall (Attrited Customer):** 0.9192

Esses resultados indicam um desempenho robusto do modelo. A acurácia geral é alta, mas a análise detalhada das métricas para a classe 'Attrited Customer' é mais reveladora devido ao desbalanceamento. Um F1-score de 0.9164 para a classe minoritária demonstra que o modelo é eficaz em identificar clientes propensos ao cancelamento, mantendo um bom equilíbrio entre precisão e recall. A precisão de 0.9137 significa que, quando o modelo prevê um cancelamento, ele está correto em mais de 91% das vezes, o que minimiza o esforço em ações de retenção desnecessárias. O recall de 0.9192 é particularmente positivo, pois significa que o modelo consegue identificar a grande maioria dos clientes que realmente irão cancelar, permitindo que a instituição financeira direcione intervenções a tempo.

A **Matriz de Confusão** reforça essa análise:

![Matriz De Confusão](img/Matriz-De-Confusao-XGBOOST.png)

* **Verdadeiro Negativo (TN):** 1762 - Clientes ativos corretamente identificados como ativos.
* **Falso Positivo (FP):** 29 - Clientes ativos erroneamente classificados como desistentes.
* **Falso Negativo (FN):** 27 - Clientes desistentes erroneamente classificados como ativos (erro mais custoso).
* **Verdadeiro Positivo (TP):** 307 - Clientes desistentes corretamente identificados como desistentes.

A baixa quantidade de Falsos Negativos (27) é crucial para o problema de churn, indicando que o modelo é eficaz em identificar a maioria dos clientes que realmente cancelarão.

# Pipeline de pesquisa e análise de dados

Nosso pipeline seguiu um conjunto organizado de processos:

1.  **Coleta dos Dados:** Dataset baixado do Kaggle via `kagglehub`.
2.  **Análise Exploratória (EDA):** Compreensão da estrutura e estatísticas descritivas (numéricas e categóricas).
3.  **Remoção de Colunas:** Exclusão de colunas que causariam vazamento de informação (data leakage).
4.  **Limpeza dos Dados:** Tratamento de valores 'Unknown', remoção de nulos, exclusão da coluna 'CLIENTNUM' e verificação de duplicatas.
5.  **Análise de Outliers:** Identificação via regra do IQR em variáveis financeiras e de comportamento.
6.  **Preparação para Análise de Classes:** Criação da variável alvo `is_desistente` e separação entre ativos e desistentes.
7.  **Visualizações Gráficas:** Exploração de churn por idade, educação, estado civil, renda, transações e inatividade.
8.  **Preparação para o Modelo:** Codificação One-Hot (dummies) e divisão em treino/teste com estratificação.
9.  **Implementação e Teste:** Testes sistemáticos com o hiperparâmetro `n_estimators`.
10. **Avaliação Final:** Treinamento final e análise detalhada via métricas e Matriz de Confusão.

## Observações importantes

Todas as tarefas realizadas nesta etapa deverão ser registradas em formato de texto junto com suas explicações de forma a apresentar os códigos desenvolvidos e também, o código deverá ser incluído, na íntegra, na pasta "src".
