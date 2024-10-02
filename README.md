## Resumo Geral

Este script em RMarkdown tem como objetivo gerar um relatório mensal de análise de keywords, comparando métricas entre meses diferentes. Ele processa dados extraídos do Google Search Console (GSC), realiza diversas análises estatísticas e gera visualizações gráficas e tabelas para apresentar os resultados.

## Estrutura do Código

O código está estruturado em diferentes seções:

1. **Setup**: Carregamento das bibliotecas necessárias e definição dos parâmetros.
2. **Definição das Funções**: Conjunto de funções criadas para processar e analisar os dados.
3. **Processamento dos Dados**: Leitura e processamento dos arquivos CSV correspondentes aos meses especificados.
4. **Visualizações e Análises**: Geração de gráficos e tabelas para visualizar os resultados das análises.

## Detalhamento das Funções

### 1. `extrair_categoria(url)`

- **Descrição**: Extrai a categoria da URL fornecida, assumindo que a categoria está localizada após `/faq/` na URL.
- **Uso**: Utilizada dentro da função `processar_dados` para criar uma nova coluna `categoria` no dataframe.

### 2. `categorizar_tier(pos)`

- **Descrição**: Classifica as posições em tiers (faixas) predefinidas.
- **Uso**: Utilizada dentro da função `processar_dados` para criar uma nova coluna `tier` no dataframe.

### 3. `processar_dados(df)`

- **Descrição**: Processa o dataframe original, convertendo colunas para formatos numéricos, extraindo categorias e classificando as posições em tiers.
- **Passos**:
  - Converte as colunas `pos`, `impre` e `cliques` para `double`, substituindo vírgulas por pontos.
  - Adiciona colunas `categoria` e `tier` utilizando as funções anteriores.
- **Uso**: Chamado durante o processamento dos dados para cada mês.

### 4. `contar_keywords_por_tier(df, mes)`

- **Descrição**: Conta o número de keywords em cada tier para um determinado mês.
- **Uso**: Utilizada para gerar contagens que serão posteriormente visualizadas em gráficos.

### 5. `contar_keywords_por_tier_categoria(df, mes)`

- **Descrição**: Conta o número de keywords em cada tier e categoria para um determinado mês.
- **Uso**: Utilizada para análises mais detalhadas por categoria.

### 6. `calcular_metricas(df)`

- **Descrição**: Calcula métricas agregadas como total de cliques, impressões, posição média, total de keywords e total de páginas.
- **Uso**: Utilizada para armazenar métricas de cada mês para posterior comparação.

### 7. `comparar_metricas(metricas_mes1, metricas_mes2)`

- **Descrição**: Compara as métricas entre dois meses, calculando crescimento ou diminuição em porcentagem ou valores absolutos.
- **Uso**: Utilizada para gerar insights sobre a evolução das métricas entre os meses.

### 8. `calcular_crescimento_categorias(df_mes1, df_mes2, mes1, mes2)`

- **Descrição**: Calcula o crescimento percentual de cliques por categoria entre dois meses.
- **Uso**: Utilizada para identificar quais categorias tiveram maior crescimento ou declínio.

### 9. `identificar_paginas_80(df)`

- **Descrição**: Identifica as páginas responsáveis por 80% dos cliques no dataframe fornecido.
- **Passos**:
  - Agrupa os dados por página e soma os cliques.
  - Calcula o percentual acumulado de cliques.
  - Filtra as páginas que, cumulativamente, representam até 80% dos cliques.
- **Uso**: Utilizada para análises de Pareto, identificando páginas mais importantes.

### 10. `identificar_paginas_perderam_trafego(df_mes1, df_mes2)`

- **Descrição**: Identifica as páginas que perderam tráfego de um mês para outro.
- **Passos**:
  - Calcula o total de cliques por página em cada mês.
  - Faz um `full_join` para combinar as informações dos dois meses.
  - Calcula a diferença de cliques entre os meses.
  - Filtra as páginas que tiveram redução nos cliques.
- **Uso**: Auxilia na identificação de páginas que precisam de atenção.

### 11. `obter_top_keywords(df, top_n = 10)`

- **Descrição**: Obtém as top `n` keywords com mais cliques no dataframe fornecido.
- **Uso**: Utilizada para destacar as keywords mais relevantes em um determinado mês.

### 12. `comparar_top_keywords(df_mes1, df_mes2, top_n = 10)`

- **Descrição**: Compara as top `n` keywords entre dois meses.
- **Passos**:
  - Obtém as top keywords de cada mês.
  - Faz um `full_join` para combinar as informações.
  - Substitui valores `NA` por zero.
- **Uso**: Auxilia na análise de mudanças nas principais keywords ao longo do tempo.

## Processamento dos Dados

- **Loop por Mês**: O código percorre cada mês especificado em `meses`, lê o arquivo CSV correspondente e processa os dados utilizando as funções definidas.
- **Armazenamento**: Os dataframes processados e as métricas são armazenados em listas para uso posterior.
- **Combinação de Contagens**: As contagens por tier e categoria são combinadas em dataframes únicos para facilitar a visualização.

## Visualizações e Análises

### 1. Visualização Geral por Tier

- **Descrição**: Gráfico de barras mostrando a quantidade de keywords em cada tier para cada mês.
- **Objetivo**: Identificar a distribuição das posições das keywords ao longo dos meses.

### 2. Visualização por Categoria

- **Descrição**: Para cada categoria, é gerado um gráfico de barras mostrando a evolução das keywords por tier.
- **Objetivo**: Analisar o desempenho de cada categoria individualmente.

### 3. Comparação de Métricas

- **Descrição**: Comparação textual das principais métricas entre dois meses, incluindo gráficos e tabelas adicionais.
- **Inclui**:
  - Crescimento dos cliques e impressões.
  - Mudança na posição média.
  - Alteração no número de keywords e páginas.
  - Análise das categorias com maior crescimento.
  - Identificação das páginas responsáveis por 80% dos cliques.
  - Páginas que mais perderam tráfego.
  - Top keywords e comparação entre meses.

### 4. Páginas Responsáveis por 80% dos Cliques no Último Mês

- **Descrição**: Tabela mostrando as páginas que acumulam 80% dos cliques no mês mais recente.
- **Objetivo**: Destacar as páginas mais influentes no tráfego atual.

## Considerações Finais

- **Uso de Parâmetros**: O script utiliza parâmetros definidos no YAML (`params`) para facilitar a alteração dos meses analisados.
- **Tratamento de Dados Faltantes**: As funções incluem tratamentos para valores `NA` e ausência de dados, garantindo robustez nas análises.
- **Mensagens de Aviso**: Caso um arquivo de dados não seja encontrado, o script emite um aviso para o usuário.

## Sugestões de Melhoria

- **Validação de Dados**: Implementar verificações adicionais para garantir que os dados lidos estão no formato esperado.
- **Paralelismo**: Se os datasets forem grandes, considerar processamento paralelo para melhorar a performance.
- **Modularização**: Organizar as funções em scripts separados ou pacotes para reutilização em outros projetos.
- **Documentação do Código**: Adicionar comentários dentro das funções para explicar partes específicas do código.
- **Interatividade**: Considerar o uso de `shiny` ou `flexdashboard` para tornar o relatório interativo.
