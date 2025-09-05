# SISTEMA DE RECONHECIMENTO DE IMAGENS DE PLANTAS POR MEIO DE INTELIGÊNCIA ARTIFICIAL

O objetivo deste trabalho é desenvolver um software simples e de fácil acesso capaz de identificar espécies de plantas por meio de imagens, utilizando técnicas de Inteligência Artificial (IA), em especial Redes Neurais Convolucionais (CNNs). O sistema foi treinado a partir de bases de dados públicas, como o dataset Pl@ntNet-300K (PL@NTNET, 2021) e a API da Global Biodiversity Information Facility (GBIF, s.d.). Além de auxiliar os usuários na identificação de espécies vegetais, o software busca oferecer uma experiência informativa mais completa, favorecendo a disseminação do conhecimento e contribuindo para o apoio a pesquisas acadêmicas na área de botânica e à biodiversidade.

## Desenvolvimento do Projeto

O software do projeto pode ser testado em [classifique-render](https://github.com/Hosamuel/classifique-render), onde se encontra disponível de forma pública. O sistema foi desenvolvido em **Flask**, um framework web simples e flexível, que permite ao usuário utilizar a aplicação de maneira intuitiva.  

A interface possibilita carregar uma imagem de planta, realizar o processamento por meio dos modelos previamente treinados e receber como saída as principais informações da espécie reconhecida. A navegação foi organizada para proporcionar uma experiência fluida, desde o envio da imagem até a apresentação dos resultados.  

A infraestrutura do projeto inclui:  
- **Templates HTML** (uma página inicial e uma de resultados);  
- **Folhas de estilo CSS** para definição visual;  
- **Scripts auxiliares** para processamento e análise (em especial o `predict.py`);  
- **Arquivo JSON (`new_names.json`)**, que associa a cada espécie um identificador único, nomes científicos e populares, além de links para materiais de referência como o Hortodidático da UFSC (HORTODIDÁTICO UFSC, s.d.), Reflora (REFLORA, s.d.) e o Biodiversity4all (BIODIVERSITY4ALL, s.d.).  

A aplicação, denominada **Deep Flora**, foi estruturada de forma modular, com destaque para:  
- `__init__.py`: configuração inicial da aplicação;  
- `routes.py`: gerenciamento das rotas;  
- `run.py`: execução do servidor.  

O sistema foi projetado para ser facilmente expandido, tanto em termos de modelos preditivos quanto na estrutura de dados e no visual da interface, reforçando seu potencial de aplicação em pesquisa, ensino e extensão.  

Para executar o software localmente, é necessário instalar as bibliotecas utilizadas no desenvolvimento. Recomendo criar um **ambiente virtual** antes da instalação.  
No Windows, por exemplo, utilize:  
`bash
venv\Scripts\activate
python run.py`

## Modelo Utilizado
Para construir o modelo de classificação, foi utilizada a técnica de **Transfer Learning** com base em arquiteturas pré-treinadas, o que possibilitou alcançar melhor performance mesmo com menos dados e menor tempo de treinamento. As arquiteturas selecionadas para essa tarefa foram ResNet-50, EfficientNet-B2, DenseNet-121 e MobileNetV2.  

Ao término de cada treinamento, foram registrados o tempo gasto e o tamanho final do modelo, conforme ilustrado na tabela abaixo:  
<img width="668" height="207" alt="image" src="https://github.com/user-attachments/assets/7ebeac74-9f33-43dc-a9ad-41324aef15aa" />

A ResNet-50, embora tenha alcançado as melhores métricas globais, resultou em um arquivo consideravelmente maior (93,7 MB), o que pode representar um desafio em cenários com restrição de armazenamento. Em contrapartida, a DenseNet-121 gerou um modelo de 29 MB, a EfficientNet-B2 de 33,2 MB e a MobileNetV2 de apenas 11,1 MB, sendo, portanto, a arquitetura mais compacta entre as avaliadas.  

Essa diferença evidencia um equilíbrio importante entre desempenho e eficiência: modelos mais leves, como o MobileNetV2, apresentam menor custo computacional e maior aplicabilidade em dispositivos com baixa capacidade; já modelos mais robustos, como a ResNet-50, oferecem maior acurácia e estabilidade em cenários complexos.  

Esses resultados confirmam o potencial das arquiteturas empregadas, que mantiveram elevado grau de acerto mesmo diante da diversidade morfológica e da complexidade taxonômica do conjunto de dados. A ResNet-50, no entanto, apresentou uma vantagem consistente sobre as demais, sendo selecionada como **modelo final** em função de sua superioridade nos indicadores globais.

## Desempenho da Aplicação
Apesar dos resultados positivos na análise geral, uma inspeção detalhada das métricas por classe revelou desafios importantes na classificação de espécies morfologicamente semelhantes ou com número reduzido de amostras. As dez classes com os piores desempenhos apresentaram valores de **recall inferiores a 0,40**, indicando dificuldade significativa na identificação automática dessas espécies. Esse resultado evidencia que tanto a escassez de imagens em determinadas classes quanto a elevada similaridade visual entre algumas espécies favoreceram o aumento de falsos negativos, reduzindo o desempenho nessas categorias específicas.  

Em contrapartida, determinadas espécies alcançaram elevado grau de acerto. Entre os destaques, *Adiantum raddianum* obteve recall de **0,96** e F1-score de **0,94**, enquanto *Agave parryi* e *Alliaria petiolata* superaram valores de **0,93** em F1-score. Resultados igualmente expressivos foram observados em espécies como *Arundina graminifolia* e *Anthurium andraeanum*, ambas com métricas acima de **0,90**, evidenciando a eficácia do modelo em classes com padrões morfológicos mais característicos e melhor representados no conjunto de dados.  

Como o número de classes é relativamente grande, a matriz de confusão completa mostrou-se inviável para visualização e interpretação neste trabalho. Por essa razão, optou-se por apresentar uma versão parcial, ilustrada abaixo, que evidencia os pares de espécies mais frequentemente confundidos pelo modelo.  
<img width="824" height="526" alt="image" src="https://github.com/user-attachments/assets/3506be81-4df7-4dd4-9c45-26098585fb59" />

Os dados demonstram que os erros de classificação se concentram, em grande parte, em espécies pertencentes a **gêneros próximos** ou com **morfologia altamente similar**, como observado nas confusões entre *Lamium maculatum* e *Lamium purpureum*, ou entre *Papaver orientale* e *Papaver rhoeas*. Esses casos de confusão evidenciam não apenas a dificuldade inerente do problema de distinguir espécies semelhantes, mas também as limitações do próprio conjunto de dados em fornecer exemplos suficientemente distintos para cada classe.  

Parte desses erros pode estar relacionada à qualidade, variedade e padronização das imagens, além de fatores como iluminação, ângulo de captura e estágio fenológico dos espécimes fotografados.

## Dataset
O conjunto de dados é composto por milhares de imagens de plantas, organizadas em três subconjuntos:

- **Treinamento**: Imagens usadas para treinar o modelo de classificação.
- **Validação**: Imagens para ajuste de hiperparâmetros.
- **Teste**: Imagens para avaliação final no desempenho do modelo.

Para fins de demonstração, uma pequena amostra do dataset foi incluida, com algumas categorias e uma quantidade limitada de imagens, organizadas nas mesmas subpastas de treino, validação e teste em [dataset_sample](dataset_sample).

## Informações das Plantas
O arquivo JSON com as informações das espécies de plantas está disponível para referência e consulta. Ele contém os nomes científicos e os identificadores utilizados no modelo.

- [Nomes das Plantas - plant_names.json](new_names.json).

## Referêcia

O conjunto de dados ultizados nesse projeto é o Pl@ntNet-300K e pode ser acessado no repositório Zenodo.

**Referência**: Garcin, C., Joly, A., Bonnet, P., Servajean, M., & Salmon, J. (2021). 
Pl@ntNet-300K image dataset (1.0) [Data set]. Zenodo. 
https://doi.org/10.5281/zenodo.4726653.
