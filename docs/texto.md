# Análise de texto: GitHub

```python
SEMESTRE  =  "2025/1"
DISCIPLINA  =  "Mineração e Análise de Redes Sociais"
ESTUDANTES  = ["Gabriel de Paula", "Wasterman Apolinário"]
PROFESSOR  =  "Vinicius Vieira"
```

&nbsp;

## 1. Introdução

Nos últimos anos, o volume de dados textuais disponíveis na internet cresceu exponencialmente, tornando essencial o desenvolvimento de técnicas eficazes para sua análise e interpretação. Nesse contexto, o presente relatório propõe uma análise textual a partir de descrições de repositórios hospedados no GitHub, uma das maiores plataformas colaborativas de desenvolvimento de software. As descrições desses repositórios constituem uma fonte de dados que podem conter informações sobre funcionalidades, propósitos, tecnologias utilizadas e até áreas de aplicação dos projetos.

O objetivo principal deste trabalho é aplicar técnicas de pré-processamento de texto,  etapa fundamental para a extração de informações relevantes. A partir desse processamento, será realizada a modelagem de tópicos, uma abordagem de aprendizado não supervisionado que permite identificar padrões semânticos recorrentes nos dados. Essa técnica é especialmente útil para organizar, resumir e compreender grandes volumes de texto, fornecendo uma visão geral sobre os principais temas abordados nos repositórios analisados.

&nbsp;

## 2. Metodologia

### 2.1 Pré-processamento
Alguns usuários possuíam a lista de repositórios substituída por mensagens de erro (ex: 404 Not Found). Esses casos foram tratados para evitar erros no carregamento.

Aps isso, para cada usuário, todas as descrições dos repositórios autorados por eles foram concatenadas, criando um único texto representativo.

Foram removidas também palavras irrelevantes (stopwords) em inglês e português, usando a biblioteca nltk

Além disso, a pontuação foi removida e os textos foram normalizados para minúsculas.

Ao utilizar o TfidfVectorizer, aplicamos dois filtros automáticos:
- max_df=0.9: ignora palavras que aparecem em mais de 90% dos documentos.
- min_df=2: ignora palavras que aparecem em apenas 1 documento.

Isso elimina termos muito comuns ou muito raros, que pouco contribuem para a modelagem.

### 2.2 Vetorização com TF-IDF
Utilizou-se o modelo TF-IDF (Term Frequency - Inverse Document Frequency) para transformar os textos em vetores numéricos. Essa abordagem dá mais peso a palavras frequentes em um usuário, mas incomuns entre os demais — ideal para distinguir perfis.

### 2.3 Modelagem de Tópicos com NMF
Foi aplicado o algoritmo NMF (Non-negative Matrix Factorization), adequado para dados esparsos como a representação textual tf-idf e interpretável para análise de tópicos.

Cada componente do NMF representa um tópico latente, composto por um conjunto de palavras com pesos significativos.

Após experimentações com 4 a 10 tópicos, decidiu-se por 6 tópicos como um bom equilíbrio entre granularidade e interpretabilidade. Essa escolha é justificada por:

- Tópicos distintos e coerentes semanticamente.

- Evita redundância

- Produz representações úteis para agrupamento ou recomendação.

&nbsp;

## 3. Análise e Resultados
Após aplicar o modelo de NMF com 6 tópicos sobre os textos de descrição dos repositórios, os seguintes grupos temáticos foram identificados:

### Tópico 0: Desenvolvimento de Aplicações com React e Node.js

Palavras-chave: ```native, nodejs, built, simple, api, application, using, project, app, react```

Este tópico aparentemente reúne usuários que trabalham com desenvolvimento de aplicações web ou mobile utilizando o ecossistema JavaScript moderno — especialmente com React (incluindo React Native) e Node.js. Os termos indicam projetos com API, aplicações completas e estruturas simples (“simple project”).

### Tópico 1: Projetos Educacionais com Alura e Rocketseat

Palavras-chave: ```alura, feito, utilizando, aplicação, rocketseat, durante, desafio, desenvolvido, curso, projeto```

Usuários agrupados neste tópico parecem estar envolvidos em projetos desenvolvidos como parte de cursos online, especialmente da Alura e da Rocketseat — duas plataformas populares de ensino em programação no Brasil. A presença de palavras como “desafio”, “durante”, “curso” indica repositórios oriundos de trilhas educacionais.

### Tópico 2: Personalização de Perfis GitHub (Readmes e Portfólios)
Palavras-chave: ```portfolio, lab, readmes, git, stats, readme, github, files, profile, config```

Este grupo de usuários está focado na personalização de seus perfis GitHub, frequentemente criando portfólios, readmes interativos e configurações visuais. Os termos indicam uma ênfase em apresentação pessoal e branding técnico.

### Tópico 3: Repositórios de Código e Bibliotecas em Python

Palavras-chave: ```source, simple, list, library, using, code, learning, repository, data, python```

Este tópico reúne usuários que publicam códigos reutilizáveis, pequenas bibliotecas e projetos de aprendizado de máquina, com ênfase em Python e ciência de dados. As palavras “library” e “data” indicam repositórios voltados ao compartilhamento de código funcional.

### Tópico 4: Criação de Sites Estáticos com HTML/CSS/JS

Palavras-chave: ```site, bootstrap, responsive, using, page, js, website, javascript, html, css```

Usuários desse grupo concentram-se na criação de sites estáticos e páginas web responsivas, frequentemente usando Bootstrap e tecnologias básicas da web (HTML, CSS, JS). É possível que esses projetos sejam portfólios, landings ou templates.

### Tópico 5: Repositórios Acadêmicos e Exercícios de Programação
Palavras-chave: ```exercícios, curso, desenvolvimento, destinado, sistemas, trabalho, dados, programação, disciplina, repositório```

Este tópico agrupa repositórios que parecem ser exercícios e trabalhos acadêmicos, associados a disciplinas de cursos de graduação. As palavras sugerem atividades obrigatórias (como “trabalho”, “disciplina”, “exercícios”).
&nbsp;

## 4. Conclusão

A análise baseada em modelagem de tópicos aplicada às descrições dos repositórios de usuários do GitHub permitiu identificar padrões semânticos relevantes sobre os interesses, perfis e contextos de uso da plataforma. Utilizando TF-IDF para vetorização textual e o algoritmo NMF (Non-negative Matrix Factorization), foi possível agrupar os textos em seis tópicos coerentes, representando:

- Perfis profissionais e técnicos com foco em frameworks como React, Node.js e Python;

- Usuários em formação participando de cursos e bootcamps como Alura e Rocketseat;

- Ações de branding e presença online, como personalização de perfis e portfólios;

- Produção acadêmica, com repositórios dedicados a exercícios e trabalhos de graduação.

Esses resultados demonstram a capacidade da abordagem em extrair valor informacional de textos não estruturados por meio de técnicas de NLP e mineração de dados. A estrutura temática obtida pode ainda servir como base para tarefas futuras de recomendação de conteúdo, agrupamento de usuários ou análise de comunidades dentro de redes sociais de desenvolvedores.

Portanto, esta metodologia oferece um caminho eficaz e escalável para compreender padrões de atividade e perfil técnico a partir de dados públicos de repositórios, especialmente em contextos educacionais, profissionais e colaborativos.


