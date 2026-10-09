# DATA

A base completa de resumos **não é publicada** neste repositório: ela fica apenas na máquina do pesquisador e é ignorada pelo `.gitignore`. Aqui estão o dicionário de dados, uma amostra sintética para testar o notebook e a lista de DOIs (quando a coleta for feita), que permite reconstruir a base.

## Arquivos

| Arquivo | Conteúdo | Publicado? |
|---|---|---|
| `artigos_sinteticos.csv` | 16 artigos **inventados**, no mesmo formato dos dados reais | ✅ |
| `dois.csv` | Lista dos DOIs dos artigos analisados | ✅ |
| `scielo_<recorte>_<data>.csv` | Exportação do Octoparse | ❌ |
| `artigos_tratados.csv` | Dados limpos e deduplicados | ❌ |
| `resultados/` | Tabelas geradas pelo notebook | ❌ (as figuras finais vão no README) |

## Dicionário de dados

| Coluna | Descrição | Exemplo |
|---|---|---|
| `id_artigo` | Identificador do artigo no SciELO (PID) | `S0100-204X2021000100001` |
| `doi` | DOI do artigo, sem o prefixo `https://doi.org/` | `10.1590/S0100-204X2021000100001` |
| `titulo` | Título em português | — |
| `periodico` | Nome do periódico | `Pesquisa Agropecuária Brasileira` |
| `ano` | Ano de publicação | `2021` |
| `idioma` | Idioma do resumo coletado | `pt` |
| `area_tematica` | Área temática do SciELO | `Agricultural Sciences` |
| `palavras_chave` | Palavras-chave separadas por `;` | `solo; carbono; manejo` |
| `resumo` | Texto do resumo em português | — |
| `url` | Link da página do artigo | — |
| `data_coleta` | Data da coleta | `2026-10-15` |

Os nomes dos autores não são necessários para a análise e por isso não são coletados.

## Coleta (Octoparse)

### 1. Definir o recorte
Antes de coletar, registre aqui: termos de busca, filtros usados e data da coleta. Isso é o que torna a coleta **reproduzível**.

| Item | Valor |
|---|---|
| Termos de busca | [ex.: `"saúde mental" AND universitários`] |
| Coleção | Brasil |
| Idioma | Português |
| Período | [aaaa–aaaa] |
| Área temática | [ex.: Health Sciences] |
| Total de resultados na busca | [n] |
| Data da coleta | [aaaa-mm-dd] |

### 2. Montar a tarefa
1. Faça a busca em [search.scielo.org](https://search.scielo.org/), aplique os filtros na barra lateral e copie a URL da página de resultados. Os filtros ficam gravados na URL.
2. No Octoparse, crie uma tarefa com essa URL e configure **dois níveis**:
   - **Lista de resultados:** loop sobre os itens da página, extraindo o título e o link do artigo, com paginação pelo botão de próxima página.
   - **Página do artigo:** para cada link, abra a página e extraia periódico, ano, DOI, palavras-chave e o resumo em português.
3. Configure a execução **local**, com intervalo de 3 a 5 s entre as ações e uma execução por vez.
4. Exporte em **CSV (UTF-8)** e renomeie as colunas conforme o dicionário acima.

> Os seletores das páginas não foram mapeados ainda. Depois de montar a tarefa, registre-os na tabela abaixo para documentar a coleta.

| Campo | Página | Seletor (XPath ou CSS) |
|---|---|---|
| `titulo` | resultados | [preencher] |
| `url` | resultados | [preencher] |
| `periodico` | artigo | [preencher] |
| `ano` | artigo | [preencher] |
| `doi` | artigo | [preencher] |
| `palavras_chave` | artigo | [preencher] |
| `resumo` | artigo | [preencher] |

### Alternativa para validação
O SciELO também oferece acesso programático aos metadados (ArticleMeta e OAI-PMH). Vale comparar uma amostra coletada pelo Octoparse com esses metadados para verificar se a extração está completa e correta.
