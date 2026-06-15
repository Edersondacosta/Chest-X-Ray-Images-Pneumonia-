# EfficientNet-B0

## Descrição

Este experimento utiliza a arquitetura **EfficientNet-B0** pré-treinada na base ImageNet para a classificação binária de radiografias de tórax em duas classes:

* NORMAL
* PNEUMONIA

A estratégia adotada foi o **Transfer Learning**, mantendo as camadas convolucionais congeladas e treinando apenas o classificador final.

Este experimento corresponde ao **Experimento 5** do artigo e apresentou o melhor desempenho entre todos os modelos avaliados.

---

## Arquitetura Utilizada

Foi empregada a arquitetura EfficientNet-B0 pré-treinada na ImageNet.

A camada classificadora original foi substituída por uma nova estrutura composta por:

* Camada Linear com 128 neurônios;
* Função de ativação ReLU;
* Duas camadas de Dropout com taxa de 0,5;
* Camada de saída com duas classes.

As camadas convolucionais da EfficientNet-B0 permaneceram congeladas durante o treinamento.

---

## Estratégia de Transfer Learning

Neste experimento:

* Todas as camadas convolucionais da EfficientNet-B0 foram congeladas;
* Apenas o classificador final foi treinado;
* Foram utilizados pesos pré-treinados da ImageNet para extração das características das imagens.

Essa estratégia permite aproveitar características previamente aprendidas em grandes bases de dados, reduzindo o tempo de treinamento e melhorando a capacidade de generalização.

---

## Hiperparâmetros

| Parâmetro               |            Valor |
| ----------------------- | ---------------: |
| Learning Rate           |            0.001 |
| Batch Size              |               64 |
| Número máximo de épocas |               30 |
| Dropout                 |              0.5 |
| Otimizador              |             Adam |
| Função de perda         | CrossEntropyLoss |
| Early Stopping          |              Sim |

---

## Base de Dados

Foi utilizada a base:

**Chest X-Ray Images (Pneumonia)**

Disponível em:

https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia

As imagens pertencem às classes:

* NORMAL
* PNEUMONIA

---

# Como Executar no Google Colab

## 1. Montar o Google Drive

```python
from google.colab import drive

drive.mount('/content/drive')
```

---

## 2. Obter a chave da API do Kaggle

No Kaggle, acesse:

```text
Account → Create New Token
```

Será baixado o arquivo:

```text
kaggle.json
```

Faça o upload para o Colab:

```python
from google.colab import files

files.upload()
```

---

## 3. Configurar a API do Kaggle

```python
!mkdir ~/.kaggle

!cp kaggle.json ~/.kaggle/

!chmod 600 ~/.kaggle/kaggle.json
```

---

## 4. Baixar a base de dados

```python
!kaggle datasets download paultimothymooney/chest-xray-pneumonia
```

---

## 5. Descompactar os arquivos

```python
!unzip chest-xray-pneumonia.zip
```

---

## 6. Abrir o notebook

Abra:

```text
EfficientNet_B0.ipynb
```

---

## 7. Executar todas as células

Ao final do treinamento serão gerados automaticamente os modelos treinados, curvas de treinamento e métricas de avaliação.

---

## Arquivos Gerados

Durante a execução do notebook são criados:

```text
experimento_5/
│
├── best_model.pth
├── checkpoint.pth
├── accuracy_curve.png
├── loss_curve.png
├── confusion_matrix.png
└── classification_report.txt
```

---

## Resultados Obtidos

| Métrica   |   Valor |
| --------- | ------: |
| Accuracy  | 88,46 % |
| Precision | 86,47 % |
| Recall    | 96,67 % |
| F1-score  | 91,28 % |

---

## Comparação com os Demais Modelos

| Modelo                       | Accuracy (%) | F1-score (%) |
| ---------------------------- | -----------: | -----------: |
| CNN Baseline                 |        71,79 |        81,55 |
| CNN + Data Augmentation      |        74,04 |        82,69 |
| ResNet18 (Transfer Learning) |        84,46 |        88,81 |
| ResNet18 (Fine Tuning)       |        81,57 |        87,10 |
| EfficientNet-B0              |        88,46 |        91,28 |

A EfficientNet-B0 apresentou o melhor desempenho entre todos os experimentos realizados.

---

## Discussão

As curvas de treinamento apresentaram comportamento estável, com pequena diferença entre treinamento e validação, indicando boa capacidade de generalização.

Além disso, a matriz de confusão revelou uma distribuição mais equilibrada entre as classes NORMAL e PNEUMONIA quando comparada aos demais modelos.

Os resultados obtidos evidenciam a superioridade das arquiteturas pré-treinadas para tarefas de classificação de imagens médicas, destacando a EfficientNet-B0 como a alternativa mais promissora entre os modelos avaliados.

---

## Conclusão

Entre todas as arquiteturas analisadas neste estudo, a EfficientNet-B0 apresentou o melhor equilíbrio entre precisão e sensibilidade, alcançando os maiores valores de Accuracy e F1-score.

Os resultados obtidos demonstram o potencial das arquiteturas profundas pré-treinadas como ferramentas de apoio ao diagnóstico assistido por computador em imagens médicas.

---

## Referências

TAN, M.; LE, Q.

*EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks.*

Proceedings of the International Conference on Machine Learning (ICML), 2019.

KERMANY, D. et al.

*Identifying Medical Diagnoses and Treatable Diseases by Image-Based Deep Learning.*

Cell, 2018.

---

## Autor

**Ederson Roberto da Costa**

Universidade Federal de Mato Grosso do Sul (UFMS)

Campo Grande - MS - Brasil
