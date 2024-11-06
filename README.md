# Plants Image Classification

Este projeto tem como objetivo criar um modelo de **classificação de imagens de plantas**. Usando um conjunto de dados extenso e diversificado, o sistema é projetado para reconhecer uma ampla variedade de espécies de plantas, o que pode ser útil em áreas como botânica, agricultura e estudos ambientais.

## Desenvolvimento do Projeto
O projeto está em aberto e em fase de aprimoramento. Os resultados iniciais indicam uma evolução significativa a cada atualização realizada. Contudo, novas análises e otimizações serão necessárias para melhorar a **eficiência** do modelo.

## Modelo Utilizado
Para construir o modelo de classificação, foi utilizada a técnica de **Transfer Learning** com base em uma arquitetura pré-treinada, permitindo uma melhor performance mesmo com menos dados e menos tempo de treinamento. A arquitetura escolhida foi:

- **Arquitetura Base**:  ResNet50 ([model.pth](model.pth))
- **Pesos Pré-Treinados**: [weights.pth](weights.pth)

Os pesos do modelo foram ajustados para identificar espécies de plantas, adaptando as camadas finais para a classificação específica das classes do conjunto de dados.

## Dataset
O conjunto de dados é composto por milhares de imagens de plantas, organizadas em três subconjuntos:

- **Treinamento**: Imagens usadas para treinar o modelo de classificação.
- **Validação**: Imagens para ajuste de hiperparâmetros e prevenção de overfitting.
- **Teste**: Imagens para avaliação final do desempenho do modelo.

Para fins de demonstração, uma pequena amostra do dataset foi incluida, com algumas categorias e uma quantidade limitada de imagens, organizadas nas mesmas subpastas de treino, validação e teste.

## Informações das Plantas
O arquivo JSON com as informações das espécies de plantas está disponível para referência e consulta. Ele contém os nomes científicos e os identificadores utilizados no modelo. Você pode baixá-lo aqui:

- [Nomes das Plantas - plant_names.json](link_para_o_json)
