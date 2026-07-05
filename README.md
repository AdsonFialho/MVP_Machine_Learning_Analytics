# (MVP) Machine Learning & Analytics: Segmentação de Clientes por Clusterização 
**Nome:** Adson Fialho Marques  
**Matrícula:** 4052025002646

Este repositório contém o MVP (Minimum Viable Product) desenvolvido para a sprint
**Machine Learning & Analytics** do curso de Pos-Graduação em Ciência de Dados e Analytics pela PUC-RIO. 
O trabalho aplica técnicas de aprendizado não supervisionado para identificar perfis de clientes de um distribuidor
atacadista a partir de seus padrões de gasto.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/AdsonFialho/MVP_Machine_Learning_Analytics/blob/main/MVP_Machine_Learning_Analytics_(4052025002646).ipynb)

## Objetivo

Identificar, sem rótulos prévios, grupos de clientes com comportamentos de compra
semelhantes, de forma a apoiar decisões de marketing e operação. Trata-se de um problema
de **clusterização**, em que o objetivo é descobrir a estrutura natural dos dados, e não
prever um valor ou categoria conhecida.

## Dataset

- **Nome:** Wholesale customers
- **Fonte:** UCI Machine Learning Repository -> [Link do Dataset](https://archive.ics.uci.edu/dataset/292/wholesale+customers)
- **Registros:** 440 clientes
- **Atributos:** 6 variáveis numéricas de gasto anual (Fresh, Milk, Grocery, Frozen,
  Detergents_Paper e Delicassen), além de duas variáveis categóricas de contexto
  (Channel e Region).
- **Licença:** Creative Commons Attribution 4.0 International (CC BY 4.0).

As variáveis Channel e Region não foram utilizadas na modelagem. O **Channel** (tipo de
cliente: Horeca ou Varejo) foi reservado como rótulo externo para validar os grupos
encontrados; o **Region** foi descartado por ser uma informação geográfica que não
descreve o comportamento de compra.

O dataset é carregado diretamente no notebook por meio de uma URL pública (arquivo raw
hospedado neste repositório), de modo que o notebook executa do início ao fim sem
necessidade de upload manual, login ou configuração local.

## Metodologia

O projeto segue o fluxo completo de um trabalho de Machine Learning:

1. **Definição do problema** — contexto, objetivo, tipo de tarefa e hipóteses.
2. **Análise exploratória (EDA)** — estatísticas descritivas, distribuições, correlações
   e identificação de assimetria e outliers.
3. **Preparação dos dados** — transformação logarítmica (para reduzir a forte assimetria)
   e padronização (para equalizar as escalas), organizadas em um pipeline reprodutível.
4. **Modelagem** — comparação entre um modelo baseline e dois modelos candidatos.
5. **Otimização de hiperparâmetros** — busca sistemática em dois dos modelos.
6. **Avaliação e interpretação** — análise dos grupos formados e validação externa.
7. **Conclusão** — fechamento conectando os resultados ao objetivo inicial.

## Modelos avaliados

- **K-Means** (baseline) — número de grupos definido pelo método do elbow e pelo
  silhouette score.
- **DBSCAN** (candidato) — agrupamento por densidade.
- **Clusterização hierárquica / Agglomerative** (candidato) — agrupamento aglomerativo.

## Métricas de avaliação

Por se tratar de um problema não supervisionado, foram utilizadas métricas próprias de
clusterização:

- **Silhouette score** — mede a coesão e a separação dos grupos.
- **Índice Davies-Bouldin** — métrica interna complementar.
- **Adjusted Rand Score** — validação externa, comparando os grupos formados com a
  variável Channel (que não participou da modelagem).

## Principais resultados

- O **K-Means com dois grupos** foi selecionado como solução final, por reunir bom
  desempenho e maior simplicidade e interpretabilidade.
- Os dois grupos encontrados correspondem a perfis de negócio claros: um voltado a
  alimentos frescos e congelados (perfil Horeca) e outro a mercearia, laticínios e
  produtos de limpeza (perfil Varejo).
- A validação externa mostrou forte correspondência com o Channel real (cerca de 86% dos
  clientes agrupados de forma coerente com seu canal), confirmando que os grupos capturam
  uma estrutura real do negócio.
- O DBSCAN não se mostrou adequado a este conjunto de dados, mesmo após otimização — um
  resultado que reforça a lição de que a escolha do algoritmo depende do formato dos dados
  e de que nenhuma métrica interna deve ser interpretada isoladamente.

## Tecnologias utilizadas

- Python 3
- pandas, numpy
- scikit-learn
- matplotlib, seaborn
- Ambiente de desenvolvimento: Google Colab

## Como executar

O notebook foi desenvolvido no Google Colab e pode ser executado do início ao fim sem
configuração adicional. O dataset é carregado automaticamente a partir da URL pública,
não sendo necessário nenhum upload manual.

## Estrutura do repositório

- `Wholesale_customers_dataset.csv` — base de dados utilizada.
- `MVP_Machine_Learning_Analytics_(4052025002646).ipynb` — Notebook de desenvolvimento completo do projeto.
- `README.md` — este arquivo.
