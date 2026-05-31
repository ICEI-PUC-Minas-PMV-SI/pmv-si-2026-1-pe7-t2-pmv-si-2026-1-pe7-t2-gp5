# Preparação dos dados

Nesta etapa foram aplicadas técnicas de pré-processamento com o objetivo de garantir a qualidade da base utilizada no treinamento e comparação dos modelos de aprendizado de máquina propostos no projeto.

A base utilizada foi composta pelos dados de clientes do banco, contendo informações demográficas, comportamentais e financeiras relacionadas ao uso do cartão de crédito. 

As atividades realizadas incluíram:

* **Limpeza de dados:** foi realizada a verificação de registros inconsistentes e análise da presença de valores ausentes. A base apresentou boa integridade, exigindo apenas ajustes pontuais e validação das colunas utilizadas no processo de treinamento.

* **Transformação de dados:** variáveis categóricas foram convertidas para formato numérico, permitindo o processamento pelos algoritmos. Também foi realizada padronização dos atributos quando necessário, tornando as variáveis comparáveis entre si.

* **Feature engineering:** foram avaliados os atributos mais relevantes para a previsão de cancelamento, considerando seu impacto no comportamento do cliente e sua contribuição para o desempenho dos modelos.

* **Tratamento de dados desbalanceados:** considerando a diferença entre clientes ativos e clientes cancelados, foi analisada a distribuição das classes para garantir que os modelos fossem capazes de identificar corretamente os casos de evasão.

* **Separação de dados:** a base foi dividida em conjuntos de treinamento e teste, permitindo avaliar o desempenho dos modelos em dados ainda não utilizados no treinamento.

* **Validação cruzada:** foram realizados testes de validação para reduzir risco de sobreajuste e melhorar a confiabilidade dos resultados.

# Descrição dos modelos

Com os dados preparados, foram selecionados três algoritmos supervisionados para comparação de desempenho no problema de classificação de clientes com risco de cancelamento.

## Regressão Logística

A Regressão Logística é um algoritmo supervisionado utilizado em problemas de classificação binária. Seu objetivo é estimar a probabilidade de determinado evento ocorrer, classificando cada registro entre duas categorias possíveis.

Principais vantagens:

* simplicidade de implementação;
* baixo custo computacional;
* facilidade de interpretação dos resultados;
* bom desempenho em bases estruturadas e problemas de classificação binária.

Como limitação, pode apresentar menor capacidade de identificar relações mais complexas entre variáveis quando comparada a algoritmos baseados em árvores.

A escolha foi realizada por ser um modelo clássico de classificação, amplamente utilizado como base de comparação e adequado ao objetivo do projeto de prever o cancelamento de clientes.

## Random Forest

O Random Forest é um algoritmo baseado em múltiplas árvores de decisão. Seu funcionamento consiste em criar diversas árvores durante o treinamento e combinar suas previsões para gerar um resultado final.

Principais vantagens:

* boa capacidade de generalização;
* redução do risco de overfitting em comparação com árvores isoladas;
* capacidade de lidar bem com grande quantidade de atributos;
* facilidade de interpretação relativa sobre importância das variáveis.

Como limitação, pode apresentar maior custo computacional quando comparado a modelos mais simples.

A escolha foi realizada por ser um modelo consolidado em problemas de classificação e por apresentar bom desempenho em conjuntos de dados estruturados semelhantes ao deste projeto.

## XGBoost

O XGBoost é um algoritmo de boosting que constrói árvores sequencialmente, corrigindo os erros identificados nas etapas anteriores.

Principais vantagens:

* alto desempenho preditivo;
* boa capacidade de aprendizado em padrões complexos;
* controle mais refinado por meio de hiperparâmetros;
* robustez em problemas de classificação tabular.

Como limitação, exige maior cuidado na configuração dos parâmetros e pode aumentar a complexidade do treinamento.

A escolha ocorreu por seu bom desempenho em problemas de churn prediction e por sua capacidade de melhorar a classificação dos clientes com maior risco de cancelamento.

Durante os testes foram realizados ajustes de parâmetros buscando equilíbrio entre desempenho e capacidade de generalização.


# Avaliação dos modelos criados

## Métricas utilizadas

### Acurácia

Mede o percentual total de previsões corretas realizadas pelos modelos.

Os resultados obtidos foram:

* **Regressão Logística:** 90,47%
* **Random Forest:** 94,35%
* **XGBoost:** 97,36%

Os resultados mostram evolução progressiva entre os modelos avaliados, com destaque para o XGBoost, que apresentou maior percentual de classificações corretas.

### Precisão

Indica quantos clientes classificados como possíveis cancelamentos realmente pertencem à classe de evasão.

Resultados obtidos:

* **Regressão Logística:** 0,76
* **Random Forest:** 0,91
* **XGBoost:** 0,9137

Os resultados mostram desempenho próximo entre Random Forest e XGBoost, ambos acima do modelo inicial.

### Recall

Mede a capacidade do modelo de encontrar clientes que efetivamente apresentam risco de cancelamento.

Resultados obtidos:

* **Regressão Logística:** 0,57
* **Random Forest:** 0,71
* **XGBoost:** 0,9192

O XGBoost apresentou maior capacidade de identificar clientes com risco real de evasão, reduzindo a chance de deixar casos importantes sem classificação.

### F1-Score

Combina precisão e recall, oferecendo uma visão equilibrada da qualidade do modelo.

Resultados obtidos:

* **Regressão Logística:** 0,65
* **Random Forest:** 0,80
* **XGBoost:** 0,9164

Esse resultado reforçou a consistência do XGBoost em relação aos demais modelos.

### Matriz de confusão

Permitiu visualizar acertos e erros de classificação entre clientes ativos e cancelados.

Os resultados observados foram:

**Regressão Logística**

* Verdadeiros negativos: 1611
* Falsos positivos: 41
* Falsos negativos: 153
* Verdadeiros positivos: 204

**Random Forest**

* Verdadeiros negativos: 1640
* Falsos positivos: 12
* Falsos negativos: 102
* Verdadeiros positivos: 255

**XGBoost**

* Verdadeiros negativos: 1621
* Falsos positivos: 31
* Falsos negativos: 29
* Verdadeiros positivos: 328

Ao analisar a matriz de confusão, o principal destaque foi a redução dos falsos negativos obtida pelo XGBoost, resultado importante para o objetivo do projeto.

## Discussão dos resultados obtidos

Principais observações:

* melhora na capacidade de prever cancelamentos;
* melhor equilíbrio entre precisão e recall;
* redução de erros de classificação;
* maior capacidade de identificação de clientes com tendência de evasão.

A Regressão Logística apresentou desempenho satisfatório como modelo inicial de comparação, com boa capacidade geral de classificação. O Random Forest apresentou resultados superiores e maior estabilidade no processo de classificação. Já o XGBoost apresentou os melhores indicadores entre todos os modelos avaliados, com maior acurácia, melhor recall e melhor F1-score.

Os resultados obtidos atenderam ao objetivo definido no projeto e responderam à questão de pesquisa relacionada à possibilidade de prever clientes com maior risco de cancelamento com base no histórico analisado.


# Pipeline de pesquisa e análise de dados

O pipeline seguiu um conjunto organizado e replicável de processos, desde a definição do problema até a avaliação comparativa dos modelos implementados nesta etapa.

**0. Especificação do problema:** identificar padrões comportamentais em clientes de cartão de crédito que indicam risco de cancelamento, com base na questão de pesquisa definida na Etapa 1: *"De que forma técnicas de aprendizado de máquina podem ser utilizadas para identificar padrões e realizar a segmentação de clientes de cartão de crédito com base em características demográficas, financeiras e comportamentais?"* O trabalho teve `Attrition_Flag` como variável-alvo e F1-score como métrica principal de avaliação.

**1. Coleta dos dados:** dataset *BankChurners.csv* baixado do Kaggle via `kagglehub`, garantindo reprodutibilidade na coleta.

**2. Análise exploratória (EDA):** compreensão da estrutura, estatísticas descritivas numéricas e categóricas, visualização de distribuições e análise de outliers via IQR.

**3. Remoção de colunas:** exclusão de `CLIENTNUM` (identificador sem valor preditivo) e das colunas Naive Bayes (causariam *data leakage*).

**4. Limpeza dos dados:** remoção de registros com valores `"Unknown"` selecionada com base em comparação empírica entre três estratégias via validação cruzada, verificação de nulos e duplicatas.

**5. Análise de outliers:** identificação via regra do IQR nas variáveis financeiras e comportamentais, com decisão de manutenção justificada.

**6. Preparação para modelagem:** criação da variável-alvo `is_desistente`, codificação One-Hot das variáveis categóricas e divisão estratificada em treino (70%) e teste (30%), feita uma única vez.

**7. Tratamento do desbalanceamento:** uso de `scale_pos_weight` para penalizar erros na classe minoritária durante o treinamento.

**8. Treinamento dos modelos:** com a base preparada, foram implementados os algoritmos de Regressão Logística, Random Forest e XGBoost. Dessa forma, foi possível comparar os modelos em condições equivalentes.

**9. Geração das previsões:** após o treinamento, cada modelo foi aplicado ao conjunto de teste para classificação dos clientes entre ativos e com risco de cancelamento.

**10. Avaliação final:** os resultados foram analisados por meio de acurácia, precisão, recall, F1-score e matriz de confusão. Com isso, foi possível comparar os desempenhos e identificar o modelo com melhor resultado para o objetivo do projeto.
