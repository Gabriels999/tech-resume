---
date: 2025-09-15
categories:
    - Books
    - Tutorials
authors:
    - gabriel
---

# Se arquitetura limpa é boa, então a suja é ruim ?

<p>Há dezenas de anos existe o debate sobre arquiteturas na engenharia de software, especialmente entre aqueles que se propõem a estudar system design.
A ideia de planejar como os fluxos irão existir dentro de um (ou de um conjunto de) sistemas parece fazer sentido investir tempo para encontrar a forma mais otimizada possível. Não necessariamente porque um sistema merece esse tipo de atenção, mas sim porque planejar, no geral, costuma ser uma atividade muito recompensadora.</p>
<p>Inclusive, essa é uma ideia simples e fácil de se transportar para outros contextos. Imagine, por exemplo, que você vai fazer uma viagem de 7 dias para outro país onde não conhece ninguém. Ou talvez conheça, isso na verdade é indiferente. O simples fato de reunir as pessoas que podem te apoiar ou que você queira visitar durante a viagem, já faz parte do ato de planejar.</p>

<!-- more -->

<p>De qualquer forma, inevitavelmente um dos seus primeiros passos vai ser pensar em como chegar lá ou talvez onde vai passar esses dias, se em um hotel, camping ou até uma pousada. Ah, também é preciso ver qual o aeroporto mais próximo, tanto de sua partida quanto de sua chegada. Mora longe do aeroporto ? Então também é preciso planejar como chegar ao aeroporto a tempo. Acho que já deu para entender, o ponto é que dificilmente você vai simplesmente começar essa jornada sem ter um mínimo de <b>planejamento</b>.</p>
<p>Não se engane, fazer todas essas considerações não faz de nós necessariamente bem preparados. A grande verdade é que é muito mais fácil planejar e fazer as escolhas mais cômodas para o contexto, do que simplesmente sair fazendo. A segunda opção vai ser frequentemente mais desconfortável e também mais cara. E sim, esse parágrafo já fala sobre arquitetura de software.</p>

## Minhas impressões sobre o livro

<p>Pois bem, finalizei recentemente a leitura do <a target="_blank" href="https://www.amazon.com.br/Arquitetura-Limpa-Artes%C3%A3o-Estrutura-Software/dp/8550804606">Arquitetura Limpa: o Guia do Artesão para Estrutura e Design de Software</a> e confesso que o que me motivou a começar essa leitura foi a curiosidade pelo tópico arquiteturas.</p>
<p>Eu não sabia exatamente o que esperar porque não estava tão familiarizado com o contexto da arquitetura para além do que mais se é falado:</p>

- Envolve organização de código de alguma maneira mais eficiente.
- Aparentemente é bom.


<p>Apesar disso, eu tinha algumas perguntas próprias que esperava serem respondidas ao longo dos capítulos: <b>Se a arquitetura boa é a limpa, a suja é ruim ? Quais são exatamente as diferenças ? Como é analisado que a limpa é melhor ?</b></p>

<p>Eu tive essas respostas ao longo da leitura, mas para minha surpresa, elas parecem ter sido diferentes do que o autor se propôs a divulgar. Não me entenda mal, eu adorei o livro e os conceitos apresentados. Inclusive, como qualquer programador com um conceito novo e empolgante, tentei uma implementação quase que imediatamente após fechar o livro.</p>
<p>Toda a explicação de porque aqueles eram conceitos relevantes fez muito sentido, e aplicar essas ideias em um projeto é algo animador porque a cada resultado obtido que se alinha com os mencionados no livro, isso dá mais vontade de continuar. Alguns desses resultados são:</p>

- Maior desacoplamento.
- Consequentemente, maior testabilidade do seu código.
- Melhor organização.
- Melhor legibilidade.
- Isso tudo vai implicar em um custo de manutenção e sustentação consideravelmente mais baixos:
    - Seja por um desenvolvedor precisar de menos tempo para resolver possíveis bugs
    - Seja por o sistema ser mais confiável devido a sua testabilidade, e naturalmente ter menos bugs.

<p>E tudo isso parece incrível. Se tenho a alternativa de seguir essa filosofia e ter esses benefícios, não existe nenhum motivo para não o fazer, certo ?</p>
<img src="https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExbWprNjN3Y2t4MjhzMzd3MTQ5eHZ1bmkyYTM1bGI1ZmdpMjlwMnF2YSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xiKgE3i7bSWUUccy1V/giphy.gif" alt="Ryan from The Office: 'Nah... Sorry man.'" />
<br>
<br>
<br>
<p>A resposta para isso, quase como sempre em nossa área, é: depende.</p>
<p><i>Agora sim devo ter virado sênior.</i></p>

## Ok, mas o que exatamente é arquitetura limpa ?

<p>Primeiramente, sugiro fortemente que tente fazer a leitura desse livro pois acho que vale a pena e recomendo a todos os colegas de profissão. Tente, ainda que você não tenha a paciência e foco necessários para ler o livro na íntegra, ou simplesmente não queira.</p>
<p>Porém, se realmente não quer fazer isso, existe essa outra alternativa: <a target="_blank" href="https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html">o blog do Uncle Bob</a>, onde, em 2012, ele fez um post a respeito da arquitetura limpa. Nesse post você vai encontrar um resumo bastante breve de tudo que é elaborado no livro ao longo de suas quase 400 páginas. Além disso, também será recebido com essa imagem:</p>

<img src="https://blog.cleancoder.com/uncle-bob/images/2012-08-13-the-clean-architecture/CleanArchitecture.jpg" alt="Diagrama da arquitetura limpa">

<p>A ideia principal dessa arquitetura é que você organize o seu projeto em camadas. Ao longo do livro, o autor elabora sobre como provavelmente vai existir um número mínimo de camadas em que faça sentido organizar o código para que tenhamos o melhor resultado com essa arquitetura, e a sugestão de Robert Martin para esse número é 4, assim como na imagem.</p>
<p>Nesse momento nós vamos nos concentrar no círculo e deliberadamente ignorar os blocos no canto inferior direito. A forma como devemos ler o círculo é na direção contrária das setas pretas que temos na imagem e em breve discutiremos sobre essas setas em si.</p>

### Entities - Enterprise Business Rules

<p>Aqui temos a camada principal da aplicação. Normalmente quando vamos criar um projeto uma das poucas coisas que temos razoavelmente estabelecidas (e que ainda assim com certeza irão mudar depois) são as entidades envolvidas com as atividades daquele projeto.</p>

<p>Algo muito importante de se mencionar é que <i>Entities</i> é na verdade um nome genérico que pode ser substituído por qualquer outra palavra que faça referência a "<i>personagens centrais da aplicação</i>". O que realmente vai nos importar nesse momento é o nome <i>Enterprise Business Rules</i>.</p>
<p>Esse nome basicamente significa: <i>O que faz o sistema da sua empresa ser diferente do corrente</i>, <i>a parte da sua empresa que o corrente pagaria para ter acesso</i>, ou ainda <i>a parte que você não quer que o seu dev fale sobre durante palestras</i>. Em outras palavras, a identidade do seu fluxo está contida nesta camada. E o motivo pelo qual essa camada está no centro é essencialmente porque não vai existir absolutamente nada nas outras camadas, ou pelo menos não deveria, que cause qualquer tipo de mudança nesta aqui.</p>
<p>Veja bem, pensar assim além de fazer sentido até dá o sentimento de ser algo produtivo. Isso porque enquanto desenvolvedores de software, precisamos de pouquíssimo tempo de experiência para entender que o Django/Laravel/NestJS/etc não deveria fazer com que a regra de negócio da minha operação mude. Essa fala por si só faz sentido e acredito que a grande maioria dos desenvolvedores concordaria com isso. Porém, mesmo assim é possível encontrar, com alguma facilidade até, sistemas em que o código do framework é tão terrivelmente acoplado à regra de negócio que a simples atualização das versões dos pacotes quebra silenciosamente alguma funcionalidade. E obviamente existe também a situação contrária, em que por medo de que algo quebre, é feita a escolha consciente de manter o sistema com versões antigas, transformando-o assim em legado, apenas por medo do que uma atualização de pacotes pode fazer com o ambiente.</p>
<p>Não preciso nem comentar que não devemos ter medo do nosso software, já que só temos medo do que não entendemos.</p>

### Use Cases - Application Business Rules

<p>Esta é possivelmente a camada mais autoexplicativa de todas. Aqui é o espaço onde todos as entidades vão realizar alguma ação. Portanto, se em um sistema para venda de livros existe a regra de que a venda de um livro deveria causar o decréscimo do mesmo em estoque, é nessa camada que essas ações e consequências serão efetivamente aplicadas durante a execução.</p>
<p>É importante que se tome o cuidado para não confundir o conceito desta camada com a da anterior. Na outra nós possivelmente teríamos determinado que um <b>usuário</b> pode fazer a compra de um <b>livro</b>. Porém, isso seria apenas a definição de que esse tipo de ação é possível.</p>
<p>Seguindo o mesmo exemplo, nesta camada haveria a execução do código que efetivamente realiza a compra, bem como de outros relacionados como por exemplo a atualização de estoque. Se eu tenho um estoque, deve ser possível diminuir ou aumentar as quantidades de itens já existentes, bem como remover ou incluir novos itens ao estoque. Todas essas definições seriam pertinentes a camada <i>Enterprise Business Rules</i>. A execução desses códigos, porém, poderia se dar em vários momentos, como por exemplo durante a navegação de um administrador pela tela de gerenciamento de estoque, ou até mesmo, efetivamente depois que uma compra é concluída com sucesso, conforme mencionado anteriormente. E essas execuções se relacionam de formas diferentes em cada cenário. Sendo assim, a composição desses relacionamentos vai ser feita de forma ordenada na camada <i>Application Business Rules</i>.</p>


### Controllers / Presenters / Gateways - Interface Adapters

<p>Tem algo particularmente interessante nessa camada, ela é a primeira que começa a apresentar mais de um nome internamente. Para nós, isso vai basicamente significar que a partir daqui, vários pedaços do sistema podem ser entendidos como peças que executam pequenas ações, em ordens variadas e que tem um mesmo objetivo no final.</p>
<p>A primeira vista esses blocos (controllers / presenters / gateways) podem não parecer fazer parte da mesma classe, mas aqui é onde começa a se fazer de maneira mais presente uma ideia bem interessante apresentada no livro:</p>

##### Coisas que mudam juntas ficam juntas

<p>As justificativas filosóficas das duas primeiras camadas fazem muito mais sentido se você encara o sistema como várias camadas que funcionam em conjunto. Porém, ao efetivamente desenvolver um sistema, nós não temos necessariamente a separação visual apresentada pelas regras de arquitetura. O que significa que pode não ser tão trivial realizar a aplicação desses conceitos já que o que vemos no fim do dia são pastas, arquivos e linhas de código.</p>
<p>Sendo assim, o autor apresenta essa abordagem bem interessante de que se as coisas que mudam pelo mesmo motivo ficarem juntas, você já vai essencialmente começar a ter a divisão de camadas em seu sistema. Podem não ser exatamente as mesmas camadas das apontadas por ele, você pode ter mais ou menos, mas talvez a ideia que traduza arquitetura limpa enquanto filosofia seja essa frase.</p>
<p><i>Coisas que mudam pelo mesmo motivo devem ficar juntas</i></p>
<p>Suponha que um novo valor deve ser considerado para a finalização de uma compra. A própria necessidade da consideração desse novo campo vem de uma necessidade real do negócio que o sistema visa representar, portanto, isso deveria significar que precisamos alterar a camada Entities. <i>Essa seria 1° alteração</i>.</p>
<p>A definição desta nova versão da função foi a 1° alteração, portanto, a 2° seria uma adaptação, ainda que mínima, no momento de execução que seja causada pela existência deste novo valor a ser considerado. Logo, a <i>2° alteração</i> seria na camada de <b>Use Cases</b>.</p>
<p>Da mesma forma, a manipulação dos formatos numéricos desse novo valor que agora participa de uma compra, é muito mais uma questão técnica do fluxo de execução da aplicação do que de negócio, sendo assim deve ficar junto com os códigos que mudam por "manipulação de dados" ou "interfaces de camadas". <i>3° alteração</i>.</p>
<p>A adição de um campo novo em uma tabela no banco de dados é uma questão técnica e portanto deve ser atrelada somente a camada pertinente (cuja a qual ainda falaremos a seguir). <i>4° alteração</i>.</p>
<p>Perceba que nesse contexto, uma alteração na camada mais interna sempre deveria ter consequência para outras mais externas. Porém, se fôssemos considerar neste exemplo que por uma questão contratual foi necessário mudar de provedor de pagamento e o novo processa os valores das transações em centavos e não em reais como anterior, isso é uma questão meramente técnica de funcionamento do próprio sistema e portanto não deveria impactar as camadas mais internas como <b>Use Cases</b> e <b>Entities</b> já que o formato e execução das ações do sistema se mantém preservadas.</p>

### Web / UI / DB / External Interfaces - Frameworks & Drivers

<p>Essas são as partes em que os iniciantes costumam perder mais tempo debatendo sobre, mas que podemos afirmar com alguma tranquilidade que nessa filosofia são as menos importantes. Isso porque se as suas regras, a aplicação delas e a forma como são comunicadas já estão bem definidas, na realidade já não importa mais tanto para onde essas coisas serão exibidas.</p>
<p>Evidentemente que essas partes merecem atenção e que precisam ser estudadas de maneira relevante. Porém, essa é a parte mais marginal do sistema onde uma mudança não deveria de forma alguma implicar consequências nas camadas mais internas.</p>
<p>Retomando o exemplo do Django/Laravel/NestJS/etc, uma atualização nesses pacotes não deveria ser responsável por mudanças em qualquer outra camada mais interna. Nesse contexto a afirmação se confirma duplamente, já que esse tipo de código pode até ser open source, mas normalmente não é mantido pela sua empresa e por consequência é bem ruim condicionar qualquer forma de dependência entre o código de sua empresa, que é usado para gerar receita e o código mantido por outras pessoas desconhecidas com interesses diferentes dos da companhia.</p>
<p>Isso NÃO significa que o próprio uso do framework é um problema, apenas o super acoplamento entre o código dele e o da sua empresa.</p>

### E as setas pretas ... ?

<p>Elas simbolizam o sentido correto em que as dependências devem acontecer. A essa altura já deve ser mais fácil de entender, mas se a camada Entities não deve ser influenciada por nenhuma outra, isso essencialmente significa que no caso de uma mudança nela, são grandes as chances de que isso impacte em algum nivel as outras subordinadas a ela.</p>
<p>Sendo assim, a relação que se estabelece entre elas é literalmente a seguinte:</p>
<ol>
<li>Frameworks & Drivers dependem de Interface Adapters.</li>
<li>Interface Adapters dependem de Application Business Rules.</li>
<li>Application Business Rules dependem de Enterprise Business Rules.</li>
</ol>
<p>Caso um sistema tenha um objeto da classe Application Business Rules que depende do Framework (caso super comum diga-se de passagem) o que começa a acontecer é que parece que estamos remando contra a maré e que o Framework é na verdade uma dificuldade a ser transposta ao invés de uma ferramenta que deveria impulsionar nosso projeto na direção em que queremos.</p>

## Consequências da arquitetura limpa

<p>Até aqui detalhamos um pouco a parte interna da arquitetura, mas, como desenvolvedores de software conscientes, não deveríamos aplicar algo desse tamanho sem embasamento teórico de porque isso é algo que vale a pena. Primeiro porque idealmente estamos frequentemente trabalhando em colaboração e é preciso saber comunicar os pontos fortes, mas também porque sem entender os verdadeiros benefícios, pode ser que o custo benefício da execução dessa arquitetura pode não ser tão valioso assim. Sendo assim, vou pontuar as consequências que percebi durante minhas implementações dessa arquitetura.</p>

### Benefícios

<p>Além da consequência mais óbvia da aplicação dessa arquitetura, que é a organização dos arquivos e pastas, temos algumas outras também positivas que podem deveriam ser as grandes motivadoras da aplicação.</p>

#### Maior testabilidade
<p>Uma delas é que como existe um foco em gerar código desacoplado, inclusive entre camadas, aumenta-se dramaticamente a testabilidade do sistema em questão. Principalmente porque o código parece funcionar como uma grande sequência de pequenas engrenagens, o que permite que seja muito fácil ter estabelecido o que deveria entrar em uma função, o que deveria sair, como ela deveria ter sucesso, falhar e o que acontece com o fluxo principal em cada cenário desse.</p>

#### Maior flexibilidade
<p>Outro benefício muito útil é a flexibilidade que isso permite e não apenas para o trabalho dos desenvolvedores, mas também para a área de neǵocio da empresa. Quem nunca passou por uma situação em que algo muito acoplado precisou mudar por qualquer que seja o motivo e além do trabalho de implementação do novo componente, existe também um trabalho,<i> que necessariamente sempre será feito</i>, para generalizar o fluxo. O que normalmente acontece é que se for feito sem planejamento, costuma ficar meia boca e causar uma terceira iteração de retrabalho. Então, já que será feito de alguma forma, por que não construir algo já com isso em mente ? A ideia não é resolver problemas do futuro, mas ter em mente que um certo nível de desacoplamento de dependências sempre vai ser bem vindo.</p>

#### Velocidade de colaboração
<p>De mãos dadas com o último ponto temos a velocidade de colaboração. Se o projeto foi construído seguindo essa filosofia, deveria ser muito simples para um desenvolvedor construir uma nova funcionalidade ou até mesmo dar manutenção em algo que existe. Isso porque o sistema já estaria coberto de testes e/ou com códigos desacoplados, o que dá muito mais segurança para que um desenvolvedor trabalhe entendendo bem as regras de negócio, assim como não quebrando funcionalidades.</p>

##### Potencialmente menos bugs
<p>Dada a elevada testabilidade do sistema, idealmente a quantidade de bugs que existem do ponto de vista técnico deveria sem bem menor, restando assim apenas uma abertura um pouco maior para <i>bugs de regra de negócio</i>. Aqueles do tipo "era esperado que o sistema fizesse X mas ele fez Y". Esses normalmente vêm muito mais do entendimento do desenvolvedor, já que o sistema estaria fazendo exatamente o que foi programado para fazer.</p>

##### Custo menor de desenvolvimento
<p> De qualquer forma, se o trabalho em um sistema é simplificado, isso vai implicar diretamente no custo de manuntenção/expansão já que o <a href="https://www.gupy.io/blog/headcount" target="_blank">HC (Headcount)</a> necessário para tais ações é bem menor. Em alguns casos pode chegar até ao caso de não ser necessário ter um desenvolvedor dedicado para este sistema.</p>
<p>PS.: Se esse é um ponto que a gerência gostaria de chegar, a aplicação dessa arquitetura poderia ser uma forma de alcançar esse objetivo.</p>

### Malefícios

<p>Eu diria que o principal malefício dessa aplicação seria a necessidade de um desenvolvedor experiente, como um techlead ou dev sênior, para que a filosofia seja respeitada não apenas no primeiro momento, mas de forma sistêmica ao longo das novas funcionalidades e manutenções que serão realizadas ao longo da vida útil do projeto. Isso porquê para um desenvolvedor que não saiba ou não compreenda na completude os benefícios da arquitetura limpa, é muito fácil surgir o discurso de que é uma forma de se trabalhar mais lenta e que no geral se cria muito mais código do que o necessário quando o sistema está no início. E tudo isso é verdade. O grande ponto é que essas escolhas se pagam <s>e muito</s> no médio/longo prazo, mas um profissional com pouca experiência em desenvolvimento e/ou gerenciamento de equipes de tecnologia não vai enxergar ou dar o devido valor aos benefícios posteriores.</p>

## Arquitetura suja

<p>No início do texto fiz a provocação: com base na definição desta arquitetura (a limpa), o que inevitavelmente concederia às outras o título de sujas ? Isso me interessou princpalmente porque existe uma certa presunção nessa denominação que poderia revelar um ego bastante inflado por parte do "criador" em um sentido que poderia representar o pensamento "certo estou eu, logo, quem pensa diferente está errado". Mas deixe-me tirar isso do caminho, o provável motivo para o emprego da palavra limpa (ou <i>clean</i> no inglês) é o mesmo pelo qual <a href="https://www.ie.edu/insights/articles/why-the-term-artificial-intelligence-is-misleading/#:~:text=The%20problematic%20origins%20of%20the,the%20name%20remain%20contested%20today." target="_blank">usamos a palavra <i>inteligência</i> na sigla IA</a>: pura e exclusivamente marketing.</p>
<p>Veja bem, primeiramente é preciso pontuar que a palavra <i>criador</i> está entre aspas no último parágrafo porque segundo o próprio Martin, ele não necessariamente inventou os conceitos por trás do que ficou conhecido como arquitetura limpa, mas sim agregou várias concepções que existiam na época em que escreveu o livro, além de é claro fazer algumas considerações próprias. Isso tudo é destacado por ele em um capítulo específico do livro, bem como no último capítulo onde ele cede espaço para um outro autor que faz algumas elaborações com estruturas diferentes das apresentadas pelo próprio Martin. A leitura deste capítulo na íntegra, apesar de ser bem menos interessante de uma forma geral, pelo menos serviu para me fazer identificar um certo fio condutor entre essas explicações que são muito mais filosóficas do que algorítimicas em si.</p>
<p>Tendo tirado tudo isso do caminho, podemos finalmente falar sobre o que seria a filosofia suja que hoje tento definir como qualquer forma de construção de software que, consciente ou inconsciemente, deixa espaço para o retrabalho. Atitudes como criar alguns #TODO: no código ou a ideia de fazer uma solução que "só quebre o galho" momentaneamente. Essas são ações que envolvem aquisição do que pode ser enxergado por alguns como <a href="https://www.alura.com.br/empresas/artigos/debito-tecnico#:~:text=Imprudente%20n%C3%A3o%20intencional,%2C%20ou%20n%C3%A3o%20p%C3%B4de%2C%20resolver." target="_blank">débito técnico</a>, o que é algo que não tenho certeza se concordo já que arquitetura é<s> ou deveria ser</s> algo muito mais estável do que funcionalidades no sistema.</p>
<p>Isso não significa que essas ações sejam condenáveis por si só, apenas que o seu fluxo de trabalho está ativamente gerando mais trabalho para ser resolvido no futuro. O problema disso é que os custos de resolução infelizmente crescem com juros compostos, já que as funcionalidades se expandem, os desenvolvedores com o contexto de negócio podem deixar a empresa ou simplesmente mudar de projetos ou o contexto pode se perder de forma geral. Esses problemas costumam a se apresentar de forma pequena, porém, a medida que o sistema se expande o problema tende a acompanhar até que seja grande demais para ser resolvido de uma vez só. De qualquer forma, é bem difícil que uma ação que resolva e/ou evite esse problema provavelmente não seja recomendada como uma das abordagens da arquitetura limpa.</p>
<p>Talvez seja até adequado então dizer que arquitetura suja é tudo que não é a limpa, mas não pelo motivo semântico explícito nesta frase e sim porque a aplicação adequada da arquitetura limpa seria: construir bases sólidas para estrutura de software mas que não sejam restritivas no longo prazo.</p>

## Então é só usar arquitetura limpa e final feliz, certo ?

<p>Bom, com certeza não.</p>
<p>Esta resposta é diferente da primeira porque agora você já está contextualizado e sabe meu ponto de vista. Sendo assim, é possível dizer que essa resposta vem sempre amarrada com uma outra pergunta que pode variar dentre as seguintes:</p>
- E se eu quiser fazer uma validação de ideia super rápida ?
- E se eu não quiser que a parte inicial do desenvolvimento seja mais lenta como apontado ?
- E se eu quiser manter conscientemente certas partes do meu código acopladas ?
<p>Felizmente para todas essas perguntas a resposta é a mesma: você literalmente ainda pode fazer tudo idêntico a como fazia antes de começar a leitura desse artigo. Inclusive, você ainda vai poder fazer tudo idêntico ao que fazia antes de ler o livro. A grande importância dessas leituras é ser capaz de fazer escolhas com mais embasamento técnico onde se sabe exatamente o que se está escolhendo e o que se está renunciando.</p>
<p>Quanto a opiniões pessoais, vou começar dizendo que humildemente <b>não concordo</b> com a arquitetura limpa apontada pelo Martin.</p>
<p>A ideia central é ótima e sou adepto dela, mas também sou adepto de ter algumas coisas razoavelmente acopladas ao sistema. Isso porque passei muito tempo em contato com frameworks web mais parrudos como Django e que determinam uma série de coisas para mim enquanto desenvolvedor. Obviamente, cada escolha é uma renúncia, então não estou necessariamente advogando que esse é o melhor formato de trabalho e sim dizendo que do ponto de vista de velocidade de desenvolvimento e também de gestão organizacional não vi em meus anos de experiência um motivo racional para evitar se apoiar em pedaços de software estruturados como é o caso deste e de outros frameworks parecidos.</p>
<p>Na realidade, os cenários em que vi problema envolviam uma heterogenização de frameworks web para se trabalhar. Os desenvolvedores nem sempre dominavam a mesma gama de frameworks, o que faz com que as features demorem mais para sair já que de uma forma geral existe sempre um trabalho extra agregado a construção, podendo esse ser o aprofundamento do contexto do sistema e/ou do contexto de o que o framework está fazendo por baixo dos panos.</p>
<p>O que quero dizer é: para uma empresa que tem uma stack de tecnologia homogênea algumas partes da arquitetura serão bastante opcionais. Se essa empresa tem 6 sistemas e todos são Spring Boot, quebrar esse padrão precisaria de um ótimo motivo, coisa que nem sempre se justifica. Porém, uma vez que se entende que se apoiar em um framework como esse é algo estável, você talvez não tenha tanto ganho focando em deixar seu sistema capaz de rodar completamente agnóstico ao framework.</p>
<p><b>Isso obviamente não significa que podemos acoplar ao framework sem pensar em mais nada.</b> Quer dizer apenas que, se o contrato de acoplar os sistemas e competências dos funcionários de uma organização com um determinado bloco, não faz sentido ter um plano 100% estruturado que te permita descumprir esse contrato quando quiser. Seria quase como comprar um carro já escolhendo o próximo.</p>
<p>Então para responder a pergunta:</p>

###### Se a arquitetura limpa é boa, então a suja é ruim ?

<p>Bom, depende de quem responde. No meu caso a resposta é não. A teoria costuma ser mais extrema que a prática. Quando estamos falando conceitualmente faz muito sentido algo simplesmente ser ou não. Ser bom ou ruim, valer a pena ou não, enfim. O motivo pelo qual isso acontece é que aqui estamos elaborando cenários hipotéticos que frequentemente são bem menos complexos do que os reais. A forma como isso se relaciona com a pergunta é que essencialmente tudo no mundo é sujo. Até as coisas que são esterelizadas, não permanecem assim para sempre. Na média elas são higienizadas até o máximo possível antes de serem usadas de forma que as deixarão sujas.</p>
<p>Sendo assim, enquanto um desenvolvedor de software que tenta resolver problemas do mundo real, prefiro ter um certo nível aceitável de "sujeira" atrelado ao código já que no mundo real até sentar na grama do parque vai sujar a roupa, mas isso não costuma ser motivo para não se sentar e apreciar a vista de qualquer forma.</p>