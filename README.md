# churn_bank_rna_mlp

Rede neural MLP para prever *churn* bancário (base Churn Modelling, do Kaggle),
implementada lado a lado em **PyTorch** e **MLX**.

## Estrutura

| Caminho | Conteúdo |
|---|---|
| `churn_rna.ipynb` | Notebook completo: análise exploratória, pré-processamento, baseline, MLP, ajuste de hiperparâmetros, desbalanceamento, avaliação final, interpretação e questões teóricas |
| `dados/Churn_Modelling.csv` | Base de dados (10.000 clientes) |
| `modelos/` | Modelos finais (`.safetensors` do MLX e `.pt` do PyTorch), pré-processador e configuração |
| `requirements.txt` | Bibliotecas e versões (gerado pelo notebook) |
| `MAC_TODO.md` | Passo a passo para a execução final no Mac com Apple Silicon |

## Como rodar

No Linux (ou WSL), com o MLX em CPU:

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install torch --index-url https://download.pytorch.org/whl/cpu
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute --inplace churn_rna.ipynb
```

No Mac com Apple Silicon (MLX na GPU), siga o `MAC_TODO.md`.
