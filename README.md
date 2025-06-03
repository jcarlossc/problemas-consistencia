# Problemas de consistencia em conjunto de dados

## Problemas de consistência
* ✅ Categorias duplicadas por erro de escrita (ex: 'Feminino', 'feminino', 'FEMININO')
* ```df['sexo'] = df['sexo'].str.strip().str.lower()```. Limpar espaços e padronizar letras(minúsculas).
* ```df['sexo'] = df['sexo'].str.strip().str.upper()```. Limpar espaços e padronizar letras(maiúscula).
* ```df['sexo'] = df['sexo'].replace({'feminino': 'Feminino','feminina': 'Feminino','fem': 'Feminino','feminio': 'Feminino','masculino': 'Masculino','masculina': 'Masculino','masc': 'Masculino'})```. Corrigir erros de digitação.
* ```df['sexo'] = df['sexo'].str.capitalize()```. Manter os nomes com a primeira letra maiúscula.
* ```df['sexo'].unique()```.  Verificar os valores únicos.
* ✅ Valores com espaços extras (' João ')
* ✅ Letras maiúsculas/minúsculas misturadas
* ✅ Datas em formatos diferentes (dd/mm/yyyy, yyyy-mm-dd)
* ✅ Unidades diferentes (ex: metros vs. centímetros)
* ✅ Codificação errada (ex: acentos quebrados por UTF-8/Latin-1)
