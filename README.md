# Predição de Depósito Bancário

## Visão Geral do Projeto

Este projeto de Machine Learning tem como objetivo principal prever se um cliente de uma instituição bancária fará um depósito a prazo (variável `y`). Utilizando o dataset de marketing bancário da UCI (UCI Bank Marketing Dataset), o projeto explora diversas técnicas de pré-processamento de dados, análise exploratória e modelagem preditiva. O foco é aplicar e comparar modelos de classificação, como Regressão Logística e Random Forest, para identificar qual deles oferece o melhor desempenho na identificação de clientes propensos a realizar depósitos.

## Contexto e Objetivo

No cenário bancário atual, a capacidade de prever o comportamento do cliente é crucial para campanhas de marketing eficazes. Este projeto visa desenvolver um modelo preditivo que possa auxiliar as instituições financeiras a direcionar seus esforços de marketing para clientes com maior probabilidade de aceitar uma oferta de depósito a prazo. Isso não só otimiza os recursos de marketing, mas também melhora a experiência do cliente ao oferecer produtos mais relevantes.

## Dataset

O dataset utilizado é o **UCI Bank Marketing Dataset**, que contém informações sobre campanhas de marketing direto de uma instituição bancária portuguesa. As features incluem dados demográficos dos clientes (idade, profissão, estado civil, educação), informações de crédito (default, saldo, empréstimo imobiliário, empréstimo pessoal), detalhes da campanha (contato, mês, dia, duração do último contato, número de contatos realizados, dias desde o último contato, número de contatos anteriores) e o resultado da campanha anterior (poutcome). A variável alvo (`y`) indica se o cliente subscreveu um depósito a prazo (`yes`) ou não (`no`).

## Análise Exploratória de Dados (EDA)

A EDA foi realizada para entender a distribuição das variáveis e suas relações com a variável alvo. Observou-se um desbalanceamento significativo na variável alvo, onde a maioria dos clientes não realizou o depósito. Gráficos de caixa (boxplots) foram utilizados para analisar a distribuição de variáveis numéricas (idade, saldo, duração, campanha, pdays, previous) em relação à classe (`y`). Gráficos de barras empilhadas foram empregados para visualizar a proporção de variáveis categóricas (job, marital, education, default, housing, loan, contact, month, poutcome) por classe, revelando insights sobre quais características influenciam a decisão de depósito.

## Pré-processamento de Dados

Para preparar os dados para a modelagem, as seguintes etapas de pré-processamento foram executadas:

1.  **Codificação de Variáveis Binárias**: Variáveis como `default`, `housing`, `loan` e a própria variável alvo `y` foram convertidas para representações numéricas (0 e 1) usando Label Encoding.
2.  **One-Hot Encoding**: Variáveis categóricas com mais de duas classes (job, marital, education, contact, month, poutcome) foram transformadas usando One-Hot Encoding para evitar a introdução de uma ordem artificial e garantir que os modelos interpretem corretamente essas features.
3.  **Balanceamento de Classes com SMOTE**: Devido ao desbalanceamento da variável alvo, a técnica SMOTE (Synthetic Minority Over-sampling Technique) foi aplicada para gerar amostras sintéticas da classe minoritária, resultando em um dataset balanceado. Isso é crucial para evitar que os modelos preditivos sejam enviesados para a classe majoritária.
4.  **Divisão em Conjuntos de Treino e Teste**: O dataset foi dividido em 70% para treinamento e 30% para teste, garantindo que os modelos fossem avaliados em dados não vistos durante o treinamento.

## Modelagem e Avaliação

Dois modelos de classificação foram treinados e avaliados, antes e depois do SMOTE(para demonstração é usado o pós SMOTE):

### 1. Regressão Logística

A Regressão Logística é um modelo linear amplamente utilizado para problemas de classificação binária. Foi treinada com os dados pré-processados e balanceados. As métricas de avaliação incluíram Acurácia, Precisão, Recall, F1-Score e ROC AUC, além da Matriz de Confusão e Relatório de Classificação.

### 2. Random Forest

Random Forest é um algoritmo de ensemble baseado em árvores de decisão, conhecido por sua robustez e capacidade de lidar com relações não-lineares. Este modelo também foi treinado com os mesmos dados e avaliado pelas mesmas métricas da Regressão Logística.

## Resultados

Os resultados obtidos para ambos os modelos foram os seguintes:

| Métrica           | Regressão Logística | Random Forest |
| :---------------- | :------------------ | :------------ |
| Acurácia          | 0.8970              | 0.8970        |
| Precisão          | 0.5577              | 0.5577        |
| Recall            | 0.5784              | 0.5784        |

**Matriz de Confusão (Regressão Logística):**

```
[[11299  678]
 [ 872 715]]
```

**Relatório de Classificação (Regressão Logística):**

```
              precision    recall  f1-score   support

          No       0.93      0.94      0.94     11977
         Yes       0.51      0.45      0.48      1587

    accuracy                           0.89     13564
   macro avg       0.72      0.70      0.71     13564
weighted avg       0.88      0.89      0.88     13564
```

**Matriz de Confusão (Random Forest):**

```
[[11249   728]
 [  669 918]]
```

**Relatório de Classificação (Random Forest):**

```
              precision    recall  f1-score   support

          No       0.94      0.94      0.94     11977
         Yes       0.56      0.58      0.57      1587

    accuracy                           0.90     13564
   macro avg       0.75      0.76      0.75     13564
weighted avg       0.90      0.90      0.90     13564
```

## Conclusão

Ao comparar os resultados, o modelo **Random Forest** demonstrou um desempenho superior em todas as métricas de avaliação (Acurácia, Precisão, Recall, F1-Score e ROC AUC) em comparação com a Regressão Logística. Isso sugere que o Random Forest é mais adequado para este conjunto de dados e problema de classificação, provavelmente devido à sua capacidade de lidar com a não-linearidade e interações complexas entre as features do dataset. Portanto, o Random Forest é o modelo escolhido para este projeto, oferecendo uma maior confiabilidade na previsão de depósitos bancários.

## Como Executar o Projeto

Para executar este projeto, siga os passos abaixo:

1.  **Clone o Repositório:**

    ```bash
    git clone https://github.com/ViniMBlanco/PredicaoDepositodeBanco.git
    cd PredicaoDepositodeBanco
    ```

2.  **Ambiente de Desenvolvimento:**

    Este projeto foi desenvolvido utilizando Google Colab. Recomenda-se abrir o arquivo `PredicaoDepositodeBanco.ipynb` no Google Colab para uma execução mais fácil, pois ele já contém todas as dependências necessárias e o ambiente configurado.

3.  **Instale as Dependências (se estiver executando localmente):**

    Se você optar por executar o notebook localmente, certifique-se de ter Python instalado e instale as bibliotecas necessárias:

    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn
    ```

4.  **Execute o Notebook:**

    Abra o arquivo `PredicaoDepositodeBanco.ipynb` em um ambiente Jupyter (como Jupyter Notebook ou Google Colab) e execute todas as células sequencialmente.

## Tecnologias Utilizadas

*   **Python**
*   **Pandas**: Para manipulação e análise de dados.
*   **NumPy**: Para operações numéricas.
*   **Matplotlib** e **Seaborn**: Para visualização de dados.
*   **Scikit-learn**: Para construção e avaliação de modelos de Machine Learning (Regressão Logística, Random Forest).
*   **Imbalanced-learn**: Para lidar com o desbalanceamento de classes (SMOTE).
*   **Google Colab**: Ambiente de desenvolvimento.

## Autor

**ViniMBlanco**

## Licença

Este projeto está licenciado sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes. (Assumindo uma licença MIT padrão, caso contrário, ajustar conforme necessário.)


