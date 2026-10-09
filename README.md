# Mapeamento da Produção Científica Brasileira com PLN: Tópicos, Termos e Cautela Científica em Artigos do SciELO

## Visão Geral do Projeto

Este projeto aplica **Processamento de Linguagem Natural (PLN)** a resumos de artigos científicos publicados no **SciELO Brasil** para mapear como uma área de pesquisa se organiza e evolui ao longo do tempo. Os resumos são coletados com o **Octoparse** e processados com o **spaCy**, com o modelo para português.

A pergunta central é: **quais temas, métodos e objetos de estudo dominam a pesquisa brasileira em [ÁREA] entre [ANO INICIAL] e [ANO FINAL], quais estão surgindo ou perdendo espaço, e quão cautelosa é a linguagem com que os resultados são apresentados?**

| Fonte | Recorte | Idioma | Período | Data da coleta | Nº de artigos |
|---|---|---|---|---|---|
| SciELO Brasil | [termos de busca / área temática] | Português | [aaaa–aaaa] | [aaaa-mm-dd] | [n] |

## Aplicabilidade

- **Revisões de literatura e revisões sistemáticas:** triagem e organização de grandes volumes de artigos por tema.
- **Identificação de lacunas:** temas pouco estudados ou em queda indicam oportunidades de pesquisa.
- **Gestão e fomento à pesquisa:** apoio a programas de pós-graduação, agências e bibliotecas na análise da produção de uma área.
- **Ciência aberta em português:** a maior parte das ferramentas de mapeamento científico é feita para o inglês. O projeto mostra um fluxo replicável para o português.

## Métodos de PLN Utilizados

| Etapa | O que faz | Exemplo |
|---|---|---|
| **Lematização e classes gramaticais** | Reduz as palavras à forma básica e mantém só as que carregam conteúdo (substantivos, adjetivos, nomes próprios) | *"avaliadas"* → *avaliar* |
| **Sintagmas nominais** | Extrai termos compostos, que representam melhor os conceitos de uma área | *"qualidade da água"*, *"atenção primária"* |
| **Reconhecimento de entidades (NER)** | Identifica locais, organizações e outras entidades citadas nos resumos | *"Cerrado"*, *"Embrapa"* |
| **Modelagem de tópicos** | Agrupa os artigos em temas a partir das palavras que coocorrem (TF-IDF + NMF; BERTopic como alternativa) | Tópico 3: *solo, carbono, manejo* |
| **Detecção de *hedging*** | Mede a linguagem de cautela (*"sugere"*, *"pode indicar"*) e de ênfase (*"demonstra"*, *"comprova"*) | Índice por 100 palavras |

### O que é *hedging*?

Em textos científicos, *hedging* é o uso de expressões que atenuam a força de uma afirmação, como *"os resultados sugerem"* em vez de *"os resultados provam"*. Medir isso ajuda a entender como uma área apresenta a certeza dos seus achados e se isso muda ao longo do tempo ou entre subáreas.

## Fluxo do Projeto

1. **Coleta de dados (Octoparse):** busca no SciELO com os termos e filtros do recorte (idioma, período, área temática) e extração dos metadados e do resumo de cada artigo. Os detalhes estão em [DATA/README.md](DATA/README.md).
2. **Preparação dos dados (pandas):** remoção de duplicatas (pelo DOI), de resumos vazios e de artigos fora do período ou do idioma, além da normalização do texto.
3. **Análise linguística (spaCy):** tokenização, lematização, classes gramaticais, sintagmas nominais e entidades com o modelo `pt_core_news_lg`.
4. **Termos e tendências:** termos mais frequentes no período e termos emergentes (crescimento entre o início e o fim da série).
5. **Tópicos:** modelagem de tópicos e participação de cada tópico por ano.
6. **Cautela científica:** índice de *hedging* e de ênfase por artigo, por ano e por tópico.
7. **Visualização:** gráficos de evolução temporal, termos por tópico e comparação entre tópicos.

## Resultados e Insights

_[Preencher ao final da análise: principais tópicos, termos emergentes, lacunas identificadas e as figuras mais relevantes.]_

## Conclusões

_[Preencher ao final da análise.]_

## Limitações

- O SciELO não indexa toda a produção brasileira. Artigos publicados em periódicos estrangeiros ou fora da base ficam de fora.
- Resumos são curtos e padronizados: mostram o que os autores destacam, não todo o conteúdo do artigo.
- O modelo do spaCy para português foi treinado com textos gerais, não científicos, e pode errar em termos técnicos e entidades específicas da área.
- O léxico de *hedging* é uma lista de expressões. Ele não capta todos os usos e pode contar falsos positivos (por exemplo, *"pode"* no sentido de permissão).

## Como Usar Este Repositório

1. **Dados:** a pasta [DATA](DATA/) contém o dicionário de dados e uma **amostra sintética** (`artigos_sinteticos.csv`, com resumos inventados) no mesmo formato dos dados reais.
2. **Notebook:** abra o notebook da pasta [NOTEBOOK](NOTEBOOK/) no Google Colab ou no Jupyter.
3. **Instalação local (opcional):**
   ```bash
   pip install -r requirements.txt
   python -m spacy download pt_core_news_lg
   ```
4. **Execução:** ajuste as variáveis da seção *Configuração* do notebook (arquivo de entrada, período, número de tópicos) e rode as células em ordem. Sem os dados reais, o notebook roda com a amostra sintética.

## Dados e Licenças

- A coleta teve finalidade exclusivamente **acadêmica e não comercial**, com intervalo entre as requisições para não sobrecarregar o site.
- O SciELO adota licenças **Creative Commons** para os artigos, mas a licença varia por periódico (CC BY, CC BY-NC etc.). Por isso, **o conjunto completo de resumos não é redistribuído aqui**. São publicados apenas os identificadores (DOI) e os resultados agregados, o que permite reconstruir a base a partir da fonte.
- Todo uso dos resumos cita a fonte original (autores, periódico e DOI).

## Contribuições

Sugestões são bem-vindas. Abra uma *issue* ou faça um *fork* e envie um *pull request*.

## Referências

BLEI, D. M. Probabilistic topic models. **Communications of the ACM**, v. 55, n. 4, p. 77-84, 2012. DOI: 10.1145/2133806.2133826.

GROOTENDORST, M. **BERTopic: neural topic modeling with a class-based TF-IDF procedure**. arXiv:2203.05794, 2022.

HONNIBAL, M.; MONTANI, I.; VAN LANDEGHEM, S.; BOYD, A. **spaCy: Industrial-strength Natural Language Processing in Python**. Zenodo, 2020. DOI: 10.5281/zenodo.1212303.

HYLAND, K. **Hedging in scientific research articles**. Amsterdam: John Benjamins, 1998.

LEE, D. D.; SEUNG, H. S. Learning the parts of objects by non-negative matrix factorization. **Nature**, v. 401, p. 788-791, 1999. DOI: 10.1038/44565.

PACKER, A. L. et al. **SciELO: 15 anos de acesso aberto**: um estudo analítico sobre acesso aberto e comunicação científica. Paris: UNESCO, 2014.

SOUZA, F.; NOGUEIRA, R.; LOTUFO, R. BERTimbau: pretrained BERT models for Brazilian Portuguese. In: BRAZILIAN CONFERENCE ON INTELLIGENT SYSTEMS (BRACIS), 9., 2020, Rio Grande. **Proceedings** […]. Cham: Springer, 2020. p. 403-417.

## Licença

O **código** deste repositório está sob a [Licença MIT](LICENSE). A licença **não cobre** os resumos e metadados dos artigos, que pertencem aos autores e periódicos e seguem a licença de cada publicação.

## Autoria

**[Seu nome]**: [Instituição/curso] · [e-mail ou LinkedIn]
