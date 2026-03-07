# Introdução

O avanço das tecnologias de análise de dados e da Inteligência Artificial (IA) tem transformado a forma como as organizações analisam informações e conduzem seus processos de decisão. A IA pode ser compreendida como um conjunto de sistemas capazes de processar grandes volumes de dados, identificar padrões, estabelecer correlações e apoiar a tomada de decisão em diferentes contextos organizacionais (YU et al., 2024). Nesse sentido, seu uso ultrapassa a automação de tarefas, passando a ocupar papel estratégico no apoio a decisões em níveis operacionais, táticos e estratégicos.

Esse movimento é particularmente relevante em setores intensivos em informação, como o financeiro, no qual a velocidade das transações, a diversidade de perfis de clientes e a complexidade dos comportamentos de consumo exigem métodos analíticos cada vez mais robustos. Estudos recentes apontam que a IA vem sendo aplicada de forma crescente em operações, marketing, finanças e gestão estratégica, tanto como ferramenta de suporte à decisão quanto como mecanismo automatizado de análise e resposta (YU et al., 2024). No setor bancário, por sua vez, a aplicação de técnicas de aprendizado de máquina e redes neurais tem se destacado na identificação de padrões suspeitos, na análise de transações em tempo real e na prevenção de fraudes financeiras, evidenciando o potencial da IA para ampliar a segurança e a eficiência das operações (TOSTA; DIAS, 2025).

A literatura mostra, portanto, que a utilização de IA no setor financeiro não se limita à detecção de irregularidades. As mesmas bases conceituais que sustentam sistemas de prevenção a fraudes também podem ser adaptadas para compreender padrões de comportamento, segmentar perfis de clientes e gerar subsídios para estratégias de relacionamento e retenção. Em outras palavras, se a IA é capaz de reconhecer anomalias em transações bancárias, ela também pode ser aplicada para identificar regularidades, perfis de uso e características comportamentais em bases de clientes, contribuindo para análises mais refinadas e para a geração de conhecimento estratégico.

Diante desse cenário, este projeto propõe investigar como técnicas de aprendizado de máquina podem ser utilizadas para identificar padrões em dados de clientes de cartão de crédito, contribuindo para a segmentação de perfis de usuários e para a compreensão do comportamento de consumo no setor financeiro. A proposta está alinhada tanto com a literatura sobre o uso organizacional da IA na tomada de decisão (YU et al., 2024) quanto com estudos que evidenciam a eficácia de métodos baseados em IA para análise de grandes volumes de dados financeiros (TOSTA; DIAS, 2025).

## Problema

Instituições financeiras enfrentam o desafio constante de compreender o comportamento de seus clientes e identificar sinais que indiquem mudanças no relacionamento com seus serviços. No caso específico de clientes de cartão de crédito, fatores como redução na frequência de uso, alterações no padrão de consumo, variações no limite utilizado e mudanças no perfil financeiro podem indicar risco de cancelamento, queda no engajamento ou transformação no perfil de relacionamento com a instituição.

A dificuldade em identificar esses padrões de forma antecipada pode resultar em perda de clientes, diminuição de receitas e aumento de custos associados à aquisição de novos usuários. Além disso, o crescimento das transações digitais e o aumento da complexidade das operações financeiras ampliam a necessidade de métodos automatizados capazes de analisar grandes volumes de dados e reconhecer comportamentos relevantes em tempo hábil. Segundo Tosta e Dias (2025), a IA tem sido aplicada com sucesso no contexto bancário justamente por sua capacidade de identificar padrões suspeitos e processar dados em larga escala, o que demonstra seu potencial para apoiar análises financeiras mais complexas.

Sob outra perspectiva, Yu et al. (2024) destacam que a IA tem sido progressivamente incorporada aos processos decisórios organizacionais como instrumento de apoio à análise, à classificação e à recomendação. Isso indica que técnicas de aprendizado de máquina podem ser empregadas não apenas para detectar eventos anômalos, mas também para compreender regularidades, relações entre variáveis e agrupamentos de perfis em bases de clientes. Dessa forma, torna-se relevante investigar métodos que permitam identificar características comuns entre clientes de cartão de crédito e compreender melhor os diferentes perfis existentes na base analisada.

Assim, o problema central deste estudo consiste em entender como técnicas de aprendizado de máquina podem ser utilizadas para identificar padrões comportamentais e segmentar clientes de cartão de crédito com base em atributos demográficos, financeiros e de relacionamento, gerando informações úteis para análises estratégicas no setor financeiro.

## Questão de pesquisa

De que forma técnicas de aprendizado de máquina podem ser utilizadas para identificar padrões e realizar a segmentação de clientes de cartão de crédito com base em características demográficas, financeiras e comportamentais presentes no conjunto de dados analisado?

## Objetivos preliminares

Explorar e aplicar modelos de aprendizado de máquina para identificar padrões e segmentar clientes de cartão de crédito com base nas características presentes no conjunto de dados selecionado.

### Objetivos específicos

- Realizar uma análise exploratória do conjunto de dados, identificando características, padrões e possíveis inconsistências nos dados disponíveis.
- Investigar diferentes abordagens de aprendizado de máquina que possam ser aplicadas para segmentação ou classificação de clientes com base em seus atributos.
- Comparar o desempenho de diferentes técnicas de modelagem para compreender quais abordagens apresentam melhores resultados no contexto do problema analisado.
- Relacionar os resultados obtidos à literatura sobre uso da IA em processos decisórios organizacionais e em análises no setor financeiro.
- Avaliar de que forma os padrões identificados podem contribuir para a compreensão do comportamento de clientes e para a geração de insights estratégicos.

## Justificativa

A análise do comportamento de clientes no setor financeiro é um tema amplamente estudado devido ao impacto direto que a retenção e o engajamento de clientes têm sobre a sustentabilidade das instituições financeiras. Estratégias de segmentação e análise de comportamento tornam-se fundamentais para compreender perfis de clientes e apoiar decisões relacionadas a marketing, relacionamento e desenvolvimento de produtos financeiros.

Com o crescimento do volume de dados disponíveis nas organizações, técnicas de ciência de dados e aprendizado de máquina passaram a ser amplamente utilizadas para extrair conhecimento desses dados e apoiar processos de tomada de decisão. A inteligência artificial tem sido empregada em diversas áreas organizacionais para apoiar gestores na análise de dados e na identificação de padrões relevantes para decisões estratégicas, táticas e operacionais (YU et al., 2024).

Nesse contexto, a análise de padrões de uso, histórico de transações e perfil dos clientes pode fornecer informações relevantes para identificar diferentes perfis de consumidores e apoiar estratégias de relacionamento. Métodos de aprendizado de máquina permitem analisar grandes conjuntos de dados e identificar relações entre variáveis que contribuem para uma compreensão mais aprofundada do comportamento dos usuários.

O conjunto de dados escolhido para este projeto contém informações relevantes sobre clientes de cartão de crédito, incluindo variáveis relacionadas ao perfil do cliente, nível de utilização do cartão, histórico de transações e relacionamento com a instituição financeira. Esses dados permitem explorar diferentes abordagens analíticas e aplicar técnicas de aprendizado de máquina para compreender melhor os padrões existentes na base de clientes.

Além disso, a investigação deste problema possui relevância acadêmica e prática, pois contribui para o entendimento de como métodos de ciência de dados podem ser aplicados para apoiar análises no setor financeiro, auxiliando na identificação de perfis de clientes e na geração de insights estratégicos.

## Público-Alvo

Os resultados deste estudo podem beneficiar diferentes perfis de profissionais e áreas de atuação relacionadas ao setor financeiro e à análise de dados.

Entre os principais grupos que podem se beneficiar da investigação estão:
* Analistas de dados e cientistas de dados, interessados em compreender como técnicas de aprendizado de máquina podem ser aplicadas para análise de comportamento de clientes.
* Profissionais do setor financeiro, especialmente aqueles envolvidos em áreas de relacionamento com clientes, marketing e gestão de produtos financeiros.
* Gestores e tomadores de decisão, que podem utilizar insights derivados da análise de dados para apoiar estratégias de retenção e segmentação de clientes.
* Pesquisadores e estudantes da área de Sistemas de Informação e Ciência de Dados, que buscam compreender aplicações práticas de aprendizado de máquina em problemas reais de negócio.

# Estado da Arte

A literatura recente tem investigado como a **Inteligência Artificial (IA)** vem sendo utilizada para apoiar processos de **tomada de decisão nas organizações**, especialmente em áreas como operações, marketing, finanças e gestão estratégica. Diversos estudos analisam aplicações de IA em contextos organizacionais, avaliando os **tipos de problemas abordados, os dados utilizados, os algoritmos empregados e os resultados obtidos**.

Nesta seção, são apresentados estudos relevantes que investigam o uso de **Inteligência Artificial em processos decisórios organizacionais**, destacando seus **métodos, métricas e principais resultados**.

---

## Estudo 1 – Yu et al. (2024)
### Problema e contexto
O estudo investiga como a Inteligência Artificial está sendo utilizada no processo de tomada de decisão dentro das organizações. O objetivo principal foi mapear aplicações de IA em diferentes áreas funcionais das empresas, identificando em quais contextos a IA atua como sistema de suporte à decisão ou como tomadora automática de decisões. A pesquisa analisa a adoção da IA em processos organizacionais, considerando diferentes níveis de decisão: estratégico, tático e operacional.

### Dados utilizados (Dataset)
O estudo utilizou dados secundários provenientes de diversas fontes públicas, incluindo relatórios de empresas, publicações especializadas e estudos de caso sobre aplicações de Inteligência Artificial. Ao todo, foram analisados 128 casos de uso de IA em organizações, coletados a partir de buscas em fontes online e literatura especializada. Esses casos foram classificados segundo área funcional da empresa, setor econômico, nível de decisão e papel da IA no processo decisório. 

### Abordagem e algoritmos
A pesquisa adotou uma abordagem qualitativa e exploratória, utilizando um método de classificação baseado em teorias de tomada de decisão organizacional. Os casos de uso foram categorizados segundo quatro dimensões principais:
* Área funcional da organização
* Área de decisão específica
* Nível de decisão (estratégico, tático ou operacional)
* Papel da IA (tomadora de decisão ou suporte à decisão)

Esse processo permitiu construir um mapa decisório das aplicações de IA nas organizações, possibilitando identificar padrões de adoção da tecnologia em diferentes setores e níveis decisórios.

### Métricas de avaliação
A análise foi realizada por meio de classificação e comparação dos casos de uso segundo diferentes dimensões organizacionais. As métricas utilizadas envolveram principalmente análises de frequência e distribuição das aplicações de IA por:
* setor econômico
* área funcional
* tipo de decisão (automatizada ou assistida)
* nível de decisão organizacional

Essa abordagem permitiu identificar padrões de adoção e concentração de aplicações de IA em determinadas áreas das organizações.

### Resultados e conclusões
Os resultados indicaram que a maior parte das aplicações de Inteligência Artificial ocorre nas áreas de Operações e Marketing, especialmente no nível operacional das organizações. Aproximadamente 67% dos casos analisados estavam relacionados à área de operações, evidenciando forte utilização da IA para otimização de processos produtivos e operacionais. 
Além disso, o estudo identificou dois padrões principais de utilização da IA:
* Decision Support Systems (DSS): sistemas que auxiliam humanos na tomada de decisão.
* Decision Makers (DM): sistemas que tomam decisões automaticamente sem intervenção humana.

Os autores concluem que a IA tem ampliado principalmente a eficiência de decisões operacionais, criando novas possibilidades de automação e apoio à gestão organizacional. Contudo, destacam que a pesquisa possui limitações relacionadas ao tamanho da amostra e à natureza exploratória do estudo, sugerindo a ampliação futura do mapeamento de aplicações de IA.

### O que levantar (mínimo 5 trabalhos)
Para **cada estudo encontrado** aderente à temática do grupo, registre de forma objetiva:
* Problema e contexto: que problema o trabalho buscou resolver e em qual domínio/cenário foi aplicado.
* Dados (dataset): origem, tamanho, período, variáveis/atributos, pré-processamentos relevantes (faltantes, balanceamento, normalização).
* Abordagem/algoritmos: algoritmos utilizados e parâmetros principais (quando informados).
* Métricas de avaliação: quais e por quê (ex.: Acurácia, F1, AUC, RMSE, MAE, etc.).
* Resultados: principais números, comparações internas, limitações citadas e conclusões.

* Texto-síntese crítico (2–4 parágrafos) respondendo:
- O que os estudos concordam? Onde divergem?
- Quais lacunas permanecem (dados, métricas, cenários, limitações técnicas/éticas)?
- Como seu projeto se alinha aos estudos identificados?

**Dica:** Prefira artigos dos últimos 5 anos ou referências clássicas indispensáveis.

### Ferramentas inteligentes permitidas
Você pode utilizar: Perplexity, SciSpace, Elicit, Research Rabbit, Litmaps.
Use-as para descoberta, organização e triagem de literatura. 

**Atenção:** 
* Sempre acesse a fonte original (PDF/artigo) antes de citar; verifique números e conclusões.
* Registre DOI/URL oficial e dados bibliográficos completos.
* Evite “alucinações” das ferramentas: desconfie de referências sem DOI ou que você não consiga localizar oficialmente.
* Use as ferramentas inteligentes para mapear redes de citação (Research Rabbit), mapas de tópicos (Litmaps), filtrar por período e gerar resumos iniciais (Perplexity/SciSpace/Elicit).
* Leia os trabalhos mais promissores e descarte estudos fora de escopo.

> **Links Úteis**:
> - [Google Scholar](https://scholar.google.com/)
> - [IEEE Xplore](https://ieeexplore.ieee.org/Xplore/home.jsp)
> - [Science Direct](https://www.sciencedirect.com/)
> - [ACM Digital Library](https://dl.acm.org/)

# Descrição do _dataset_ selecionado

Nesta seção, apresente uma visão clara e objetiva do dataset selecionado, incluindo:
* Identificação e origem – Nome, link de acesso, fonte (instituição, repositório, API etc.) e licença de uso.
* Visão geral – Total de registros e atributos, período coberto e breve contextualização.
* Atributos – Tabela com nome, descrição, tipo, unidade de medida (se aplicável) e exemplos de valores.
* Qualidade dos dados – Presença de valores faltantes, inconsistências, duplicatas ou outliers.

**Dica:** Seja objetivo, mas inclua detalhes suficientes para que outra pessoa possa entender e reutilizar o conjunto de dados sem buscar informações extras.

# Canvas analítico

Nesta seção, você deverá estruturar e preencher o seu Canvas Analítico, que tem como objetivo registrar a organização das ideias e apresentar o modelo de negócio do projeto.

O Canvas deve ser preenchido integralmente, mesmo que algumas informações ainda não estejam totalmente definidas. Nessa etapa inicial, é aceitável trabalhar com hipóteses ou estimativas, desde que sejam coerentes com o problema e o contexto definidos.

**Dica:** O Canvas Analítico serve como guia visual para alinhar expectativas e direcionar o desenvolvimento. Ele poderá (e deverá) ser revisitado e atualizado ao longo do projeto.

> **Links Úteis**:
> - [Modelo do Canvas Analítico](https://github.com/ICEI-PUC-Minas-PMV-SI/PesquisaExperimentacao-Template/blob/main/help/Software-Analtics-Canvas-v1.0.pdf)

# Vídeo de apresentação da Etapa 01

Nesta etapa, o grupo deverá produzir um vídeo de 5 a 8 minutos apresentando o trabalho realizado, no qual cada integrante deve dizer seu nome e apresentar uma parte do conteúdo desenvolvido, garantindo que todos participem ativamente da gravação. A ausência de participação de qualquer membro resultará em penalização na nota final desta etapa. Recomenda-se que o grupo elabore previamente um roteiro para organizar a ordem das falas, distribuir o tempo de forma equilibrada e assegurar que todos os tópicos relevantes sejam apresentados de maneira clara e objetiva.

# Referências

YU, Abraham Sin Oih et al. Tomada de decisão nas organizações: o que muda com a inteligência artificial? Estudos Avançados, São Paulo, v. 38, n. 111, p. 327–348, maio/ago. 2024. Disponível em: https://doi.org/10.1590/s0103-4014.202438111.017
. Acesso em: 6 mar. 2026.

Tosta, P. L. M., & Dias, J. C. (2025). Detecção de fraudes em transações bancárias utilizando inteligência artificial. Revista processando o saber, 17(01), 21–37. https://doi.org/10.5281/zenodo.15477217 Acesso em: 7 mar. 2026.

Inclua todas as referências (livros, artigos, sites, etc) utilizados no desenvolvimento do trabalho utilizando o padrão ABNT.

> **Links Úteis**:
> - [Padrão ABNT PUC Minas](https://portal.pucminas.br/biblioteca/index_padrao.php?pagina=5886)
