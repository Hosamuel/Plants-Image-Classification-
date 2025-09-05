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

Para executar o software localmente, é necessário instalar as bibliotecas utilizadas no desenvolvimento. Recomenda-se criar um **ambiente virtual** antes da instalação.  
No Windows, por exemplo, utilize:  
```bash
venv\Scripts\activate
python run.py


## Modelo Utilizado
Para construir o modelo de classificação, foi utilizada a técnica de **Transfer Learning** com base em uma arquitetura pré-treinada, permitindo uma melhor performance mesmo com menos dados e menos tempo de treinamento. A arquitetura escolhida foi:

- **Arquitetura Base**:  ResNet50 e o modelo gerado foi: [model.pth](model.pth).
- **Pesos Pré-Treinados**: [weights.pth](weights.pth).

Os pesos do modelo foram ajustados para identificar espécies de plantas, adaptando as camadas finais para a classificação específica das classes do conjunto de dados.

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
