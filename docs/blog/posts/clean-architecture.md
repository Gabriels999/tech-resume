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

<p>Eu tive essas respostas ao longo da leitura, mas para minha surpresa, elas parecem ter sido diferentes do que o autor ser propôs a divulgar. Não me entenda mal, eu adorei o livro e os conceitos apresentados. Inclusive, como qualquer programador com um conceito novo e empolgante tentei uma implementação quase que imediatamente após fechar o livro.</p>
<p>Toda a explicação de porque aqueles eram conceitos relevantes fez muito sentido, e aplicar essas ideias em um projeto é algo animador porque a cada resultado que você obtém que se alinha com os mencionados no livro, isso te dá mais vontade de continuar. Alguns desses resultados são:</p>

- Maior desacoplamento.
- Consequentemente, maior testabilidade do seu código.
- Melhor organização.
- Melhor legibilidade.
- Isso tudo vai implicar em um custo de manutenção e sustentação consideravelmente mais baixos:
    - Seja por um desenvolvedor precisar de menos tempo para resolver possíveis bugs
    - Seja pelo o sistema ser mais confiável devido a sua testabilidade, e naturalmente ter menos bugs.

<p>E tudo isso parece incrível. Se eu tenho a alternativa de seguir essa filosofia e ter esses benefícios, não existe nenhum motivo para não o fazer, certo ?</p>
<p>A resposta para isso, quase como sempre em nossa área, é: depende.</p>
<p><i>Agora eu devo ter virado sênior.</i></p>

## Ok, mas o que exatamente é arquitetura limpa ?

<p>Primeiramente, eu sugiro fortemente que tente fazer a leitura desse livro pois acho que vale a pena e recomendo a todos os colegas de profissão. Tente, ainda que você não tenha a paciência e foco necessários para ler o livro na íntegra, ou simplesmente não queira.</p>
<p>Porém, se realmente não quer fazer isso, existe essa outra alternativa: <a target="_blank" href="https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html">o blog do Uncle Bob</a>, onde ele em 2012 ele fez um post a respeito da arquitetura limpa. Nesse post você vai encontrar um resumo bastante breve de tudo que é elaborado no livro ao longo de suas quase 400 páginas. Além disso, também será recebido com essa imagem:</p>

<img src="https://blog.cleancoder.com/uncle-bob/images/2012-08-13-the-clean-architecture/CleanArchitecture.jpg" alt="Diagrama da arquitetura limpa">

<p>A ideia principal dessa arquitetura é que você organize o seu projeto em camadas. Ao longo do livro é elaborado sobre como provavelmente vai existir um número mínimo de camadas em que faça sentido organizar o código para que tenhamos o melhor resultado com essa arquitetura, e a sugestão de Robert Martin para esse número é 4, assim como na imagem.</p>
<p>Nesse momento nós vamos nos concentrar no círculo e deliberadamente ignorar os blocos no canto inferior direito. A forma como devemos ler o círculo é na direção contrária das setas pretas que temos na imagem e em breve discutiremos sobre essas setas em si.</p>

### Entities - Enterprise Business Rules

<p>Aqui temos a camada principal da aplicação. Normalmente quando vamos criar um projeto uma das poucas coisas que temos razoavelmente estabelecidas (e que ainda assim com certeza irão mudar depois) são as entidades envolvidas com as atividades daquele projeto.</p>

<p>Algo muito importante de se mencionar é que <i>Entities</i> é na verdade um nome genérico que pode ser substituído por qualquer outra palavra que faça referência a "<i>personagens centrais da aplicação</i>". O que realmente vai nos importar é o nome <i>Enterprise Business Rules</i>.</p>
<p>Esse nome basicamente significa: <i>O que faz o sistema da sua empresa ser diferente do corrente</i>, <i>a parte da sua empresa que o corrente pagaria para ter acesso</i>, ou ainda <i>a parte que você não quer que o seu dev fale sobre durante palestras</i>. Em outras palavras, a identidade do seu fluxo está contida nesta camada. E o motivo pelo qual essa camada está no centro é essencialmente porque não vai existir absolutamente nada nas outras camadas, ou pelo menos não deveria, que cause qualquer tipo de mudança nesta aqui.</p>
<p>Veja bem, pensar assim além de fazer sentido até dá o sentimento de ser algo produtivo. Isso porque enquanto desenvolvedores de software, precisamos de pouquíssimo tempo de experiência para entender que o Django/Laravel/NestJS/etc não deveria fazer com que a regra de negócio da minha operação mude. Essa fala por si só faz sentido e acredito que a grande maioria dos desenvolvedores concordaria com isso. Porém, mesmo assim é possível encontrar, com alguma facilidade até, sistemas em que o código do framework é tão terrivelmente acoplado à regra de negócio que a simples atualização das versões dos pacotes quebra silenciosamente alguma funcionalidade. E obviamente existe também a situação contrária, em que por medo de que algo quebre, é feita a escolha consciente de manter o sistema com versões antigas, transformando-o assim em legado, apenas por medo do que uma atualização de pacotes pode fazer com o ambiente.</p>
<p>Não preciso nem comentar que não devemos ter medo do nosso software, já que só temos medo do que não entendemos.</p>

### Use Cases - Application Business Rules

<p>Esta é possivelmente a camada mais autoexplicativa de todas. Aqui é o espaço onde todos as entidades vão realizar alguma ação. Portanto, se em um sistema para venda de livros existe a regra de que a venda de um livro deveria causar o decréscimo do mesmo em estoque, é nessa camada que essas ações e consequências serão efetivamente aplicadas durante a execução.</p>
<p>É importante que se tome o cuidado para não confundir o conceito desta camada com a da anterior. Na outra nós possivelmente teríamos determinado que um <bold>usuário</bold> pode fazer a compra de um <bold>livro</bold>. Porém, isso seria apenas a definição de que esse tipo de ação é possível.</p>
<p>Seguindo o mesmo exemplo, nesta camada haveria a execução do código que efetivamente realiza a compra, bem como de outros relacionados como por exemplo a atualização de estoque. Se eu tenho um estoque, deve ser possível diminuir ou aumentar as quantidades de itens já existentes, bem como remover ou incluir novos itens ao estoque. Todas essas definições seriam pertinentes a camada <i>Enterprise Business Rules</i>. A execução desses códigos, porém, poderia se dar em vários momentos, como por exemplo durante a navegação de um administrador pela tela de gerenciamento de estoque, ou até mesmo, efetivamente depois que uma compra é concluída com sucesso, conforme mencionado anteriormente.</p>


### Controllers / Presenters / Gateways - Interface Adapters

<p>Tem algo particularmente interessante nessa camada, ela é a primeira que começa a apresentar mais de um nome internamente. Para nós, isso vai basicamente significar que a partir daqui, vários pedaços do sistema podem ser entendidos como peças que executam pequenas ações, em ordens variadas e que tem um mesmo objetivo no final.</p>
<p>A primeira vista eles podem não parecer fazer parte da mesma classe, mas aqui é onde começa a se fazer de maneira mais presente uma ideia bem interessante apresentada no livro:</p>

##### Coisas que mudam juntas ficam juntas

<p>As justificativas filosóficas das duas primeiras camadas fazem muito mais sentido se você encara o sistema como várias camadas que funcionam em conjunto. Porém, ao efetivamente desenvolver um sistema, nós não temos necessariamente a separação visual apresentada pelas regras de arquitetura. O que significa que pode não ser tão trivial realizar a aplicação desses conceitos já que o que vemos no fim do dia são pastas, arquivos e linhas de código.</p>
<p>Sendo assim, o autor apresenta essa abordagem bem interessante de que se as coisas que mudam pelo mesmo motivo ficarem juntas, você já vai essencialmente começar a ter a divisão de camadas em seu sistema. Podem não ser exatamente as mesmas camadas das apontadas por ele, você pode ter mais ou menos, mas talvez a ideia que traduza arquitetura limpa enquanto filosofia seja essa frase.</p>
<p><i>Coisas que mudam pelo mesmo motivo devem ficar juntas</i></p>
<p>Suponha que um novo valor deve ser considerado para a finalização de uma compra. A própria necessidade da consideração desse novo campo vem de uma necessidade real do negócio que o sistema visa representar, portanto, isso deveria significar que precisamos alterar a camada Entities. <i>Essa seria 1° alteração</i>.</p>
<p>A definição desta nova versão da função foi a 1° alteração, portanto, a 2° seria uma adaptação, ainda que mínima, ao momento de execução que seja causada pela existência deste novo valor a ser considerado. Logo, a <i>2° alteração</i> seria na camada de <bold>Use Cases</bold>.</p>
<p>Da mesma forma, a manipulação dos formatos numéricos desse novo valor que agora participa de uma compra, é muito mais uma questão técnica do que de negócio, sendo assim deve ficar junto com os códigos que mudam por "manipulação de dados" ou "interfaces de camadas". <i>3° alteração</i>.</p>
<p>A adição de um campo novo em uma tabela no banco de dados é uma questão técnica e portanto deve ser atrelada somente a camada pertinente (cuja a qual ainda falaremos a seguir). <i>4° alteração</i>.</p>
<p>Perceba que nesse contexto, uma alteração na camada mais interna sempre deveria ter consequência para outras mais externas. Porém, se fôssemos considerar neste exemplo que por uma questão contratual foi necessário mudar de provedor de pagamento e o novo processa os valores das transações em centavos e não em reais como anterior, isso é uma questão meramente técnica de funcionamento do próprio sistema e portanto não deveria impactar as camadas mais internas como <bold>Use Cases</bold> e <bold>Entities</bold> já que o formato e execução das ações do sistema se mantém preservadas.</p>

### Web / UI / DB / External Interfaces - Frameworks & Drivers

<p>Essas são as partes em que os iniciantes costumam perder mais tempo debatendo sobre, mas que podemos afirmar com alguma tranquilidade que nessa filosofia são as menos importante. Isso porque se as suas regras, a aplicação delas e a forma como são comunicadas já estão bem definidas, na realidade já não importa mais tanto para onde essas coisas serão exibidas.</p>
<p>Evidentemente que essas partes merecem atenção e que precisam ser estudadas de maneira relevante. Porém, essa é a parte mais marginal do sistema onde uma mudança não deveria de forma alguma implicar consequências nas camadas mais internas.</p>
<p>Retomando o exemplo do Django/Laravel/NestJS/etc, uma atualização nesses pacotes não deveria ser responsável por mudanças em qualquer outra camada mais interna. Nesse contexto a afirmação se confirma duplamente, já que esse tipo de código pode até ser open source, mas normalmente não é mantido pela sua empresa e por consequência é bem ruim condicionar qualquer forma de dependência entre o código de sua empresa, que é usado para gerar receita e o código mantido por outras pessoas desconhecidas com interesses diferentes dos da companhia.</p>
<p>Isso NÃO significa que o próprio uso do framework é um problema, apenas o super acoplamento entre o código dele e o da sua empresa.</p>