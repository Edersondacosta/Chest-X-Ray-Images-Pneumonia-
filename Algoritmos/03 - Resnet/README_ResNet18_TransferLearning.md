# ResNet18 com Transfer Learning

## Descrição

Este experimento utiliza a arquitetura ResNet18 pré-treinada na base ImageNet para a classificação binária de radiografias de tórax em duas classes:

* NORMAL
* PNEUMONIA

A estratégia adotada foi o **Transfer Learning**, em que as camadas convolucionais previamente treinadas foram mantidas congeladas, sendo treinada apenas a camada classificadora final.

Este experimento corresponde ao **Experimento 3** do artigo.

---

## Arquitetura Utilizada

Foi empregada a arquitetura ResNet18 pré-treinada na ImageNet.

A camada totalmente conectada original foi substituída por uma nova estrutura composta por:

* Camada Linear com 128 neurônios;
* Função de ativação ReLU;
* Dropout de 0,5;
* Camada de saída com duas classes.

Todas as demais camadas convolucionais permaneceram congeladas durante o treinamento.

---

## Estratégia de Transfer Learning

Neste experimento:

* Todas as camadas da ResNet18 foram congeladas;
* Apenas a camada classificadora final foi treinada;
* Os pesos pré-treinados da ImageNet foram utilizados para extração das características das imagens.

Essa estratégia permite reduzir o tempo de treinamento e aproveitar características previamente aprendidas em grandes bases de dados.

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

## 4. Baixar o dataset

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
ResNet18_TransferLearning.ipynb
```

---

## 7. Executar todas as células

Ao final do treinamento serão gerados automaticamente os modelos treinados, curvas de treinamento e métricas de avaliação.

---

## Arquivos Gerados

Durante a execução do notebook são criados:

```text
experimento_3/
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
| Accuracy  | 84,46 % |
| Precision | 80,71 % |
| Recall    | 98,72 % |
| F1-score  | 88,81 % |

---

## Comparação com os Modelos Anteriores

| Modelo                       | Accuracy (%) | F1-score (%) |
| ---------------------------- | -----------: | -----------: |
| CNN Baseline                 |        71,79 |        81,55 |
| CNN + Data Augmentation      |        74,04 |        82,69 |
| ResNet18 (Transfer Learning) |        84,46 |        88,81 |

Observa-se um ganho significativo em relação à CNN desenvolvida do zero. O uso de pesos pré-treinados permitiu melhorar a capacidade de generalização do modelo e reduzir a quantidade de erros de classificação.

---

## Discussão

As curvas de treinamento apresentaram comportamento estável e rápida convergência. O modelo demonstrou maior equilíbrio entre as classes NORMAL e PNEUMONIA quando comparado aos experimentos anteriores.

Os resultados obtidos evidenciam a eficácia da estratégia de Transfer Learning para aplicações em imagens médicas, especialmente em cenários com quantidade limitada de dados rotulados.

---

## Próximos Experimentos

Os próximos experimentos deste repositório utilizam:

* ResNet18 com Fine Tuning;
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
