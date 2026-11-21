# Segmentação e Análise Morfológica da Árvore Vascular da Retina

Projeto prático desenvolvido para a disciplina de **Processamento Digital de Imagens (PDI)**, focado na extração, segmentação e quantificação morfológica de vasos sanguíneos em imagens de fundo de olho utilizando **exclusivamente técnicas clássicas de processamento de imagens** (sem uso de redes neurais).

### 🗂️ Estrutura do Repositório

* **`Segmentacao Vasos Retina Trabalho Final Processamento Digital de Imagens.ipynb`** *(Principal)*: Pipeline completo, análise de sensibilidade, testes estatísticos e avaliação detalhada aplicados à base **DRIVE**.

* **`CHASE.ipynb`**: Adaptação e validação do pipeline no dataset **CHASE_DB1**.

* **`FIVES.ipynb`**: Adaptação e validação do pipeline em imagens do dataset **FIVES**.

## ⚙️ Metodologia e Etapas do Pipeline

1. **Pré-processamento e Realce:**

   * Extração do **canal verde** (maior contraste entre os vasos e o fundo retiniano).

   * Equalização adaptativa de histograma com limitação de contraste (**CLAHE**).

   * Filtragem morfológica **Top-Hat** para isolamento de estruturas tubulares escuras (comparado quantitativamente contra filtros de linha).

2. **Segmentação (Limiarização):**

   * Comparação sistemática entre limiarização global (**Otsu**, **Percentil**) e técnicas locais/contextuais (**Limiar Adaptativo** e **Histerese**).

3. **Pós-processamento e Limpeza Morfológica:**

   * Restrição estrita à máscara do campo de visão (*Field of View* — **FOV**).

   * Remoção de componentes conexos soltos e preenchimento de pequenas falhas estruturais.

4. **Esqueletização e Extração de Características:**

   * Redução da máscara vascular a um esqueleto topológico de 1 pixel de espessura.

   * Cálculo do **comprimento total** da árvore vascular e detecção de **pontos de bifurcação/ramificação**.

## 📊 Resultados

* **Análise de Sensibilidade:** Varredura sistemática (*grid search*) dos hiperparâmetros principais com geração de curvas de desempenho e desvio padrão.

* **Avaliação Quantitativa:** Cálculo das métricas **Dice**, **IoU (Jaccard)**, **Sensibilidade**, **Especificidade**, **Acurácia**, além dos erros relativos de **comprimento** e **contagem de ramificações**.

* **Robustez a Ruído:** Simulação de ruído gaussiano em múltiplos níveis ($\sigma \in \{0, 10, 20, 30\}$) avaliando a recuperação via filtros *Gaussiano*, *Mediana* e *Bilateral* com métricas de **PSNR** e **Dice**.

* **Auditoria Qualitativa e Análise de Falhas:** Geração de mapas de erro coloridos (Verdadeiros Positivos, Falsos Positivos e Falsos Negativos), análise de *Recall* por calibre de vaso e localização espacial dos maiores aglomerados de falso positivo.

## 🚀 Como Executar

### Pré-requisitos

Certifique-se de ter o Python 3.8+ instalado (ou utilize o ambiente **Google Colab**). As dependências principais são:

```
pip install numpy scipy scikit-image opencv-python-headless pandas matplotlib pillow
```

### Passo a Passo

1. Clone este repositório:

   ```
   git clone https://github.com/JhonnyBn/ProjetoPDI-Vasos.git
   cd ProjetoPDI-Vasos
   ```

2. Abra o notebook principal (`Segmentacao Vasos Retina Trabalho Final Processamento Digital de Imagens.ipynb`) no Jupyter Notebook, VS Code ou Google Colab.

3. Configure o caminho da base de dados **DRIVE** na célula inicial de parâmetros (ou utilize o download automático configurado no ambiente).

4. Execute todas as células sequencialmente (`Run All`).

5. Ao final da execução, os resultados serão exportados automaticamente para o diretório `/resultados`:

   * `/resultados/tabelas/*.csv`: Métricas detalhadas, testes de Wilcoxon e sensibilidade.

   * `/resultados/figuras/*.png`: Painéis comparativos dos melhores e piores casos e mapas de erro.

   * `/resultados/parametros_finais.json`: Hiperparâmetros ótimos congelados.

## 📚 Referências

* **Revisão da Literatura:** BANSAL, Avinash et al. Retinal Vessel Segmentation: A Comprehensive Review From Classical Methods to Deep Learning Advances (1982–2025). Advanced Intelligent Systems, p. e202501279, 2026.

* **DRIVE:** STAAL, Joes et al. Ridge-based vessel segmentation in color images of the retina. IEEE transactions on medical imaging, v. 23, n. 4, p. 501-509, 2004.

* **CHASE_DB1**: FRAZ, Muhammad Moazam et al. An ensemble classification-based approach applied to retinal blood vessel segmentation. IEEE transactions on biomedical engineering, v. 59, n. 9, p. 2538-2548, 2012.

* **FIVES**: JIN, Kai et al. Fives: A fundus image dataset for artificial intelligence based vessel segmentation. Scientific data, v. 9, n. 1, p. 475, 2022.