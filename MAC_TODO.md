# ⚠️ MAC: o que fazer no Mac com chip M

No PC (Ubuntu/WSL), o notebook já roda do início ao fim, mas o MLX usa só a CPU.
No Mac, o MLX usa a GPU (Metal) automaticamente, sem mudar nada no código.

## 1. Levar o projeto para o Mac

A pasta `churn_bank_rna_mlp` é um repositório Git. O jeito mais fácil é publicá-la
no GitHub (repositório **privado**) e, no Mac, rodar:

```bash
git clone <endereço-do-repositório> churn_bank_rna_mlp
```

Também dá para copiar a pasta por pendrive ou Google Drive, mas **sem a pasta `.venv`**
(ela só funciona no Linux). O arquivo de dados `dados/Churn_Modelling.csv` precisa ir
junto (ele já está no repositório).

## 2. Criar o ambiente no Mac (uma vez só)

No Terminal do Mac:

```bash
cd caminho/para/churn_bank_rna_mlp
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install mlx torch numpy pandas matplotlib seaborn scikit-learn imbalanced-learn joblib jupyter
```

Teste rápido (deve mostrar `Device(gpu, 0)`):

```bash
python -c "import mlx.core as mx; print(mx.default_device())"
```

## 3. Executar o notebook do início ao fim

```bash
jupyter nbconvert --to notebook --execute --inplace --ExecutePreprocessor.timeout=3600 churn_rna.ipynb
```

Ou abra no VS Code e use "Run All".

Isso faz automaticamente:
- [ ] treinar todos os modelos usando a GPU no MLX;
- [ ] gerar o benchmark da Parte 7 com os números reais do Apple Silicon;
- [ ] salvar `modelos/mlp_final_mlx.safetensors` e `modelos/mlp_final_pytorch.pt`;
- [ ] gerar o `requirements.txt` com as versões do Mac.

## 4. Conferir depois de executar

- [ ] A primeira célula diz "✅ Rodando num Mac com Apple Silicon".
- [ ] Nenhuma célula com erro.
- [ ] Os textos de análise continuam batendo com os números. Os resultados podem
      variar um pouco em relação ao PC (a GPU muda levemente os cálculos). Se a
      melhor configuração (Parte 4) ou o tratamento escolhido (Parte 5) mudarem,
      revise os textos dessas partes.
- [ ] A Parte 7 (benchmark) mostra o MLX rodando na GPU. Comente o resultado.

## 5. Montar a entrega

```bash
zip -r churn_rna_<seu_nome>.zip churn_rna.ipynb requirements.txt modelos/
```
