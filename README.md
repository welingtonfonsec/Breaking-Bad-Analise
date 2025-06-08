# ESTUDO DE CASO: 
## A Jornada de Breaking Bad: De Série Promissora a Fenômeno Aclamado – Os Dados Comprovam

Autor: Welington Fonseca

Apresentação em forma de [Storytelling no Power BI](https://app.powerbi.com/view?r=eyJrIjoiOGU4Mzc2YTUtMDI1OS00ZDQzLTk2YjUtNjM2MmQ5NDczYmUwIiwidCI6Ijk5NWRiNjhkLThmNGMtNGM5OS05NDA2LTkzOTVjNGY3ZDA0ZSJ9)

## Índice

[1. Introdução](#introdução)

[2. Tarefa de Negócios](#tarefa-de-negócios)

[3. Dados](#dados)

[4. Processamento e Exploração](#processamento-e-exploração)







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

Dataset df_episodes possui 8 colunas:
**Season**: O número da temporada a que o episódio pertence;
**Episode_Number_in_Season**: O número do episódio dentro daquela temporada específica;
**Episode_Number_Overall**: O número sequencial do episódio considerando a série inteira;
**Title:** O título do episódio;
**Directed_by:** O nome do diretor do episódio;
**Written_by**: O nome do roteirista do episódio;
**Original_Air_Date:** A data em que o episódio foi originalmente exibido nos Estados Unidos;
**US_Viewers_Millions:** O número de espectadores (em milhões) que assistiram à primeira exibição do episódio nos EUA.

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


