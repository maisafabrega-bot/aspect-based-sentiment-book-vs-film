# DATA

A exportação do Octoparse fica apenas no computador de quem fez a coleta e é ignorada pelo `.gitignore`. Aqui estão o dicionário de dados e uma amostra sintética para testar o notebook.

## Arquivos

| Arquivo | Conteúdo | Publicado? |
|---|---|---|
| `teses_sinteticas.csv` | 16 trabalhos **inventados**, para testar o notebook sem os dados reais | ✅ |
| `Biblioteca_de_Teses_Scraping_xml.xlsx` | Exportação do Octoparse, uma linha por trabalho | ❌ |
| `teses_usp_pln.csv` | Base limpa e sem a coluna de autor (gerada pelo notebook) | ❌ por enquanto |
| `anotacao_manual.csv` | Amostra para a validação manual (gerada pelo notebook) | ❌ |
| `resultados/` | Tabelas geradas pelo notebook, incluindo a de lacunas | ❌ (as figuras finais vão no README) |

## Dicionário de dados

Colunas da exportação do Octoparse e como o notebook as usa:

| Coluna no Octoparse | Coluna no notebook | Descrição | Exemplo |
|---|---|---|---|
| `DOI` | `doi` | DOI do trabalho (também gera o link `url`) | `10.11606/D.45.2021.tde-07062021-135753` |
| `Documento` | `nivel` | Tipo de trabalho | `Dissertação de Mestrado` |
| `Autor` | — | Não usado (dado pessoal) | — |
| `Unidade_USP` | `unidade` | Unidade da USP | `Escola Politécnica (EP)` |
| `Area` | `area` | Área de concentração do programa | `Ciência da Computação` |
| `Data_Defesa` | `ano` | Data de defesa (o notebook usa só o ano) | `2021-05-04` |
| `Imprenta` | — | Não usado (cidade e ano) | `São Paulo, 2021` |
| `Título_Port` | `titulo` | Título em português | — |
| `Palavras_chave_Port` | `palavras_chave` | Palavras-chave, separadas por `;` | `BERT; Acórdãos` |
| `Resumo_Port` | `resumo` | Resumo (em 16 trabalhos, o texto está em inglês) | — |
| `Data_Publicação` | — | Não usado | `2021-06-14` |

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

Configuração da execução: **local**, com intervalo de 3 a 5 s entre as ações e uma execução por vez. Exporte em **Excel** com uma linha por trabalho, nomeie as colunas como na tabela acima e salve nesta pasta.

> ⚠️ **Desative a remoção de duplicatas do Octoparse** e confira se todas as páginas de resultados foram coletadas (127 trabalhos). Numa primeira coleta, uma página inteira faltou e vários campos saíram vazios por causa da remoção de duplicatas.

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
