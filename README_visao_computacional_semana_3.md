# Recomendação de Produtos por Similaridade Visual

Este projeto implementa um protótipo de busca e recomendação de produtos visualmente semelhantes utilizando embeddings extraídos por uma CNN pré-treinada.

Autores: Ana Carolina Dutra Ramos, Camila Gois de Jesus e Guilherme Magalhães Júnior.

## Notebook

- `Visão_Computacional_Desafio_Semana_3_(aula).ipynb`

## Objetivo

Dada uma imagem de produto, o sistema retorna as cinco imagens mais semelhantes. O fluxo também aceita uma imagem externa que não fazia parte do conjunto original.

## Dataset

O notebook baixa do Kaggle o Mini Product Image and Text Dataset e utiliza 44.441 imagens armazenadas em `/content/data`.

As imagens são redimensionadas para `256 × 256`. O dataset não está incluído neste repositório e seu download exige uma conta e credenciais válidas do Kaggle.

## Metodologia

1. leitura e redimensionamento das imagens;
2. extração de características com EfficientNetB0 pré-treinada no ImageNet;
3. remoção da cabeça de classificação e uso de global average pooling;
4. geração de embeddings com 1.280 dimensões;
5. agrupamento exploratório com K-Means em 20 clusters;
6. visualização bidimensional com t-SNE;
7. cálculo de similaridade cosseno;
8. recuperação das cinco imagens mais próximas.

## Resultados registrados

- Embeddings gerados: `(44.441, 1.280)`;
- clusters exploratórios: 20;
- recomendações exibidas para uma imagem interna e uma imagem externa;
- a busca interna apresentou boa coerência visual na avaliação qualitativa dos autores;
- na imagem externa, algumas recomendações foram influenciadas principalmente pela cor vermelha, mesmo quando a categoria visual não era tão semelhante.

O notebook não possui rótulos de relevância ou uma métrica quantitativa de recomendação. Os resultados são avaliados visualmente.

## Como executar com segurança

1. Configure as credenciais do Kaggle fora do notebook, usando variável de ambiente ou `~/.kaggle/kaggle.json`.
2. Nunca grave tokens diretamente no código.
3. Instale as dependências:

```bash
pip install jupyter tensorflow kaggle scikit-learn pandas numpy matplotlib pillow opencv-python
```

4. Disponibilize a imagem externa como `/content/Imagem_blusa.jpg` ou ajuste o caminho.
5. Execute o notebook em ambiente com bastante RAM; t-SNE e K-Means sobre 44 mil embeddings são operações custosas.

## Limitações e melhorias

- A avaliação é apenas qualitativa.
- Cor e fundo podem dominar a similaridade sem representar equivalência semântica.
- O índice da imagem externa está fixado em `44441` e depende do tamanho exato do dataset.
- O notebook modifica o array global de embeddings ao adicionar a imagem externa.
- t-SNE sobre todo o conjunto pode ser lento e consumir muita memória.
- Para produção, recomenda-se usar FAISS ou outro índice vetorial, normalizar embeddings e avaliar Precision@K ou Recall@K.
- Podem ser comparados EfficientNet, ResNet50, MobileNetV2 e DenseNet121.

## Segurança

O notebook original contém uma credencial do Kaggle diretamente em uma célula. Ela deve ser removida e revogada antes da publicação. O README não contém essa credencial.

## Tecnologias

Python, TensorFlow/Keras, EfficientNetB0, scikit-learn, Kaggle API, NumPy, pandas e Matplotlib.

## Licença

Nenhuma licença foi definida. Verifique os termos do dataset e do ImageNet antes de redistribuir dados ou artefatos.
