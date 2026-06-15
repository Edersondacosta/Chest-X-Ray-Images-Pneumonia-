# Detecção de Pneumonia Utilizando Deep Learning

## Visão Geral

Este repositório contém a implementação e os resultados experimentais apresentados no trabalho:

**Análise Comparativa de Arquiteturas de Deep Learning para Detecção de Pneumonia em Radiografias de Tórax**

O objetivo deste estudo é avaliar diferentes arquiteturas de Aprendizado Profundo para a detecção automática de pneumonia em imagens de radiografia de tórax.

Foram realizados cinco experimentos:

1. CNN Baseline;
2. CNN com Data Augmentation;
3. ResNet18 com Transfer Learning;
4. ResNet18 com Fine Tuning;
5. EfficientNet-B0.

---

## Base de Dados

Os experimentos foram realizados utilizando a base de dados **Chest X-Ray Images (Pneumonia)**, disponibilizada no Kaggle:

https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia

A base contém imagens de radiografia de tórax pertencentes às seguintes classes:

* NORMAL
* PNEUMONIA

---

## Estrutura do Repositório

```text
.
├── Baseline/
│   ├── notebook.ipynb
│   └── README.md
│
├── Baseline_DataAugmentation/
│   ├── notebook.ipynb
│   └── README.md
│
├── ResNet18_TransferLearning/
│   ├── notebook.ipynb
│   └── README.md
│
├── ResNet18_FineTuning/
│   ├── notebook.ipynb
│   └── README.md
│
├── EfficientNet_B0/
│   ├── notebook.ipynb
│   └── README.md
│
└── README.md
```

Cada pasta contém o notebook correspondente ao experimento e um arquivo README com instruções detalhadas para reprodução dos resultados.

---

## Configuração dos Experimentos

Todos os modelos foram implementados utilizando a biblioteca PyTorch.

### Hiperparâmetros

| Parâmetro               |            Valor |
| ----------------------- | ---------------: |
| Batch Size              |               64 |
| Número máximo de épocas |               30 |
| Função de perda         | CrossEntropyLoss |
| Otimizador              |             Adam |
| Early Stopping          |              Sim |

---

## Resultados Obtidos

| Modelo                       | Accuracy (%) | Precision (%) | Recall (%) | F1-score (%) |
| ---------------------------- | -----------: | ------------: | ---------: | -----------: |
| CNN Baseline                 |        71,79 |         68,97 |      99,74 |        81,55 |
| CNN + Data Augmentation      |        74,04 |         70,88 |      99,23 |        82,69 |
| ResNet18 (Transfer Learning) |        84,46 |         80,71 |      98,72 |        88,81 |
| ResNet18 (Fine Tuning)       |        81,57 |         77,45 |      99,49 |        87,10 |
| EfficientNet-B0              |        88,46 |         86,47 |      96,67 |        91,28 |

Entre os modelos avaliados, a arquitetura **EfficientNet-B0** apresentou o melhor desempenho, alcançando 88,46% de acurácia e F1-score de 91,28%.

---

# Como Executar os Experimentos no Google Colab

## 1. Montar o Google Drive

```python
from google.colab import drive

drive.mount('/content/drive')
```

---

## 2. Configurar a API do Kaggle

No Kaggle, acesse:

**Account → Create New Token**

Será baixado o arquivo:

```text
kaggle.json
```

Faça o upload do arquivo para o Colab:

```python
from google.colab import files

files.upload()
```

---

## 3. Configurar o acesso ao Kaggle

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

## 6. Executar o notebook desejado

Cada pasta do projeto possui um notebook correspondente ao experimento.

Basta abrir o arquivo `.ipynb` no Google Colab e executar todas as células.

---

## Arquivos Gerados

Durante a execução dos experimentos são gerados automaticamente:

* `best_model.pth`
* `checkpoint.pth`
* Curvas de treinamento e validação;
* Curvas de perda;
* Matrizes de confusão;
* Métricas de avaliação;
* Relatórios de classificação.

---

## Principais Referências

* KERMANY, D. et al. *Identifying Medical Diagnoses and Treatable Diseases by Image-Based Deep Learning*. Cell, 2018.

* HE, K. et al. *Deep Residual Learning for Image Recognition*. CVPR, 2016.

* TAN, M.; LE, Q. *EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks*. ICML, 2019.

---

## Como Citar

Caso utilize este repositório em pesquisas ou trabalhos acadêmicos, recomenda-se citar:

```bibtex
@article{costa2026,
  author = {Costa, Ederson Roberto da},
  title = {Análise Comparativa de Arquiteturas de Deep Learning para Detecção de Pneumonia em Radiografias de Tórax},
  year = {2026}
}
```

---

## Autor

**Ederson Roberto da Costa**

Universidade Federal de Mato Grosso do Sul (UFMS)

Campo Grande - MS - Brasil
