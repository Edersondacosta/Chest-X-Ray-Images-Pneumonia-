# CNN Baseline com Data Augmentation

## Descrição

Este experimento implementa uma Rede Neural Convolucional (CNN) desenvolvida do zero para a classificação binária de radiografias de tórax em duas classes:

* NORMAL
* PNEUMONIA

Diferentemente do experimento anterior, foram aplicadas técnicas de **Data Augmentation** durante o treinamento com o objetivo de aumentar a diversidade das imagens e melhorar a capacidade de generalização do modelo.

Este experimento corresponde ao **Experimento 2** do artigo.

---

## Arquitetura da Rede

A CNN Baseline é composta por:

* 3 camadas convolucionais;
* Função de ativação ReLU;
* Camadas de Max Pooling;
* Camada Flatten;
* Camada totalmente conectada;
* Dropout de 0,5;
* Camada de saída contendo duas classes.

A arquitetura utilizada é a mesma do experimento Baseline, sendo alterado apenas o pré-processamento aplicado às imagens do conjunto de treinamento.

---

## Técnicas de Data Augmentation

Foram utilizadas transformações aleatórias durante o treinamento visando aumentar a variabilidade das imagens e reduzir os efeitos do overfitting.

As seguintes técnicas foram empregadas:

* Rotação aleatória;
* Espelhamento horizontal (*Horizontal Flip*);
* Pequenos deslocamentos;
* Redimensionamento para 224 × 224 pixels;
* Conversão para tensor.

As transformações foram aplicadas somente ao conjunto de treinamento.

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
Baseline_DataAugmentation.ipynb
```

---

## 7. Executar todas as células

Ao final do treinamento serão gerados automaticamente os modelos treinados, curvas de treinamento e métricas de avaliação.

---

## Arquivos Gerados

Durante a execução do notebook são criados:

```text
experimento_2/
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
| Accuracy  | 74,04 % |
| Precision | 70,88 % |
| Recall    | 99,23 % |
| F1-score  | 82,69 % |

---

## Comparação com o Baseline

| Modelo                  | Accuracy (%) | F1-score (%) |
| ----------------------- | -----------: | -----------: |
| CNN Baseline            |        71,79 |        81,55 |
| CNN + Data Augmentation |        74,04 |        82,69 |

A utilização de técnicas de Data Augmentation proporcionou uma melhora no desempenho geral da rede, aumentando a acurácia e o F1-score em relação ao modelo treinado sem aumento artificial dos dados.

---

## Discussão

Embora os ganhos tenham sido modestos, a aplicação de Data Augmentation contribuiu para reduzir o sobreajuste e melhorar a capacidade de generalização do modelo. Entretanto, os resultados obtidos ainda foram inferiores aos alcançados pelas arquiteturas pré-treinadas avaliadas posteriormente.

---

## Próximos Experimentos

Os próximos experimentos deste repositório utilizam arquiteturas pré-treinadas:

* ResNet18 com Transfer Learning;
* ResNet18 com Fine Tuning;
* EfficientNet-B0.

---

## Referências

KERMANY, D. et al.

*Identifying Medical Diagnoses and Treatable Diseases by Image-Based Deep Learning.*

Cell, 2018.

---

## Autor

**Ederson Roberto da Costa**

Universidade Federal de Mato Grosso do Sul (UFMS)

Campo Grande - MS - Brasil
