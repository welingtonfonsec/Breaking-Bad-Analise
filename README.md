# ESTUDO DE CASO: 
## A Jornada de Breaking Bad: De Série Promissora a Fenômeno Aclamado – Os Dados Comprovam

Autor: Welington Fonseca

Apresentação em forma de [Storytelling no Power BI](https://app.powerbi.com/view?r=eyJrIjoiOGU4Mzc2YTUtMDI1OS00ZDQzLTk2YjUtNjM2MmQ5NDczYmUwIiwidCI6Ijk5NWRiNjhkLThmNGMtNGM5OS05NDA2LTkzOTVjNGY3ZDA0ZSJ9)

## Índice

[1. Introdução](#introdução)

[2. Tarefa de Negócios](#tarefa-de-negócios)

[3. Dados](#dados)

[4. Processamento e Exploração](#processamento-e-exploração)

[5. Análise e Visualização](#análise-e-visualização)







## Introdução

Este estudo de caso integra um portfólio de análise de dados e se aprofunda na aclamada série 'Breaking Bad', um fenômeno televisivo criado por Vince Gilligan, composta por 5 temporadas e um total de 62 episódios, originalmente exibidos entre **20 de janeiro de 2008 e 29 de setembro de 2013**. O projeto utiliza dados de avaliação do IMDb (Internet Movie Database) e audiência dos EUA para desvendar os segredos por trás de seu sucesso global. O objetivo não é apenas apresentar números; ele constrói um storytelling completo, traçando a trajetória da série desde seu início promissor, passando por sua ascensão meteórica, até sua consagração com episódios lendários e um final épico.

Para a obtenção dos insights, o trabalho iniciou-se com a etapa de Extração, Transformação e Carga (ETL) dos dados. Este processo envolveu a limpeza, organização e unificação dos datasets de episódios e avaliações, conforme detalhado nos arquivos breaking_bad.py. Posteriormente, as visualizações e análises foram desenvolvidas tanto em Python (com a criação de gráficos específicos) quanto no Power BI. No Power BI, a comunicação dos insights chave foi estruturada em um storytelling visual detalhado, e, adicionalmente, foi preparada uma apresentação mais concisa, também em Power BI, focada nos pontos mais impactantes.

O propósito deste estudo é ilustrar como a análise de dados e o storytelling visual são ferramentas poderosas. Elas permitem validar percepções, identificar tendências e, neste contexto, provar com base em evidências numéricas por que 'Breaking Bad' é considerada uma das maiores obras televisivas de todos os tempos.


## Tarefa de negócios

Este estudo de caso de 'Breaking Bad' foi desenvolvido para demonstrar a aplicação prática da análise de dados na identificação de tendências e na formulação de recomendações estratégicas, habilidades essenciais para desafios de negócio. A partir da análise detalhada de uma propriedade intelectual de entretenimento, o projeto é capaz de responder a questões fundamentais que são diretamente transferíveis a outros contextos, como o uso de dispositivos inteligentes e a estratégia de marketing de produtos.

Especificamente, este estudo de caso permite responder a perguntas como:

  * Quais são os padrões de evolução da qualidade e engajamento do público de 'Breaking Bad' ao longo do tempo? 
  * Como a aceitação inicial de 'Breaking Bad' se compara à sua performance no auge da série? 
  * Quais características ou momentos de 'Breaking Bad' geraram os maiores picos de satisfação e engajamento dos usuários? 
  * Como a análise de dados pode quantificar o sucesso de 'Breaking Bad' e fornecer argumentos baseados em evidências? 
  * De que forma insights baseados em dados sobre 'Breaking Bad' podem apoiar ou influenciar estratégias de marketing e comunicação de um produto, ao destacar seus pontos fortes e sua trajetória de sucesso?

## Dados

* **Fonte de dados**: A [fonte de dados](https://www.kaggle.com/datasets/bcruise/breaking-bad-episode-data/data) utilizada neste estudo de caso provém do Kaggle, especificamente o dataset "Breaking Bad Episode Data".
* **Acessibilidade e privacidade de dados**: O proprietário dedicou o trabalho ao domínio público renunciando a todos os seus direitos sobre o trabalho em todo o mundo sob a lei de direitos autorais, incluindo todos os direitos relacionados e conexos, na medida permitida por lei. É possível copiar, modificar, distribuir e executar o trabalho, mesmo para fins comerciais, tudo sem pedir permissão.    
* **Tamanho e formato**: Dois arquivos no formato CSV (breaking_bad_episodes.csv e breaking_bad_imdb.csv), com um tamanho compacto e gerenciável para análise tabular;
* **Intervalo dos dados da análise**: Os dados abrangem o período de exibição original da série, de **20 de janeiro de 2008 a 29 de setembro de 2013**; 
* **Mais informações**: 
  * O conjunto de dados contém registros detalhados para cada um dos 62 episódios da série;
  * Cada episódio possui identificadores únicos, como número geral do episódio, número na temporada e título;
  * Os arquivos CSV apresentam diferentes dados quantitativos e textuais por episódio, como título, diretor, roteirista, data de exibição original, avaliação do IMDb, número de votos no IMDb e audiência nos EUA em milhões;
  * Os dados são registrados por episódio, com sua respectiva data de exibição.
* **Pontos negativos** da base de dados: 
  * Pequeno Tamanho: Embora o dataset seja completo para o escopo da série, a quantidade de registros (62 episódios) é considerada pequena em comparação a bases de dados mais abrangentes, o que pode limitar análises estatísticas mais complexas em outros contextos;
  * Dados Ausentes ou Parciais: Identificou-se que alguns episódios apresentavam valores ausentes em certas colunas, como US_Viewers_Millions, especialmente nas primeiras temporadas, porém foi realizado um tratamento para preencher ou gerenciar esses valores ausentes, garantindo a integridade dos dados para a análise.
  
## Processamento e Exploração

### Carregamento dos Dados

```
import pandas as pd
from google.colab import drive

# Montar o Google Drive
drive.mount('/content/drive')

# Carregando o primeiro arquivo
df_episodes = pd.read_csv('/content/drive/MyDrive/Projetos_Analise_de_Dados/Breaking_Bad/breaking_bad_episodes.csv')

# Carregando o segundo arquivo
df_imdb = pd.read_csv('/content/drive/MyDrive/Projetos_Analise_de_Dados/Breaking_Bad/breaking_bad_imdb.csv')
```

### Exploração Inicial e Compreensão dos Dados

#### Explorando df_episodes

```
#Visualizando as primeiras linhas
print("\n1. df_episodes.head():")
print(df_episodes.head())
```
```
# df_episodes.head():
   season  episode_num_in_season  episode_num_overall  \
0       1                      1                    1   
1       1                      2                    2   
2       1                      3                    3   
3       1                      4                    4   
4       1                      5                    5   

                           title     directed_by      written_by  \
0                          Pilot  Vince Gilligan  Vince Gilligan   
1            Cat's in the Bag...  Adam Bernstein  Vince Gilligan   
2  ...And the Bag's in the River  Adam Bernstein  Vince Gilligan   
3                     Cancer Man       Jim McKay  Vince Gilligan   
4                    Gray Matter    Tricia Brock       Patty Lin   

  original_air_date  us_viewers  
0        2008-01-20   1410000.0  
1        2008-01-27   1490000.0  
2        2008-02-10   1080000.0  
3        2008-02-17   1090000.0  
4        2008-02-24    970000.0  
```

Dataset `df_episodes` possui 8 colunas:

- **Season**: O número da temporada a que o episódio pertence;
- **Episode_Number_in_Season**: O número do episódio dentro daquela temporada específica;
- **Episode_Number_Overall**: O número sequencial do episódio considerando a série inteira;
- **Title**: O título do episódio;
- **Directed_by**: O nome do diretor do episódio;
- **Written_by**: O nome do roteirista do episódio;
- **Original_Air_Date**: A data em que o episódio foi originalmente exibido nos Estados Unidos;
- **US_Viewers_Millions**: O número de espectadores (em milhões) que assistiram à primeira exibição do episódio nos EUA.

```
# Visualizando as últimas linhas
print("\n2. df_episodes.tail():")
print(df_episodes.tail())


df_episodes.tail():
    season  episode_num_in_season  episode_num_overall          title  \
57       5                     12                   58      Rabid Dog   
58       5                     13                   59    To'hajiilee   
59       5                     14                   60     Ozymandias   
60       5                     15                   61  Granite State   
61       5                     16                   62         Felina   

          directed_by            written_by original_air_date  us_viewers  
57         Sam Catlin            Sam Catlin        2013-09-01   4410000.0  
58  Michelle MacLaren        George Mastras        2013-09-08   5110000.0  
59       Rian Johnson  Moira Walley-Beckett        2013-09-15   6370000.0  
60        Peter Gould           Peter Gould        2013-09-22   6580000.0  
61     Vince Gilligan        Vince Gilligan        2013-09-29  10280000.0
```

Dataset df_episodes possui **62 linhas** contando com a linha 0. Informação que confirma o número de episódios da série.

```
# Obtendo informações sobre tipos de dados e valores não nulos
print("\n3. df_episodes.info():")
df_episodes.info()

df_episodes.info():
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 62 entries, 0 to 61
Data columns (total 8 columns):
 #   Column                 Non-Null Count  Dtype  
---  ------                 --------------  -----  
 0   season                 62 non-null     int64  
 1   episode_num_in_season  62 non-null     int64  
 2   episode_num_overall    62 non-null     int64  
 3   title                  62 non-null     object 
 4   directed_by            62 non-null     object 
 5   written_by             62 non-null     object 
 6   original_air_date      62 non-null     object 
 7   us_viewers             57 non-null     float64
dtypes: float64(1), int64(3), object(4)
memory usage: 4.0+ KB
```
As colunas (season, episode_num_in_season, episode_num_overall, title, directed_by, written_by) parecem estar com os tipos de dados corretos e sem valores ausentes.

Porém, temos problemas:

original_air_date (object): Embora não tenha valores ausentes, o tipo é object (string). Para fazer análises temporais (como evolução por data), será necessário converter esta coluna para o tipo datetime.
us_viewers (float64): 57 non-null de 62. Ponto Crucial de Tratamento! Esta coluna possui 5 valores ausentes. O tipo float64 está correto para representar milhões de espectadores (números com casas decimais), mas será necessário decidir como tratar esses valores faltantes.

```
# Gerando estatísticas descritivas para colunas numéricas
print("\n5. df_episodes.describe():")
print(df_episodes.describe())

df_episodes.describe():
          season  episode_num_in_season  episode_num_overall    us_viewers
count  62.000000              62.000000            62.000000  5.700000e+01
mean    3.290323               7.048387            31.500000  2.324386e+06
std     1.359690               4.074822            18.041619  1.719224e+06
min     1.000000               1.000000             1.000000  9.700000e+05
25%     2.000000               4.000000            16.250000  1.460000e+06
50%     3.000000               7.000000            31.500000  1.710000e+06
75%     4.750000              10.000000            46.750000  2.290000e+06
max     5.000000              16.000000            62.000000  1.028000e+07
```

Estrutura da Série:

- **count (62 em todas)**: Confirma que temos dados para todos os 62 episódios.
- **season**: O valor máximo de 5 confirma que a série tem **5 temporadas**.
- **episode_num_in_season**: O valor máximo de 16 revela que uma temporada teve **16 episódios**.
- **episode_num_overall**: O valor máximo de 62 confirma o **total de episódios na série**.

---

Audiência (`us_viewers`):

**Destaques da coluna `us_viewers`:**
- **count (57.000000)**: Há **5 valores ausentes** (62 total - 57 preenchidos).  Um ponto que precisa de tratamento.
- **mean (2.324386 milhões)**: A **média de espectadores por episódio** em toda a série.
- **min (0.970000 milhões)**: O episódio **menos assistido** teve **970 mil espectadores**.
- **max (10.280000 milhões)**: O episódio **mais assistido** teve **10.28 milhões de espectadores**.
- **50% (mediana): 1.71 milhões**: Metade dos episódios teve **menos de 1.71 milhões de espectadores**.  
  Isso indica que a audiência foi **crescendo gradualmente ao longo da série**.

#### Explorando df_imdb
```
# Visualizando as primeiras linhas
print("\n1. df_imdb.head():")
print(df_imdb.head())

df_imdb.head():
   season  episode_num                          title original_air_date  \
0       1            1                          Pilot        2008-01-20   
1       1            2            Cat's in the Bag...        2008-01-27   
2       1            3  ...And the Bag's in the River        2008-02-10   
3       1            4                     Cancer Man        2008-02-17   
4       1            5                    Gray Matter        2008-02-24   

   imdb_rating  total_votes                                               desc  
0          9.1        30419  Diagnosed with terminal lung cancer, chemistry...  
1          8.7        22282  After their first drug deal goes terribly wron...  
2          8.8        21633  Walt and Jesse clean up after the bathtub inci...  
3          8.3        20912  Walt tells the rest of his family about his ca...  
4          8.4        20546  Walt rejects everyone who tries to help him wi... 
```

Dataset df_episodes possui 8 colunas:
- **season**: Número da temporada.
- **episode_num**: Número do episódio dentro da temporada.
- **title**: Título do episódio.
- **original_air_date**: Data de exibição original.
- **imdb_rating**: Avaliação do episódio no IMDb.
- **total_votes**: Número total de votos no IMDb.
- **desc**: Descrição ou sinopse do episódio.

```
# Visualizando as últimas linhas
print("\n2. df_imdb.tail():")
print(df_imdb.tail())

df_imdb.tail():
    season  episode_num          title original_air_date  imdb_rating  \
57       5           12      Rabid Dog        2013-09-01          9.2   
58       5           13    To'hajiilee        2013-09-08          9.8   
59       5           14     Ozymandias        2013-09-15         10.0   
60       5           15  Granite State        2013-09-22          9.7   
61       5           16         Felina        2013-09-29          9.9   

    total_votes                                               desc  
57        23661  Walt discovers Jesse broke into his house and ...  
58        39551  Jesse and Hank come up with an idea to take Wa...  
59       150341  Walt goes on the run. Jesse is taken hostage. ...  
60        39590  Walt struggles as he adapts to aspects of his ...  
61       101628  Walter White makes one last attempt to secure ... 
```

Dataset df_episodes possui **62 linhas** contando com a linha 0. Como no dataset anterior.

```
# Obtendo informações sobre tipos de dados e valores não nulos
print("\n3. df_imdb.info():")
df_imdb.info()

3. df_imdb.info():
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 62 entries, 0 to 61
Data columns (total 7 columns):
 #   Column             Non-Null Count  Dtype  
---  ------             --------------  -----  
 0   season             62 non-null     int64  
 1   episode_num        62 non-null     int64  
 2   title              62 non-null     object 
 3   original_air_date  62 non-null     object 
 4   imdb_rating        62 non-null     float64
 5   total_votes        62 non-null     int64  
 6   desc               62 non-null     object 
dtypes: float64(1), int64(3), object(3)
memory usage: 3.5+ KB
```

Qualidade dos Dados - Dataset IMDb:
Valores Ausentes:
Não há valores ausentes em nenhuma coluna deste DataFrame. Isso é um ponto muito positivo para a qualidade dos dados do IMDb!

Tipo de Dados Incorreto para Análise:
A coluna original_air_date está como object (string) e precisa ser convertida para datetime, assim como foi necessário no df_episodes.

Outras Colunas:
As demais colunas (season, episode_num, title, imdb_rating, total_votes, desc) parecem estar com os tipos de dados corretos e sem valores ausentes.

```
# Gerando estatísticas descritivas para colunas numéricas
print("\n5. df_imdb.describe():")
print(df_imdb.describe())

df_imdb.describe():
          season  episode_num  imdb_rating    total_votes
count  62.000000    62.000000    62.000000      62.000000
mean    3.290323     7.048387     9.027419   25414.838710
std     1.359690     4.074822     0.507378   20045.035902
min     1.000000     1.000000     7.900000   16545.000000
25%     2.000000     4.000000     8.700000   17714.250000
50%     3.000000     7.000000     8.900000   20582.500000
75%     4.750000    10.000000     9.450000   23945.000000
max     5.000000    16.000000    10.000000  150341.000000
```

Estrutura (Revisão):

- As colunas `season` e `episode_num` fornecem informações consistentes sobre a estrutura da série, com **62 episódios distribuídos em 5 temporadas**, como já observado no `df_episodes`.

---

Aclamação da Crítica e do Público (`imdb_rating`):

- **count (62)**: Temos **avaliações do IMDb para todos os 62 episódios**, sem valores ausentes.
- **mean (9.017742)**: A **média de 9.02** de notas no IMDb
- **min (7.90)**: O episódio com a nota mais baixa no IMDb
- **max (10.00)**: Um episódio atingiu a **nota máxima de 10.0** .
- **50% (mediana): 9.00**: Metade dos episódios tem **nota igual ou superior a 9.0**.

---

Engajamento Massivo do Público (`total_votes`):

- **count (62)**: Sem valores ausentes.
- **mean (25.414,84 votos)**: A média de mais de **25 mil votos por episódio**
- **min (16.545 votos)**: Episódio com **menos votos** teve mais de **16 mil votos**.
- **max (158.341 votos)**: Esse valor é o **dado mais impactante**: reflete como a série se tornou **viral**, especialmente nos episódios finais.

#### Tratamento de Valores Ausentes (Missing Values)

#### Identificar Valores Ausentes

Anteriormente identificamos que a variável us_viewers (espectadores) apresentava 5 valores ausentes. Chegou o momento de ajustar esse problema. Primeiro, vamos confirmar a contagem de valores ausentes em ambos os DataFrames, para ter certeza e documentar.

```
print("--- Verificação de Valores Ausentes ---")

print("\nValores ausentes em df_episodes:")
print(df_episodes.isnull().sum())

print("\nValores ausentes em df_imdb:")
print(df_imdb.isnull().sum())

--- Verificação de Valores Ausentes ---

Valores ausentes em df_episodes:
season                   0
episode_num_in_season    0
episode_num_overall      0
title                    0
directed_by              0
written_by               0
original_air_date        0
us_viewers               5
dtype: int64

Valores ausentes em df_imdb:
season               0
episode_num          0
title                0
original_air_date    0
imdb_rating          0
total_votes          0
desc                 0
dtype: int64
```

Com a confirmação acima, seguiremos com os próximos passos. Note que outro dataset df_imdb não há valores ausentes.

#### Estratégia de Tratamento para us_viewers em df_episodes

Optei por preencher os valores ausentes com a mediana porque ela é uma medida de tendência central menos influenciada por outliers. Como a distribuição da audiência apresenta assimetrias — com alguns episódios muito acima da média —, a mediana se mostra uma alternativa mais robusta e representativa do comportamento típico da variável.

```
print("\n--- Tratamento de Valores Ausentes em df_episodes ---")
# 1. Calculando a mediana da coluna 'us_viewers'
median_us_viewers = df_episodes['us_viewers'].median()
print(f"Mediana da coluna 'us_viewers': {median_us_viewers:.2f} milhões")

# 2. Preenchendo os valores ausentes (NaN) na coluna 'us_viewers' com a mediana
df_episodes['us_viewers'].fillna(median_us_viewers, inplace=True)
print("Valores ausentes em 'us_viewers' preenchidos com a mediana.")

# 3. Verificar novamente os valores ausentes para confirmar o tratamento
print("\nVerificação final de valores ausentes em df_episodes:")
print(df_episodes.isnull().sum())

--- Tratamento de Valores Ausentes em df_episodes ---
Mediana da coluna 'us_viewers': 1710000.00 milhões
Valores ausentes em 'us_viewers' preenchidos com a mediana.

Verificação final de valores ausentes em df_episodes:
season                   0
episode_num_in_season    0
episode_num_overall      0
title                    0
directed_by              0
written_by               0
original_air_date        0
us_viewers               0
dtype: int64
<ipython-input-43-67d1357ea5e9>:8: FutureWarning: A value is trying to be set on a copy of a DataFrame or Series through chained assignment using an inplace method.
The behavior will change in pandas 3.0. This inplace method will never work because the intermediate object on which we are setting values always behaves as a copy.

For example, when doing 'df[col].method(value, inplace=True)', try using 'df.method({col: value}, inplace=True)' or df[col] = df[col].method(value) instead, to perform the operation inplace on the original object.

df_episodes['us_viewers'].fillna(median_us_viewers, inplace=True)

```

#### Padronização e Limpeza de Dados

#### Conversão de Tipos de Dados

A conversão de original_air_date para datetime é essencial, já que o formato atual como texto limita qualquer análise temporal.

```
print("--- 4.1. Conversão de Tipos de Dados ---")

# Convertendo 'original_air_date' em df_episodes para datetime
df_episodes['original_air_date'] = pd.to_datetime(df_episodes['original_air_date'])
print("Coluna 'original_air_date' em df_episodes convertida para datetime.")

# Convertendo 'original_air_date' em df_imdb para datetime
df_imdb['original_air_date'] = pd.to_datetime(df_imdb['original_air_date'])
print("Coluna 'original_air_date' em df_imdb convertida para datetime.")

# Verificando os tipos de dados novamente para confirmar
print("\nNovos tipos de dados em df_episodes:")
df_episodes.info()

print("\nNovos tipos de dados em df_imdb:")
df_imdb.info()

--- 4.1. Conversão de Tipos de Dados ---
Coluna 'original_air_date' em df_episodes convertida para datetime.
Coluna 'original_air_date' em df_imdb convertida para datetime.

Novos tipos de dados em df_episodes:
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 62 entries, 0 to 61
Data columns (total 8 columns):
 #   Column                 Non-Null Count  Dtype         
---  ------                 --------------  -----         
 0   season                 62 non-null     int64         
 1   episode_num_in_season  62 non-null     int64         
 2   episode_num_overall    62 non-null     int64         
 3   title                  62 non-null     object        
 4   directed_by            62 non-null     object        
 5   written_by             62 non-null     object        
 6   original_air_date      62 non-null     datetime64[ns]
 7   us_viewers             62 non-null     float64       
dtypes: datetime64[ns](1), float64(1), int64(3), object(3)
memory usage: 4.0+ KB

Novos tipos de dados em df_imdb:
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 62 entries, 0 to 61
Data columns (total 7 columns):
 #   Column             Non-Null Count  Dtype         
---  ------             --------------  -----         
 0   season             62 non-null     int64         
 1   episode_num        62 non-null     int64         
 2   title              62 non-null     object        
 3   original_air_date  62 non-null     datetime64[ns]
 4   imdb_rating        62 non-null     float64       
 5   total_votes        62 non-null     int64         
 6   desc               62 non-null     object        
dtypes: datetime64[ns](1), float64(1), int64(3), object(2)
memory usage: 3.5+ KB
```


#### Unificação/Combinação de Dados

#### Criar a Coluna episode_ID em df_episodes

Agora será criada uma coluna chamada episode_ID concatenando a season e episode_num_in_season, com um formato SXXEXX (Temporada X, Episódio Y).
```
print("--- 6.1. Criar a Coluna 'episode_ID' em df_episodes ---")

# Para garantir a formatação 'S01E01', convertemos para string e preenchemos com zeros à esquerda
df_episodes['episode_ID'] = 'S' + df_episodes['season'].astype(str).str.zfill(2) + \
                            'E' + df_episodes['episode_num_in_season'].astype(str).str.zfill(2)

print("Coluna 'episode_ID' criada em df_episodes.")
print(df_episodes[['season', 'episode_num_in_season', 'episode_ID']].head())

--- 6.1. Criar a Coluna 'episode_ID' em df_episodes ---
Coluna 'episode_ID' criada em df_episodes.
   season  episode_num_in_season episode_ID
0       1                      1     S01E01
1       1                      2     S01E02
2       1                      3     S01E03
3       1                      4     S01E04
4       1                      5     S01E05
```

#### Criar a Coluna episode_ID em df_imdb

```
Da mesma forma, criaremos a coluna episode_ID em df_imdb usando season e episode_num.

print("\n--- 6.2. Criar a Coluna 'episode_ID' em df_imdb ---")

# Para garantir a formatação 'S01E01', convertemos para string e preenchemos com zeros à esquerda
df_imdb['episode_ID'] = 'S' + df_imdb['season'].astype(str).str.zfill(2) + \
                        'E' + df_imdb['episode_num'].astype(str).str.zfill(2)

print("Coluna 'episode_ID' criada em df_imdb.")
print(df_imdb[['season', 'episode_num', 'episode_ID']].head())

--- 6.2. Criar a Coluna 'episode_ID' em df_imdb ---
Coluna 'episode_ID' criada em df_imdb.
   season  episode_num episode_ID
0       1            1     S01E01
1       1            2     S01E02
2       1            3     S01E03
3       1            4     S01E04
4       1            5     S01E05
```

#### Executar o Merge dos DataFrames Usando episode_ID

Agora que temos uma chave comum e única em ambos os DataFrames, podemos realizar o inner merge para juntar ambos de forma segura.

```
print("\n--- 6.3. Executar o Merge dos DataFrames Usando 'episode_ID' ---")

# Realizar o inner merge usando 'episode_ID' como chave
# Note que 'title' e 'original_air_date' ainda serão duplicados e renomeados com sufixos
df_combined = pd.merge(df_episodes, df_imdb,
                       on='episode_ID', # Apenas uma coluna de chave agora!
                       how='inner',
                       suffixes=('_episodes', '_imdb'))

print("DataFrames df_episodes e df_imdb combinados com sucesso em df_combined usando 'episode_ID'!")

# Verificar o shape do DataFrame combinado
print(f"\nShape do DataFrame combinado (df_combined): {df_combined.shape}")

# Exibir as primeiras linhas do DataFrame combinado para inspeção
print("\n--- Primeiras 5 linhas de df_combined ---")
print(df_combined.head())

--- 6.3. Executar o Merge dos DataFrames Usando 'episode_ID' ---
DataFrames df_episodes e df_imdb combinados com sucesso em df_combined usando 'episode_ID'!

Shape do DataFrame combinado (df_combined): (62, 16)

--- Primeiras 5 linhas de df_combined ---
   season_episodes  episode_num_in_season  episode_num_overall  \
0                1                      1                    1   
1                1                      2                    2   
2                1                      3                    3   
3                1                      4                    4   
4                1                      5                    5   

                  title_episodes     directed_by      written_by  \
0                          Pilot  Vince Gilligan  Vince Gilligan   
1            Cat's in the Bag...  Adam Bernstein  Vince Gilligan   
2  ...And the Bag's in the River  Adam Bernstein  Vince Gilligan   
3                     Cancer Man       Jim McKay  Vince Gilligan   
4                    Gray Matter    Tricia Brock       Patty Lin   

  original_air_date_episodes  us_viewers episode_ID  season_imdb  episode_num  \
0                 2008-01-20   1410000.0     S01E01            1            1   
1                 2008-01-27   1490000.0     S01E02            1            2   
2                 2008-02-10   1080000.0     S01E03            1            3   
3                 2008-02-17   1090000.0     S01E04            1            4   
4                 2008-02-24    970000.0     S01E05            1            5   

                      title_imdb original_air_date_imdb  imdb_rating  \
0                          Pilot             2008-01-20          9.1   
1            Cat's in the Bag...             2008-01-27          8.7   
2  ...And the Bag's in the River             2008-02-10          8.8   
3                     Cancer Man             2008-02-17          8.3   
4                    Gray Matter             2008-02-24          8.4   

   total_votes                                               desc  
0        30419  Diagnosed with terminal lung cancer, chemistry...  
1        22282  After their first drug deal goes terribly wron...  
2        21633  Walt and Jesse clean up after the bathtub inci...  
3        20912  Walt tells the rest of his family about his ca...  
4        20546  Walt rejects everyone who tries to help him wi...  

```

#### Tratamento de Colunas

Após o merge, ainda teremos algumas colunas redundantes que vieram de ambos os DataFrames (além do episode_ID que foi a chave de junção). Mas antes, será preciso mudar o nome de algumas para deixar de mais facil entendimento.
```
# Renomeando as colunas que vieram do df_imdb para algo mais claro
df_combined.rename(columns={
    'total_votes': 'imdb_total_votes',
    'desc': 'episode_description',
    'season_imdb': 'season_from_imdb',
    'episode_num_in_season_imdb': 'episode_num_in_season_from_imdb'
}, inplace=True)


# Removendo as colunas que não precisamos
# Vamos remover a versão '_imdb' das colunas que já temos do df_episodes (title, original_air_date)
# E também as chaves season e episode_num_in_season que vieram do df_imdb (se você quer manter apenas a de df_episodes)
columns_to_drop = [
    'season_from_imdb', # Já temos 'season' do df_episodes
    'episode_num_in_season_from_imdb', # Já temos 'episode_num_in_season' do df_episodes
    'title_imdb', # Já temos 'title' do df_episodes
    'original_air_date_imdb' # Já temos 'original_air_date' do df_episodes
]


# Remover as colunas se existirem no DataFrame
for col in columns_to_drop:
    if col in df_combined.columns:
        df_combined.drop(columns=[col], inplace=True)
        print(f"Coluna '{col}' removida.")

Coluna 'season_from_imdb' removida.
Coluna 'title_imdb' removida.
Coluna 'original_air_date_imdb' removida.


# Uma última verificação para o shape final
print(f"\nShape final do DataFrame combinado (df_combined) após remover redundâncias: {df_combined.shape}")

Shape final do DataFrame combinado (df_combined) após remover redundâncias: (62, 13)

# E as colunas finais
print("\nColunas finais do DataFrame combinado:")
print(df_combined.columns.tolist())

Colunas finais do DataFrame combinado:
['season_episodes', 'episode_num_in_season', 'episode_num_overall', 'title_episodes', 'directed_by', 'written_by', 'original_air_date_episodes', 'us_viewers', 'episode_ID', 'episode_num', 'imdb_rating', 'imdb_total_votes', 'episode_description']

# Exibir as primeiras linhas do DataFrame FINAL combinado para inspeção
print("\n--- Primeiras 5 linhas do df_combined FINAL ---")
print(df_combined.head()


--- Primeiras 5 linhas do df_combined FINAL ---
   season_episodes  episode_num_in_season  episode_num_overall  \
0                1                      1                    1   
1                1                      2                    2   
2                1                      3                    3   
3                1                      4                    4   
4                1                      5                    5   

                  title_episodes     directed_by      written_by  \
0                          Pilot  Vince Gilligan  Vince Gilligan   
1            Cat's in the Bag...  Adam Bernstein  Vince Gilligan   
2  ...And the Bag's in the River  Adam Bernstein  Vince Gilligan   
3                     Cancer Man       Jim McKay  Vince Gilligan   
4                    Gray Matter    Tricia Brock       Patty Lin   

  original_air_date_episodes  us_viewers episode_ID  episode_num  imdb_rating  \
0                 2008-01-20   1410000.0     S01E01            1          9.1   
1                 2008-01-27   1490000.0     S01E02            2          8.7   
2                 2008-02-10   1080000.0     S01E03            3          8.8   
3                 2008-02-17   1090000.0     S01E04            4          8.3   
4                 2008-02-24    970000.0     S01E05            5          8.4   

   imdb_total_votes                                episode_description  
0             30419  Diagnosed with terminal lung cancer, chemistry...  
1             22282  After their first drug deal goes terribly wron...  
2             21633  Walt and Jesse clean up after the bathtub inci...  
3             20912  Walt tells the rest of his family about his ca...  
4             20546  Walt rejects everyone who tries to help him wi...

```

#### Verificação Final e Preparação para Análise

```
print("--- 7.1. Verificação Final: df_combined.info() ---")
print("\nInformações sobre o DataFrame combinado após todo o tratamento:")
df_combined.info()

print("\n\n--- 7.1. Verificação Final: df_combined.describe() ---")
print("\nEstatísticas descritivas do DataFrame combinado após todo o tratamento:")
print(df_combined.describe())

--- 7.1. Verificação Final: df_combined.info() ---

Informações sobre o DataFrame combinado após todo o tratamento:
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 62 entries, 0 to 61
Data columns (total 13 columns):
 #   Column                      Non-Null Count  Dtype         
---  ------                      --------------  -----         
 0   season_episodes             62 non-null     int64         
 1   episode_num_in_season       62 non-null     int64         
 2   episode_num_overall         62 non-null     int64         
 3   title_episodes              62 non-null     object        
 4   directed_by                 62 non-null     object        
 5   written_by                  62 non-null     object        
 6   original_air_date_episodes  62 non-null     datetime64[ns]
 7   us_viewers                  62 non-null     float64       
 8   episode_ID                  62 non-null     object        
 9   episode_num                 62 non-null     int64         
 10  imdb_rating                 62 non-null     float64       
 11  imdb_total_votes            62 non-null     int64         
 12  episode_description         62 non-null     object        
dtypes: datetime64[ns](1), float64(2), int64(5), object(5)
memory usage: 6.4+ KB


--- 7.1. Verificação Final: df_combined.describe() ---

Estatísticas descritivas do DataFrame combinado após todo o tratamento:
       season_episodes  episode_num_in_season  episode_num_overall  \
count        62.000000              62.000000            62.000000   
mean          3.290323               7.048387            31.500000   
min           1.000000               1.000000             1.000000   
25%           2.000000               4.000000            16.250000   
50%           3.000000               7.000000            31.500000   
75%           4.750000              10.000000            46.750000   
max           5.000000              16.000000            62.000000   
std           1.359690               4.074822            18.041619   

          original_air_date_episodes    us_viewers  episode_num  imdb_rating  \
count                             62  6.200000e+01    62.000000    62.000000   
mean   2010-11-13 13:09:40.645161216  2.274839e+06     7.048387     9.027419   
min              2008-01-20 00:00:00  9.700000e+05     1.000000     7.900000   
25%              2009-05-04 18:00:00  1.492500e+06     4.000000     8.700000   
50%              2010-06-02 12:00:00  1.710000e+06     7.000000     8.900000   
75%              2012-05-06 00:00:00  2.267500e+06    10.000000     9.450000   
max              2013-09-29 00:00:00  1.028000e+07    16.000000    10.000000   
std                              NaN  1.655870e+06     4.074822     0.507378   

       imdb_total_votes  
count         62.000000  
mean       25414.838710  
min        16545.000000  
25%        17714.250000  
50%        20582.500000  
75%        23945.000000  
max       150341.000000  
std        20045.035902
```

Após o merge dos dois DataFrames, o resultado ficou excelente: mantivemos os 62 episódios e todas as colunas esperadas estão lá. A renomeação da sinopse para episode_description funcionou, assim como o tratamento de valores ausentes em us_viewers — agora todas as colunas estão completas, sem nenhum NaN.

Em relação aos tipos de dados, tudo está no formato ideal: datas convertidas corretamente, colunas numéricas e categóricas bem definidas. A saída do .describe() só confirma o que já vínhamos observando — dados bem estruturados, padrões claros de audiência e notas altas no IMDb. Isso mostra que o processo de integração e limpeza foi bem-sucedido e o dataset final está pronto para análises mais aprofundadas.

## Análise e Visualização

#### A Jornada de Breaking Bad: De Série Promissora a Fenômeno Aclamado – Os Dados Comprovam

###### Início Promissor

```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Filtrar apenas a 1ª temporada
temporada_1 = df_combined[df_combined['season_episodes'] == 1]

# Definir estilo
sns.set(style="whitegrid")
plt.figure(figsize=(12, 6))

# Gráfico 1: IMDb Rating por episódio da 1ª temporada
sns.barplot(data=temporada_1, x="episode_num_in_season", y="imdb_rating", palette="Blues_d")
plt.title("Avaliação IMDb por Episódio - Temporada 1")
plt.xlabel("Episódio")
plt.ylabel("IMDb Rating")
plt.ylim(0, 10)
plt.show()
```

<img src="https://github.com/welingtonfonsec/Breaking-Bad-Analise/blob/main/Graficos/1.png" alt="" width="50%">

```
plt.figure(figsize=(12, 6))
sns.barplot(data=temporada_1, x="episode_num_in_season", y="imdb_total_votes", palette="Greens_d")
plt.title("Total de Votos no IMDb por Episódio - Temporada 1")
plt.xlabel("Episódio")
plt.ylabel("Número de Votos")
plt.show()
```

<img src="https://github.com/welingtonfonsec/Breaking-Bad-Analise/blob/main/Graficos/2.png" alt="" width="50%">

```
plt.figure(figsize=(12, 6))
sns.barplot(data=temporada_1, x="episode_num_in_season", y=temporada_1["us_viewers"] / 1_000_000, palette="Oranges_d")
plt.title("Audiência nos EUA por Episódio - Temporada 1")
plt.xlabel("Episódio")
plt.ylabel("Espectadores (milhões)")
plt.ylim(0, 2)  # limite ajustado conforme valores da 1ª temporada (~1.5M)
plt.show()
```

<img src="https://github.com/welingtonfonsec/Breaking-Bad-Analise/blob/main/Graficos/3.png" alt="" width="50%">

Mesmo em seus primeiros episódios, Breaking Bad já mostrava sinais claros de qualidade e potencial. A 1ª temporada apresentou avaliações sólidas no IMDb — todas acima de 8 —, um volume considerável de votos do público, e uma audiência que, embora modesta no início, se manteve estável e engajada até o final da temporada. Esses dados mostram que a série começou bem, conquistando aos poucos um público fiel e uma recepção crítica muito positiva.

E o mais interessante vem agora: a partir da segunda temporada, esse engajamento inicial se transforma em crescimento acelerado — tanto em popularidade quanto em aclamação crítica. Vamos ver como Breaking Bad saiu de um bom começo para se tornar um verdadeiro fenômeno.

##### Crescimento e Reconhecimento
```
plt.figure(figsize=(14, 6))
sns.lineplot(data=df_combined, x="episode_num_overall", y="imdb_rating", marker="o", color="steelblue")
plt.title("Evolução da Avaliação IMDb por Episódio")
plt.xlabel("Episódio (ordem geral)")
plt.ylabel("IMDb Rating")
plt.ylim(0, 10)
plt.grid(True)
plt.show()
```

<img src="https://github.com/welingtonfonsec/Breaking-Bad-Analise/blob/main/Graficos/4.png" alt="" width="50%">
```
plt.figure(figsize=(10, 6))
sns.barplot(data=df_combined, x="season_episodes", y="imdb_rating", palette="Blues_d")
plt.title("Média da Avaliação IMDb por Temporada")
plt.xlabel("Temporada")
plt.ylabel("IMDb Rating (Média)")
plt.ylim(0, 10)
plt.show()
```

<img src="https://github.com/welingtonfonsec/Breaking-Bad-Analise/blob/main/Graficos/5.png" alt="" width="50%">

```
plt.figure(figsize=(14, 6))
sns.lineplot(data=df_combined, x="episode_num_overall", y="imdb_total_votes", marker="o", color="seagreen")
plt.title("Total de Votos no IMDb por Episódio")
plt.xlabel("Episódio (ordem geral)")
plt.ylabel("Número de Votos")
plt.grid(True)
plt.show()
```

<img src="https://github.com/welingtonfonsec/Breaking-Bad-Analise/blob/main/Graficos/6.png" alt="" width="50%">

```
plt.figure(figsize=(14, 6))
sns.lineplot(data=df_combined, x="episode_num_overall", y=df_combined["us_viewers"] / 1_000_000, marker="o", color="darkorange")
plt.title("Audiência nos EUA por Episódio")
plt.xlabel("Episódio (ordem geral)")
plt.ylabel("Espectadores (milhões)")
plt.grid(True)
plt.show()
```

<img src="https://github.com/welingtonfonsec/Breaking-Bad-Analise/blob/main/Graficos/7.png" alt="" width="50%">

À medida que a série avança, Breaking Bad deixa de ser apenas promissora e se transforma em um fenômeno. As avaliações no IMDb seguem em uma trajetória crescente, com a média subindo temporada após temporada e diversos episódios ultrapassando a nota 9 — algo raro em séries de longa duração.

O público também responde: o número de votos por episódio dispara nas temporadas finais, chegando a picos impressionantes, sinal de um engajamento massivo e de uma base de fãs cada vez mais ativa. Esse crescimento é reforçado pelos dados de audiência: enquanto muitas séries perdem força com o tempo, Breaking Bad segue o caminho oposto, atraindo cada vez mais espectadores, especialmente em seus momentos decisivos.

Os dados não deixam dúvidas: a série não apenas manteve sua qualidade ao longo dos anos — ela evoluiu, conquistando crítica e público de forma consistente.

##### A Consagração – Episódios Lendários e um Final Épico

```
# Selecionar os top 5 episódios com maior nota

top_5 = df_combined.sort_values(by="imdb_rating", ascending=False).head(5)

plt.figure(figsize=(10, 6))
sns.barplot(data=top_5, y="title_episodes", x="imdb_rating", palette="Blues_d")
plt.title("Top 5 Episódios Mais Bem Avaliados no IMDb")
plt.xlabel("Nota IMDb")
plt.ylabel("Episódio")
plt.xlim(9, 10.1)
plt.show()
```

<img src="https://github.com/welingtonfonsec/Breaking-Bad-Analise/blob/main/Graficos/8.png" alt="" width="50%">

```
# Filtrar os últimos 6 episódios
final_episodios = df_combined.sort_values(by="episode_num_overall", ascending=False).head(6).sort_values(by="episode_num_overall")

plt.figure(figsize=(10, 6))
sns.lineplot(data=final_episodios, x="title_episodes", y=final_episodios["us_viewers"] / 1_000_000, marker="o", color="darkorange")
plt.title("Audiência dos Episódios Finais de Breaking Bad")
plt.xlabel("Episódio")
plt.ylabel("Espectadores (milhões)")
plt.xticks(rotation=45)
plt.grid(True)
plt.show()
```

<img src="https://github.com/welingtonfonsec/Breaking-Bad-Analise/blob/main/Graficos/9.png" alt="" width="50%">

```
plt.figure(figsize=(10, 6))
sns.barplot(data=final_episodios, x="title_episodes", y="imdb_total_votes", palette="Greens_d")
plt.title("Total de Votos no IMDb – Episódios Finais")
plt.xlabel("Episódio")
plt.ylabel("Número de Votos")
plt.xticks(rotation=45)
plt.show()
```

<img src="https://github.com/welingtonfonsec/Breaking-Bad-Analise/blob/main/Graficos/10.png" alt="" width="50%">

Os dados confirmam o que muitos fãs já sentem: Breaking Bad terminou em seu auge. O gráfico dos episódios mais bem avaliados mostra um feito raro — não apenas por ter um episódio com nota 10 (“Ozymandias”), mas por concentrar os cinco melhores episódios justamente nas temporadas finais. Isso demonstra uma consistência crescente, algo difícil de alcançar em séries longas.

Esse reconhecimento também se reflete na audiência: os últimos episódios apresentam uma escalada nítida de espectadores, culminando com mais de 10 milhões de pessoas assistindo ao episódio final, “Felina”. E o engajamento do público foi igualmente impressionante — episódios como “Ozymandias” e “Felina” somam dezenas de milhares de votos no IMDb, consolidando seu impacto cultural.

A reta final de Breaking Bad não apenas manteve o nível. Ela elevou a série a um patamar histórico.


##### Conclusão: Dados que Contam uma História

Ao longo das cinco temporadas de Breaking Bad, vimos uma narrativa poderosa não apenas na tela, mas também nos dados.

A série começou bem, com boas avaliações e uma base de público sólida. Mas foi com o passar dos episódios que ela realmente se transformou em um fenômeno. As notas no IMDb cresceram, a média por temporada se manteve altíssima, e os episódios finais atingiram um nível de aclamação raramente visto — inclusive com um episódio nota 10, milhares de votos e mais de 10 milhões de espectadores no encerramento.

A trajetória revelada pelos dados reforça aquilo que a crítica e o público já sabiam: Breaking Bad não só manteve sua qualidade ao longo do tempo — ela melhorou. Cresceu em relevância, conquistou uma audiência cada vez mais engajada e entregou um final à altura da sua história.

Mais do que estatísticas, esses números contam uma verdade difícil de ignorar: Breaking Bad é, sem dúvida, uma das maiores séries já feitas. E os dados só ajudam a provar isso.





