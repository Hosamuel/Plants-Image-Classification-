# SISTEMA DE RECONHECIMENTO DE IMAGENS DE PLANTAS POR MEIO DE INTELIGÊNCIA ARTIFICIAL

## Introdução

O presente trabalho propõe o desenvolvimento do Deep Flora, um sistema de classificação automática de plantas a partir de imagens, utilizando datasets públicos de grande escala, como Pl@ntNet-300K (PL@NTNET, 2021) e GBIF (GBIF, s.d.). Com interface intuitiva e responsiva, a ferramenta foi projetada para atender tanto especialistas quanto o público em geral, incentivando práticas da ciência cidadã, reconhecidas por seu potencial de engajamento social e de produção de dados úteis ao monitoramento da biodiversidade e às políticas públicas (Pegler & Ranieri, 2024). Nesse contexto, esse trabalho se torna relevante para a preservação da biodiversidade, para a valorização da flora e para o fortalecimento da interação entre sociedade, ciência e natureza, cumprindo um papel relevante ao avanço tecnológico e no desenvolvimento sustentável.

## Objetivo

O objetivo deste trabalho é desenvolver um software simples e de fácil acesso capaz de identificar espécies de plantas por meio de imagens, utilizando técnicas de Inteligência Artificial (IA), em especial Redes Neurais Convolucionais (CNNs). O sistema foi treinado a partir de bases de dados públicas, como o dataset Pl@ntNet-300K (PL@NTNET, 2021) e a API da Global Biodiversity Information Facility (GBIF, s.d.). Além de auxiliar os usuários na identificação de espécies vegetais, o software busca oferecer uma experiência informativa mais completa, favorecendo a disseminação do conhecimento e contribuindo para o apoio a pesquisas acadêmicas na área de botânica e à biodiversidade.

## Dataset

O conjunto de dados utilizado neste trabalho é composto por milhares de imagens de plantas, organizadas em três subconjuntos principais:

- **Treinamento**: imagens usadas para treinar o modelo de classificação;  
- **Validação**: imagens destinadas ao ajuste de hiperparâmetros;  
- **Teste**: imagens reservadas para a avaliação final do desempenho do modelo.  

Os dados foram obtidos a partir de plataformas amplamente reconhecidas, como o **Zenodo** e a **API da GBIF** (Global Biodiversity Information Facility). Após um extenso processo de tratamento, balanceamento e Data Augmentation, foi gerado um novo dataset consolidado para o desenvolvimento deste trabalho, disponível para consulta no seguinte link: [Google Drive](https://drive.google.com/file/d/10p8soon1274GFD5O5IhWtsNmaaHc8bhY/view?usp=sharing).  

A distribuição das imagens pode ser verificada na figura abaixo, sendo a quantidade mínima de imagens por classe 402. Esse balanceamento foi fundamental para reduzir o impacto de classes sub-representadas e melhorar a robustez do modelo.
<p align= "center"> <img width="776" height="447" alt="image" src="https://github.com/user-attachments/assets/4fabeb97-b083-4e41-9254-389b9c6a594e" /> </p>

## Informações das Plantas
O arquivo JSON com as informações das espécies de plantas está disponível para referência e consulta. Ele contém os nomes científicos e os identificadores utilizados no modelo.

- [Nomes das Plantas - plant_names.json](https://github.com/Hosamuel/Plants-Image-Classification-/blob/main/new_names.json).
  
## Modelo Utilizado
Para construir o modelo de classificação, foi utilizada a técnica de **Transfer Learning** com base em arquiteturas pré-treinadas, o que possibilitou alcançar melhor performance mesmo com menos dados e menor tempo de treinamento. As arquiteturas selecionadas para essa tarefa foram ResNet-50, EfficientNet-B2, DenseNet-121 e MobileNetV2.  

Ao término de cada treinamento, foram registrados o tempo gasto e o tamanho final do modelo, conforme ilustrado na tabela abaixo:  
<p align= "center"> <img width="668" height="207" alt="image" src="https://github.com/user-attachments/assets/7ebeac74-9f33-43dc-a9ad-41324aef15aa" /> </p>

A ResNet-50, embora tenha alcançado as melhores métricas globais, resultou em um arquivo consideravelmente maior (93,7 MB), o que pode representar um desafio em cenários com restrição de armazenamento. Em contrapartida, a DenseNet-121 gerou um modelo de 29 MB, a EfficientNet-B2 de 33,2 MB e a MobileNetV2 de apenas 11,1 MB, sendo, portanto, a arquitetura mais compacta entre as avaliadas.  

Essa diferença evidencia um equilíbrio importante entre desempenho e eficiência: modelos mais leves, como o MobileNetV2, apresentam menor custo computacional e maior aplicabilidade em dispositivos com baixa capacidade; já modelos mais robustos, como a ResNet-50, oferecem maior acurácia e estabilidade em cenários complexos.  

Esses resultados confirmam o potencial das arquiteturas empregadas, que mantiveram elevado grau de acerto mesmo diante da diversidade morfológica e da complexidade taxonômica do conjunto de dados. A ResNet-50, no entanto, apresentou uma vantagem consistente sobre as demais, sendo selecionada como **modelo final** em função de sua superioridade nos indicadores globais.

Todos os modelos gerados neste projeto e os respectivos scripts de treinamento estão disponíveis nos links abaixo:  
- [Modelos treinados (Google Drive)](https://drive.google.com/file/d/1n7WrpIGYccOEzOGY4OMCl2QL7J44aGbx/view?usp=sharing)  
- [Scripts de treinamento (GitHub)](https://github.com/Hosamuel/plant-training-scripts) 

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

Para executar o software localmente, é necessário instalar as bibliotecas utilizadas no desenvolvimento. Recomendo criar um ambiente virtual antes da instalação.  
No Windows, por exemplo, utilize:  
```bash
venv\Scripts\activate```
```python run.py```

## Desempenho da Aplicação

Apesar dos resultados positivos na análise geral, uma inspeção detalhada das métricas por classe revelou desafios importantes na classificação de espécies morfologicamente semelhantes ou com número reduzido de amostras. As dez classes com os piores desempenhos apresentaram valores de **recall inferiores a 0,40**, indicando dificuldade significativa na identificação automática dessas espécies. Esse resultado evidencia que tanto a escassez de imagens em determinadas classes quanto a elevada similaridade visual entre algumas espécies favoreceram o aumento de falsos negativos, reduzindo o desempenho nessas categorias específicas.  

Em contrapartida, determinadas espécies alcançaram elevado grau de acerto. Entre os destaques, *Adiantum raddianum* obteve recall de **0,96** e F1-score de **0,94**, enquanto *Agave parryi* e *Alliaria petiolata* superaram valores de **0,93** em F1-score. Resultados igualmente expressivos foram observados em espécies como *Arundina graminifolia* e *Anthurium andraeanum*, ambas com métricas acima de **0,90**, evidenciando a eficácia do modelo em classes com padrões morfológicos mais característicos e melhor representados no conjunto de dados.  

Como o número de classes é relativamente grande, a matriz de confusão completa mostrou-se inviável para visualização e interpretação neste trabalho. Por essa razão, optou-se por apresentar uma versão parcial, ilustrada abaixo, que evidencia os pares de espécies mais frequentemente confundidos pelo modelo.  
<p align= "center"> <img width="824" height="526" alt="image" src="https://github.com/user-attachments/assets/3506be81-4df7-4dd4-9c45-26098585fb59" /> </p>

Os dados demonstram que os erros de classificação se concentram, em grande parte, em espécies pertencentes a **gêneros próximos** ou com **morfologia altamente similar**, como observado nas confusões entre *Lamium maculatum* e *Lamium purpureum*, ou entre *Papaver orientale* e *Papaver rhoeas*. Esses casos de confusão evidenciam não apenas a dificuldade inerente do problema de distinguir espécies semelhantes, mas também as limitações do próprio conjunto de dados em fornecer exemplos suficientemente distintos para cada classe.  

Parte desses erros pode estar relacionada à qualidade, variedade e padronização das imagens, além de fatores como iluminação, ângulo de captura e estágio fenológico dos espécimes fotografados.

## Resultados

A avaliação quantitativa dos modelos ResNet-50, EfficientNet-B2, DenseNet-121 e MobileNetV2 evidenciou desempenhos distintos na tarefa de classificação de espécies vegetais, conforme sintetizado na tabela abaixo.  
<p align= "center"> <img width="601" height="152" alt="image" src="https://github.com/user-attachments/assets/f3c82890-13d3-4b82-93f3-1e89443be8ea" /> </p>

O modelo ResNet-50 destacou-se como a arquitetura de melhor desempenho, alcançando valores ponderados (*weighted average*) de precisão = 0,85, recall = 0,84 e F1-score = 0,84. A EfficientNet-B2 apresentou métricas globais próximas, com precisão = 0,81, recall = 0,80 e F1-score = 0,80, confirmando sua competitividade, embora com leve perda em relação à ResNet-50.  

### Aplicação desenvolvida

Além dos resultados quantitativos, a pesquisa resultou em entregas tecnológicas de caráter prático e acessível. O principal produto desenvolvido foi uma aplicação web protótipo, denominada **Deep Flora**, que permite a identificação de espécies vegetais a partir do upload de imagens.  

A interface foi projetada para ser simples, responsiva e compatível com diferentes dispositivos e navegadores, possibilitando o uso em campo por pesquisadores, estudantes e cidadãos interessados.  
A figura abaixo ilustra as principais etapas de utilização da aplicação:  
- envio da imagem;  
- apresentação da classificação sugerida pelo modelo e dos resultados probabilísticos;  
- disponibilização de links externos para aprofundamento do conhecimento sobre a espécie reconhecida (descrições botânicas, imagens complementares e mapas de distribuição geográfica).  

<p align= "center"> <img width="852" height="342" alt="image" src="https://github.com/user-attachments/assets/ad7ab691-e759-487a-9d00-b9fd36583001" /> </p>

### Potencial de aplicação

O sistema foi concebido para aplicações práticas de baixo custo, podendo ser explorado em atividades educativas, em projetos de monitoramento da biodiversidade e como apoio em iniciativas de agricultura sustentável.  

A simplicidade da interface garante acessibilidade a diferentes perfis de usuários, enquanto os links externos asseguram maior confiabilidade das informações fornecidas.

## Conclusão

O projeto **Deep Flora** mostrou que é possível utilizar técnicas de *Deep Learning* para a identificação de plantas a partir de imagens, alcançando bons resultados mesmo com a alta diversidade morfológica e a complexidade taxonômica do conjunto de dados. Entre os modelos testados, a ResNet-50 foi a que apresentou melhor desempenho, com precisão, recall e F1-score em torno de 0,85, sendo definida como o modelo final da aplicação.  

Além dos testes e métricas, o trabalho resultou na criação de uma aplicação web protótipo, capaz de classificar automaticamente 487 espécies vegetais e apresentar informações adicionais, como nome científico, nome popular e links de referência. Essa ferramenta foi pensada para ser simples, responsiva e acessível, podendo ser usada em diferentes cenários, como apoio ao ensino, monitoramento da biodiversidade, agricultura sustentável e práticas de ciência cidadã.  

Mesmo com as limitações encontradas como a dificuldade em espécies com poucas imagens ou morfologicamente muito semelhantes, os resultados confirmam a eficiência da abordagem e abrem espaço para melhorias futuras, como ampliar o dataset, refinar os modelos e adaptar a aplicação para versões móveis.  

O Deep Flora reforça como a Inteligência Artificial pode apoiar a conservação da biodiversidade e tornar o conhecimento botânico mais acessível para pesquisadores, estudantes e para o público em geral.

## Referêcia

BIODIVERSITY4ALL. Plataforma de ciência cidadã. [s.l.], [s.d.]. Disponível em: 
https://www.biodiversity4all.org/. Acesso em: 17 ago. 2025.

GLOBAL BIODIVERSITY INFORMATION FACILITY (GBIF). Global Biodiversity 
Information Facility: free and open access to biodiversity data. [s.l.], [s.d.]. Disponível em: 
https://www.gbif.org/. Acesso em: 17 ago. 2025. 

HORTODIDÁTICO UFSC. Hortodidático – Plantas Medicinais. Universidade Federal de Santa Catarina, [s.d.]. Disponível em:
http://hortodidatico.ufsc.br/. Acesso em: 17 ago. 2025.

PEGLER, G. F.; RANIERI, V. E. L. Ciência cidadã em áreas protegidas: boas práticas para 
formulação e implementação de projetos. Ambiente & Sociedade, v. 27, p. 1–20, 2024. DOI: 
https://doi.org/10.1590/1809-4422asoc01521vu27L4AO.

PL@NTNET-300K. Pl@ntNet-300K: A plant image dataset with high label ambiguity. Zenodo, 
2021. DOI: https://doi.org/10.5281/zenodo.5645731. 

REFLORA. Projeto Reflora – Flora do Brasil 2020. Jardim Botânico do Rio de Janeiro, [s.d.]. 
Disponível em: http://reflora.jbrj.gov.br/. Acesso em: 17 ago. 2025.
