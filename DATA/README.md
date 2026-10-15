# DATA

Coloque aqui a planilha exportada do Octoparse (`.xlsx` ou `.csv`). Ela não é enviada ao GitHub (veja o `.gitignore`).

## Nomes das colunas

Renomeie as colunas da planilha exatamente assim:

| Coluna original | Nome a usar | Usada na análise? |
|---|---|---|
| `DOI` | `doi` | Sim |
| `Documento` | `nivel` | Sim |
| `Primeiro_Autor` | `autor` | Não |
| `Unidade_USP` | `unidade` | Sim |
| `Area` | `area` | Não |
| `Data_Defesa` | `data_defesa` | Sim (o notebook tira o ano) |
| `Imprenta` | `imprenta` | Não |
| `Título_Port` | `titulo` | Sim |
| `Palavras_chave_Port` | `palavras_chave` | Sim |
| `Resumo_Port` | `resumo` | Sim |
| `Data_Publicação` | `data_publicacao` | Não |

As colunas não usadas podem ficar na planilha ou ser apagadas.

## Coleta

- **Fonte:** Biblioteca Digital de Teses e Dissertações da USP
- **Busca:** "processamento de linguagem natural" (termo exato) em palavra-chave OU título
- **Resultado:** 127 trabalhos
- **Ferramenta:** Octoparse
- **Data da coleta:** [aaaa-mm-dd]

Em 16 trabalhos, título, palavras-chave ou resumo estavam só em inglês e foram traduzidos para o português depois da coleta. [Descrever como foi feita a tradução.]
