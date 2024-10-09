# Ciencia-de-dados-55
# Passo a passo
# Passo 1: Importar base de dados
# Passo 2: Visualizar base de dados
# Passo 3: Corrigir cagadas da base de dados
# Passo 4: Análise dos cancelamentos
# Passo 5: Análise da causa dos cancelamentos (como as colunas impactam no cancelamento?)

# !pip install pandas numpy openpyxl nbformat ipykernel plotly
# Passo a passo do projeto
# Passo 1: Importar a base de dados
import pandas as pd

tabela = pd.read_csv("cancelamentos.csv")

# Passo 2: Visualizar a base de dados
tabela = tabela.drop(columns="CustomerID")
print(tabela)
# colunas inúteis - informações que não te ajudam, te atrapalham

# Passo 3: Corrigir as cagadas da base de dados
print(tabela.info())
# valores vazios - excluir as linhas que têm valores vazios
tabela = tabela.dropna()

print(tabela.info())

# Passo 4: Análise inicial dos cancelamentos

# quantas pessoas cancelaram e quantas não cancelaram
print(tabela["cancelou"].value_counts())

# em percentual
print(tabela["cancelou"].value_counts(normalize=True))
# display(tabela["cancelou"].value_counts(normalize=True).map("{:.1%}".format))

# Passo 5: Análise das causas dos cancelamentos (como as colunas da base impactam no cancelamento)
# gráficos/dashboards
# !pip install plotly
import plotly.express as px

# criar o grafico

for coluna in tabela.columns:
    grafico = px.histogram(tabela, x=coluna, color="cancelou")
    # exibir o grafico
    grafico.show()

tabela = tabela[tabela["duracao_contrato"] != "Monthly"]
tabela = tabela[tabela["ligacoes_callcenter"] <= 4]
tabela = tabela[tabela["dias_atraso"] <= 20]

print(tabela["cancelou"].value_counts())
# em percentual
print(tabela["cancelou"].value_counts(normalize=True))

