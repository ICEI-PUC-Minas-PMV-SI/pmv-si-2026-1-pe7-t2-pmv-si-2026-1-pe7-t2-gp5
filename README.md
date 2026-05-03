# Análise de Perfis de Clientes de Cartão de Crédito utilizando Técnicas de Inteligência Artificial

`CURSO: Sistemas de Informação`
`DISCIPLINA: Projeto - Pesquisa e Experimentação em Sistemas de Informação`
`SEMESTRE: 7º`

Este projeto aplica técnicas de ciência de dados e aprendizado de máquina para identificar padrões de comportamento entre clientes de cartão de crédito e prever o cancelamento do serviço (churn). A partir de variáveis relacionadas ao uso do cartão, perfil financeiro e histórico de relacionamento com a instituição, foi construído um modelo preditivo capaz de identificar clientes com maior risco de cancelamento, gerando insights que apoiam estratégias de retenção no setor financeiro.

O modelo final utiliza o algoritmo **XGBoost**, treinado sobre uma base de 7.081 clientes, e atingiu **97,36% de acurácia** e **F1-score de 0,9164** para a classe de clientes desistentes, demonstrando alta capacidade de detecção antecipada de churn.

## Integrantes

* Andre Murilo Neves Vasconcelos
* Carlos Eduardo de Lima Assis
* Déborah Thaís de Matos
* Júnio dos Reis Firmino
* Maria Eduarda Sousa
* Warley Junio Martins Vieira

## Orientador

* Neil Paiva Tizzo

---

# Planejamento

| Etapa         | Atividades |
|  :----:   | ----------- |
| ETAPA 1         |[Documentação de Contexto e levantamento dos dados](docs/contexto.md) <br> |
| ETAPA 2         |[Conhecendo os dados](docs/conhecendo-dados.md) <br> |
| ETAPA 3         |[Preparação dos dados, construção e avaliação do modelo proposto](docs/construindo-modelo.md) |
| ETAPA 4         |[Preparação dos dados, construção, avaliação e comparação dos modelos propostos](docs/construindo-modelos.md) |
| ETAPA 5         |[Implantação e apresentação da solução](docs/implantação-apresentacao.md) <br>  |

---

# Dataset

O projeto utiliza o dataset **BankChurners.csv**, disponibilizado publicamente no Kaggle sob licença de uso público.

* Fonte: [Predicting Credit Card Customer Attrition](https://www.kaggle.com/datasets/thedevastator/predicting-credit-card-customer-attrition-with-m)
* Volume original: 10.127 registros e 23 colunas
* Volume após limpeza: 7.081 registros e 22 colunas
* Variável-alvo: `Attrition_Flag` (cliente ativo ou desistente)

---

# Resultados do Modelo

| Métrica | Valor |
| ------- | ----- |
| Acurácia Geral | 97,36% |
| F1-score (Attrited Customer) | 0,9164 |
| Precisão (Attrited Customer) | 91,37% |
| Recall (Attrited Customer) | 91,92% |

---

# Colab

Notebook completo com todas as análises e treinamento do modelo:

[Abrir no Google Colab](https://colab.research.google.com/drive/121pJndHhc7jqSxwHJbIWy4_fCjM8Jpa6?usp=sharing)

---

## Instruções de utilização

Acesso em Produção (quando disponível)
* URL: https://<seu-dominio>/...
* Status: online/homologação


# Código

<li><a href="src/README.md"> Código Fonte</a></li>

# Apresentação

<li><a href="presentation/README.md"> Apresentação da solução</a></li>
