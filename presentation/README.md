# Apresentação da Solução

### Resumo Executivo do Projeto

O projeto desenvolvido consistiu na criação e implementação de uma solução completa de Machine learning voltada para a previsão de *churn* de clientes. Dessa fora, a aplicação foi estruturada de forma a integrar um modelo preditivo robusto a uma infraestrutura de nuvem escalável e de baixo custo.
Assim, a solução engloba os seguintes pilares:
* **Modelo Preditivo:** Utilização do algoritmo **XGBoost** para realizar inferências rápidas e precisas sobre a probabilidade de perda de clientes.
* **Backend e API:** Desenvolvimento de uma API em **Python utilizando Flask**, responsável por receber os dados, aplicar as transformações necessárias para o pipeline de Machine Learning, acionar o modelo preditivo e responder imediatamente com a probabilidade de churn através da rota `/api/predict`.
* **Arquitetura na Nuvem (Microsoft Azure):** Hospedagem da API através do **Azure App Service** em ambiente Linux contínuo, evitando problemas de *Cold Start*, e com a interface do usuário disponibilizada via **Azure Static Web Apps**. 

### Vídeo de Apresentação Final
* **Acesso Online:** O vídeo de apresentação está disponível através do link: [Vídeo de Apresentação da Solução](https://drive.google.com/file/d/1fNITHzowEchIthecmPaW2VGUq6HqnHj4/view?usp=drive_link).
