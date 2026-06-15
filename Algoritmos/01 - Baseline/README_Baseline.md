# CNN Baseline

## Descrição

Este experimento implementa uma Rede Neural Convolucional (CNN) desenvolvida do zero para a classificação binária de radiografias de tórax em duas classes:

* NORMAL
* PNEUMONIA

O objetivo deste experimento é estabelecer um modelo de referência (*baseline*) para comparação com arquiteturas mais complexas, como ResNet18 e EfficientNet-B0.

Neste experimento **não foram utilizadas técnicas de Data Augmentation**, sendo empregado apenas o conjunto original de imagens.

---

## Arquitetura da Rede

A CNN Baseline é composta por:

* 3 camadas convolucionais;
* Função de ativação ReLU;
* Camadas de Max Pooling;
* Camada Flatten;
* Camada totalmente conectada;
* Dropout de 0,5;
* Camada de saída com duas classes.

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

As imagens são divididas em duas classes:

* NORMAL
* PNEUMONIA

---

## Como Executar no Google Colab

### 1. Montar o Google Drive

```python
from google.colab import drive

drive.mount('/content/drive')
```

---

### 2. Configurar a API do Kaggle

No Kaggle, acesse:

```
Account → Create New Token
```

Será baixado o arquivo:

```text
kaggle.json
```

Faça o upload para o Google Colab:

```python
from google.colab import files

files.upload()
```

---

### 3. Configurar a chave do Kaggle

```python
!mkdir ~/.kaggle

!cp kaggle.json ~/.kaggle/

!chmod 600 ~/.kaggle/kaggle.json
```

---

### 4. Baixar a base de dados

```python
!kaggle datasets download paultimothymooney/chest-xray-pneumonia
```

---

### 5. Descompactar os arquivos

```python
!unzip chest-xray-pneumonia.zip
```

---

### 6. Abrir o notebook

Abra o notebook correspondente ao experimento:

```text
Baseline.ipynb
```

---

### 7. Executar todas as células

Ao final do treinamento serão gerados automaticamente os arquivos de checkpoint e os gráficos utilizados na análise dos resultados.

---

## Arquivos Gerados

Durante a execução do notebook são criados:

```text
experimento_1/
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
| Accuracy  | 71,79 % |
| Precision | 68,97 % |
| Recall    | 99,74 % |
| F1-score  | 81,55 % |

---

## Matriz de Confusão

O modelo apresentou elevada sensibilidade para a detecção de pneumonia, porém demonstrou dificuldade em identificar corretamente imagens da classe NORMAL, resultando em uma maior quantidade de falsos positivos.

---

## Limitações

Por se tratar de uma CNN desenvolvida do zero e treinada sem técnicas de aumento de dados, observou-se uma tendência ao sobreajuste (*overfitting*) e menor capacidade de generalização quando comparada às arquiteturas pré-treinadas avaliadas posteriormente.

---

## Próximos Experimentos

Os experimentos seguintes deste repositório avaliam:

* CNN com Data Augmentation;
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
