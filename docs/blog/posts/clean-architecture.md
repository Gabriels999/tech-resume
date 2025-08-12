---
date: 2025-08-11
categories:
    - Books
    - Tutorials
authors:
    - gabriel
---

# Se arquitetura limpa é boa, então a suja é ruim ?

<p>Há alguns anos existe uma certo debate sobre arquiteturas no meio tech, especialmente entre aqueles que se propõem a estudar system design.
A ideia de planejar como os fluxos irão existir dentro de um (ou de um conjunto de) sistemas parece ser algo que faz sentido. Não necessariamente por ser um sistema, mas sim pelo planejamento.</p>
<p>Esse é um conceito simples de se transportar para outros contextos. Imagine por exemplo que você vai fazer uma viagem de 7 dias para outro país onde não conhece ninguém.</p>
<!-- more -->
<p>Inevitavelmente um dos seus primeiros passos vai ser pensar em como chegar lá ou talvez onde vai passar esses dias. Talvez um hotel ou uma pousada sirvam. Mas o ponto é que dificilmente você vai simplesmente começar essa jornada sem ter um mínimo de <strong>planejamento</strong>, e é sobre isso que eu quero falar.</p>
<p>Pois bem, recentemente eu finalizei a leitura do <a href="https://www.amazon.com.br/Arquitetura-Limpa-Artes%C3%A3o-Estrutura-Software/dp/8550804606">Arquitetura Limpa: o Guia do Artesão para Estrutura e Design de Software</a> e confesso que o que me motivou a começar essa leitura foi a curiosidade pelo tópico arquiteturas.</p>
<p>Eu não sabia exatamente o que esperar porque não estava tão familiarizado com todo o contexto da arquitetura para além do que mais se é falado:</p>

- Envolve organização de código de alguma maneira mais eficiente.
- Aparentemente é bom.


<p>Apesar disso, eu tinha algumas perguntas próprias que esperava serem respondidas ao longo dos capítulos: <strong>Se a arquitetura boa é a limpa, a suja é ruim ? Como exatamente a limpa se difere da suja e como isso é analisado ?</strong></p>

<p>Para a minha surpresa, eu tive essas respostas ao longo da leitura, mas elas parecem ter sido diferentes do que o autor ser propôs a divulgar. Não me entenda mal, eu adorei o livro, os conceitos apresentados e como qualquer programador com um conceito novo e empolgante tentei uma implementação quase que imediatamente após fechar o livro.</p>
<p>Toda a explicação de porque aqueles eram conceitos relevantes fez muito sentido, e aplicar essas ideias em um projeto é algo animador porque a cada resultado que você obtém que se alinha com os mencionados no livro, isso te dá mais vontade de continuar. Alguns desses resultados são:</p>

- Maior testabilidade do seu código.
- Melhor legibilidade.
- Melhor organização.

<p>E tudo isso parece incrível. Se eu tenho a alternativa de seguir essa filosofia e ter esses benefícios, não existe nenhum motivo para não o fazer, certo ?</p>
<p>A resposta para isso, quase como sempre em nossa área, é: depende.</p>
<p><i>Agora eu devo ter virado sênior.</i></p>

## Ok, mas o que exatamente é arquitetura limpa ?