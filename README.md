# Segmentação de Clientes e Previsão de Faturamento (LTV) em E-commerce

🌐 *[Click here for the English version](README-en.md)*

Este projeto foi desenvolvido para resolver um desafio clássico do comércio eletrônico: entender o comportamento dos clientes e prever quanto eles vão gastar no futuro. Com essas informações, uma empresa consegue economizar recusrsos com campanhas gerais e passa a focar nos clientes certos.

A solução foi dividida em duas partes:
1. **Agrupamento (Clusterização):** Identificar o perfil dos clientes atuais.
2. **Previsão (Regressão):** Tentar prever o faturamento de cada cliente nos próximos 3 meses.

---

## 🛠️ Como o Projeto foi Desenvolvido

O projeto foi construído passo a passo seguindo uma linha lógica de análise de dados:

### 1. Limpeza e Preparação dos Dados
Os dados brutos continham transações de um e-commerce do Reino Unido. Nesta etapa:
* Foram removidos registros sem identificação de cliente.
* Compras canceladas ou devolvidas foram analisadas e corrigidas para não distorcer o faturamento real.

### 2. Criação de Novas Variáveis (Modelo RFM)
Para entender o cliente, as milhares de linhas de notas fiscais foram condensadas em 3 indicadores principais para cada pessoa:
* **Recência (R):** Há quantos dias foi a última compra.
* **Frequência (F):** Quantas vezes o cliente comprou na loja.
* **Monetário (M):** O total de dinheiro que o cliente já gastou.

### 3. Agrupamento de Clientes (K-Means)
Por meio do algoritmo K-Means, a base de clientes foi dividida em grupos com comportamentos similares. Para encontrar o número ideal de grupos, foi utilizada uma técnica visual chamada **Método do Cotovelo** e assim prosseguiu-se à análise da distribuição dos centroides (o "cliente típico" de cada grupo).

### 4. Previsão de LTV (Machine Learning com XGBoost)
Para testar se seria possível prever o gasto futuro dos clientes nos 3 meses seguintes, o período total do dataset de cerca de 12 meses foi dividido em duas partes: o modelo foi treinado com um período de 9 meses e o resultado testado nos meses finais (evitando que o modelo conhecesse os dados futuros a serem previstos antes da hora).

Houve dois grandes problemas do mundo real: muitos clientes não compraram nada no futuro (gerando muitos zeros) e alguns poucos clientes compraram valores extremamente altos. 
Modelos tradicionais como Regressão Linear e Random Forest falharam, então a solução final foi usar o algoritmo **XGBoost com configuração Tweedie**, que é uma técnica específica do mercado para lidar com as dificuldades desse tipo de base de dados.

---

## 📊 Principais Descobertas e Resultados

### Os 3 Perfis de Clientes Identificados:
* **Grupo Top:** Clientes que compram muito, com alta frequência e de forma muito recente. Devem receber atenção e atendimento exclusivo.
* **Grupo Intermediário:** Clientes que compram de vez em quando. Precisam de estímulos (cupons, recomendações) para virarem Tops.
* **Grupo Inativo:** Clientes que gastaram pouco e não compram há muito tempo. Campanhas agressivas de reconquista podem ser aplicadas aqui.

### O Resultado do Modelo de Previsão:
O modelo final conseguiu sair do zero e pontuar um $R^2$ positivo de **0.0554**. Isso significa que, mesmo o comportamento humano sendo muito imprevisível em compras livres, o modelo conseguiu capturar inteligência real sobre o negócio. 
O gráfico de importância de variáveis provou que o histórico **Monetário** do cliente é o fator que mais pesa para prever o seu gasto futuro.

## Visualizações Geradas no Projeto:

### Agrupamentos:

![Visualização dos Clusters](images/grafico_pairplot.png)

![Gráfico de Centroides](images/grafico_centroides.png)

![Método do Cotovelo](images/grafico_cotovelo.png)

### Distribuições:

![Gráfico das Distribuições sem Tratamento](images/grafico_distribuicoes.png)

![Variáveis Normalizadas](images/grafico_normalizadas.png)

### Feature Importances:

![Importância das Variáveis](images/grafico_importancias.png)

---

## 🧠 Conclusão e Aprendizados

Este projeto demonstrou que os dados do mundo real são complexos e raramente seguem padrões perfeitos. O principal neste projeto foi entender por que os modelos iniciais falharam e conseguir aplicar uma solução avançada (Tweedie Loss) para domar as distorções causadas pelos clientes que mais gastam e pelo excesso de zeros na base.

Como próximos passos para melhorar o modelo, seria interessante criar novas variáveis, como as categorias de produtos mais comprados por cada cliente, além de investigar outros possíveis modelos e suas configurações.

---

## 📁 Estrutura do Repositório

* `images/`: Gráficos gerados durante as análises.
* `Projeto_LTV_e_Segmentação.ipynb`: Notebook com todo o código Python desenvolvido.
* `requirements.txt`: Lista de bibliotecas necessárias para rodar o código.
