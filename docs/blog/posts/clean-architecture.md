---
date: 2025-08-12
categories:
    - Books
    - Tutorials
authors:
    - gabriel
---

# Se arquitetura limpa é boa, então a suja é ruim ?

<p>Há dezenas de anos existe o debate sobre arquiteturas na engenharia de software, especialmente entre aqueles que se propõem a estudar system design.
A ideia de planejar como os fluxos irão existir dentro de um (ou de um conjunto de) sistemas parece ser algo que faz sentido investir tempo a fim de encontrar a forma mais otimizada possível. Não necessariamente porque um sistema merece esse tipo de atenção, mas sim porque planejar, no geral, costuma ser uma atividade muito recompensadora.</p>
<p>Essa é uma ideia simples e fácil de se transportar para outros contextos. Imagine por exemplo que você vai fazer uma viagem de 7 dias para outro país onde não conhece ninguém.</p>

<!-- more -->

<p>Inevitavelmente um dos seus primeiros passos vai ser pensar em como chegar lá ou talvez onde vai passar esses dias, talvez um hotel ou uma pousada. Mas o ponto é que dificilmente você vai simplesmente começar essa jornada sem ter um mínimo de <strong>planejamento</strong>, e é sobre isso que eu quero falar.</p>

## -- Nome genérico de subtítulo --

<p>Pois bem, recentemente eu finalizei a leitura do <a target="_blank" href="https://www.amazon.com.br/Arquitetura-Limpa-Artes%C3%A3o-Estrutura-Software/dp/8550804606">Arquitetura Limpa: o Guia do Artesão para Estrutura e Design de Software</a> e confesso que o que me motivou a começar essa leitura foi a curiosidade pelo tópico arquiteturas.</p>
<p>Eu não sabia exatamente o que esperar porque não estava tão familiarizado com o contexto da arquitetura para além do que mais se é falado:</p>

- Envolve organização de código de alguma maneira mais eficiente.
- Aparentemente é bom.


<p>Apesar disso, eu tinha algumas perguntas próprias que esperava serem respondidas ao longo dos capítulos: <strong>Se a arquitetura boa é a limpa, a suja é ruim ? Quais são exatamente as diferenças ? Como é analisado que a limpa é melhor ?</strong></p>

<p>Para a minha surpresa, eu tive essas respostas ao longo da leitura, mas elas parecem ter sido diferentes do que o autor ser propôs a divulgar. Não me entenda mal, eu adorei o livro, os conceitos apresentados e como qualquer programador com um conceito novo e empolgante tentei uma implementação quase que imediatamente após fechar o livro.</p>
<p>Toda a explicação de porque aqueles eram conceitos relevantes fez muito sentido, e aplicar essas ideias em um projeto é algo animador porque a cada resultado que você obtém que se alinha com os mencionados no livro, isso te dá mais vontade de continuar. Alguns desses resultados são:</p>

- Maior desacoplamento.
- Maior testabilidade do seu código.
- Melhor organização.
- Melhor legibilidade.
- Isso tudo vai implicar em um custo de manutenção e sustentação consideravelmente mais baixos:
    - Seja por um desenvolvedor precisar de menos tempo para resolver possíveis bugs
    - Seja pelo o sistema ser mais confiável devido a sua testabilidade, e naturalmente ter menos bugs.

<p>E tudo isso parece incrível. Se eu tenho a alternativa de seguir essa filosofia e ter esses benefícios, não existe nenhum motivo para não o fazer, certo ?</p>
<p>A resposta para isso, quase como sempre em nossa área, é: depende.</p>
<p><i>Agora eu devo ter virado sênior.</i></p>

## Ok, mas o que exatamente é arquitetura limpa ?

<p>Caso você não tenha a paciência e foco necessários para ler o livro na íntegra, ou simplesmente não queira, eu sugiro fortemente que tente mesmo assim pois essa é uma leitura que vale a pena e recomendo a todos os colegas de profissão.</p>
<p>Porém, se realmente não quer fazer isso, existe essa outra alternativa: <a target="_blank" href="https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html">o blog do Uncle Bob</a>, onde ele em 2012 ele fez um post a respeito da arquitetura limpa. Nesse post você vai encontrar um resumo bastante breve de tudo que é elaborado no livro ao longo de quase 400 páginas. Além disso, também será recebido com essa imagem:</p>

<img src="https://blog.cleancoder.com/uncle-bob/images/2012-08-13-the-clean-architecture/CleanArchitecture.jpg" alt="Diagrama da arquitetura limpa">

<p>A ideia principal dessa arquitetura é que você organize o seu projeto em camadas. Ao longo do livro é elaborado sobre como provavelmente vai existir um número mínimo de camadas em que faça sentido organizar o código para que tenhamos o melhor resultado com essa arquitetura, e a sugestão de Robert Martin para esse número é 4, assim como na imagem.</p>
<p>Nós vamos nos concentrar no círculo e deliberadamente ignorar os blocos no canto inferior direito. A forma como devemos ler o círculo é na direção contrária das setas pretas que temos na imagem e em breve discutiremos sobre essas setas em si.</p>

### Entities

<p>Aqui temos a camada principal da aplicação. Normalmente quando vamos criar um projeto uma das poucas coisas que temos razoavelmente estabelecidas (e que ainda assim com certeza irão mudar depois) são as entidades envolvidas com as atividades daquele projeto. Suponha que você vai criar um projeto em que donos de livrarias vão entrar e anunciar seus livros para que os usuários finais possam entrar e comprá-los e eventualmente até lê-los. Algo parecido com isso:</p>

<img src="../../../../../assets/images/entities.png">

<p>Ou seja, você sabe que esses são os blocos que vão estar envolvidos nas ações dos usuários. E até esse momento é possível pensar no sistema por dois pontos de vista, tanto pelo do User quanto pelo do BookstoreOwner. A princípio não parece que Book vai ser responsável por alguma ação. Essa análise inicial nos permite pensar na próxima camada.</p>

### Use Cases

<p>Esta é possivelmente a camada mais autoexplicativa de todas. Aqui é o espaço onde todos as entidades vão realizar alguma ação. Na última seção identificamos os agentes do fluxo, que seriam o BookstoreOwner e o User. Então aqui é o espaço onde criaremos o fluxo necessário para essas ações. Alguns exemplos são:</p>

- BookstoreOwner
    - createBook()
    - inactivateBook()
- User
    - buyBook()
    - readBook()
    - updateBookProgress()

<img src="../../../../../assets/images/usecases.png">


### Controllers