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
5. **Ações de PLN e metodologia:** classificação de cada trabalho por dicionário de expressões (`PhraseMatcher`). As ações seguem os níveis clássicos da arquitetura do PLN:

   | Nível | O que é analisado |
   |---|---|
   | Fonético-fonológico | Sons da fala |
   | Morfológico-lexical | Formação e classe das palavras |
   | Sintático | Estrutura das frases |
   | Semântico | Significado de palavras, frases e textos |
   | Discursivo-pragmático | Relação entre frases, intenção e contexto |
   | Geração de linguagem | Produção de texto a partir de dados ou de outro texto |

   Os cinco primeiros são os níveis de análise linguística (Liddy, 2001; Jurafsky; Martin, 2009; Indurkhya; Damerau, 2010). A geração de linguagem completa a arquitetura (Reiter; Dale, 2000; Gatt; Krahmer, 2018).

   As metodologias seguem os paradigmas pelos quais o PLN passou:

   | Metodologia | Paradigma | Referências |
   |---|---|---|
   | Regras e léxicos | Simbólico | Jurafsky; Martin (2009) |
   | Estatística e aprendizado de máquina | Estatístico (engenharia de atributos) | Manning; Schütze (1999); Liu et al. (2023) |
   | Redes neurais e *embeddings* | Neural (engenharia de arquitetura) | Mikolov et al. (2013); Goldberg (2017); Liu et al. (2023) |
   | Transformers e BERT | Pré-treino e ajuste fino | Vaswani et al. (2017); Devlin et al. (2019); Liu et al. (2023) |
   | LLMs | Pré-treino, *prompt* e predição | Brown et al. (2020); Liu et al. (2023); Zhao et al. (2023) |
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

BROWN, T. B. et al. Language models are few-shot learners. In: ADVANCES IN NEURAL INFORMATION PROCESSING SYSTEMS (NeurIPS), 33., 2020. **Proceedings** […]. Red Hook: Curran Associates, 2020. p. 1877-1901.

DEVLIN, J.; CHANG, M.-W.; LEE, K.; TOUTANOVA, K. BERT: pre-training of deep bidirectional transformers for language understanding. In: CONFERENCE OF THE NORTH AMERICAN CHAPTER OF THE ASSOCIATION FOR COMPUTATIONAL LINGUISTICS (NAACL), 2019, Minneapolis. **Proceedings** […]. Minneapolis: ACL, 2019. p. 4171-4186.

GATT, A.; KRAHMER, E. Survey of the state of the art in natural language generation: core tasks, applications and evaluation. **Journal of Artificial Intelligence Research**, v. 61, p. 65-170, 2018.

GOLDBERG, Y. **Neural Network Methods for Natural Language Processing**. San Rafael: Morgan & Claypool, 2017. (Synthesis Lectures on Human Language Technologies).

HONNIBAL, M.; MONTANI, I.; VAN LANDEGHEM, S.; BOYD, A. **spaCy: Industrial-strength Natural Language Processing in Python**. Zenodo, 2020. DOI: 10.5281/zenodo.1212303.

INDURKHYA, N.; DAMERAU, F. J. (ed.). **Handbook of Natural Language Processing**. 2. ed. Boca Raton: CRC Press, 2010.

JURAFSKY, D.; MARTIN, J. H. **Speech and Language Processing**. 2. ed. Upper Saddle River: Pearson Prentice Hall, 2009.

LEE, D. D.; SEUNG, H. S. Learning the parts of objects by non-negative matrix factorization. **Nature**, v. 401, p. 788-791, 1999. DOI: 10.1038/44565.

LIDDY, E. D. Natural language processing. In: **Encyclopedia of Library and Information Science**. 2. ed. New York: Marcel Dekker, 2001.

LIU, P.; YUAN, W.; FU, J.; JIANG, Z.; HAYASHI, H.; NEUBIG, G. Pre-train, prompt, and predict: a systematic survey of prompting methods in natural language processing. **ACM Computing Surveys**, v. 55, n. 9, p. 1-35, 2023. DOI: 10.1145/3560815.

MANNING, C. D.; SCHÜTZE, H. **Foundations of Statistical Natural Language Processing**. Cambridge: MIT Press, 1999.

MIKOLOV, T.; CHEN, K.; CORRADO, G.; DEAN, J. **Efficient estimation of word representations in vector space**. arXiv:1301.3781, 2013.

PEDREGOSA, F. et al. Scikit-learn: machine learning in Python. **Journal of Machine Learning Research**, v. 12, p. 2825-2830, 2011.

REITER, E.; DALE, R. **Building Natural Language Generation Systems**. Cambridge: Cambridge University Press, 2000.

VASWANI, A. et al. Attention is all you need. In: ADVANCES IN NEURAL INFORMATION PROCESSING SYSTEMS (NeurIPS), 30., 2017, Long Beach. **Proceedings** […]. Red Hook: Curran Associates, 2017. p. 5998-6008.

ZHAO, W. X. et al. **A survey of large language models**. arXiv:2303.18223, 2023.

## Licença

O código está sob a [Licença MIT](LICENSE). Os títulos e resumos das teses e dissertações pertencem aos seus autores.
