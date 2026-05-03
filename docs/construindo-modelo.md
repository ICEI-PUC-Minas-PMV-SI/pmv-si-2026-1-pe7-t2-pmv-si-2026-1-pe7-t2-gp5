# Preparação dos dados

Nesta etapa, deverão ser descritas todas as técnicas utilizadas para pré-processamento/tratamento dos dados.

Algumas das etapas podem estar relacionadas à:

* Limpeza de Dados: trate valores ausentes: decida como lidar com dados faltantes, seja removendo linhas, preenchendo com médias, medianas ou usando métodos mais avançados; remova _outliers_: identifique e trate valores que se desviam significativamente da maioria dos dados.

* Transformação de Dados: normalize/padronize: torne os dados comparáveis, normalizando ou padronizando os valores para uma escala específica; codifique variáveis categóricas: converta variáveis categóricas em uma forma numérica, usando técnicas como _one-hot encoding_.

* _Feature Engineering_: crie novos atributos que possam ser mais informativos para o modelo; selecione características relevantes e descarte as menos importantes.

* Tratamento de dados desbalanceados: se as classes de interesse forem desbalanceadas, considere técnicas como _oversampling_, _undersampling_ ou o uso de algoritmos que lidam naturalmente com desbalanceamento.

* Separação de dados: divida os dados em conjuntos de treinamento, validação e teste para avaliar o desempenho do modelo de maneira adequada.
  
* Manuseio de Dados Temporais: se lidar com dados temporais, considere a ordenação adequada e técnicas específicas para esse tipo de dado.
  
* Redução de Dimensionalidade: aplique técnicas como PCA (Análise de Componentes Principais) se a dimensionalidade dos dados for muito alta.

* Validação Cruzada: utilize validação cruzada para avaliar o desempenho do modelo de forma mais robusta.

* Monitoramento Contínuo: atualize e adapte o pré-processamento conforme necessário ao longo do tempo, especialmente se os dados ou as condições do problema mudarem.

* Entre outras....

Avalie quais etapas são importantes para o contexto dos dados que você está trabalhando, pois a qualidade dos dados e a eficácia do pré-processamento desempenham um papel fundamental no sucesso de modelo(s) de aprendizado de máquina. É importante entender o contexto do problema e ajustar as etapas de preparação de dados de acordo com as necessidades específicas de cada projeto.

# Descrição do modelo

Nesta seção, o algoritmo de aprendizado de máquina selecionado para a construção do modelo de previsão de churn foi o **XGBoost (Extreme Gradient Boosting)**. Esta escolha foi justificada pela sua reconhecida alta performance em problemas de classificação tabular, eficiência no tratamento de conjuntos de dados desbalanceados (comum em cenários de churn), capacidade de regularização (L1 e L2 para prevenir overfitting) e fornecimento de importância de features para interpretabilidade. A seleção do XGBoost foi embasada por estudos de ponta na área, como os de Al-Najjar et al. (2022) e Li e Yan (2025), que demonstram a eficácia deste algoritmo na previsão de churn em contextos financeiros e bancários.

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
