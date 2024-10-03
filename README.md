# Resumo Geral

Este script em **RMarkdown** tem como objetivo gerar um relatório mensal de análise de keywords, comparando métricas entre períodos específicos. Ele processa dados extraídos do **Google Search Console (GSC)**, realiza análises estatísticas detalhadas e gera visualizações gráficas e tabelas para apresentar os resultados de forma clara e concisa.

# Estrutura do Código

O código está organizado em diferentes seções para facilitar a compreensão e manutenção:

1. **Setup**: Carregamento das bibliotecas necessárias e definição das configurações iniciais.
2. **Definição das Funções**: Conjunto de funções personalizadas criadas para processar e analisar os dados.
3. **Processamento dos Dados**: Leitura e processamento dos arquivos CSV correspondentes aos meses especificados.
4. **Análise Geral do Mês Atual**: Apresentação das métricas gerais do mês mais recente.
5. **Visualizações e Análises**: Geração de gráficos e tabelas para visualizar os resultados das análises.
6. **Comparação de Métricas**: Comparação detalhada das métricas entre o mês atual e o mês anterior.
7. **Análises Adicionais**: Análises específicas, como crescimento por categoria e identificação de páginas que perderam tráfego.
8. **Conclusão**: Considerações finais e sugestões de melhoria.

# Detalhamento das Funções

## 1. `extrair_categoria(url)`

- **Descrição**: Extrai a categoria da URL fornecida, assumindo que a categoria está localizada após `/faq/` na URL.
- **Uso**: Utilizada dentro da função `processar_dados` para criar uma nova coluna `categoria` no dataframe.

## 2. `categorizar_tier(pos)`

- **Descrição**: Classifica as posições em tiers (faixas) predefinidas.
- **Uso**: Utilizada dentro da função `processar_dados` para criar uma nova coluna `tier` no dataframe.

## 3. `processar_dados(df)`

- **Descrição**: Processa o dataframe original, convertendo colunas para formatos numéricos, extraindo categorias e classificando as posições em tiers.
- **Passos**:
  - Converte as colunas `pos`, `impre` e `cliques` para `double`, substituindo vírgulas por pontos.
  - Adiciona colunas `categoria` e `tier` utilizando as funções anteriores.
- **Uso**: Chamado durante o processamento dos dados para cada mês.

## 4. `contar_keywords_por_tier(df, mes)`

- **Descrição**: Conta o número de keywords em cada tier para um determinado mês.
- **Uso**: Utilizada para gerar contagens que serão posteriormente visualizadas em gráficos.

## 5. `contar_keywords_por_tier_categoria(df, mes)`

- **Descrição**: Conta o número de keywords em cada tier e categoria para um determinado mês.
- **Uso**: Utilizada para análises mais detalhadas por categoria.

## 6. `calcular_metricas(df)`

- **Descrição**: Calcula métricas agregadas como total de cliques, impressões, posição média, total de keywords e total de páginas.
- **Uso**: Utilizada para armazenar métricas de cada mês para posterior comparação.

## 7. `comparar_metricas(metricas_mes_anterior, metricas_mes_atual)`

- **Descrição**: Compara as métricas entre dois meses, calculando crescimento ou diminuição em porcentagem ou valores absolutos.
- **Uso**: Utilizada para gerar insights sobre a evolução das métricas entre os meses.

## 8. `calcular_crescimento_categorias(df_mes_anterior, df_mes_atual)`

- **Descrição**: Calcula o crescimento percentual de cliques por categoria entre dois meses.
- **Passos**:
  - Soma os cliques por categoria em cada mês.
  - Calcula a variação e o crescimento percentual.
- **Uso**: Utilizada para identificar quais categorias tiveram maior crescimento ou declínio.

## 9. `identificar_paginas_80(df)`

- **Descrição**: Identifica as páginas responsáveis por 80% dos cliques no dataframe fornecido (Análise de Pareto).
- **Passos**:
  - Agrupa os dados por página e soma os cliques.
  - Calcula o percentual acumulado de cliques.
  - Filtra as páginas que, cumulativamente, representam até 80% dos cliques.
- **Uso**: Auxilia na identificação das páginas mais influentes no tráfego atual.

## 10. `identificar_paginas_perderam_trafego(df_mes_anterior, df_mes_atual)`

- **Descrição**: Identifica as páginas que perderam tráfego de um mês para outro.
- **Passos**:
  - Calcula o total de cliques por página em cada mês.
  - Combina as informações dos dois meses.
  - Calcula a diferença de cliques entre os meses.
  - Filtra as páginas que tiveram redução nos cliques.
- **Uso**: Auxilia na identificação de páginas que precisam de atenção.

## 11. `obter_top_keywords(df, top_n = 10)`

- **Descrição**: Obtém as top `n` keywords com mais cliques no dataframe fornecido.
- **Uso**: Utilizada para destacar as keywords mais relevantes em um determinado mês.

## 12. `comparar_top_keywords(df_mes_anterior, df_mes_atual, top_n = 10)`

- **Descrição**: Compara as top `n` keywords entre dois meses.
- **Passos**:
  - Obtém as top keywords de cada mês.
  - Combina as informações.
  - Substitui valores `NA` por zero.
- **Uso**: Auxilia na análise de mudanças nas principais keywords ao longo do tempo.

## 13. `mes_para_numero(mes_nome)`

- **Descrição**: Converte o nome do mês em número, auxiliando na ordenação correta dos meses.
- **Uso**: Utilizada para garantir que os meses estejam ordenados do mais antigo para o mais recente.

# Processamento dos Dados

- **Parâmetros**: O script utiliza a variável `params$meses` para determinar quais meses serão analisados.
- **Ordenação dos Meses**: Os meses são ordenados do mais antigo para o mais recente usando a função `mes_para_numero()`.
- **Loop por Mês**: O código percorre cada mês especificado, lê o arquivo CSV correspondente (`resultados-gsc-mes.csv`) e processa os dados utilizando as funções definidas.
- **Armazenamento**: Os dataframes processados e as métricas são armazenados em listas para uso posterior.
- **Combinação de Contagens**: As contagens por tier e categoria são combinadas em dataframes únicos para facilitar a visualização.

# Análise Geral do Mês Atual

- **Apresentação das Métricas**: As principais métricas do mês mais recente são apresentadas utilizando texto em Markdown com código R inline, garantindo formatação consistente e legibilidade.
- **Formatação de Números**: Os números são formatados para evitar notação científica, utilizando separadores de milhares e decimais adequados ao padrão brasileiro.

# Visualizações e Análises

## 1. Visualização Geral por Tier

- **Descrição**: Gráfico de barras mostrando a quantidade de keywords em cada tier para cada mês.
- **Objetivo**: Identificar a distribuição das posições das keywords ao longo dos meses.
- **Ferramentas**: Utiliza o pacote `ggplot2` para gerar gráficos esteticamente agradáveis.

## 2. Visualização por Categoria

- **Descrição**: Para cada categoria, é gerado um gráfico de barras mostrando a evolução das keywords por tier.
- **Objetivo**: Analisar o desempenho de cada categoria individualmente.
- **Automação**: Utiliza um loop para gerar gráficos para todas as categorias presentes nos dados.

# Comparação de Métricas

- **Condição**: A comparação é realizada somente se houver pelo menos dois meses de dados.
- **Apresentação**: As métricas são comparadas entre o mês atual e o mês anterior, utilizando texto em Markdown com código R inline.
- **Métricas Comparadas**:
  - Total de cliques
  - Total de impressões
  - Posição média
  - Quantidade de keywords
  - Quantidade de páginas
- **Formatação**:
  - Números formatados com separadores de milhares e decimais.
  - Percentuais apresentados com duas casas decimais.

# Análises Adicionais

## 1. Crescimento por Categoria

- **Descrição**: Analisa o crescimento percentual de cliques por categoria entre o mês anterior e o mês atual.
- **Visualizações**:
  - Gráfico destacando as top 5 categorias com maior crescimento.
  - Gráfico mostrando o crescimento percentual de todas as categorias, indicando crescimento ou declínio.

## 2. Páginas que Mais Perderam Tráfego

- **Descrição**: Identifica as páginas que tiveram maior redução de cliques entre os meses comparados.
- **Apresentação**: Tabela exibindo as páginas e a diferença nos cliques, destacando as áreas que precisam de atenção.

## 3. Comparação das Top Keywords

- **Descrição**: Compara as top 10 keywords entre o mês anterior e o mês atual.
- **Objetivo**: Identificar mudanças significativas nas principais keywords que direcionam tráfego.

# Páginas Responsáveis por 80% dos Cliques no Mês Atual

- **Análise de Pareto**: Identifica o grupo de páginas que contribuem para 80% dos cliques no mês atual.
- **Apresentação**:
  - Percentual que esse grupo representa em relação ao total de páginas únicas.
  - Tabela listando as páginas, total de cliques e contribuição acumulada em porcentagem.

# Keywords com Mais Cliques no Mês Atual

- **Descrição**: Lista as top 10 keywords que geraram mais cliques no mês atual.
- **Apresentação**: Tabela exibindo as keywords e o total de cliques, auxiliando na identificação de tendências e oportunidades.

# Considerações Finais

- **Melhorias Implementadas**:
  - Substituição do uso de `cat()` por texto em Markdown com código R inline, melhorando a legibilidade e a manutenção do código.
  - Formatação adequada dos números para evitar notação científica indesejada.
  - Uso de condicionais em Markdown para controlar a exibição de conteúdo com base na disponibilidade de dados.
- **Uso de Boas Práticas**:
  - Separação clara entre processamento de dados e apresentação de resultados.
  - Aplicação de funções personalizadas para modularizar e reutilizar código.
  - Documentação detalhada das funções e seções do código.
- **Sugestões Futuras**:
  - **Interatividade**: Considerar o uso de `shiny` ou `flexdashboard` para tornar o relatório interativo.
  - **Automatização**: Implementar agendamento automatizado para geração dos relatórios mensais.
  - **Alertas Automáticos**: Criar mecanismos para destacar automaticamente métricas que ultrapassem determinados thresholds.
  - **Expansão das Análises**: Incluir análises adicionais, como avaliação de CTR (Click-Through Rate) e análise de concorrentes.

# Como Utilizar o Script

1. **Preparação dos Dados**: Certifique-se de que os arquivos CSV correspondentes aos meses que deseja analisar estão disponíveis e nomeados no formato `resultados-gsc-mes.csv`, onde `mes` é o nome do mês em minúsculas (por exemplo, `resultados-gsc-setembro.csv`).

2. **Configuração dos Parâmetros**: No início do script, ajuste o parâmetro `params$meses` com os meses que deseja analisar, em ordem cronológica. Exemplo:

   ```yaml
   params:
     meses: ["agosto", "setembro"]
   ```

3. **Execução do Script**: Rode o script em um ambiente compatível com RMarkdown (como o RStudio), garantindo que todas as bibliotecas necessárias estão instaladas.

4. **Visualização do Relatório**: Ao final da execução, um relatório em formato HTML será gerado, contendo todas as análises e visualizações.

# Dependências

Certifique-se de que os seguintes pacotes do R estão instalados:

- `tidyverse`
- `stringr`
- `knitr`
- `kableExtra`
- `scales`
- `ggplot2` (incluso no `tidyverse`)

# Contato

Para dúvidas ou sugestões relacionadas ao script, entre em contato com **Vitor R. Galante**.
