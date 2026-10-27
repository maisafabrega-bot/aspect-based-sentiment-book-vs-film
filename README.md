# Análise de Lacunas da Pesquisa em Processamento de Linguagem Natural na USP

Projeto de pesquisa que analisa a produção de teses e dissertações voltadas para Processamento de Linguagem Natural (PLN) na Universidade de São Paulo. Os títulos, palavras-chave e resumos dos trabalhos são processados com técnicas de PLN para identificar quais ações e metodologias já foram pesquisadas e quais ainda são pouco exploradas.

## Coleta

- **Fonte:** Biblioteca Digital de Teses e Dissertações da USP
- **Busca:** "processamento de linguagem natural" (termo exato) no título ou nas palavras-chave
- **Resultado:** 127 trabalhos
- **Ferramenta:** Octoparse
- **Data da coleta:** 09/10/2026

## Ferramentas

- **Octoparse:** coleta dos dados (web scraping)
- **Python e pandas:** leitura e organização dos dados
- **spaCy (`pt_core_news_lg`):** tokenização, lematização, classes gramaticais, sintagmas nominais e classificação por dicionário
- **scikit-learn:** TF-IDF e modelagem de tópicos (NMF)
- **Matplotlib, Seaborn e WordCloud:** gráficos, mapas de calor e nuvens de palavras
- **Google Colab:** execução do notebook

## Etapas do Projeto

- **Pré-processamento:** normalização do texto, tokenização e remoção de *stopwords*
- **Lematização e etiquetagem morfossintática** com spaCy
- **Extração de sintagmas nominais**
- **Análise de frequência de termos**, com nuvens de palavras e de sintagmas
- **Classificação por dicionário** das ações de PLN e das metodologias de cada trabalho
- **Modelagem de tópicos** com TF-IDF e NMF
- **Análise de lacunas:** cruzamento das ações com as metodologias, as unidades da USP e as décadas de defesa

## Projeto

As ações e metodologias foram divididas de acordo com a arquitetura clássica do Processamento de Linguagem Natural, com base nos referenciais listados ao final.

**Ações de PLN**, pelos níveis de análise linguística (Jurafsky; Martin, 2009):

| Nível | O que é analisado |
|---|---|
| Fonético-fonológico | Sons da fala |
| Morfológico-lexical | Formação e classe das palavras |
| Sintático | Estrutura das frases |
| Semântico | Significado de palavras, frases e textos |
| Discursivo-pragmático | Relação entre frases, intenção e contexto |
| Geração de linguagem | Produção de texto a partir de dados ou de outro texto |

**Metodologias**, pelos paradigmas do PLN (Jurafsky; Martin, 2009; Manning; Schütze, 1999; Liu et al., 2023):

| Metodologia | Paradigma |
|---|---|
| Regras e léxicos | Simbólico |
| Estatística e aprendizado de máquina | Estatístico |
| Redes neurais e *embeddings* | Neural |
| Transformers e BERT | Pré-treino e ajuste fino |
| LLMs | Pré-treino, *prompt* e predição |

## Como usar o repositório

1. **Base de dados:** baixe o arquivo `Biblioteca_de_Teses_Scraping.csv`.
2. **No Google Colab (recomendado):** abra o notebook da pasta `NOTEBOOK`, rode as células em ordem e envie o arquivo CSV quando o notebook pedir. Não é preciso instalar nada além do que o próprio notebook instala.
3. **No computador (Jupyter):** instale os requisitos e o modelo de português do spaCy:
   ```bash
   pip install -r requirements.txt
   python -m spacy download pt_core_news_lg
   ```
   Depois, abra o notebook no Jupyter e rode as células em ordem.
4. **Resultados:** os gráficos e as tabelas são salvos na pasta `RESULTADOS`.

**Requisitos:** Python 3.10 ou superior, com as bibliotecas listadas em [requirements.txt](requirements.txt).

## Resultados

_[Preencher com os principais gráficos e tabelas da pasta RESULTADOS: trabalhos por ano e por unidade, termos e sintagmas mais frequentes, tópicos encontrados, ações por metodologia e lacunas identificadas.]_

## Dados e Ética

- A coleta teve finalidade exclusivamente acadêmica e não comercial, com intervalo entre as requisições para não sobrecarregar o site.
- Os títulos e resumos pertencem aos autores dos trabalhos. Cada registro mantém o DOI, que dá o crédito e leva à fonte original.
- Em 16 trabalhos, título, palavras-chave ou resumo estavam apenas em inglês e foram traduzidos para o português depois da coleta.

## Referências

JURAFSKY, D.; MARTIN, J. H. **Speech and Language Processing**. 2. ed. Upper Saddle River: Pearson Prentice Hall, 2009.

LIU, P.; YUAN, W.; FU, J.; JIANG, Z.; HAYASHI, H.; NEUBIG, G. Pre-train, prompt, and predict: a systematic survey of prompting methods in natural language processing. **ACM Computing Surveys**, v. 55, n. 9, p. 1-35, 2023. DOI: 10.1145/3560815.

MANNING, C. D.; SCHÜTZE, H. **Foundations of Statistical Natural Language Processing**. Cambridge: MIT Press, 1999.

## Licença

O código está sob a [Licença MIT](LICENSE). Os títulos e resumos das teses e dissertações pertencem aos seus autores.
