# Problemas de consistência em conjunto de dados

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
* ```df['coluna'] = df['coluna'].str.lower()```. Tudo em minúsculas.
* ```df['coluna'] = df['coluna'].str.upper()```. Tudo em maiúsculas.
* ```df['coluna'] = df['coluna'].str.capitalize()```. Primeira letra maiúscula.
* ```df['coluna'] = df['coluna'].str.title()```. Todas as palavras com primeira letra maiúscula (título).
* ```for col in df.select_dtypes(include='object').columns:  df[col] = df[col].str.strip().str.lower()```. Aplicar a todas as colunas de texto.
## ✅ Datas em formatos diferentes (dd/mm/yyyy, yyyy-mm-dd)
* ```df['data'] = pd.to_datetime(df['data'], dayfirst=True, errors='coerce')```. Usar pd.to_datetime() para conversão automática.
* ```df['data_formatada'] = df['data'].dt.strftime('%Y-%m-%d')```. Depois de converter, você pode formatar como string padronizada.
* ```df['data'].isna().sum()```. Verifique se há NaT (erros na conversão).
## ✅ Unidades diferentes (ex: metros vs. centímetros)
* ```df['altura_padrao'] = df['altura'].apply(lambda x: x / 100 if x > 10 else x)```. Se valores normais estão entre 1.0 e 2.5, então os que forem > 10 provavelmente estão em centímetros.
* ```df['peso_kg'] = df['peso'].apply(lambda x: x / 1000 if x > 300 else x)```. Para múltiplas unidades.
  * Origem - Destino - Fórmula
    * ```cm → m_____m_____x / 100```
    * ```mm → m_____m_____x / 1000```
    * ```kg → g_____g_____x * 1000```
    * ```ºF → ºC____ºC____(x - 32) * 5/9```
    * ```in → cm____cm____x * 2.54```
## ✅ Codificação errada (ex: acentos quebrados por UTF-8/Latin-1)
