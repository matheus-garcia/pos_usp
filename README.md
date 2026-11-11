# Modelo de Agrupamentos para Dados Mistos: Acidentes de Trânsito em Porto Alegre

Projeto de conclusão do **MBA em Data Science & Analytics (USP/ESALQ, 2023)**.
Orientador: Diego Pedroso dos Santos.

## Problema

O Rio Grande do Sul registra uma taxa de óbitos no trânsito acima da média nacional, e Porto Alegre concentra a maior parte desses acidentes no estado. O objetivo deste trabalho foi responder: **quais padrões podem ser encontrados nos acidentes de trânsito de Porto Alegre?** A partir desses padrões, o estudo busca apoiar ações de prevenção e a melhoria da mobilidade urbana.

## Dados

- **Fonte:** portal de Dados Abertos da Prefeitura de Porto Alegre (dadosabertos.poa.br), conjunto "Acidentes de trânsito".
- **Período:** janeiro de 2018 a março de 2023.
- **Volume:** cerca de **64 mil ocorrências e 33 variáveis**, incluindo vítimas (feridos, feridos graves, fatais), veículos envolvidos, tipo de acidente, dia da semana, turno e região da cidade.

O arquivo de dados (`cat_acidentes.csv`) não está no repositório; ele pode ser baixado diretamente no portal.

## Método

O notebook `clustering_acidentes_poa.ipynb` reúne as etapas do trabalho:

1. **Exploração:** estatísticas descritivas e diagnóstico de valores ausentes.
2. **Limpeza e preparação (pandas e NumPy):**
   - recuperação da região de ocorrências a partir de registros do mesmo cruzamento e exclusão das linhas restantes sem região;
   - remoção de variáveis com muitos ausentes ou sem valor analítico (coordenadas, logradouros, consórcio, data de extração);
   - criação das variáveis de **mês** e **ano** a partir da data;
   - tipagem das variáveis categóricas (tipo de acidente, dia da semana, turno, região, mês e ano);
   - padronização das variáveis numéricas.
3. **Modelagem (kmodes e scikit-learn):**
   - algoritmo **k-prototypes**, que combina k-means (numéricas) e k-modes (categóricas) e por isso é adequado a dados mistos;
   - teste de 2 a 10 grupos, avaliados por **coeficiente de silhueta**, **Davies-Bouldin** e **Calinski-Harabasz**;
   - comparação de cenários com e sem a variável tipo de acidente.
4. **Interpretação (Matplotlib e Seaborn):** médias das variáveis numéricas, moda das categóricas e distribuição de cada grupo por dia, turno, região, mês, ano e tipo de acidente.

## Resultados

O modelo final, com **3 clusters**, obteve coeficiente de silhueta de **0,46** e identificou perfis bem definidos:

| Cluster | Ocorrências | Perfil |
|---|---|---|
| 1 | 42.402 | Acidentes entre automóveis, majoritariamente diurnos e de **baixa gravidade**. |
| 2 | 20.144 | Predomínio de **motocicletas**, maior gravidade (média de um ferido por acidente), mais ocorrências noturnas, atropelamentos e quedas. |
| 3 | 1.863 | Forte presença de **bicicletas e ônibus intermunicipais**, com gravidade intermediária. |

Os resultados sugerem, por exemplo, a relação entre o crescimento das entregas por aplicativo e a gravidade dos acidentes com motocicletas, e indicam onde ações de prevenção podem ser mais efetivas.

**Limitações:** ausência de dados espaciais completos e de dados demográficos, que permitiriam análises ainda mais ricas.

## Tecnologias

Python · pandas · NumPy · scikit-learn · kmodes · Matplotlib · Seaborn · VS Code

## Como executar

1. Baixe a base de acidentes no portal de Dados Abertos de Porto Alegre e salve como `cat_acidentes.csv` na mesma pasta do notebook.
2. Instale as dependências: `pip install pandas numpy scikit-learn kmodes matplotlib seaborn`.
3. Execute `clustering_acidentes_poa.ipynb` em ordem.

## Projeto relacionado

Este trabalho foi a base para uma análise em escala nacional, com 1,88 milhão de acidentes nas capitais brasileiras:
[clusterizacao-acidentes-transito](https://github.com/matheus-garcia/clusterizacao-acidentes-transito).

## Autor

**Matheus dos Santos Garcia** – Analista de Dados
[LinkedIn](https://www.linkedin.com/in/matheussgarcia/)
