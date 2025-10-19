# Previsão de Séries Temporais - IBOVESPA (POSTECH)

Este repositório contém o projeto final para o desafio de Data Analytics da POSTECH, focado na previsão do preço de fechamento diário da IBOVESPA (`^BVSP`). O objetivo era atingir uma "assertividade" de 80% (definida como um **SMAPE < 20%**).

## Metodologia Resumida

O *pipeline* de análise seguiu 5 etapas principais:

1.  **Carga e Limpeza:** Carregamento do `dados10anos.csv` e tratamento robusto de formatos de preço (ex: `145.517`) e volume (ex: `8,34B`, `3,74M`).
2.  **Estacionaridade (Teste ADF):** A série de preços original foi confirmada como **não-estacionária**.
3.  **Engenharia de Features:** Para modelagem, foram usadas as séries **diferenciadas** (estacionárias) do preço (`y_diff`) e do volume (`volume_diff`).
4.  **Modelagem:** Três modelos foram comparados:
    * `SeasonalNaive` (Baseline)
    * `AutoARIMA (c/ Volume)` (Usando `volume_diff` como *feature* exógena)
    * `LSTM (c/ Volume)` (Usando `y_diff` e `volume_diff` como *features* de entrada)
5.  **Validação:** Foi usada uma divisão cronológica (backtesting), com os **últimos 100 dias** como conjunto de teste. As previsões foram revertidas para a escala de preço original para uma comparação justa.

## 📊 Resultados Finais

O modelo `AutoARIMA` demonstrou performance superior, superando massivamente a meta do desafio.

| Modelo | MAE | RMSE | SMAPE % | Assertividade (1-SMAPE) |
|:---|---:|---:|---:|---:|
| **AutoARIMA (c/ Volume)** | **2938.00** | **3652.89** | **2.12%** | **97.88%** |
| LSTM (c/ Volume) | 7083.86 | 9832.11 | 5.26% | 94.74% |
| SeasonalNaive | 55063.33 | 62638.08 | 31.71% | 68.29% |

**Conclusão:** O objetivo foi atingido com uma assertividade final de **97.88%**.

## 🚀 Como Executar

1.  **Clonar o repositório:**
    ```bash
    git clone [URL-DO-SEU-REPOSITORIO]
    cd [NOME-DO-REPOSITORIO]
    ```
2.  **Criar e ativar o ambiente virtual:**
    ```bash
    python -m venv .venv
    .\.venv\Scripts\activate 
    ```
3.  **Instalar dependências:**
    ```bash
    pip install pandas statsforecast tensorflow scikit-learn matplotlib seaborn tabulate
    ```
4.  **Executar o Notebook:**
    Abra e execute o `notebook.ipynb` (ou o nome do seu notebook principal) no VS Code ou Jupyter.