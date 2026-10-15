# Análise de Lacunas da Pesquisa em Processamento de Linguagem Natural na USP

## Visão Geral do Projeto

Este projeto usa Processamento de Linguagem Natural (PLN) para estudar a própria pesquisa em PLN feita na Universidade de São Paulo. Foram analisados os títulos, as palavras-chave e os resumos de 127 teses e dissertações da Biblioteca Digital de Teses e Dissertações da USP, com o objetivo de identificar quais ações de PLN e quais metodologias já foram pesquisadas e quais ainda são pouco exploradas.

## O que é PLN?

Processamento de Linguagem Natural é a área da computação que ensina computadores a ler, interpretar e analisar textos escritos por pessoas. Neste projeto, o PLN é usado para transformar 127 resumos em informações comparáveis: palavras mais frequentes, temas, ações de PLN e metodologias de cada trabalho.

## Fluxo do Projeto

1. **Coleta de dados:** busca por "processamento de linguagem natural" (termo exato) no título ou nas palavras-chave, na Biblioteca Digital da USP, e coleta dos trabalhos com o Octoparse.
2. **Processamento com spaCy:** tokenização, lematização e classes gramaticais dos resumos, com o modelo `pt_core_news_lg`.
3. **Palavras e sintagmas:** palavras e sintagmas nominais mais frequentes e nuvem de palavras.
4. **Evolução no tempo:** palavras que ganharam e perderam espaço nos trabalhos mais recentes.
5. **Ações de PLN e metodologia:** classificação de cada trabalho por dicionário de expressões (`PhraseMatcher`).
6. **Modelagem de tópicos:** TF-IDF e NMF para agrupar os trabalhos por assunto.
7. **Análise de lacunas:** mapas de calor que cruzam ações de PLN com metodologia, unidade e década.

## Resultados e Insights

_[Preencher com os principais gráficos da pasta RESULTADOS e o que eles mostram.]_

## Conclusões

_[Preencher ao final da análise.]_

## Como Usar Este Repositório

1. **Dados:** coloque a planilha exportada do Octoparse na pasta `DATA`, com as colunas descritas em [DATA/README.md](DATA/README.md).
2. **Instalação:**
   ```bash
   pip install -r requirements.txt
   python -m spacy download pt_core_news_lg
   ```
3. **Notebook:** abra [NOTEBOOK/analise_teses_pln.ipynb](NOTEBOOK/analise_teses_pln.ipynb) no Jupyter ou no Google Colab e rode as células em ordem.
4. **Resultados:** os gráficos e as tabelas são salvos na pasta `RESULTADOS`.

## Contribuições

Sugestões são bem-vindas. Abra uma *issue* ou faça um *fork* e envie um *pull request*.

## Referências

HONNIBAL, M.; MONTANI, I.; VAN LANDEGHEM, S.; BOYD, A. **spaCy: Industrial-strength Natural Language Processing in Python**. Zenodo, 2020. DOI: 10.5281/zenodo.1212303.

LEE, D. D.; SEUNG, H. S. Learning the parts of objects by non-negative matrix factorization. **Nature**, v. 401, p. 788-791, 1999. DOI: 10.1038/44565.

PEDREGOSA, F. et al. Scikit-learn: machine learning in Python. **Journal of Machine Learning Research**, v. 12, p. 2825-2830, 2011.

## Licença

O código está sob a [Licença MIT](LICENSE). Os títulos e resumos das teses e dissertações pertencem aos seus autores.
