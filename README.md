# 🛵 Análise de Dados de Delivery

Projeto prático de análise exploratória, tratamento de dados e geração de indicadores de desempenho (KPIs) para uma operação de delivery de alimentos.

---

## 📌 Visão Geral do Projeto

O objetivo deste projeto foi analisar o histórico de vendas de um serviço de delivery a partir de dados transacionais e de cardápio, realizando desde a limpeza e preparação dos dados até a geração de métricas de negócio e análises temporais.

Toda a análise foi desenvolvida em Python no Jupyter Notebook [`main.ipynb`](main.ipynb), utilizando as bibliotecas **Pandas** e **NumPy**.

---

## 📁 Estrutura de Arquivos

```text
delivery_analise/
├── dados/
│   ├── cardapio.csv      # Catálogo com itens, categorias e preços base
│   └── pedidos.csv       # Histórico de pedidos (datas, itens, quantidades e preços)
├── main.ipynb            # Notebook principal com o pipeline analítico
├── pyproject.toml        # Gerenciamento de dependências do projeto
└── README.md             # Documentação do projeto
```

---

## 🛠️ O que foi feito no projeto

O pipeline analítico foi estruturado em **8 etapas principais**:

1. **Análise Exploratória de Dados (EDA)**
   - Inspeção inicial das dimensões do dataset (`shape`), primeiras e últimas linhas (`head` e `tail`).
   - Verificação de tipos de dados (`info`) e levantamento de estatísticas descritivas (`describe`).

2. **Engenharia de Recursos (Feature Engineering)**
   - Criação da coluna `Receita_Item`, calculada pela multiplicação de `Quantidade` por `Preco_Unitario`.

3. **Tratamento de Dados Ausentes**
   - Mapeamento e percentual de valores nulos.
   - Preenchimento (*fillna*) dos valores ausentes na coluna `Quantidade` com base na média.
   - Remoção (*dropna*) dos registros com valores nulos na coluna `Preco_Unitario`.
   - Recálculo da receita dos itens para garantir consistência.

4. **Agregações por Item**
   - Agrupamento para calcular a quantidade total vendida e o faturamento por produto.
   - Identificação do **Top 5 itens mais vendidos** em volume e do **Top 5 com maior faturamento**.

5. **Análise Temporal**
   - Conversão do campo de data para formato `datetime`.
   - Extração de mês e períodos (`Ano_Mes`).
   - Acompanhamento da evolução mensal da receita, identificando os períodos de pico e sazonalidade.

6. **Integração de Bases (Merge)**
   - Junção (*left join*) da base de pedidos com a base do cardápio (`cardapio.csv`) utilizando a coluna `Item`.
   - Classificação das vendas por categorias (Salgados, Doces, Bebidas, etc.).
   - Identificação da categoria líder de vendas.

7. **Filtros e Consultas de Negócio**
   - Filtragem e análise segmentada de pedidos da categoria **Salgados** com volume superior a **10 unidades**.

8. **KPIs e Análise Estatística com NumPy**
   - Cálculo das métricas gerais do negócio: Receita Total, Volume Total Vendido, Total de Pedidos e Ticket Médio.
   - Cálculo de percentis (25%, 50% e 75%) de `Preco_Unitario` e `Quantidade` através da função `np.percentile`.

---

## 📊 Principais Resultados Encontrados

- **Receita Total:** ~R$ 122.652,59
- **Volume Vendido:** ~6.833 unidades
- **Ticket Médio por Pedido:** ~R$ 285,24
- **Categoria Destaque:** **Salgados** representou a maior fatia do faturamento (mais de 40% do total).
- **Comportamento de Compra:** Metade dos pedidos possui volumes de 16 ou mais unidades (mediana), indicando forte presença de pedidos compartilhados/corporativos.

---

## 💻 Tecnologias Utilizadas

- **Python** (versão 3.14+)
- **Pandas** (manipulação, limpeza e agregação de dados)
- **NumPy** (cálculo de percentis e suporte numérico)
- **Jupyter Notebook** (ambiente interativo de execução)
- **uv** (gerenciador de dependências e ambiente virtual)

---

## 🚀 Como Executar o Projeto

1. **Clone o repositório:**
   ```bash
   git clone <url-do-repositorio>
   cd delivery_analise
   ```

2. **Instale as dependências:**
   Caso utilize `uv`:
   ```bash
   uv sync
   ```
   Ou via `pip`:
   ```bash
   pip install pandas numpy notebook
   ```

3. **Inicie o Jupyter Notebook:**
   ```bash
   jupyter notebook main.ipynb
   ```
   Ou abra o arquivo [`main.ipynb`](main.ipynb) diretamente no VS Code / seu editor de preferência e execute todas as células.
