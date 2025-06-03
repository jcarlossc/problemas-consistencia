# Problemas de consistencia em conjunto de dados

## Problemas de consistência
## ✅ Categorias duplicadas por erro de escrita (ex: 'Feminino', 'feminino', 'FEMININO')
* ```df['sexo'] = df['sexo'].str.strip().str.lower()```. Limpar espaços e padronizar letras(minúsculas).
* ```df['sexo'] = df['sexo'].str.strip().str.upper()```. Limpar espaços e padronizar letras(maiúscula).
* ```df['sexo'] = df['sexo'].replace({'feminino': 'Feminino','feminina': 'Feminino','fem': 'Feminino','feminio': 'Feminino','masculino': 'Masculino','masculina': 'Masculino','masc': 'Masculino'})```. Corrigir erros de digitação.
* ```df['sexo'] = df['sexo'].str.capitalize()```. Manter os nomes com a primeira letra maiúscula.
* ```df['sexo'].unique()```.  Verificar os valores únicos.
* ```df['coluna'] = df['coluna'].str.title()```. Maiúscula no início das palavras.
## ✅ Valores com espaços extras (' João ')
* ```df['coluna'] = df['coluna'].str.strip()```. Remover espaços no início e fim (mais comum).
* ```df['coluna'] = df['coluna'].str.replace(r'\s+', ' ', regex=True)```. Remover múltiplos espaços entre palavras.
* ```df['coluna'] = df['coluna'].str.strip().str.replace(r'\s+', ' ', regex=True)```. Limpeza completa (combinar os dois anteriores).
* ```for col in df.select_dtypes(include='object').columns:  df[col] = df[col].str.strip().str.replace(r'\s+', ' ', regex=True)```. Aplicar em todo o DataFrame.
## ✅ Letras maiúsculas/minúsculas misturadas
## ✅ Datas em formatos diferentes (dd/mm/yyyy, yyyy-mm-dd)
## ✅ Unidades diferentes (ex: metros vs. centímetros)
## ✅ Codificação errada (ex: acentos quebrados por UTF-8/Latin-1)
