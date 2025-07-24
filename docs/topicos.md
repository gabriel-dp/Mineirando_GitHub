# Análise de tópicos por comunidade: GitHub

```python
SEMESTRE  =  "2025/1"
DISCIPLINA  =  "Mineração e Análise de Redes Sociais"
ESTUDANTES  = ["Gabriel de Paula", "Wasterman Apolinário"]
PROFESSOR  =  "Vinicius Vieira"
```

&nbsp;

## 1. Introdução

Com o crescimento de redes sociais técnicas como o GitHub, torna-se relevante explorar tanto as conexões entre usuários (seguidores, contribuições) quanto o conteúdo que eles produzem ou descrevem. Esta análise busca investigar a relação entre comunidades estruturais — derivadas da rede de seguidores — e agrupamentos temáticos, com base em descrições textuais de usuários.

A proposta é, portanto, aplicar uma metodologia integrada de análise de redes sociais e mineração de texto, com foco em:

- Identificação de comunidades estruturais via o algoritmo de Louvain

- Extração de temas dominantes por comunidade utilizando modelagem de tópicos com TF-IDF e KMeans;

- Avaliação da sobreposição entre as estruturas detectadas via métricas de similaridade entre partições.

## 2. Metodologia

### 2.1 Modelagem de Tópicos

- Foi aplicada uma redução temática com KMeans (k=6) diretamente nos vetores TF-IDF.

- Para cada cluster, foram analisadas as palavras mais representativas.

- Em seguida, para cada comunidade detectada via Louvain, foi calculado o vetor médio de tópicos e identificado o tópico dominante.

### 2.2 Análise de Similaridade

Comparou-se a atribuição de clusters temáticos (via KMeans) com as comunidades topológicas (via Louvain), usando:

- Adjusted Rand Index (ARI) — mede concordância entre agrupamentos ajustada ao acaso.

- Normalized Mutual Information (NMI) — mede informação compartilhada entre partições.

## 3. Análise de Resultados

### 3.1 Distribuição de Tópicos por Comunidade

Abaixo está o tópico dominante identificado em cada comunidade da rede:

| Comunidade | Tópico Dominante |                                                 Palavras-Chave                                                 |
|:----------:|:----------------:|:--------------------------------------------------------------------------------------------------------------:|
| 0          | Tópico 3         | python, data, repository, learning, code, using, library, list, simple, source                                 |
| 1          | Tópico 3         | python, data, repository, learning, code, using, library, list, simple, source                                 |
| 2          | Tópico 1         | projeto, curso, desenvolvido, desafio, durante, rocketseat, aplicação, utilizando, feito, alura                |
| 3          | Tópico 3         | python, data, repository, learning, code, using, library, list, simple, source                                 |
| 4          | Tópico 5         | repositório, disciplina, programação, dados, trabalho, sistemas, destinado, desenvolvimento, curso, exercícios |
| 5          | Tópico 3         | python, data, repository, learning, code, using, library, list, simple, source                                 |
| 6          | Tópico 0         | react, app, project, using, application, api, simple, built, nodejs, native                                    |
| 7          | Tópico 1         | projeto, curso, desenvolvido, desafio, durante, rocketseat, aplicação, utilizando, feito, alura                |
| 8          | Tópico 5         | repositório, disciplina, programação, dados, trabalho, sistemas, destinado, desenvolvimento, curso, exercícios |
| 9          | Tópico 5         | repositório, disciplina, programação, dados, trabalho, sistemas, destinado, desenvolvimento, curso, exercícios |
| 10         | Tópico 3         | python, data, repository, learning, code, using, library, list, simple, source                                 |
| 11         | Tópico 1         | projeto, curso, desenvolvido, desafio, durante, rocketseat, aplicação, utilizando, feito, alura                |
| 12         | Tópico 0         | react, app, project, using, application, api, simple, built, nodejs, native                                    |
| 13         | Tópico 5         | repositório, disciplina, programação, dados, trabalho, sistemas, destinado, desenvolvimento, curso, exercícios |
| 14         | Tópico 5         | repositório, disciplina, programação, dados, trabalho, sistemas, destinado, desenvolvimento, curso, exercícios |
| 15         | Tópico 5         | repositório, disciplina, programação, dados, trabalho, sistemas, destinado, desenvolvimento, curso, exercícios |
| 16         | Tópico 1         | projeto, curso, desenvolvido, desafio, durante, rocketseat, aplicação, utilizando, feito, alura                |

É possível observar uma tendência temática recorrente em várias comunidades:

- O Tópico 3 (Python/Data) é dominante em muitas comunidades (ex: 0, 1, 3, 5, 10).

- O Tópico 5 (trabalhos acadêmicos/disciplinares) também se repete fortemente.

- Há poucas comunidades com predominância de tópicos voltados a frameworks como React (Tópico 0).

### 3.2 Sobreposição entre Agrupamentos
Ao comparar as comunidades Louvain com os clusters obtidos via KMeans:

- Adjusted Rand Index (ARI): 0.0341

- Normalized Mutual Information (NMI): 0.0817

Esses valores são baixos, indicando que os dois tipos de agrupamento compartilham pouca estrutura comum. Ou seja, os agrupamentos baseados na rede (quem segue quem) não coincidem com os agrupamentos baseados nos temas dos perfis.

## 4. Conclusão

Esta análise demonstra como a estrutura da rede social (comunidades Louvain) e a semântica dos usuários (modelagem de tópicos via TF-IDF + KMeans) podem revelar dimensões distintas de agrupamento em um conjunto de dados.

A baixa sobreposição entre as partições (ARI ≈ 0.03, NMI ≈ 0.08) sugere que, no contexto estudado (usuários do GitHub), as conexões sociais não refletem diretamente similaridade de interesse temático. Fatores como reputação, colaboração esporádica, ou aleatoriedade nas conexões podem explicar essa dissociação.

Apesar disso, a análise permite identificar comunidades com perfis técnicos similares, o que pode ser útil para:

- Recomendar conexões (usuários com temas semelhantes mas fora da comunidade),

- Identificar áreas de interesse para curadoria ou sugestão de conteúdo,

- Aprofundar a segmentação de usuários em redes profissionais.