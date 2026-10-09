# DATA

A base completa **não é publicada** neste repositório: ela fica apenas no computador de quem fez a coleta e é ignorada pelo `.gitignore`. Aqui estão o dicionário de dados, uma amostra sintética para testar o notebook e a lista de URLs (quando a coleta for feita), que permite reconstruir a base.

## Arquivos

| Arquivo | Conteúdo | Publicado? |
|---|---|---|
| `teses_sinteticas.csv` | 16 trabalhos **inventados**, no mesmo formato dos dados reais | ✅ |
| `urls.csv` | Lista das URLs dos trabalhos analisados (gerada pelo notebook) | ✅ |
| `teses_usp_pln_<data>.csv` | Exportação do Octoparse | ❌ |
| `anotacao_manual.csv` | Amostra anotada à mão para a validação (gerada pelo notebook) | ❌ |
| `resultados/` | Tabelas geradas pelo notebook | ❌ (as figuras finais vão no README) |

## Dicionário de dados

| Coluna | Descrição | Exemplo |
|---|---|---|
| `id_trabalho` | Identificador do trabalho (parte final da URL) | `tde-01012021-120000` |
| `titulo` | Título do trabalho | — |
| `nivel` | Mestrado ou doutorado | `Dissertação de Mestrado` |
| `unidade` | Unidade da USP | `Escola Politécnica` |
| `area_concentracao` | Área de concentração do programa | `Engenharia de Computação` |
| `orientador` | Nome do orientador ou orientadora | — |
| `ano` | Ano de defesa | `2021` |
| `palavras_chave` | Palavras-chave em português, separadas por `;` | `PLN; aumento de dados` |
| `resumo_pt` | Resumo em português | — |
| `resumo_en` | Resumo em inglês (*abstract*) | — |
| `url` | Link da página do trabalho | — |
| `data_coleta` | Data da coleta | `2026-10-15` |

O nome do autor do trabalho não é necessário para a análise e por isso não é coletado.

## Coleta (Octoparse)

### 1. Recorte da busca
| Item | Valor |
|---|---|
| Site | Biblioteca Digital de Teses e Dissertações da USP |
| Condição 1 | Palavra-chave contém "processamento de linguagem natural" (**termo exato**) |
| Condição 2 | OU Título contém "processamento de linguagem natural" (**termo exato**) |
| Total de resultados | 127 |
| Data da busca | [aaaa-mm-dd] |

> Sem marcar "Termo exato", a busca procura as palavras separadas e retorna mais de 126 mil documentos, quase todos fora do tema.

### 2. Montar a tarefa
A tabela de resultados não mostra o resumo, então a tarefa tem **dois níveis**:

1. **Lista de resultados:** depois de fazer a busca no navegador do Octoparse, mude a paginação para **50 por página**. Crie um loop sobre as linhas da tabela e extraia título, link, área de concentração, nível, unidade e ano de defesa. Configure a paginação pelo botão **"Próxima página →"** (*Pagination → Click to paginate*). Com 127 resultados, são 3 páginas.
2. **Página de cada trabalho:** para cada link, abra a página e extraia orientador, palavras-chave, resumo em português e resumo em inglês.

Configuração da execução: **local**, com intervalo de 3 a 5 s entre as ações e uma execução por vez. Exporte em **CSV (UTF-8)** e renomeie as colunas conforme o dicionário acima.

### 3. Conferência
- O número de linhas exportadas deve ser igual ao total da busca (127).
- Abra 5 trabalhos ao acaso no site e compare com a planilha, para confirmar que o resumo veio inteiro e no campo certo.

### Seletores (preencher ao montar a tarefa)
| Campo | Página | Seletor (XPath ou CSS) |
|---|---|---|
| `titulo`, `url` | resultados | [preencher] |
| `area_concentracao`, `nivel`, `unidade`, `ano` | resultados | [preencher] |
| `orientador` | trabalho | [preencher] |
| `palavras_chave` | trabalho | [preencher] |
| `resumo_pt` | trabalho | [preencher] |
| `resumo_en` | trabalho | [preencher] |
