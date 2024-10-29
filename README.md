Aqui está uma documentação simplificada e organizada do script atual:

### Informações Gerais
**Versão do Script:** 1.3  
**Autor:** Vitor R. Galante  
**Finalidade:** O script gera um relatório mensal de SEO, analisando métricas de keywords e páginas a partir dos dados do Google Search Console (GSC) entre meses configurados.

### Parâmetros
- **meses**: Lista com dois meses de análise, definidos no início do script (`params$meses`).

### Funções Principais

1. **`extrair_categoria`**: Extrai a categoria principal de uma URL.
2. **`categorizar_tier`**: Categoriza posições de keywords em “tiers” (ex.: 1-3, 4-10).
3. **`processar_dados`**: Processa o dataframe do GSC, converte variáveis e aplica funções para categorizar.
4. **`contar_keywords_por_tier`**: Conta keywords por faixa de posição em um mês.
5. **`calcular_metricas`**: Calcula métricas de SEO, como total de cliques, impressões e posição média.
6. **`comparar_metricas`**: Compara métricas entre dois meses (crescimento em cliques, impressões e mudança de posição média).
7. **`calcular_crescimento_categorias`**: Calcula o crescimento em cliques de cada categoria entre dois meses.
8. **`identificar_paginas_80`**: Identifica páginas responsáveis por 80% dos cliques em um mês.
9. **`identificar_paginas_perderam_trafego`**: Detecta páginas com queda de cliques.
10. **`obter_top_keywords`**: Retorna as 10 principais keywords com mais cliques.
11. **`comparar_top_keywords`**: Compara as 10 principais keywords entre dois meses.

### Seções do Relatório

- **Análise Geral**: Exibe as métricas principais (cliques, impressões, posição média) para o mês atual.
- **Visualização por Tier e Categoria**: Gráficos comparativos de keywords por faixa de posição e categoria.
- **Comparação de Métricas**: Compara as métricas dos meses analisados.
- **Páginas Responsáveis por 80% dos Cliques**: Lista as páginas com maior contribuição para cliques.
- **Top Keywords**: Exibe as 10 principais keywords no mês atual.

### Melhorias Potenciais
1. **Função `extrair_categoria`**: Ajustar para tratar URLs de categoria pai e marcá-las adequadamente.
2. **Validação**: Adicionar controle para casos onde dados de meses ausentes ou anômalos possam impactar cálculos.

Essa documentação pode ser expandida conforme futuras atualizações e ajustes no script.
