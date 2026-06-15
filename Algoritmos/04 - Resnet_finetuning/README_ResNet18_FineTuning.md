# ResNet18 com Fine Tuning

## Descrição

Este experimento utiliza a arquitetura ResNet18 pré-treinada na base ImageNet para a classificação binária de radiografias de tórax em duas classes:

* NORMAL
* PNEUMONIA

Diferentemente do experimento anterior, foi empregada a estratégia de **Fine Tuning**, permitindo que parte das camadas convolucionais da rede fosse ajustada ao domínio das imagens médicas.

Este experimento corresponde ao **Experimento 4** do artigo.

---

## Arquitetura Utilizada

Foi empregada a arquitetura ResNet18 pré-treinada na ImageNet.

A camada totalmente conectada original foi substituída por uma nova estrutura composta por:

* Camada Linear com 128 neurônios;
* Função de ativação ReLU;
* Dropout de 0,5;
* Camada de saída com duas classes.

---

## Estratégia de Fine Tuning

Inicialmente, todas as camadas da ResNet18 foram congeladas.

Posteriormente:

* O bloco residual final (**Layer4**) foi liberado para treinamento;
* A camada classificadora final também foi treinada;
* As demais camadas permaneceram congeladas.

Essa estratégia permite adaptar as características extraídas pela rede às particularidades das imagens de radiografia de tórax.

---

## Hiperparâmetros

| Parâmetro               |            Valor |
| ----------------------- | ---------------: |
| Learning Rate           |           0.0001 |
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
ResNet18_FineTuning.ipynb
```

---

## 7. Executar todas as células

Ao final do treinamento serão gerados automaticamente os modelos treinados, curvas de treinamento e métricas de avaliação.

---

## Arquivos Gerados

Durante a execução do notebook são criados:

```text
experimento_4/
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
| Accuracy  | 81,57 % |
| Precision | 77,45 % |
| Recall    | 99,49 % |
| F1-score  | 87,10 % |

---

## Comparação com os Experimentos Anteriores

| Modelo                       | Accuracy (%) | F1-score (%) |
| ---------------------------- | -----------: | -----------: |
| CNN Baseline                 |        71,79 |        81,55 |
| CNN + Data Augmentation      |        74,04 |        82,69 |
| ResNet18 (Transfer Learning) |        84,46 |        88,81 |
| ResNet18 (Fine Tuning)       |        81,57 |        87,10 |

Embora o Fine Tuning tenha proporcionado elevada sensibilidade para a detecção da classe PNEUMONIA, o desempenho global foi inferior ao obtido utilizando apenas a estratégia de Transfer Learning.

---

## Discussão

As curvas de treinamento apresentaram comportamento estável e pequena diferença entre treinamento e validação, indicando boa capacidade de generalização.

Entretanto, observou-se um aumento no número de falsos positivos em relação ao experimento com Transfer Learning. Isso sugere que o ajuste do bloco Layer4 pode ter levado a uma especialização excessiva do modelo para as características do conjunto de treinamento.

Para a base utilizada neste estudo, a estratégia de Transfer Learning tradicional apresentou melhor desempenho que o Fine Tuning.

---

## Próximo Experimento

O próximo experimento avalia a arquitetura:

* EfficientNet-B0.

---

## Referências

HE, K. et al.

*Deep Residual Learning for Image Recognition.*

Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2016.

KERMANY, D. et al.

*Identifying Medical Diagnoses and Treatable Diseases by Image-Based Deep Learning.*

Cell, 2018.

---

## Autor

**Ederson Roberto da Costa**

Universidade Federal de Mato Grosso do Sul (UFMS)

Campo Grande - MS - Brasil
