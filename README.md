## 📌 Projeto Fogo na Fake — Processamento e Análise de Dados

Este projeto faz parte do **Projeto Fogo na Fake**, voltado à análise de *fake news sobre o Cerrado*.  
Ele automatiza o processamento de planilhas com dados coletados via **web scraping do Google**, desde a limpeza até a classificação e análise dos dados.

---

## 📂 O que cada arquivo faz

### 1. `limpar_arquivos.ipynb`
Responsável pela limpeza inicial dos dados brutos.

- Acessa arquivos Excel armazenados no Google Drive  
- Identifica arquivos não processados (sem `"unificado"` ou `"limpo"` no nome)  
- Remove caracteres inválidos de colunas de texto  
- Filtra e remove linhas marcadas com **`x`** na coluna `marcacao_X`  
- Remove colunas específicas (`var1`, `var2`, `var3`)  
- Salva os arquivos limpos no formato `*_limpo.xlsx`

---

### 2. `unir_planilhas.ipynb`
Unifica os arquivos já tratados em uma única base.

- Combina múltiplos arquivos Excel em um único arquivo  
- Padroniza os nomes das colunas para:  
  `link`, `excluir`, `conteudo`, `marcacao_X`, `status_revisao`  
- Remove linhas de cabeçalho duplicadas  
- Salva o resultado em `planilha_combinada.xlsx`

---

### 3. `classificar_arquivos.ipynb`
Responsável pela classificação automática dos textos.

- Treina um modelo de **classificação de texto** usando  
  `TfidfVectorizer` + `LogisticRegression`  
- Carrega dados de entrada (CSV ou Excel) com texto e rótulos  
- Processa o rótulo (`x` → `1`, demais → `0`)  
- Salva o modelo e o vetorizador treinados em arquivos `.joblib`  
- Utiliza os modelos para classificação em lote de novos arquivos  
- Gera status de revisão (*confiante*, *duvidoso*, *incerto*) com base em limiares de confiança

---

### 4. `gerar_planilhas.py`
Geração de análises e relatórios comparativos.

- Analisa dados a partir do arquivo `linhas_grupos.csv`  
- Compara diferenças entre grupos por ano  
- Calcula percentuais de diferença entre grupos  
- Gera resumo total de linhas por grupo  
- Salva os resultados em:
  - `analise_diferenca_por_ano.csv`
  - `analise_resumo_por_grupo.csv`

---

## 🔄 Fluxo Geral do Projeto

**Web Scraping → Limpeza → Unificação → Classificação → Análises 📊**
