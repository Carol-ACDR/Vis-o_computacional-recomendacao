# Recomendação de produtos por similaridade visual

Projeto do Grupo 7 para o Desafio da Semana 3 da unidade de Visão Computacional da Residência em Inteligência Artificial.

O sistema recebe uma foto de produto e retorna as cinco imagens visualmente mais próximas no catálogo. A consulta pode usar uma foto do próprio catálogo ou uma imagem externa.

## Como funciona

1. O notebook baixa as 44.441 imagens do catálogo de moda, redimensiona cada uma para 256 × 256 pixels e a converte para tons de cinza. [Mini Fashion Product Images and Text Dataset](https://www.kaggle.com/datasets/nirmalsankalana/mini-product-image-and-text-dataset)
2. Cinco CNNs com pesos pré-treinados no ImageNet geram vetores de características por meio de `GlobalAveragePooling2D`. Os modelos são ResNet50, EfficientNetB0, MobileNetV2, VGG19 e InceptionV3.
3. O KNN compara os vetores usando distância cosseno, euclidiana ou de correlação. O notebook testa as 15 combinações na consulta interna e usa VGG19 com distância cosseno na consulta externa.
4. Cada resultado usa a mesma ordem de arquivos da extração dos vetores. Os painéis exibem as imagens originais em cores, com o nome do arquivo e a distância ao lado de cada recomendação.

## Como executar no Colab

1. Baixe o [notebook do projeto](Desafio_Semana_3_Grupo7.ipynb) e importe-o no Google Colab.
2. Selecione um ambiente de execução com GPU para acelerar a extração dos vetores.
3. Para testar uma imagem externa, envie um arquivo `Teste2.jpg` ao ambiente do Colab ou atualize o caminho na variável `imagem_teste_externa`.
4. Execute todas as células em ordem. O notebook baixa o catálogo pelo KaggleHub e os pesos pré-treinados pelo TensorFlow.

## Resultados

| Consulta | Resultado observado |
| --- | --- |
| Saia jeans (`10001.jpg`) | As 15 combinações retornaram cinco saias jeans. Alguns arquivos diferentes mostraram peças visualmente quase idênticas. |
| Tênis (`Teste2.jpg`) | A VGG19 retornou cinco calçados, entre modelos esportivos e casuais, com distâncias cosseno de 0,137 a 0,163. |

O notebook inclui os gráficos salvos da execução no Colab.

## Tecnologias

Python, TensorFlow/Keras, scikit-learn, NumPy, pandas, Matplotlib e KaggleHub.

## Equipe

Ana Carolina Dutra, Camila Gois de Jesus e Guilherme Magalhães Junior.  
Professor: Matheus Vanzan.
