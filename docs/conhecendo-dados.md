# Conhecendo os dados

Nesta seção, deverá ser registrada uma detalhada análise descritiva e exploratória sobre a base de dados selecionada na Etapa 1 com o objetivo de compreender a estrutura dos dados, detectar eventuais _outliers_ e também, avaliar/detectar as relações existentes entre as variáveis analisadas.
Para isso, sugere-se que sejam utilizados cálculos de medidas de tendência central, como média, mediana e moda, para entender a centralidade dos dados; sejam exploradas medidas de dispersão como desvio padrão e intervalos interquartil para avaliar a variabilidade dos dados; sejam utilizados gráficos descritivos como histogramas e box plots, para representar visualmente as características essenciais dos dados, pois essas visualizações podem facilitar a identificação de padrões e anomalias; sejam analisadas as relações entre as variáveis por meio de análise de correlação, gráficos de dispersões, mapas de calor, entre outras técnicas. 
Inclua nesta seção, gráficos, tabelas, trechos de código e demais artefatos que você considere relevantes para entender os dados com os quais você irá trabalhar.  Além disso, inclua e comente os trechos de código mais relevantes desenvolvidos para realizar suas análises. Na pasta "src", inclua o código fonte completo.

## Descrição dos achados

### Visão geral do dataset

O dataset utilizado — *BankChurners.csv* — contém originalmente 10.127 registros e 23 colunas, abrangendo informações demográficas, financeiras e comportamentais de clientes de cartão de crédito. Após a etapa de limpeza, na qual foram removidos registros com valores "Unknown" nas colunas `Education_Level`, `Marital_Status` e `Income_Category`, além da exclusão da coluna identificadora `CLIENTNUM`, o dataset ficou com **7.081 registros e 22 colunas**, sem linhas duplicadas.

### Desbalanceamento de classes

A variável-alvo `Attrition_Flag` apresenta um claro desbalanceamento: a grande maioria dos registros corresponde a clientes ativos (*Existing Customer*), enquanto os clientes que cancelaram (*Attrited Customer*) representam uma parcela significativamente menor. Esse desbalanceamento é um ponto de atenção importante para a etapa de modelagem, pois pode enviesar algoritmos de classificação em favor da classe majoritária.

![Distribuição de clientes por status](img/Gráfico-Distribuição-Por-Classe.png)

### Perfil demográfico e sua relação com o churn

**Nível educacional:** A distribuição por escolaridade é bastante similar entre clientes ativos e desistentes. Em ambos os grupos, as categorias *Graduate* e *High School* concentram o maior volume de clientes, o que indica que o nível de educação, isoladamente, não é um fator diferenciador forte para o cancelamento.

![Nível de educação por classe](img/Grafico-Nivel-Educacao.png)

**Faixa etária:** A distribuição de idades segue um padrão próximo da normal em ambos os grupos, com concentração entre 40 e 55 anos. Não foram observadas diferenças significativas na centralidade ou dispersão das idades entre clientes ativos e desistentes, sugerindo que a idade por si só não é determinante para o churn.

![Idade dos clientes por classe](img/Gráfico-Idade-Clientes-ativos.png)

**Estado civil:** Casados e solteiros dominam ambos os grupos de forma proporcional. Assim como na escolaridade, o estado civil não revelou um padrão diferenciador relevante entre as classes.

![Estado civil por classe](img/Gráfico-Estado-Civil-Por-Classe.png)

**Faixa de renda:** A categoria *Less than $40K* é a mais frequente nos dois grupos. A proporção entre as faixas de renda permanece relativamente estável entre ativos e desistentes, indicando que a renda declarada não é, sozinha, um preditor forte de cancelamento.

![Renda por classe](img/Grafico-Renda-Por-Classe.png)

### Variáveis comportamentais — principais diferenciadores

As variáveis que mais revelaram diferenças entre os grupos foram aquelas relacionadas ao **comportamento transacional** dos clientes:

**Volume de transações (`Total_Trans_Ct`):** O boxplot e o histograma mostram uma separação clara entre os grupos. Clientes ativos apresentam uma mediana de transações consideravelmente maior do que os desistentes. No histograma, observa-se que a distribuição dos desistentes concentra-se em faixas mais baixas de transações, enquanto os ativos se distribuem por faixas mais altas. Isso sugere que a **queda no uso do cartão é um dos sinais mais fortes de propensão ao cancelamento**.

![Total de transações por classe](img/Grafico-Total-de-Transação-Por-Classe.png)

![Histograma de uso do cartão por grupo](img/Gráfico-Hisograma-Do-Uso-De-Cartão.png)

**Inatividade nos últimos 12 meses (`Months_Inactive_12_mon`):** O boxplot revela que clientes desistentes tendem a apresentar mais meses de inatividade do que os ativos. A mediana do grupo desistente é ligeiramente superior, e a dispersão indica que períodos prolongados sem uso do cartão estão correlacionados com maior probabilidade de churn.

![Inatividade dos clientes por grupo](img/Gráfico-Inatividade-Dos-Clientes-Por-Grupo.png)

### Taxa de churn por categoria de cartão

A análise da taxa de cancelamento por tipo de cartão (*Blue*, *Silver*, *Gold*, *Platinum*) mostra que a proporção de churn é relativamente similar entre as categorias. O cartão *Blue*, por ser o mais popular, concentra o maior volume absoluto tanto de ativos quanto de desistentes. Essa uniformidade indica que a categoria do cartão não é, por si só, um fator determinante para o cancelamento.

![Taxa de desistência por tipo de cartão](img/Gráfico-Taxa-De-Desistencia-Por-Tipo-De-Cartão-De-Crédito.png)

### Síntese dos achados

Em resumo, os achados mais relevantes da análise exploratória são:

- O dataset é **desbalanceado**, com predominância de clientes ativos, o que demandará técnicas de balanceamento na fase de modelagem.
- **Variáveis demográficas** (idade, escolaridade, estado civil e renda) apresentaram distribuições proporcionalmente similares entre os dois grupos, sem diferenças marcantes que as qualifiquem como preditores isolados de churn.
- As **variáveis comportamentais** se mostraram as mais discriminativas: clientes desistentes apresentam menor volume de transações e maior período de inatividade, configurando os sinais mais claros de propensão ao cancelamento.
- A **categoria do cartão** não demonstrou influência significativa sobre a taxa de churn.

Esses achados reforçam a importância de monitorar o **engajamento transacional** dos clientes como estratégia de prevenção ao cancelamento.

## Ferramentas utilizadas

O projeto foi desenvolvido inteiramente em **Python**, utilizando o ambiente **Google Colab** para execução e prototipação do código. As principais bibliotecas empregadas foram:

- **Pandas** — manipulação, limpeza e transformação dos dados tabulares. Utilizada para leitura do CSV, remoção de registros inconsistentes, agrupamentos e cálculo de estatísticas descritivas (`describe()`, `value_counts()`, `crosstab()`).
- **Matplotlib** — criação dos gráficos estáticos. Foi a biblioteca principal para a geração de histogramas, boxplots e gráficos de barras que comparam os grupos de clientes ativos e desistentes.
- **Seaborn** — complemento ao Matplotlib para visualizações estatísticas com estilização aprimorada.
- **NumPy** — suporte a operações numéricas e vetorizadas utilizadas internamente pelas demais bibliotecas.
- **KaggleHub** — download automatizado do dataset diretamente da plataforma Kaggle, garantindo reprodutibilidade na coleta dos dados.
