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
1. df_episodes.head():
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


# ESTUDO DE CASO: A Jornada de Dados de Breaking Bad: Desvendando o Fenômeno Televisivo

**Autor: Welington Fonseca**

**Apresentação em forma de [Storytelling no Power BI](SUA_URL_DO_POWER_BI_AQUI)**
*(Certifique-se de publicar seu dashboard do Power BI Service e colar o link público aqui!)*
**Notebook Python de Processamento e Análise de Dados: [breaking_bad.ipynb](LINK_PARA_O_ARQUIVO_IPYNB_NO_SEU_REPOSITORIO)**
*(Substitua pelo link direto para o seu notebook .ipynb no seu repositório GitHub.)*

---

## Índice

1.  [Introdução](#introdução)
2.  [Tarefa de Negócios](#tarefa-de-negócios)
3.  [Dados](#dados)
4.  [Processamento e Exploração](#processamento-e-exploração)
5.  [Análise e Visualização](#análise-e-visualização)
6.  [Conclusão e Recomendações](#conclusão-e-recomendações)

---

## 1. Introdução

Este estudo de caso integra um **portfólio de análise de dados**, visando demonstrar a capacidade de **limpar, analisar e visualizar dados para identificar oportunidades potenciais de crescimento e influenciar estratégias de mercado**. Embora o foco primário desta análise seja a aclamada série 'Breaking Bad' — um fenômeno televisivo criado por **Vince Gilligan**, composta por **5 temporadas** e um total de **62 episódios**, originalmente exibidos entre **20 de janeiro de 2008 e 29 de setembro de 2013** — a metodologia empregada e os insights obtidos são diretamente aplicáveis a desafios de negócios, como a identificação de tendências no uso de dispositivos inteligentes e a otimização de estratégias de marketing para clientes.

O projeto utiliza dados de avaliação do IMDb (Internet Movie Database) e audiência dos EUA para desvendar os segredos por trás do sucesso global de 'Breaking Bad'. Ele constrói um **storytelling completo**, traçando a trajetória da série desde seu início promissor, passando por sua ascensão meteórica, até sua consagração com episódios lendários e um final épico. Esta abordagem reflete a capacidade de transformar dados brutos em narrativas acionáveis, essencial para compreender padrões de consumo e comportamento do usuário.

Para a obtenção dos insights, o trabalho iniciou-se com a etapa de **Extração, Transformação e Carga (ETL)** dos dados. Este processo envolveu a limpeza, organização e unificação dos datasets de episódios e avaliações. Posteriormente, as visualizações e análises foram desenvolvidas tanto em **Python** (com a criação de gráficos específicos para exploração detalhada) quanto no **Power BI**. No Power BI, a comunicação dos insights chave foi estruturada em um **storytelling visual detalhado**, e, adicionalmente, foi preparada uma **apresentação mais concisa**, também em Power BI, focada nos pontos mais impactantes, demonstrando adaptabilidade na entrega de informações.

O propósito deste estudo é ilustrar como a **análise de dados e o storytelling visual** são ferramentas poderosas. Elas permitem validar percepções, identificar tendências de engajamento (seja em entretenimento ou uso de dispositivos), e assim, fundamentar decisões estratégicas. Neste contexto, o projeto de 'Breaking Bad' serve como uma prova concreta da metodologia e das habilidades analíticas necessárias para responder a questões de negócio complexas.

---

## 2. Tarefa de Negócios

Este estudo de caso de 'Breaking Bad' foi concebido para demonstrar a aplicação prática da análise de dados na identificação de tendências e na formulação de recomendações estratégicas, habilidades essenciais para desafios de negócio. A partir da análise detalhada de uma propriedade intelectual de entretenimento, o projeto é capaz de responder a questões fundamentais que são diretamente transferíveis a outros contextos, como o uso de dispositivos inteligentes e a estratégia de marketing de produtos.

Especificamente, este estudo de caso permite responder a perguntas como:

* **Quais são os padrões de evolução da qualidade e engajamento do público de 'Breaking Bad' ao longo do tempo?** (Refletindo a análise de IMDb Rating e audiência por temporada/episódio).
* **Como a aceitação inicial de 'Breaking Bad' se compara à sua performance no auge da série?** (Comparando as análises das temporadas iniciais com as finais).
* **Quais características ou momentos (episódios/funcionalidades) de 'Breaking Bad' geraram os maiores picos de satisfação e engajamento dos usuários?** (Evidenciado pela identificação dos 'Episódios de Ouro' e seus respectivos indicadores).
* **Como a análise de dados pode quantificar o sucesso de 'Breaking Bad' e fornecer argumentos baseados em evidências?** (Demonstrando a metodologia completa de ETL, análise e storytelling).
* **De que forma insights baseados em dados sobre 'Breaking Bad' podem apoiar ou influenciar estratégias de marketing e comunicação de um produto, ao destacar seus pontos fortes e sua trajetória de sucesso?** (O storytelling visa exatamente isso).

**Objetivo:** Limpar, analisar e visualizar os dados de 'Breaking Bad' para identificar padrões de sucesso, quantificar o impacto da série e, por extensão, apresentar recomendações sobre como uma abordagem analítica similar pode ser empregada para a melhoria de estratégias de marketing em diversos setores, com base nas tendências de uso e aceitação de produtos.

---

## 3. Dados

**# Fonte de Dados #**
A fonte de dados utilizada neste estudo de caso provém do **Kaggle**, especificamente o dataset "Breaking Bad Episode Data". Este conjunto de dados é publicamente acessível e foi disponibilizado através da plataforma.

* **Acessibilidade e Privacidade de Dados:** O proprietário dedicou o trabalho ao domínio público (licença CC0 ou similar), renunciando a todos os seus direitos sobre o trabalho em todo o mundo sob a lei de direitos autorais, incluindo todos os direitos relacionados e conexos, na medida permitida por lei. É possível copiar, modificar, distribuir e executar o trabalho, mesmo para fins comerciais, tudo sem pedir permissão.
* **Tamanho e Formato:** Dois arquivos no formato **CSV** (`breaking_bad_episodes.csv` e `breaking_bad_imdb.csv`), com um tamanho compacto e gerenciável para análise tabular.
* **Intervalo dos Dados da Análise:** Os dados abrangem o período de exibição original da série, de **20 de janeiro de 2008 a 29 de setembro de 2013**.
* **Mais informações:**
    * O conjunto de dados contém registros detalhados para cada um dos **62 episódios** da série.
    * Cada episódio possui identificadores únicos, como número geral do episódio, número na temporada e título.
    * Os arquivos CSV apresentam diferentes dados quantitativos e textuais por episódio, como título, diretor, roteirista, data de exibição original, avaliação do IMDb, número de votos no IMDb e audiência nos EUA em milhões.
    * Os dados são registrados por episódio, com sua respectiva data de exibição.

**# Pontos Negativos da Base de Dados (e Abordagens): #**

* **Pequeno Tamanho:** Embora o dataset seja completo para o escopo da série, a quantidade de registros (62 episódios) é considerada pequena em comparação a bases de dados mais abrangentes, o que pode limitar análises estatísticas mais complexas em outros contextos.
* **Dados Ausentes ou Parciais:** Identificou-se que alguns episódios apresentavam valores ausentes em certas colunas, como `US_Viewers_Millions`, especialmente nas primeiras temporadas.
    * *Abordagem:* No processo de ETL (detalhado no notebook Python), foi realizado um tratamento para preencher ou gerenciar esses valores ausentes, garantindo a integridade dos dados para a análise.
* **Escopo Limitado:** O dataset se concentra exclusivamente nos dados de episódios e suas métricas de performance. Não inclui, por exemplo, dados demográficos dos espectadores ou engajamento em outras plataformas de streaming, o que poderia oferecer uma visão ainda mais ampla do sucesso da série.

---

## 4. Processamento e Exploração

Nesta seção, será detalhado o processo de **Extração, Transformação e Carga (ETL)** dos dados, que é fundamental para garantir a qualidade e a confiabilidade das análises subsequentes. As etapas incluem:

* **Carregamento dos Dados:** Importação dos arquivos CSV para o ambiente de Python (DataFrames Pandas).
* **Exploração Inicial e Compreensão dos Dados:** Análise da estrutura, tipos de dados, e conteúdo inicial dos DataFrames (`.head()`, `.info()`, `.shape`, `.describe()`).
* **Tratamento de Valores Ausentes:** Identificação e manejo de dados faltantes (ex: preenchimento ou remoção, conforme a estratégia definida).
* **Limpeza e Padronização de Dados:** Correção de inconsistências, formatação de textos, e ajuste de tipos de dados (ex: conversão de datas, tratamento de valores numéricos).
* **Criação de Novas Colunas/Features:** Desenvolvimento de variáveis adicionais que possam enriquecer a análise (ex: categorias de avaliação, média de votos por temporada).
* **Unificação/Combinação de Dados:** Integração de DataFrames distintos em um único conjunto de dados coerente para a análise integrada.
* **Verificação Final e Preparação para Análise:** Validação da estrutura final dos dados antes da fase de análise e visualização.

*(Detalhes técnicos e códigos podem ser encontrados no [breaking_bad.ipynb](https://github.com/welingtonfonsec/Breaking-Bad-Analise/blob/main/breaking_bad.py)).*

---

## 5. Análise e Visualização

Nesta etapa, os dados processados foram explorados para extrair insights significativos e construir a narrativa sobre a jornada de 'Breaking Bad'. As análises focaram em:

* **Avaliação da Qualidade e Engajamento Inicial:** Explorando os ratings e a audiência das primeiras temporadas para entender a base de partida da série.
* **Ascensão da Popularidade:** Análise do crescimento dos votos no IMDb e da audiência ao longo das temporadas intermediárias, identificando o ponto de virada da série.
* **Consagração e Impacto Final:** Destaque para os episódios de maior aclamação (Top IMDb Ratings) e os picos de audiência nas temporadas finais, incluindo o desfecho.
* **Correlação entre Métricas:** Observação da relação entre IMDb Rating, IMDb Votes e US Viewers para compreender como a qualidade percebida e o engajamento do público se influenciaram.

As visualizações foram desenvolvidas tanto em **Python** (utilizando bibliotecas como Matplotlib e Seaborn para análises exploratórias e gráficos estáticos) quanto no **Power BI** para a criação de um dashboard interativo e um storytelling visual dinâmico. O dashboard do Power BI permite uma exploração intuitiva dos dados e conta a história da série de forma clara e envolvente.

*(As visualizações interativas podem ser exploradas no [Storytelling no Power BI](SUA_URL_DO_POWER_BI_AQUI)).*

---

## 6. Conclusão e Recomendações

Este projeto culmina na apresentação de insights claros sobre o sucesso de 'Breaking Bad', validando a percepção da crítica e do público com dados concretos. A análise demonstrou que:

* A série apresentou uma **qualidade consistentemente alta** desde o início, com uma notável **escalada em aclamação** nas temporadas finais, culminando em notas quase perfeitas no IMDb.
* O **engajamento da audiência e o volume de votos** cresceram exponencialmente, indicando uma base de fãs cada vez maior e mais ativa à medida que a narrativa avançava.
* A capacidade de 'Breaking Bad' de manter e até mesmo elevar sua qualidade ao longo do tempo é um fator chave para seu status de 'fenômeno'.

**Recomendações e Transferibilidade de Habilidades:**

Este estudo de caso de 'Breaking Bad' serve como um exemplo prático de como a análise de dados pode ser aplicada para:

* **Quantificar o sucesso de um produto:** Definir métricas chave e acompanhar seu desempenho ao longo do tempo.
* **Identificar pontos de destaque e momentos de engajamento máximo:** Compreender o que ressoa mais com o público.
* **Fundamentar estratégias de marketing e comunicação:** Utilizar dados para destacar os pontos fortes de um produto e criar narrativas convincentes que impulsionem o engajamento e a aquisição de novos usuários.
* **Melhorar produtos e serviços:** Aplicar o monitoramento de feedback e uso para identificar oportunidades de aprimoramento contínuo.

A metodologia empregada aqui é diretamente aplicável a outros domínios, como a análise de tendências de uso de dispositivos inteligentes (como o cenário da Bellabeat), auxiliando na otimização de produtos e campanhas de marketing baseadas em evidências.

---
