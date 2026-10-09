# PLN na USP: Mapeamento de Teses e Dissertações sobre Processamento de Linguagem Natural

## Visão Geral do Projeto

Este projeto usa **Processamento de Linguagem Natural (PLN)** para mapear a própria pesquisa em PLN feita na **Universidade de São Paulo**. Os dados são as teses e dissertações da **Biblioteca Digital de Teses e Dissertações da USP**, coletadas com o **Octoparse** e analisadas com o **spaCy**.

A pergunta central é: **quais tarefas e métodos de PLN são pesquisados na USP, como eles evoluíram ao longo do tempo e como o PLN se espalhou por unidades e áreas além da Computação?**

| Fonte | Busca | Nº de trabalhos | Data da coleta |
|---|---|---|---|
| Biblioteca Digital de Teses e Dissertações da USP | "processamento de linguagem natural" (termo exato) em palavra-chave OU título | 127 | [aaaa-mm-dd] |

## Aplicabilidade

- **Mapa da área:** mostra onde o PLN é pesquisado na USP, com quais métodos e em quais aplicações (Saúde, Direito, Linguística, Computação).
- **Identificação de lacunas:** tarefas pouco estudadas e unidades que usam PLN sem diálogo com os grupos da área indicam oportunidades de pesquisa e de colaboração.
- **Apoio à gestão da pós-graduação:** programas e bibliotecas podem usar o mesmo fluxo para acompanhar a produção de qualquer tema.
- **Fluxo replicável:** o notebook funciona para outras buscas e outras bibliotecas de teses com a mesma estrutura de dados.

## Métodos de PLN Utilizados

| Etapa | O que faz | Exemplo |
|---|---|---|
| **Classificação por dicionário** (`PhraseMatcher` do spaCy) | Identifica a tarefa e o método de cada trabalho a partir de expressões no título, nas palavras-chave e no resumo | *"ajuste fino de um modelo BERT"* → **transformers e BERT** |
| **Lematização e classes gramaticais** | Reduz as palavras à forma básica e mantém só as que carregam conteúdo | *"classificadores"* → *classificador* |
| **Sintagmas nominais** | Extrai termos compostos, que representam melhor os conceitos da área | *"reconhecimento de entidades nomeadas"* |
| **Termos emergentes** | Compara a frequência dos termos entre a primeira e a segunda metade do período | *BERT*, *LLM* em alta |
| **Modelagem de tópicos** (TF-IDF + NMF) | Agrupa os trabalhos por temas sem usar o dicionário, o que pode revelar temas não previstos | Tópico 2: *modelo, neural, transformer* |
| **Validação com anotação manual** | Compara a classificação automática com uma amostra anotada à mão (precisão e cobertura) | Precisão e cobertura por tarefa e por método |

### Categorias de métodos

Os métodos são agrupados em cinco fases, que acompanham a história do PLN:

1. **Regras e léxicos:** gramáticas, regras construídas à mão e dicionários.
2. **Aprendizado de máquina clássico:** SVM, Naive Bayes, CRF.
3. **Redes neurais e *embeddings*:** word2vec, LSTM, CNN.
4. ***Transformers* e BERT:** BERT, BERTimbau, ajuste fino.
5. **Grandes modelos de linguagem (LLMs):** GPT, Llama, engenharia de *prompt*.

## Fluxo do Projeto

1. **Coleta de dados (Octoparse):** busca na Biblioteca Digital da USP e extração dos metadados e do resumo de cada trabalho. Os detalhes estão em [DATA/README.md](DATA/README.md).
2. **Tratamento da coleta (pandas):** o Octoparse exporta uma linha por campo. O notebook [01_tratamento_coleta](NOTEBOOK/01_tratamento_coleta.ipynb) transforma isso em uma linha por trabalho, limpa os textos, remove dados pessoais e confere se a coleta está completa.
3. **Perfil da produção:** trabalhos por ano, nível (mestrado e doutorado) e unidade.
4. **Tarefas e métodos:** classificação por dicionário e evolução dos métodos ao longo do tempo.
5. **Termos e tópicos (spaCy e scikit-learn):** termos frequentes, termos emergentes e modelagem de tópicos.
6. **Validação:** anotação manual de uma amostra de cerca de 40 trabalhos e cálculo de precisão e cobertura da classificação automática.

## Resultados e Insights

_[Preencher ao final da análise: tarefas e métodos predominantes, evolução ao longo do tempo, unidades fora da Computação e as figuras mais relevantes.]_

## Conclusões

_[Preencher ao final da análise.]_

## Limitações

- O recorte cobre **apenas a USP**. O resultado não representa toda a pesquisa brasileira em PLN.
- A busca depende de o termo *"processamento de linguagem natural"* aparecer no título ou nas palavras-chave. Trabalhos que usam só termos como *"linguística computacional"* ou *"mineração de texto"* podem ficar de fora.
- Com cerca de 130 trabalhos, alguns anos têm poucos casos. As tendências são descritivas e não permitem testes estatísticos robustos.
- O dicionário de tarefas e métodos foi construído manualmente para este projeto e pode não prever todos os termos. A validação manual mede esse erro.
- O modelo do spaCy para português foi treinado com textos gerais, não científicos.

## Como Usar Este Repositório

1. **Dados:** a pasta [DATA](DATA/) contém o dicionário de dados e uma **amostra sintética** (`teses_sinteticas.csv`, com trabalhos inventados) no mesmo formato dos dados reais.
2. **Notebooks:** rode primeiro o [01_tratamento_coleta](NOTEBOOK/01_tratamento_coleta.ipynb), que gera `DATA/teses_usp_pln.csv` a partir da exportação do Octoparse, e depois o [02_analise_teses_pln](NOTEBOOK/02_analise_teses_pln.ipynb), no Google Colab ou no Jupyter.
3. **Instalação local (opcional):**
   ```bash
   pip install -r requirements.txt
   python -m spacy download pt_core_news_lg
   ```
4. **Execução:** ajuste a seção *Configuração* de cada notebook (arquivo de entrada, total esperado, número de tópicos) e rode as células em ordem. Sem os dados reais, o notebook de análise roda com a amostra sintética.

## Dados e Ética

- A coleta teve finalidade exclusivamente **acadêmica e não comercial**, com intervalo entre as requisições para não sobrecarregar o site.
- **Os resumos não são redistribuídos neste repositório**, porque pertencem aos autores dos trabalhos. É publicada apenas a lista de URLs, que permite reconstruir a base a partir da fonte.
- Os nomes de autores não são usados na análise. Os orientadores aparecem apenas de forma agregada.

## Contribuições

Sugestões são bem-vindas. Abra uma *issue* ou faça um *fork* e envie um *pull request*.

## Referências

DEVLIN, J.; CHANG, M.-W.; LEE, K.; TOUTANOVA, K. BERT: pre-training of deep bidirectional transformers for language understanding. In: CONFERENCE OF THE NORTH AMERICAN CHAPTER OF THE ASSOCIATION FOR COMPUTATIONAL LINGUISTICS (NAACL), 2019, Minneapolis. **Proceedings** […]. Minneapolis: ACL, 2019. p. 4171-4186.

HONNIBAL, M.; MONTANI, I.; VAN LANDEGHEM, S.; BOYD, A. **spaCy: Industrial-strength Natural Language Processing in Python**. Zenodo, 2020. DOI: 10.5281/zenodo.1212303.

JURAFSKY, D.; MARTIN, J. H. **Speech and Language Processing**. 3. ed. (rascunho). Stanford, 2024. Disponível em: https://web.stanford.edu/~jurafsky/slp3/.

LEE, D. D.; SEUNG, H. S. Learning the parts of objects by non-negative matrix factorization. **Nature**, v. 401, p. 788-791, 1999. DOI: 10.1038/44565.

MIKOLOV, T.; CHEN, K.; CORRADO, G.; DEAN, J. **Efficient estimation of word representations in vector space**. arXiv:1301.3781, 2013.

SOUZA, F.; NOGUEIRA, R.; LOTUFO, R. BERTimbau: pretrained BERT models for Brazilian Portuguese. In: BRAZILIAN CONFERENCE ON INTELLIGENT SYSTEMS (BRACIS), 9., 2020, Rio Grande. **Proceedings** […]. Cham: Springer, 2020. p. 403-417.

VASWANI, A. et al. Attention is all you need. In: ADVANCES IN NEURAL INFORMATION PROCESSING SYSTEMS (NeurIPS), 30., 2017, Long Beach. **Proceedings** […]. Red Hook: Curran Associates, 2017. p. 5998-6008.

## Licença

O **código** deste repositório está sob a [Licença MIT](LICENSE). A licença **não cobre** os resumos e metadados das teses e dissertações, que pertencem aos seus autores.

## Autoria

**[Seu nome]**: [Instituição/curso] · [e-mail ou LinkedIn]
