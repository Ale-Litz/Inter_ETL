import pandas as pd

extrato_inter = pd.read_csv('/content/Extrato-20220125.csv' ,sep = ';', skiprows = 5)
print(extrato_inter)

# carregando arquivo do extrato bancario até a data do arquivo

extrato_inter.columns = ['data_lancamento','historico','valor','saldo']
print(extrato_inter)

# renomeando as colunas

extrato_inter # simples exibição

extrato_inter_aux = extrato_inter['historico'].str.split(' - ', expand = True)
extrato_inter_aux.columns = ['1','2','3']
extrato_inter_aux = extrato_inter_aux.drop(columns=['3'])
extrato_inter_aux

# separando a coluna de historico em mais categorias 

extrato_inter[['categoria', 'descricao']] = extrato_inter_aux
extrato_inter

# separação da colunas de historico resulta em duas novas colunas - 'categoria' e 'descricao'

extrato_inter = extrato_inter.drop(columns=['historico'])
extrato_inter

# tirando coluna de historico

extrato_inter.info()

# Verificando o tipo de dado de cada coluna

extrato_inter['valor'] = extrato_inter['valor'].apply(lambda x: str(x).replace('.',''))
extrato_inter['valor'] = extrato_inter['valor'].apply(lambda x: str(x).replace(',','.'))
extrato_inter['valor'] = extrato_inter['valor'].astype('float64')
extrato_inter['saldo'] = extrato_inter['saldo'].apply(lambda x: str(x).replace('.',''))
extrato_inter['saldo'] = extrato_inter['saldo'].apply(lambda x: str(x).replace(',','.'))
extrato_inter['saldo'] = extrato_inter['saldo'].astype('float64')

# mudando os tipos de dados para somarização

extrato_inter.info()

# verificando se a mudança funcionou

extrato_inter[['dia','mes','ano']] = extrato_inter['data_lancamento'].str.split('/', expand = True)
extrato_inter

# separando as colunas de data em - 'dia','mes' e 'ano'

extrato_inter['ano_mes'] = extrato_inter['ano'] + '-' + extrato_inter['mes']
extrato_inter

# Criando colunas de ano_mes

saldo_atual = extrato_inter['valor'].sum() # simples soma da columa de movimentação de valores
print(saldo_atual)


ultima_linha = len(extrato_inter.index)-1
saldo_atual_ = extrato_inter['saldo'][ultima_linha]  # valor do saldo dado pelo proprio banco
print(saldo_atual_)

# com os dois batendo quase que perfeitamente podemos ver que o banco de dados esta coerente

soma_categoria = []

soma_categoria_aux = extrato_inter[['categoria', 'valor']]
soma_categoria = soma_categoria_aux.groupby(by = 'categoria').sum()
soma_categoria

# Resumo de movimentação por categoria

import matplotlib.pyplot as plt

x = extrato_inter['categoria']
y = extrato_inter['valor']

plt.figure(figsize=(8, 8))
plt.xticks(rotation=90)
plt.bar(x, y)

plt.show()

# Plotagem da categoria x valor

soma_ano_mes = []

soma_ano_mes_aux = extrato_inter[['ano_mes', 'valor']]
soma_ano_mes = soma_ano_mes_aux.groupby(by = 'ano_mes').sum()
soma_ano_mes

# Resumo de movimentação por ano_mes

x = extrato_inter['ano_mes']
y = extrato_inter['valor']

plt.figure(figsize=(8, 8))
plt.xticks(rotation=90)
plt.bar(x, y)

plt.show()

# Plotagem da ano_mes x valor

