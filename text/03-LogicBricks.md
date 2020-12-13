**Table of Contents**

- [Chapter 3: Logic Bricks](#Chapter_3_Logic_Bricks)
	- [General Overview](#General_Overview)
		- [Simple Example](#Simple_Example)
	- [Architecture](#Architecture)
	- [Interface](#Interface)
		- [Add](#Add)
		- [Remove](#Remove)
		- [Move](#Move)
		- [Link](#Link)
		- [Unlink](#Unlink)
		- [Expand/Show/Hide](#Expand/Show/Hide)
		- [States](#States)
		- [Properties](#Properties)
		- [Sensors](#Sensors)
			- [Header](#Header)
			- [Always](#Always)
			- [Delay](#Delay)
			- [Actuator](#Actuator)
			- [Joystick](#Joystick)
			- [Keyboard](#Keyboard)
			- [Mouse](#Mouse)
			- [Armature](#Armature)
			- [Touch](#Touch)
			- [Collision](#Collision)
			- [Near](#Near)
			- [Radar](#Radar)
			- [Ray](#Ray)
			- [Random](#Random)
			- [Message](#Message)
			- [Property](Property)
		- [Controllers](#Controllers)
			- [Header](#Header)
			- [Booleans](#Booleans)
			- [Expression](#Expression)
			- [Values](#Values)
			- [Comparison Tests](#Comparison_Tests)
			- [Arithmetic Operations](#Arithmetic_Operations)
			- [Boolean Operations](#Boolean_Operations)
			- [Python Controller](#Python_Controller)
		- [Actuators](#Actuators)
			- [Header](#Header)
			- [Action](#Action)
				- [What Can Be Animated](#What_Can_Be_Animated)
				- [What Cannot Be Animated](#What_Cannot_Be_Animated)
				- [Object Settings](#Object_Settings)
				- [Play Modes](#Play_Modes)
				- [Blendin, Layers, and Priority](#Blendin,_Layers,_and_Priority)
			- [Armature](#Armature)
			- [Camera](#Camera)
			- [Constraint](#Constraint)
				- [Location Constraint](#Location_Constraint)
				- [Distance](#Distance)
			- [Orientation Constraint](#Orientation_Constraint)
			- [Force Field Constraint](#Force_Field_Constraint)
			- [Edit Object](#Edit_Object)
			- [Message](#Message)
			- [Motion](#Motion)
				- [Simple Motion](#Simple_Motion)
				- [Servo Control](#Servo_Control)
				- [Character Motion](#Character_Motion)
			- [Parent](#Parent)
			- [Property](#Property)
			- [Random](#Random)
			- [Sound](#Sound)
			- [State](#State)
			- [Visibility](#Visibility)
			- [Scene](#Scene)
			- [Filter 2D](#Filter_2D)
				- [Enable, Disable, Remove](#Enable,_Disable,_Remove)
			- [Game](#Game)
	- [State Machine](#State_Machine)
	- [Sharing and Group Instancing](#Sharing_and_Group_Instancing)
	- [To the Infinite and Beyond](#To_the_Infinite_and_Beyond)

# Capítulo 3: Logic Bricks <a id="Chapter_3_Logic_Bricks"></a>

O que torna um jogo diferente de um filme? Vamos ver. Em ambos, você pode se encontrar enterrado em um assento confortável comendo junk food e alienado do mundo. E óculos 3D engraçados não são exclusivos de nenhum dos dois. Mas e quanto à interatividade? Em um jogo, você pode controlar um jogador e interagir com o mundo virtual (ou real!) E os elementos do jogo. A história pode ser criada dinamicamente na frente de seus olhos.

Portanto, como diretor e criador de conteúdo, você desempenhará diferentes papéis em um filme ou jogo. Em um filme, por exemplo, você deve direcionar o fluxo da história, mas para um jogo, você deve direcionar como o jogador controla e experimenta esse fluxo. Essa é a época dos supercomputadores para o Watson, a máquina "inteligente" Jeopardy da IBM. Mais do que nunca, é hora de diminuir a lacuna entre o que a tecnologia pode oferecer e o que o público pode experimentar e assimilar como parte de sua própria natureza. Como Kevin Flynn elogiou em _Tron_ e _Tron Legacy_ o filme relacionado ao jogo da Disney e prequela _todo o poder para o usuário_.

Tradicionalmente, para projetar sua interação de jogo no passado, você precisaria de especialização em codificação e um conhecimento altamente técnico. Se, como um artista criativo, quaisquer palavras como _técnica, código _ ou _programação_ assustam você, tenha confiança!

"Artistas puros" ainda se assustam com o código. A ideia aqui não é que eles não tenham mais medo disso. Em vez disso, com o BGE, eles não terão que enfrentar seus medos. Os Logic Bricks são uma alternativa à codificação hardcore, conhecida por ser mais "amiga do artista". O Logic Bricks está aqui para resgatá-lo. Logic Bricks é um conjunto visual de ferramentas responsáveis por integrar os componentes do jogo. Usando o Logic Bricks, você pode determinar o que fazer após um clique do mouse, quando reproduzir uma animação, como mover seu personagem e assim por diante, conforme mostrado na Figura 3.1.

![Example of playing an animation when pressing Space](../figures/Chapter3/Fig03-01.png "Example of playing an animation when pressing Space")

>**Note**
>
>O Logic Bricks é uma programação visual de alto nível.

O sistema Logic Brick é composto por três elementos principais: ** sensores **, ** controladores ** e ** atuadores **. Sensores são um sistema de eventos usado para disparar uma ação em um evento específico (por exemplo, um objeto colide com outro objeto ou o joystick é usado). Depois que um ou mais sensores são acionados, você pode usar um controlador para controlar se esse conjunto de eventos produzirá ou não um evento no jogo (e qual efeito). Os controladores funcionam como tubos lógicos, avaliando sensores por meio de condições lógicas simples, como And, Or e Not. Finalmente, quando um controlador valida um conjunto de sensores, ele ativará um atuador. Um atuador é responsável por uma ação específica do jogo (como encerrar o jogo, mover um objeto e assim por diante).

Neste capítulo, vamos cobrir os sensores, controladores e atuadores em detalhes, especificamente, como e quando usá-los. Além disso, você aprenderá sobre as propriedades do jogo de objetos, o sistema State Machine, como a interface funciona e a arquitetura do sistema como um todo. Como um sistema usado para construir novos mundos, este não é lugar para _fazer_ e _não_. Caberá a você encontrar o melhor conjunto de recursos que se adequa ao seu projeto e criatividade. No entanto, quando possível, apresentaremos sugestões de quando e como as pessoas usaram as ferramentas no passado, mas você não precisa se sentir limitado por isso. Trate os Tijolos Lógicos como pequenas peças de Lego e surpreenda a nós e a você.

>**Deixe seu Python na porta**
>
>Os blocos lógicos são realmente fáceis e rápidos de usar. Você pode fazer jogos inteiros com eles sem absolutamente nenhuma necessidade de codificação.

## Visao geral <a id="General_Overview"></a>
Até agora, você sabe que todo este sistema permitirá que você crie aquelas pequenas peças que compõem a interação do seu jogo. Existem várias maneiras de colocar essas pequenas partes juntas e ainda mais maneiras de combiná-las. É impossível mostrar todas as possibilidades, mas existe um princípio comum de como elas funcionam que podemos observar.

### Exemplo Simple <a id="Simple_Example"></a>

Nos arquivos do livro, abra _Book / Chapter3 / bowling \ _base.blend_.
Neste arquivo, você tem um pequeno jogo de boliche que inclui a bola de boliche, os pinheiros e a pista para a bola rolar. O objetivo aqui é lançar a bola e mantê-la rolando o máximo que puder. Se você for ao menu do jogo do Blender e iniciar o jogo, verá que nada parece acontecer. Aqui estão algumas coisas de que você pode precisar:
- Sensor de teclado para reagir quando as teclas são pressionadas.

- Atuador para mover a bola.

- Controlador para ativar o atuador quando o sensor for positivo.

Selecione a bola, e você verá que alguns daqueles tijolos lógicos já estão lá, conforme ilustrado na Figura 3.2. Clique no soquete pelo sensor do teclado e arraste a linha até o soquete pelo atuador de movimento. Se o seu objetivo foi bom, isso criará um controlador para conectar o sensor com o atuador. Comece o jogo novamente e pressione a barra de espaço algumas vezes para rolar um golpe.

![Exemplo de jogo de boliche simples](../figures/Chapter3/Fig03-02.png "Simple bowling sample game")

Para tornar as coisas mais interessantes, há também um cronômetro que será iniciado quando o jogo começar. Se você conectar o sensor de propriedade (já no arquivo) ao mesmo controlador que o sensor do teclado, você só poderá mover a bola por alguns segundos. O sensor de propriedade será positivo enquanto o cronômetro estiver dentro de um intervalo especificado. Portanto, o controlador And será positivo apenas quando o teclado e os sensores de propriedade forem positivos.

Este é um exemplo simples, mas deve ajudá-lo a começar para que possa experimentar as opções disponíveis e outros blocos lógicos. Vá em frente e mude algumas coisas. Não se preocupe porque nada vai quebrar. Na Figura 3.3, você pode ver a aparência dos seus blocos lógicos vinculados finais. Observe que existem alguns tijolos lógicos pré-criados para a câmera e o primeiro pinheiro. Se você conectá-los como mostrado, a câmera será animada assim que a bola atingir o pinheiro.

![Bowling Logic Bricks](../figures/Chapter3/Fig03-03.png "Bowling Logic Bricks")


## Arquitetura <a id="Architecture"></a>

O motor do jogo foi projetado para girar em torno dos objetos do jogo. Quinze anos atrás, quando foi desenvolvido pela primeira vez, este foi um design inovador. A ideia de ter eventos controlados por objeto, ao invés de um controlador central, funcionou bem para os primeiros dias dos motores 3D. Hoje em dia, algumas pessoas podem defender que controlar os elementos por objeto é menos escalonável e mais difícil de gerenciar. Isso caberá a você decidir. Independentemente do que você pensa sobre o assunto, a engine do jogo ainda permite que você emule um sistema de controle centralizado, enquanto dá autonomia a cada objeto para lidar com seu próprio negócio. Parte dessa flexibilidade se deve à camada Python conectada e ao sistema Logic Brick. Por meio da interface Python, você pode substituir ou pelo menos controlar a maioria dos efeitos e configurações lógicas que você cria com os blocos lógicos. Com o Logic Bricks, você pode configurar rapidamente um sistema fácil de visualizar, implementar e testar. A força do motor de jogo vem do trade-off entre os dois sistemas irmãos. Um design flexível pode carecer de recursos e desempenho em comparação com motores específicos. No entanto, os diferentes tipos de aplicativos que você pode prototipar e desenvolver rapidamente com o mecanismo de jogo compensam o compromisso.

Se você olhar em um nível profundo na estrutura do objeto, verá que a arquitetura do sistema Logic Bricks é "centrada no controlador". Ele gira em torno dos controladores do jogo porque são eles que determinam o que fazer com os sensores e quais atuadores ativar. Isso não precisa ser seguido à risca, mas com base neste projeto, você desejará manter seus sensores e atuadores no mínimo e otimizar seu uso com os controladores. Na verdade, para otimizar o desempenho, o mecanismo de jogo desabilita qualquer sensor e atuador que esteja desvinculado de um controlador ou vinculado a um controlador em um estado não ativo. Esta é uma das (muitas) razões pelas quais os controladores Python são tão populares. Eles permitem que você substitua o uso de vários sensores e atuadores por chamadas diretas para seus equivalentes no código-fonte. O Capítulo 7, "Python Scripting", é inteiramente dedicado a esse aspecto do mecanismo de jogo e complementará os aplicativos dos blocos lógicos discutidos neste capítulo.

## Interface <a id="Interface"></a>

O Logic Bricks possui seu próprio editor dentro da interface do Blender. Enquanto outras configurações do jogo estão espalhadas por todos os painéis e menus, a edição dos Logic Bricks pode ser feita inteiramente dentro do Logic Editor.

Você pode ver que os tijolos lógicos são classificados por objeto e organizados de acordo com suas próprias necessidades. Para cada objeto individual, os controladores são executados de cima para baixo, conforme apresentado na interface. No entanto, não há muito controle sobre qual dos blocos lógicos do objeto é executado primeiro. Os critérios de organização para os blocos lógicos tendem a refletir mais preferências pessoais e necessidades de clareza visual do que requisitos internos.

Aqui estão algumas instruções sobre como usar a interface do Logic Editor.

>**Note**
>
>Para aqueles que estão acostumados com a interface do Blender 2.49, você pode precisar de algum tempo para se acostumar com o novo design aprimorado do Blender. A primeira coisa que você notará é que o painel Physics foi movido para a guia Physics no Properties Logic Editor. Se você pulou direto para este capítulo e está um pouco perdido na navegação pela interface do Blender, o Capítulo 1 deve ajudá-lo a encontrar o elemento de IU pretendido.


### Adicionar <a id="Add"></a>

Para adicionar novos Logic bricks, só é possível para o objeto ativo. Este sempre é exibido como o primeiro na lista do Logic Editor. Você pode ver o botão Adicionar Sensor / Controlador / Atuador logo após o nome do objeto ativo em sua respectiva coluna, conforme mostrado na Figura 3.4.

![Adicionar Controlador](../figures/Chapter3/Fig03-04.png "Add controller")

Ao clicar no botão, uma lista pop-up mostrará todos os blocos lógicos disponíveis que são compatíveis com este tipo de objeto (por exemplo, os sensores de armadura estão disponíveis apenas para objetos de armadura). Selecionar o tipo desejado criará um novo Logic Brick com os parâmetros padrão para este tipo específico (que você provavelmente precisará alterar). O nome do Logic Brick é criado automaticamente, com base em seu tipo, por pura conveniência.

>**Maneiras rápidas de adicionar um bloco lógico**
>
>As a quick alternative, you can use the Add Menu (in the Logic Editor header bar) or press Shift+A (while mouse pointer is in the Logic Editor).

### Remove <a id="Remove"></a>

Para excluir blocos lógicos individuais, você precisa clicar no ícone "x" presente no cabeçalho de cada bloco lógico. Ao fazer isso, você está desvinculando cada Logic Brick com qualquer Logic Brick conectado e removendo-o. Embora esta ação possa ser revertida com Undo (Ctrl + Z), simplesmente desvincular um Logic Brick ou movê-lo para um estado inativo (para controladores) é suficiente para desativá-lo. Há também um botão de caixa de seleção que define o estado ativo do sensor. O mecanismo de jogo não calculará blocos lógicos desassociados e desabilitados. Portanto, pode ser útil ter sensores e atuadores de teste pendurados para uso posterior sem impacto no desempenho.

### Link <a id="Link"></a>

Cada Logic Brick possui um conector usado para ligá-lo a outros Logic Bricks. Os sensores mostram o conector no lado direito de seu cabeçalho, enquanto os atuadores o mostram no lado esquerdo. Os controladores são colocados entre os sensores e atuadores, de forma que os conectores são apresentados em ambos os lados. Arraste o conector de um Logic Brick e solte-o no conector ao qual deseja se vincular.

>**Mate dois pássaros com uma pedra: ligando e adicionando um controlador**
>
>Tente ligar um sensor diretamente a um atuador no mesmo objeto. O Blender irá criar automaticamente um controlador And e ligá-lo entre eles.

Você não precisa manter a lógica autocontida em objetos individuais. Ao selecionar mais de um objeto ao mesmo tempo, você verá todos eles no Logic Editor. Esse recurso permite que você conecte um sensor de um objeto ao controlador de outro e novamente ao atuador de outro objeto. Este é um dos elementos-chave para instanciar grupos [md] uma maneira avançada de compartilhar blocos lógicos, que é abordado no final deste capítulo.

>**Sistema de Mensagens**
>
>Se você descobriu que objetos com ligações cruzadas podem facilmente se tornar difíceis de controlar, bem-vindo à equipe. Antes de ficar desesperado, certifique-se de ler sobre a alternativa elegante apresentada pelo sensor Message e pelo atuador Message. Esteja ciente de que se você decidir pelo sistema de mensagens, seus eventos sempre serão atrasados por um tique lógico, já que só disparará o sensor no próximo loop lógico.

### Desvincular <a id="Unlink"></a>

Arraste o mouse segurando o botão esquerdo do mouse e a tecla Control para usar o recurso Desvincular. Isso ativará um sistema de faca para cortar os links entre os tijolos lógicos que você deseja desvincular. Funciona da mesma forma que o Editor de Nó no Blender.

### Expandir / Mostrar / Ocultar <a id="Expand/Show/Hide"></a>

A organização visual é um aspecto fundamental do trabalho com blocos lógicos. Você não precisa editar os valores de um Logic Brick o tempo todo, então você pode manter a maioria deles ocultos. Você pode ocultar / mostrar um Logic Brick em particular usando a seta à esquerda de seu cabeçalho. Se você deseja ocultar / mostrar todos os sensores ou controladores ou atuadores de um objeto, basta clicar no cabeçalho correspondente.

>**Ocultar e Mostrar Menus**
>
>No topo do Logic Editor, você pode acessar um menu para ocultar ou mostrar rapidamente os tijolos para sensores, controladores e atuadores para todos os objetos selecionados, como visto na Figura 3.5.

![Mostrar / ocultar menu suspenso](../figures/Chapter3/Fig03-05.png "Show/Hide drop-down menu")

### Move <a id="Move"></a>

Quando você adiciona um novo Logic Brick, ele aparecerá na parte inferior da pilha de Logic Bricks do objeto ativo. Você pode movê-lo para cima e para baixo de acordo com sua necessidade. Para reorganizá-los, você precisa definir o Logic Brick como não expandido e usar os ícones de seta para cima e para baixo.

### Estados <a id="States"></a>

Acima da lista de um controlador de objeto, você pode ver um pequeno, mas importante ícone de adição. Mostra e esconde o controle dos Estados. Você também pode definir os estados iniciais do jogo e aqueles que deseja ver naquele momento na interface. Para aprender a usar o sistema de estado, olhe para o final deste capítulo na seção "Máquina de estado".

![Controlador de Estados](../figures/Chapter3/Fig03-06.png "Controller states")

>**Camdas de Estados**
>
>Quando você joga o jogo, os estados ativos de um controlador são aqueles na linha inferior mostrada na Figura 3.6, conhecidos como _estados iniciais._ Os estados presentes na linha superior, ou seja, os estados visíveis, são uma ferramenta para ajudá-lo a visualizar diferentes estados sem mexer com o conjunto de estados iniciais. Eles são redefinidos para os Estados iniciais sempre que você reabre o arquivo.

A interface de estados funciona como o sistema de camadas no Blender [md] clique para selecionar um estado e Shift + clique para selecionar mais de um. Quanto às camadas do Blender, os estados não têm nomes individuais por enquanto.

### Propriedades <a id="Properties"></a>

O painel esquerdo do Logic Editor permite que você adicione e edite as propriedades do jogo de objetos (consulte a Figura 3.7). Ao contrário dos blocos lógicos, as propriedades visíveis do jogo são apenas as do objeto ativo atual. Assim como em outras áreas do editor no Blender, você pode ocultar / mostrar esta área com o atalho do painel de propriedades (N).

![Painel de propriedades do jogo](../figures/Chapter3/Fig03-07.png "Game Properties panel")

As propriedades são freqüentemente usadas para armazenar uma característica variável de um objeto de jogo (por exemplo, vida, energia ou velocidade). Nesse caso, você usará atuadores de propriedade para alterar os valores de uma propriedade ao atingir um inimigo, acelerar e outros tipos de eventos. Além disso, os sensores de propriedade ou controladores de expressão podem invocar ações diferentes quando você chega a certos valores (por exemplo, terminar o jogo quando a vida e a energia forem zero).

Outra maneira de usar as propriedades é determinar como outros objetos reagirão a cada um. Como veremos mais adiante neste capítulo, existem alguns sensores que dependem da existência de uma propriedade para interagir com um objeto. Esses sensores físicos (Near, Collision, etc.) funcionam independentemente do valor da propriedade; eles verificam apenas o nome da propriedade, que não pode ser alterado dentro do jogo.

As propriedades disponíveis são: Float, Integer, Timer, Boolean e String.

Agora, vamos seguir em frente e ver as funcionalidades que você pode usar.

### Sensores <a id="Sensors"></a>

Os sensores são a primeira camada de interação entre os objetos do jogo e o próprio jogo, portanto, eles precisam ser planejados com cuidado para evitar sobrecarga no desempenho lógico. Geralmente é uma troca entre facilidade de manutenção e velocidade de trabalho. Para os primeiros estágios de seu projeto, você pode ter vários sensores para os mesmos testes (por exemplo, sensores de colisão individuais para diferentes verificações de propriedades e materiais). Mais tarde, quando e se o desempenho se tornar um problema, você pode substituí-los por uma solução mais elegante com a mesma funcionalidade. Mas, por enquanto, você deve se concentrar apenas em jogar e experimentar as ferramentas apresentadas.

A próxima parte do capítulo está estruturada para servir como uma leitura contínua e como um guia de referência. Se você ler, terá uma visão geral do sistema, o que pode fazer e quando pode usar os recursos específicos. Eu recomendo que você leia tudo pelo menos uma vez. Posteriormente, você pode revisitar este capítulo para uma perspectiva mais aprofundada das funcionalidades apresentadas.

#### Header <a id="Header"></a>

Na primeira parte deste capítulo mencionamos algumas opções presentes em todos os blocos lógicos. Agora veremos com mais detalhes as propriedades que são específicas para cabeçalhos de sensor, conforme mostrado na Figura 3.8.

![Sensor header](../figures/Chapter3/Fig03-08.png "Sensor header")

- **Name:** Pode ser usado para identificar o seu sensor, mesmo quando não está expandido. Você vai se referir a ele de dentro dos controladores Expression e Python.

- **Pulse Positive:** Envia continuamente pulsos positivos para o controlador enquanto o sensor está ativo.

- **Pulse Negative:** Envia continuamente pulsos negativos para o controlador enquanto o sensor não está ativo. Um pulso negativo não será enviado antes que o sensor seja positivo pelo menos uma vez ou o nível seja habilitado.

- **Frequency:** Define a frequência com que o pulso acionará o sensor. A frequência é realmente o número de tiques lógicos que serão ignorados antes de acionar o sensor novamente. Mantenha-o em zero para ter o sensor pulsando a cada tique lógico.

- **Level:** Aciona o controlador no início do jogo ou quando os controladores são ativados a partir de um estado desativado. Com esta opção, você pode forçar sinais negativos (por exemplo, uma propriedade não está dentro de um intervalo, um mouse não está sobre seu objeto, uma tecla não é pressionada) para acionar o controlador, mesmo se ele nunca ficar positivo. Geralmente usado como parte de um sistema de estado para forçar um sensor a ser avaliado logo após a mudança de estado de um objeto.

- **Tap:** Aciona o sensor apenas um de cada vez. Ele funciona em oposição ao pulso e é especialmente útil para sensores físicos, sensores de teclado e sensores de mouse.

- **Invert:** Ainda aciona o sensor como faria normalmente, mas envia um sinal negativo quando ele inicia e um positivo quando deixa de ser válido (por exemplo, quando uma tecla não é mais pressionada). Se você precisa que o sensor envie um sinal negativo antes de ser positivo, lembre-se de ligar o Nível.

#### Always <a id="Always"></a>

Always, conforme mostrado na Figura 3.9, é o sensor mais simples e usado com mais frequência. Existem basicamente duas maneiras de usá-lo. Quando o pulso está desligado, ele será executado uma vez quando o nível começar e nunca mais. Quando o Pulso está ativado, o sensor funciona repetidamente, acionando os controladores de acordo com sua frequência.

![Always sensor](../figures/Chapter3/Fig03-09.png "Always sensor")

Os sensores Always são comumente usados para inicializar atuadores, como Filtros 2D, Movimento, Cena, Som e assim por diante. Quando combinado com o controlador Python, esse sensor costuma ser usado para chamar scripts que precisam ser inicializados primeiro (quando a frequência é zero) e scripts que tratam de eventos globais (com a frequência definida de acordo com as necessidades de um script específico).

#### Delay <a id="Delay"></a>

Semelhante ao sensor Always, o sensor Delay permite adiar a inicialização de algumas ações por alguns tiques lógicos (consulte a Figura 3.10). Você notará três opções aqui: Delay, Duration e Repeat.

![Delay sensor](../figures/Chapter3/Fig03-10.png "Delay sensor")

_Delay_ é o período de espera inicial antes que o sensor seja acionado. _Duração_ representa quanto tempo (uma vez disparado) o sensor ficará positivo / ativo. Se quiser que isso aconteça ciclicamente, você pode ativar a repetição. É importante observar que a opção Pulso funciona com base nesses três parâmetros.
In combination with the Python controller, this sensor is often used to call scripts that require other scripts to run first.

#### Actuator <a id="Actuator"></a>

Aí vem a situação do ovo e da galinha. Para entender este sensor, você pode precisar se familiarizar mais com os atuadores primeiro. O sensor do atuador é acionado quando o atuador selecionado muda de estado (ativo / inativo), conforme mostrado na Figura 3.11. Uma aplicação típica disso é com o atuador Action. Se você usar um controlador de Expressão para verificar o status do sensor do atuador (por exemplo, attensor = false), poderá acionar outra ação logo após a conclusão de uma animação.

![Actuator sensor](../figures/Chapter3/Fig03-11.png "Actuator sensor")

>**Sensor do atuador e o sistema de mensagens**
>
>Nos arquivos online, você pode encontrar um arquivo que ilustra como este sensor pode ser usado com a mensagem e o sistema de animação: _\Book\Chapter3\sensor\_actuator.blend_

#### Joystick <a id="Joystick"></a>

Não dê ouvidos aos fanboys do Kinect, os joysticks ainda estão aqui para ficar (veja a Figura 3.12). Comece selecionando seu Índice de Joystick, o que significa que você pode trabalhar com vários joysticks no mesmo jogo. Para cada sensor de Joystick, você pode controlar um dos seguintes: Chapéu, Eixo, Botão e Eixo único.

![Joystick sensor](../figures/Chapter3/Fig03-12.png "Joystick sensor")

#### Keyboard <a id="Keyboard"></a>

Você não deseja mapear seu teclado, tecla por tecla, para sensores de teclado individuais (consulte a Figura 3.13). No entanto, você pode. Para fornecer flexibilidade aos desenvolvedores de jogos, o mecanismo de jogo pode controlar ações com base em uma tecla individual, capturar modificadores (tradicionalmente Alt, Ctrl, Shift, mas estendidos a qualquer tecla) ou em nenhuma tecla específica. Para o último, a opção Todas as teclas vinculadas a um controlador Python é o caminho a percorrer, embora para uma abordagem Python completa, você nem mesmo precise do sensor de teclado.

![Keyboard sensor](../figures/Chapter3/Fig03-13.png "Keyboard sensor")

Log Toggle e Target trabalham juntos. Quando o valor da propriedade Log Toggle for True e uma String for definida como Target, você pode acompanhar todas as teclas pressionadas por um determinado sensor. Pode ser usado para depuração ou mesmo para entrada direta de textos para uma propriedade.

Nos arquivos online, você pode ver uma amostra disso: _\Book\Chapter3\sensor\_keyboard.blend_

>**Keys Status on Python**
>
>O sensor do teclado enviará um pulso positivo quando a tecla especificada for pressionada e um pulso negativo quando for liberada. O status da chave é representado por constantes Python: bge.logic.KX\_INPUT\_JUST\_ACTIVATED logo quando é pressionado, bge.logic.KX\_INPUT\_ACTIVE enquanto está sendo pressionado e bge.logic.KX\_INPUT\_JUST\_RELEASED logo após ter sido lançado. Seu status só pode ser acessado a partir de um controlador Python.

#### Mouse <a id="Mouse"></a>

O sensor do mouse é usado para controlar a entrada do mouse no jogo. Ele pode ser usado inteiramente com Logic Bricks ou integrado com Python. Esteja ciente de que sensores individuais são necessários para lidar com diferentes eventos do mouse e a maioria deles não é tratada por objeto (consulte a Figura 3.14). Os eventos do mouse são separados em dois tipos diferentes comumente combinados:

- **Mouse inputs** - entrada geral: movimento, roda para baixo, roda para cima, botão direito, botão do meio e botão esquerdo.

- **Mouse actions** - por objeto: Mouse Over e Mouse Over Any.

![Mouse sensor event types](../figures/Chapter3/Fig03-14.png "Mouse sensor event types")

Se você executar um atuador quando uma entrada do mouse for acionada (por exemplo, botão esquerdo), a ação acontecerá, independentemente de onde o clique estiver. Se você precisa que um atuador aconteça quando você clica em um objeto específico, você precisa de um Mouse Over e um Botão Esquerdo vinculados por meio de um Controlador And.

>**Collision, Physics and Mouse Click**
>
>Para ser clicável, um objeto deve ter a colisão habilitada no Painel de Física.

#### Armature <a id="Armature"></a>

Armature é um sensor avançado para ajudá-lo a detectar o limite de erro nas restrições ósseas (consulte a Figura 3.15). Ele foi criado como parte da implementação do solver IK integrado pelo desenvolvedor Benoit Bolsée.

![Armature sensor](../figures/Chapter3/Fig03-15.png "Armature sensor")

O objetivo original deste conjunto de funcionalidades era voltado para estudos robóticos, portanto, pode ficar fora do escopo de seu projeto. Se você for usar o iTaSC (especificação de tarefa instantânea usando restrições), este sensor o ajudará a controlar as restrições de armadura. Para obter mais informações, visite: [http://wiki.blender.org/index.php/Dev:Source/GameEngine/RobotIKSolver](http://wiki.blender.org/index.php/Dev:Source/GameEngine/RobotIKSolver)

>**Para César, o que é de César**
>
>O sensor de armadura está disponível apenas para objetos de armadura. Se você copiar este sensor para objetos que não sejam de armadura, o painel mostrará "Sensor disponível apenas para armaduras" e o sensor ficará inoperante.


#### Touch <a id="Touch"></a>

O sensor de toque é um subconjunto do sensor de colisão. Na verdade, eles compartilham o mesmo código internamente. É provável que seja suspenso no futuro.

#### Collision <a id="Collision"></a>

O sensor de colisão pode ser usado para detectar colisões entre um objeto do jogo e outros objetos ou o ambiente (ver Figura 3.16). Você pode filtrar a colisão para acionar o sensor apenas quando o objeto atinge uma face com um material específico ou um objeto com uma propriedade particular (use o botão M/P para alternar entre eles). Como ocorre com os sensores de Física, esse sensor depende das propriedades físicas dos objetos envolvidos na interação (colisão, fantasma, caixa delimitadora e assim por diante). Consulte o Capítulo 6, "Física", para ler sobre as configurações físicas dos objetos e do jogo.

![Collision sensor](../figures/Chapter3/Fig03-16.png "Collision sensor")

Este sensor é frequentemente usado com proxies de colisão, que são malhas invisíveis de baixo polímero criadas para poupar seus pesados objetos gráficos dos caros testes de colisão.

>**Use It Moderately**
>
>Junto com os outros sensores de Física, este sensor é considerado caro em termos de computação, então use-o razoavelmente e use proxies físicos sempre que possível [md] um tópico discutido no Capítulo 6 e Capítulo 8, "Fluxo de Trabalho e Otimização."

#### Near <a id="Near"></a>

Para um controle mais avançado sobre a interação física do seu jogo, você pode disparar ações com base na distância dos objetos em sua cena antes mesmo de eles colidirem. Ao contrário do sensor de colisão, o sensor Near é sensível apenas à detecção de propriedade (consulte a Figura 3.17). Deixe a propriedade em branco e ela detectará todos os objetos.

![Near sensor](../figures/Chapter3/Fig03-17.png "Near sensor")

Este sensor será acionado quando um objeto detectado estiver mais perto do que a distância de disparo. Uma vez acionado, ele só deixará de ser válido depois que o objeto estiver mais longe do que a distância de reinicialização.

>**The Amazing Near Sensor**
>
>O sensor Near detecta todas as direções. É o motor de jogo equivalente ao sentido do Homem-Aranha.

#### Radar <a id="Radar"></a>

O sensor de radar cria um cone de detecção travado em uma direção (consulte a Figura 3.18). Você deve escolher o eixo, a distância e o ângulo de seu radar de detecção. Semelhante à maioria dos outros sensores de física, você pode filtrar a detecção por propriedade.

![Radar sensor](../figures/Chapter3/Fig03-18.png "Radar sensor")

>**Troubleshooting and Debugging**
>
>Para depurar facilmente as configurações do seu radar no jogo, você pode ativar a opção Mostrar Visualização Física no Menu do Jogo. O resultado é mostrado na Figura 3.19.


![Radar Sensor Physic Visualization](../figures/Chapter3/Fig03-19.png "Radar Sensor Physic Visualization")

#### Ray <a id="Ray"></a>

O sensor de raio só pode lançar raios em um eixo especificado (em relação ao objeto) e na medida em que a distância de alcance determinada vai. Embora possa parecer limitante, isso o torna o sensor de física mais rápido disponível (veja a Figura 3.20).

Para obter mais dados do raio fundido, você pode acessar o sensor de um Controlador Python. A API permite que você acesse hitObject, hitPosition e hitNormal.

Se o Modo de Raios-X estiver ativado, o raio só irá parar quando atingir um objeto com a propriedade ou material especificado. Caso contrário, ele irá parar quando o primeiro objeto retornar Nenhum, no caso de uma não correspondência.

![Ray sensor](../figures/Chapter3/Fig03-20.png "Ray sensor")

#### Random <a id="Random"></a>

O sensor Random gera pulsos aleatoriamente (consulte a Figura 3.21). Seu uso é tão genérico que é enganoso definir uma aplicação específica para ele. Você pode alterar a propriedade Seed para produzir pulsos pseudo-aleatórios. Quando a semente é zero, ele funciona como um sensor Always normal.

![Random sensor](../figures/Chapter3/Fig03-21.png "Random sensor")

>**Do Not Use It Randomly**
>
>Use o sensor Random junto com outros sensores para adicionar uma dinâmica orgânica a eles. É especialmente útil para o comportamento do ambiente e inteligência artificial (I.A.).


#### Message <a id="Message"></a>

O sensor Message recebe uma mensagem enviada de um atuador Message ou de um controlador Python (consulte a Figura 3.22). Um objeto de jogo receberá qualquer mensagem enviada especificamente para ele ou transmitida para todos os objetos. Para atingir outro nível de controle, você pode usar o campo opcional Assunto para filtrar as mensagens de um determinado assunto (não acionando de outra forma). Dê uma olhada no atuador Message para obter uma explicação mais detalhada.

![Message sensor](../figures/Chapter3/Fig03-22.png "Message sensor")

>**Extra Message Information**
>
>>As informações extras disponíveis na mensagem (assunto, corpo) podem ser acessadas apenas por um controlador Python.

#### Property <a id="Property"></a>

O sensor Property ajuda você a usar Properties de maneira eficaz para seus objetos de jogo (consulte a Figura 3.23). Uma propriedade do jogo geralmente não altera nenhum aspecto do jogo diretamente (consulte a nota "Expressões"). Em vez disso, eles armazenam um valor (por exemplo, pontos vitais) a ser interpretado e para invocar ações e efeitos específicos.

![Property sensor](../figures/Chapter3/Fig03-23.png "Property sensor")

Este sensor possui diferentes tipos de avaliação que permitem detectar valores específicos, faixas de rastreamento ou detectar qualquer alteração de propriedade. Respectivamente, eles são: iguais, diferentes, intervalos e alterados. Esteja ciente de que a opção de intervalo não deve ser usada por Strings e Booleanos, mas é a única recomendada para propriedades de Timer.

As exceções são propriedades usadas por scripts Python, aqueles usados por Filtros 2D e strings de texto usadas por textos de bitmap.

>**Expressions**
>
>Em vez de valores diretos, você pode usar uma expressão nos campos de valor para este sensor. Dê uma olhada em Controller Expression para mais detalhes.

### Controllers <a id="Controllers"></a>

Os sensores não podem fazer muito por si próprios sem controladores. Conforme explicado na seção de arquitetura, os controladores são a peça central dos Tijolos Lógicos, pois todos os eventos passam por eles, assim como as ações do jogo. No entanto, eles são simples de entender e usar. Para jogos que usam apenas Logic Bricks, você usará um ou dois tipos de controladores na maioria das vezes. Na verdade, até algumas versões do Blender atrás, não tínhamos mais do que quatro tipos de controladores.

Nesta seção, o Expression Controller merece atenção especial pelas possibilidades que traz. O Python Controller, por outro lado, é a estrela que brilha em outra seção do livro, pois revela um mundo de complexidade e promessas. Ele pode ser ignorado por enquanto e revisitado quando você chegar ao Capítulo 7, "Scripting Python".

>**Using States as Organization Layers**
>
>O sistema de estado do controlador foi projetado para ajudar na construção de sistemas de máquina de estado avançados. Mas acabou funcionando muito bem como uma forma de organizar seus blocos lógicos. Você pode usar diferentes estados como camadas para agrupar controladores e seus sensores e atuadores vinculados. O estado inicial do controlador precisa incluir todos os estados que você definiu. Mas enquanto trabalha, você pode alternar os estados visíveis para mostrar apenas uma pequena parcela deles por vez.

#### Header <a id="Header"></a>

Semelhante aos sensores, cada controlador carrega um conjunto único de informações, independentemente de seu tipo. Preste atenção especial às opções de Estado e Marca, ambas exclusivas dos Controladores. Na Figura 3.24, você encontrará todas as opções disponíveis em seus cabeçalhos.

![Controller header](../figures/Chapter3/Fig03-24.png "Controller header")

- **Name** : Ao contrário dos sensores e atuadores, o nome aqui não tem nenhuma importância além de manter seus controladores fáceis de identificar quando não estão expandidos.

- **State** : Defina o estado (de 1 a 30) do controlador. Para ler sobre o sistema State Machine, verifique a seção "State Machine" neste capítulo.

- **Mark** : Força o controlador a funcionar antes de controladores não marcados.

#### Booleans <a id="Booleans"></a>

Quando você tem um único sensor que precisa chamar um atuador, não há muito com que se preocupar. Neste caso, um simples controlador And fará com que funcione. Se, em vez disso, você precisar ativar o atuador apenas quando o sensor for False, poderá usar a opção Inverter para continuar usando o mesmo controlador Adicionar. Tão simples? Vamos complicar um pouco então. E se você tiver dois sensores e apenas um deles precisar ser verdadeiro? Você pode criar dois controladores And ligados ao mesmo atuador. Não é elegante, mas funcionaria.

>**Quantas vezes você pode ativar um atuador?
>
>Se você acha que a configuração acima chamaria o atuador duas vezes, divirta-se testando-o. Um atuador é ativado apenas uma vez por quadro, independentemente do número de controladores que o chamam.

Mas e se você quisesse usar apenas um controlador para lidar com esses dois sensores? Nesse caso, seria o controlador Or, criado especificamente para isso. Mas isso não é tudo. Por conveniência ou para um controle mais avançado, você pode simplificar seus controladores usando os outros controladores booleanos. Junto com And e Or, essas são as outras chaves lógicas a serem usadas ao combinar vários sensores e seus resultados.

- **And** : Verdadeiro se _all_the sensors forem verdadeiros. False se _any_ dos sensores for False. 

- **Or** : Verdadeiro se _any_ dos sensores forem verdadadeiro Verdadeiro. Falso se _all_ sensores forem falsos.

- **Nand** : True if _any_ of the sensors is False. False if _all_ the sensors are True

- **Nor** : True if _all_ the sensors are False. False if _any_ of the sensors is True

- **Xor** : True when _only one_ sensor is True. False if _more than one_ sensor is True or if _all_ the sensors are False.

- **Xnor** : True if _more than one_ sensor is True or if _all_ the sensors are False. False when _only one_ sensor is True and _all_ the other sensors are False.

#### Expression <a id="Expression"></a>

Às vezes, os interruptores lógicos não fornecem controle suficiente para avaliar seus sensores. Você pode querer comparar o valor de mais de uma propriedade ao mesmo tempo, ou talvez até mesmo verificar arranjos específicos em seus sensores, chamando o atuador apenas quando alguns sensores são positivos e outros negativos. Ou por que não (afinal de contas é o seu jogo) fazer tudo isso juntos? Como você adivinhou, as expressões podem lidar com todas essas situações e algumas outras.

Antes de entrar em todas as opções, vamos primeiro dar uma olhada em alguns exemplos:

Primeiro caso: Queremos eliminar o seu jogador quando a energia for zero e não houver mais vidas. Portanto, criamos duas propriedades de jogo, chamadas "energia" e "vida", e as controlamos com a expressão:

energy<=0 AND life==0

Simples, certo? Mas e se você quiser terminar o jogo ao digitar "sair"? Agora você precisa de um sensor de teclado com todas as teclas registradas em uma propriedade de texto. A expressão seria:

text=="quit\n"

>**Fim da Linha**
>
>Aqui, estamos usando \ n para identificar um Return (Enter) logo após a palavra. Você pode ver esta última técnica combinada com outros atuadores e objetos diferentes em: _\Book\Chapter3\controller\_expression.blend._
>Isso é especialmente poderoso para prototipagem rápida e depuração de seu jogo.


As expressões tendem a ser tão simples quanto os exemplos apresentados. Eles podem crescer muito, entretanto, e as partes a seguir mostrarão como combinar expressões simples para criar controladores mais avançados. Lembre-se de que as expressões também são usadas no sensor de propriedade e no atuador de propriedade. A diferença é que para eles o resultado será utilizado diretamente como valor da propriedade. Portanto, você usará principalmente Valores e Operações Aritméticas. Para o controlador de Expressão, o valor esperado é sempre um Booleano, então você acaba usando o Teste de Comparação e as Operações Booleanas com mais frequência.

>**Error Checkpoint**
>
>Sempre verifique se há erros no console. Se a expressão estiver incorreta, o mecanismo de jogo imprimirá um erro quando você chamar o controlador.

#### Values <a id="Values"></a>

A expressão mais simples não contém mais do que um único valor. Se você deseja verificar se uma propriedade booleana é verdadeira, você só precisa usar seu nome como um valor:

my\_property\_that\_may\_be\_true

Para a expressão do controlador, você usará apenas o valor solitário ao lidar com booleanos; no entanto, para o sensor de propriedade, atuador de propriedade e como parte de grandes expressões, você também pode usar os seguintes tipos como valores:

- **Boolean** : True, False

- **Number** : 5, [ms]7, 3.5, 40, 3.5[md]inteiros e floats, positivo, negativo e até zero.

- **String** : "text"[md]sempre entre aspas.

- **Property** : propertyName[md]fornece o valor da propriedade.

- **Sensor** : sensorName[md]dá Verdadeiro ou Falso de acordo com o status do sensor.


Um único valor não é exatamente uma expressão. Vamos prosseguir e ver que tipo de expressões e operações podemos fazer ao combiná-los:

>**Sensors in an Expression**
>
>Para usar um nome de sensor, o sensor deve estar vinculado ao controlador Expression. Sensores não podem ser usados nas expressões para o sensor de propriedade e o atuador de propriedade.

#### Comparison Tests <a id="Comparison"></a>

Se, em vez de testar uma única variável, você precisar comparar dois valores, existem cinco testes de comparação diferentes que você pode usar. O teste pode ser entre uma variável (propriedade ou sensor) e um valor, dois valores ou duas variáveis:

- **Equal** : fruit = "jabuticaba"

- **Greater** : 2.5 > 2.49

- **Lesser** : energy < 37

- **Greater or Equal** : speed >= 100.0

- **Lesser or Equal** : timer <= 2011

O resultado de um teste de comparação sempre será um booleano. Se você precisar retornar um valor diferente de True ou False, o que você está procurando é:

**Condition Statement** : IF (frame < 0, [ms]1, 0)

A sintaxe é: IF (Condition, ValueWhenTrue, ValueWhenFalse). Se você usar a expressão acima como um valor para o modo Adicionar em um atuador de propriedade, ele diminuirá o contador (por exemplo, quadro) se o valor for maior que zero.

#### Arithmetic Operations <a id="Arithmetic_Operations"></a>

Se o seu valor for numérico, você também pode manipulá-lo um pouco. Isso pode ser usado para atribuir um valor com base em uma variável (por exemplo, velocidade \ * tempo) ou como parte de um teste (por exemplo, energia + poção> 0). As operações matemáticas mais básicas são suportadas para operar seu valor, para os registros:

- **Addition** : 1 + 3.8

- **Subtraction** : 10.5 - 5

- **Multiplication** : 23 \* 1000

- **Division** : 37 / 400

- **Modulus** : 10 % 3

#### Boolean Operations <a id="Boolean_Operations"></a>

Finalmente, você tem a capacidade de combinar testes booleanos. Um teste booleano pode ser um valor booleano simples (por exemplo, um sensor ou um valor de propriedade) ou o resultado de um teste de comparação. Eles funcionam como agregadores por meio dos quais você pode compilar grandes testes de expressão.

- **And** : potionKeyboardSensor AND numberPotions > 0 AND energy + 30 < 60

- **Or** : speed <= 0.0 OR stopKeyboardSensor

- **Not** : jumpKeyboardSensor AND NOT floorCollisionSensor

As operações booleanas não são comutativas ou associativas quando agrupadas. Por exemplo, tente ler as seguintes expressões:

1 = 2 AND 3 > 4 OR 5<6

False AND False OR True

Eles são intencionalmente ambíguos. Estamos testando o AND ou o OR primeiro? Para resolver esse problema, você pode usar parênteses para isolar suas expressões. As expressões anteriores são avaliadas como:

(1 = 2 AND 3 > 4) OR 5 < 6

(False AND False) OR True

Essas expressões resultarão em verdadeiro (falso ou verdadeiro = verdadeiro). Se o resultado esperado fosse falso, deveríamos ter agrupado como:

1 = 2 AND (3 > 4 OR 5 < 6)

False AND (False OR True)

Você pode encontrar um uso elegante dos operadores booleanos para criar um mecanismo de alternância em: _\Book\Chapter3\controller\_expression\_toggle.blend._

>**Fake Flipper Animation with Expressions**
>
>No material que acompanha, você pode ver uma simulação do modo de animação Flipper implementado usando o modo Property. Isso é feito de duas maneiras diferentes: uma com um controlador Expression, outra com controladores Nand e And e um atuador Expression in a Property. Mostra a flexibilidade do sistema e é uma boa maneira de regular a velocidade de sua animação: _\Book\Chapter3\controller\_expression\_flipper.blend_.

#### Python Controller <a id="Python_Controller"></a>

Com um controlador Python, você pode avaliar sensores e ativar atuadores da mesma forma que faria com outros controladores. Na verdade, você pode substituir qualquer um dos testes (opções ou expressões lógicas) por um equivalente em Python. Na verdade, não apenas os outros controladores podem ser substituídos por este, mas também a maioria dos seus blocos lógicos. O Capítulo 7 é inteiramente dedicado a como e quando usar este controlador. Mesmo que você não goste de programação, recomendamos que leia as seções de introdução deste capítulo para entender suas diferenças e vantagens.

Existem dois tipos de controladores Python: Script e Módulo.

- **Script** : Isso pegará um bloco de dados interno de texto e o executará como um script.

- **Module** : Isso chamará um módulo de um arquivo de script dentro ou fora do arquivo do jogo. O modo Módulo tem uma opção de depuração que força o módulo a ser recompilado toda vez que você o chama. Isso é muito lento, mas permite que você faça alterações em seu script enquanto o jogo está jogando.

>**Which Came First, the Controller or the Controller?**
>
>Para scripts, a ordem em que os controladores são executados é importante. Nos casos em que você precisa que um script seja executado antes dos outros, você pode usar a opção Mark presente no cabeçalho do Controlador. Isso é comumente usado para controladores Python que executam scripts que são responsáveis pela inicialização das variáveis e configurações do jogo.

### Actuators <a id="Actuators"></a>

Por último, mas não menos importante, existem os atuadores. O trabalho que você teve ao configurar sensores, controladores e vinculação de macarrão finalmente valerá a pena. Os atuadores são agrupados por temas (cena, jogo, objeto, ações e assim por diante), e seus nomes e aplicativos podem surpreendê-lo. (Por exemplo, você sabia que o atuador da câmera não precisa ser usado por um objeto de câmera?) Recomendamos que você se familiarize com todas as opções e subopções e as experimente o máximo que puder. Embora alguns efeitos funcionem por si próprios (por exemplo, o atuador do jogo), alguns serão mais úteis quando combinados (por exemplo, atuadores de movimento e ação). Diverta-se!

#### Header <a id="Header"></a>

O cabeçalho dos atuadores é semelhante aos sensores. Como os sensores, o Nome é um elemento essencial ao usar o atuador com um controlador Python. Na Figura 3.25, você também pode ver o Pin, uma opção especial disponível para ser usada com os estados do controlador.

![Actuator header](../figures/Chapter3/Fig03-25.png "Actuator header")

- **Name** : Isso pode ser usado para identificar o seu atuador, mesmo quando não está expandido. Também é usado em scripts Python para ativá-lo.

- **Pin** : Ao trabalhar com o sistema State Machine, você pode usar a opção State no topo da lista de atuadores para mostrar apenas os atuadores vinculados aos controladores de estados visíveis. Com a opção Pin no cabeçalho do atuador, você pode definir seu atuador para estar sempre visível.

#### Action <a id="Action"></a>

Câmera, luzes, ação! E vamos começar a animação. Quer você queira animar sua armadura ou quer jogar uma ação pré-gravada, você vai acabar usando este atuador. Uma ação pode conter diferentes Curvas F, controlando várias propriedades do objeto. Se você dividir suas curvas de propriedade em diferentes ações, poderá controlá-las uma de cada vez. Por exemplo, deixe Size e ObColor na mesma ação, e você pode ter uma banana que é verde quando ainda é pequena e fica amarela enquanto cresce.

Você também pode ter a mesma propriedade presente em várias ações e usar ações individuais para armazenar diferentes animações.

>**Short Actions in the Long Run**
>
>Antes do redesenho do sistema de animação no Blender, só era possível ter várias ações para armaduras e chaves de forma. Portanto, para qualquer outra ação animada, as pessoas criariam uma ação realmente longa com diferentes animações em diferentes intervalos de quadros. Isso ainda funciona bem, mas é difícil de gerenciar se você precisar alterar a duração de uma das animações [md], você terá que atualizar o início e o fim de todos os atuadores que estavam jogando as outras subanimações. Você ainda pode usar essa técnica para organizar seu arquivo; no entanto, às vezes, uma ação longa pode ser mais fácil de gerenciar do que várias ações pequenas.

O atuador permitirá que você escolha uma ação, defina o intervalo do quadro e configure como deseja jogá-la (consulte a Figura 3.26). Se você está planejando reutilizar este atuador [md] por exemplo, para blocos lógicos vinculados/compartilhados [md], você pode deixar a ação em branco e configurá-la por meio da API Python durante o mecanismo de jogo. No Capítulo 4, "Animação", usaremos esse atuador em uma série de tutoriais.
![Action actuator](../figures/Chapter3/Fig03-26.png "Action actuator")

##### What Can Be Animated <a id="What_Can_Be_Animated"></a>

Algumas das animações que você cria no Blender podem ser usadas no motor de jogo. O mesmo resultado que você vê na janela de exibição ao reproduzi-los com Alt + A, também pode ser obtido no mecanismo de jogo. Isso inclui poses de armadura, teclas de forma e algumas das propriedades de objeto, material, luz e câmera como a seguir:

- **Pose** :Qualquer sequência gravada em um objeto Armature pode ser reproduzida. É comum ter diferentes ciclos animados [md] caminhada, corrida, salto, caminhada cansada, fazer uma pausa [md] e alternar entre eles durante um evento. Ao usar vários atuadores de ação, você pode ter uma ação em execução ao iniciar uma nova. Para fazer a transição sem problemas, você pode definir o Blend In e Priority para, respectivamente, misturar as animações para um determinado número de quadros e para reproduzir a nova animação sobre a antiga.

- **Shape Keys** : Semelhante às poses, você pode reproduzir as ações-chave da forma criadas no DopeSheet Editor com controle sobre a combinação, prioridade, quadros e assim por diante. Há até uma opção Continuar comum a ambos, que permite iniciar a animação quando você saiu da última vez que a ativou. Lembre-se de que você não toca as teclas de forma individual, mas sim a ação que armazena sua influência uma na outra ao longo do tempo.

- **Object Properties** : Propriedades de localização, rotação, escala, cor e físicas (amortecimento de localização e rotação, atrito anisotrópico).

- **Material** : Diffuse Color.

- **Light** : Energia, cor, distância, atenuação, tamanho do ponto e mistura do ponto.

- **Camera** : Início/fim do corte e distância focal.

##### What Cannot Be Animated <a id="What_Cannot_Be_Animated"></a>

Infelizmente, nem tudo o que podemos animar dentro do Blender pode ser animado no motor de jogo. Mais especificamente, os seguintes elementos não podem ser animados com o atuador de Ação: Drivers, Cena, Mundo, Objeto restante, Material, Câmera e propriedades de luz.

Esteja ciente de que isso pode mudar em um futuro próximo. E algumas dessas configurações se comportam de maneira diferente, dependendo do modo de renderização (GLSL, MultiTexture).

>**Animating More Elements via Scripting**
>
>Algumas configurações de cena, como Modo de sombreamento, Cursor do mouse e Separação de olhos, podem ser definidas por meio da API Python. O mesmo é válido para configurações de mundo, como Névoa, Cor de fundo, Física e Etapas máximas lógicas e FPS.

##### Object Settings <a id="Object_Settings"></a>

Se você não estiver animando uma Armature Pose ou uma ShapeKey, existem opções extras que você pode usar, conforme abaixo e destacadas na Figura 3.27.

![Action Actuator - Dynamic Object settings](../figures/Chapter3/Fig03-27.png "Action Actuator - Dynamic Object settings")

- **Force** : Se o seu objeto for Físico Dinâmico, você pode aplicar as transformações (por exemplo, localização) como uma força mecânica. Isso evita o efeito "fantasma" de objetos que se sobrepõem uns aos outros quando sua nova localização se sobrepõe. Com a força, eles simplesmente colidirão.

- **Add** : Avalie as fcurvas como valores relativos. Desta forma, você pode adicionar as transformações umas sobre as outras, ao invés de definir uma nova posição/tamanho/rotação.

- **Local** : Aplique as transformações em coordenadas locais ou mundiais.

##### Play Modes <a id="Play_Modes"></a>

O motor do jogo, por padrão, reproduz as ações do início ao fim do quadro e para. Há momentos em que você pode querer repetir a animação, reproduzi-la ao contrário ou até mesmo controlar a velocidade de reprodução de uma maneira diferente. Isso pode ser obtido alterando o tipo de reprodução do atuador Action, como você pode ver na Figura 3.28.

![Action Actuator – Play Mode](../figures/Chapter3/Fig03-28.png "Action Actuator – Play Mode")

- **Play** : Reproduz a ação do início ao fim dos quadros. Se você quiser que ele toque novamente, você deve enviar um novo sinal positivo para o atuador (por exemplo, um sensor de teclado com pulso habilitado pode ter a reprodução da animação interrompida se uma tecla continuar sendo pressionada).

- **Ping Pong** : Reproduz a animação do início ao fim. Da próxima vez, ele irá reproduzi-lo do início ao fim. Então comece para o fim e termine para começar de novo. E ping, ping, ping, pong.

- **Flipper** : Joga até você mantê-lo válido. Assim que você para com o sinal positivo (por exemplo, você solta a tecla), ele reproduz o quadro inicial. Isso acontece mesmo que a animação esteja apenas na metade dos quadros.

- **Loop Stop** : Reproduz a animação enquanto o atuador é válido. Se a animação chegar ao quadro final, ela retornará ao quadro inicial. Se o atuador não estiver mais ativo, ele para imediatamente.

- **Loop End** : Reproduz a animação continuamente indo para o quadro inicial após atingir o final. Se você interromper o sinal no meio da ação, ele se comportará como o modo Play e será reproduzido até o final do quadro.

- **Property** : Em vez de usar os quadros inicial e final, você dirige a animação por um valor de propriedade do jogo. Você pode usar qualquer número, inteiro ou não, como o valor da propriedade. Dessa forma, você pode ter reproduções bem suaves. Com essa opção, você também pode simular câmera lenta, lapso de tempo ou até mesmo criar seu próprio modo de jogo controlando a alteração da propriedade como quiser.

##### Blendin, Layers, and Priority <a id="Blendin,_Layers,_and_Priority"></a>

Se você precisa executar várias ações para o mesmo objeto, você precisa configurar suas transições e como eles irão interagir. Portanto, você precisa explorar as opções restantes na interface do atuador de ação: Blendin, Layers e Priority. O Blendin funciona como um efeito de desvanecimento cruzado entre as ações, enquanto o Layer permite que diferentes ações sejam reproduzidas ao mesmo tempo.

- **Blendin** é necessário quando você precisa alternar ações. Mais especificamente, é vital quando você deseja esmaecer suavemente de uma animação para outra. Imagine, por exemplo, que seu personagem está caminhando e depois começa a correr. Mesmo que os quadros de ambos os ciclos de animação comecem e terminem exatamente da mesma forma, o efeito será estranho. A diferença na velocidade das ações tornará a transição muito perceptível e não natural. Portanto, a menos que você esteja animando um carro antigo com alguns problemas de motor, você não quer que a transição seja tão abrupta. Portanto, você pode combinar a nova ação (por exemplo, correr) com a atual (andar). O Blendin funciona mesmo se a animação anterior não estiver mais sendo reproduzida. Observe que o Blendin só funciona entre atuadores de ação que estão nas mesmas camadas de animação.

- **Priority**irá determinar a ordem de execução de diferentes ações na mesma camada. Se você tiver duas ou mais ações em execução ao mesmo tempo, qual será executada? Isso caberá à prioridade decidir. O atuador com a prioridade mais baixa será aquele tocado (então um número de baixa prioridade é igual a uma alta prioridade de execução).

- **Layer**permite que você reproduza animações simultaneamente. Em outras palavras, você pode empilhar várias ações para serem executadas independentemente. Por exemplo, você pode ter uma camada de base para as ações do corpo e uma camada superior para as animações de rosto. Embora o corpo possa reproduzir uma animação de caminhada, o rosto pode estar reproduzindo diferentes ações inativas. Dividir ações em camadas separadas (e atuadores de ação separados) também permite a fusão gradual entre as ações.

- **Layer Weight** define a proporção de influência das camadas de animação anteriores para combinar com o atuador de ação atual.

#### Armature <a id="Armature"></a>

O atuador Action não é a única maneira de mover e controlar sua armadura. Com a ajuda de restrições ósseas, as armaduras podem realizar uma interação autônoma com outros objetos. Junto com o sensor Armature, este atuador foi originalmente criado para simulações robóticas. No entanto, esses tipos de animações de osso não preparadas / pré-feitas podem servir a vários propósitos. Para obter uma explicação adequada sobre quando isso pode ser usado e como funciona, consulte a seção iTaSC no Capítulo 4, "Animação".

E para obter mais informações, visite: [http://wiki.blender.org/index.php/Dev:Source/GameEngine/RobotIKSolver](http://wiki.blender.org/index.php/Dev:Source/ GameEngine/RobotIKSolver)

![Armature actuator](../figures/Chapter3/Fig03-29.png "Armature actuator")

Os modos do atuador são os seguintes:

- **Run Armature** : Executa a simulação nesta armadura.

- **Enable** / **Disable** : Utiliza um osso e uma restrição de osso como argumentos. Ele permite que você controle quando essa restrição específica deve ser executada.

- **Set Influence** : Define a influência de uma restrição de osso dinamicamente.

- **Set Weight** : Define o peso da influência IK em um osso.

- **Set Target** :Define os alvos para uma restrição de osso. Ao usar a restrição cinemática inversa, você também pode definir o alvo secundário (também conhecido como _alvo polar_).

>**Dynamic Constraints**
>
Este atuador só funciona para objetos de armadura. Se você deseja conduzir alguns dos parâmetros do bone (por exemplo, uma influência de restrição do bone), você precisa ter um atuador de armadura ativo com a opção "Executar armadura".
Você pode encontrar um exemplo de Set Influence with Run Armature no arquivo de amostra \Book\Chapter3\Influence\_dynamic.blend.

#### Camera <a id="Camera"></a>

O atuador da câmera moverá seu objeto (geralmente sua câmera ativa) atrás do eixo especificado (X ou Y) do objeto de câmera (consulte a Figura 3.30). A parte frontal do seu objeto é o eixo Y, porque este é o eixo usado no alinhamento final. Não vai agir imediatamente, no entanto. Quanto mais você o ativa, mais perto você se aproxima dos parâmetros especificados: Mín, Máx e Altura. Depois de atingir o alvo, seu objeto continuará "balançando", enquanto se certifica de que se mantém dentro da distância determinada pelo intervalo Mín e Máx.

![Camera actuator](../figures/Chapter3/Fig03-30.png "Camera actuator")

>**Tips**
>
>Se você deseja alterar a câmera ativa, continue procurando
>
>Se você está tentando mudar a câmera ativa da cena, por favor, olhe para o atuador de cena.

#### Constraint <a id="Constraint"></a>

O atuador de restrição assume o controle sobre a posição e orientação do objeto. Você pode usá-lo para garantir que um objeto esteja sempre próximo ao solo, o que é provavelmente a aplicação mais popular dele. Se você gosta de demos de física e jogos de ficção científica, pode usá-lo para simular um campo antigravitacional. E se você quiser fazer um bop bag? Um atuador de restrição fará isso por você. (Bem, você tem que configurá-lo.)

##### Location Constraint <a id="Location_Constraint"></a>

Com a opção Location Constraint, o atuador moverá seu objeto dentro do intervalo especificado (consulte a Figura 3.31). Não precisa acontecer imediatamente, e essa é uma das belezas disso. Você pode definir um fator de amortecimento, que determinará quantos quadros serão necessários para que o objeto fique na posição correta; isso produz resultados muito suaves.

![Constraint actuator – location](../figures/Chapter3/Fig03-31.png "Constraint actuator – location")

O Mín e Máx são coordenadas globais e podem restringir apenas um eixo de cada vez. Para travar seu objeto em uma gaiola tridimensional, você precisa de três atuadores de restrição distintos. Isso lhe dará controle total sobre a gama de posições onde seu objeto deve estar.

##### Distance <a id="Distance"></a>

A opção Restrição de distância compara e controla a distância entre seu objeto e os objetos próximos (veja a Figura 3.32). Você primeiro deve determinar qual eixo deseja usar para a verificação da distância. Se você alternar o **L** botão, o atuador usa o eixo do objeto; caso contrário, ele usa o global. O motor do jogo lançará um raio nessa direção e tentará encontrar uma superfície que tenha a propriedade do jogo ou o material especificado com a opção M / P. Ele usa o Alcance para determinar o comprimento máximo do raio lançado. Se o raio atingir uma face, as seguintes opções serão consideradas:

- **Force Distance** : Define a nova distância entre seu objeto e a superfície encontrada/atingida.

- **Damping** : O número de quadros para que o reposicionamento seja concluído.

- **N** : Ligue-o e seu objeto ficará alinhado com a superfície (normal da) encontrada/atingida.

- **RotDamping** : O número de quadros para completar a rotação do alinhamento.

![Constraint actuator – Distance](../figures/Chapter3/Fig03-32.png "Constraint actuator – Distance")

>**Until a Negative Signal Do Us Part**
>
>Este atuador estará ativo assim que for acionado e permanecerá ativo até receber um sinal negativo ou não conseguir mais encontrar uma superfície (por exemplo, o piso) na faixa fornecida. Se você deseja manter o seu atuador ativo mesmo quando ele não encontra uma superfície para ser restringido, você pode ativar a Persistência**(PER)** opção. Se o tempo for maior que zero, definirá o período máximo de ativação do atuador.

#### Orientation Constraint <a id="Orientation_Constraint"></a>

Em vez de afetar a posição do seu objeto, a opção Orientation Constraint restringirá sua rotação em eixos individuais (veja a Figura 3.33). Ele alinha o eixo especificado com a direção de referência. Por exemplo, se você quiser fazer seu saco de bop ficar reto, você pode usar Z como direção e 0, 0, 1 como direção de referência. Tal como acontece com as outras opções do atuador de restrição, você pode definir os ângulos mínimo e máximo, quadros de amortecimento e o tempo.

![Constraint actuator – Orientation](../figures/Chapter3/Fig03-33.png "Constraint actuator – Orientation")

#### Force Field Constraint <a id="Force_Field_Constraint"></a>

A restrição de campo de força simula um campo de mola sob seu objeto (consulte a Figura 3.34). O efeito é semelhante a pairar sobre a água ou flutuação simples. Os campos de força também podem ser definidos com as configurações de Física no Painel de Materiais (consulte o Capítulo 6 para obter detalhes).

![Constraint actuator - Force Field](../figures/Chapter3/Fig03-34.png "Constraint actuator - Force Field")

As opções especiais são as seguintes:

- **Force** : Força da mola do campo de força.

- **Distance** : Altura do campo de força.

- **RotFh** : Alinha o eixo do objeto com a normal do campo de força.

- **N** : Adiciona uma força horizontal (nas inclinações) do campo.

O resto das opções se comportam como as apresentadas para os outros tipos de atuador de restrição **:** Direção, M/P, PER, Tempo, Amortecimento e RotDamping.

#### Edit Object <a id="Edit_Object"></a>

Existem alguns atuadores que parecem poder ser divididos em unidades individuais. O Edit Object é certamente um deles (veja a Figura 3.35). Com este atuador, você pode adicionar mais objetos em sua cena, remover seu objeto dele, substituir sua malha, rastrear sua orientação para outro objeto ou, eventualmente, alterar algumas de suas configurações de dinâmica física. Vamos dar uma olhada neles:

![Edit Object actuator](../figures/Chapter3/Fig03-35.png "Edit Object actuator")

- **AddObject** : Se você tiver objetos em uma das camadas não visíveis, poderá adicioná-los ao jogo com esta opção. O objeto adicionado estará na posição e com a orientação do objeto que controla o atuador. A escala, no entanto, será uma combinação de ambos os objetos. Fora isso, o novo objeto é bastante autônomo [md], na verdade, a propriedade do jogo e os tijolos lógicos no novo objeto serão tão bons como se o objeto existisse desde o primeiro quadro. A única exceção são as propriedades do jogo Timer que começam a contar apenas quando o objeto é adicionado. Você pode adicionar várias instâncias do mesmo objeto, e qualquer uma delas se comportará como uma cópia duplicada independente dele.

Por meio das opções da interface, você pode alterar a velocidade linear e angular inicial do objeto e sua duração de vida.

>**For More Control Go with Python**
>
>Existem tantos aplicativos para esse recurso que é difícil restringi-los a um exemplo. Eles vão desde o preenchimento dinâmico do seu jogo até a criação de efeitos de partículas de curta duração. Você pode encontrar-se procurando por mais controle sobre os objetos adicionados, e os scripts podem resolver isso para você. Por meio da API Python, você pode acessar o objeto adicionado anteriormente, obter sua vida útil ou até mesmo substituir completamente o atuador por sua função equivalente em Python KX\_Scene.addObject ().

- **EndObject** : Dê uma olhada em seu objeto de jogo. Agora vire-se e diga tchau! Não apenas seu objeto será removido do jogo, mas também qualquer objeto filho a ele relacionado.

- **ReplaceMesh** :Se o seu objeto não for uma Armadura, uma Câmera, um Vazio, uma Lâmpada ou um Texto, ele tem uma malha anexada a ele. E se tiver uma malha, pode trocá-la por outra. Existem duas opções aqui: substituir a malha gráfica [md] aquela que você vê renderizada [md] ou substituir a malha física [md] aquela usada para interações físicas, vista com Mostrar Visualização de Física.

>**But Isn't This Slow? Not Really**
>
>Este recurso funciona muito rápido. Todas as malhas no arquivo do blender são pré-convertidas quando o jogo é iniciado. Quando o atuador é ativado, o mecanismo de jogo simplesmente troca a malha atual pela nova. Isso funciona mesmo se não houver nenhum objeto visível usando a malha que você deseja substituir ou se não houver nenhum objeto; apenas certifique-se de manter a malha viva com a opção "falso usuário".

Esta opção pode ser usada para implementar o que é conhecido como nível de detalhe: você troca a malha do seu objeto com base na distância da câmera. Depende do seu jogo em particular se o estresse extra em seu Logic e eventual script compensam o ganho no desempenho do rasterizador.

- **TrackTo:** Ao contrário do atuador da Câmera, esta opção Editar Objeto não moverá seu objeto, mas mudará sua rotação. Seu objeto funcionará como uma câmera de segurança rastreando o objeto especificado no campo Objeto. A opção de rastreamento 3D permite três graus de liberdade no objeto rastreador. Se o tempo for maior que zero, ele determinará quanto tempo dura um rastreamento antes que o atuador seja reativado. Para alterar os eixos de rastreamento, vá para as opções Extras de relações no painel Objeto.

- **Dynamics** : Rigid Body and Dynamics podem ser desativados e ativados aqui. Isso não transforma um objeto estático em um corpo rígido ou dinâmico. Ele funciona para desativar temporariamente (ou permanentemente) o comportamento físico de um. A massa do objeto também pode ser alterada aqui.

#### Message <a id="Message"></a>

Existem diferentes maneiras de coordenar ações entre diferentes objetos. Conforme apresentado anteriormente, um deles é através da ligação de blocos lógicos de objetos diferentes. Isso não é apenas confuso, mas também limitante; você só pode vincular objetos se ambos estiverem presentes no jogo (descartando objetos adicionados dinâmicos); nem você pode transmitir uma ação sobre vários objetos sem vinculá-los manualmente. Uma boa alternativa é usar o atuador Message para enviar uma mensagem para outros objetos (ou para si mesmo). Os três campos opcionais disponíveis são: Para, Assunto e Corpo. Você pode vê-los na Figura 3.36.

![Message actuator](../figures/Chapter3/Fig03-36.png "Message actuator")

Se você não sabe para qual objeto enviar a mensagem (ou deseja enviá-la para mais de um), você pode transmiti-la. Para isso, basta omitir o parâmetro To. Um sensor de mensagem [md] a outra parte da história [md] pode filtrar mensagens por assunto. O corpo só pode ser recuperado por um script Python e normalmente é deixado em branco quando você deseja apenas acionar um evento, não para passar um valor. O corpo pode ser um texto ou o valor de uma propriedade.

> **The Real Thing About Real-Time Is That It Has a Delay**
>
>Esteja ciente de que as mensagens só serão detectadas pelo sensor de Mensagem no próximo ciclo lógico. Portanto, não é um substituto completo para os blocos lógicos vinculados.

#### Motion <a id="Motion"></a>

_ "Meu corpo se move, move, meu corpo ... move!" _ [Md] hipopótamo dance / pickup line (um dos melhores momentos de _Madagascar 2_ da DreamWorks).

Ele se move, mas o faz de maneiras distintas. Por exemplo, um personagem animado usará um atuador para controlar os ossos e um atuador de movimento para controlar o movimento geral do objeto na cena [md] sua orientação e posição. Portanto, a menos que o personagem do jogo esteja fazendo um exercício de moinho de vento, sua bicicleta de caminhada precisará deste atuador. Na verdade, qualquer objeto [md] com ou sem uma ação atribuída a ele [md] pode precisar girar e se mover. Portanto, este é um dos atuadores mais importantes e amplamente utilizado para um jogo. Vamos dar uma olhada nos dois métodos disponíveis: Simple Motion e Servo Control.

>**Rotate It Just a Bit**
>
>Uma vez ativado, este atuador continuará tocando até receber um sinal negativo ou até que ele pare de receber os positivos. Portanto, se você deseja girar seu objeto alguns graus apenas ao pressionar uma tecla, deve usar a opção Toque no sensor do teclado.

##### Simple Motion <a id="Simple_Motion"></a>

A maneira mais simples de mover um objeto é alterando sua localização em uma direção específica. Você pode determinar o deslocamento no eixo X / Y / Z e no próximo quadro, seu objeto estará muito longe de sua posição original. Você pode aplicar uma rotação da mesma maneira, considerando o ângulo que deseja girar cada um dos eixos todas as vezes. Na Figura 3.37, você pode ver os barebones desse atuador.

![Motion actuator - Simple Motion](../figures/Chapter3/Fig03-37.png "Motion actuator - Simple Motion")

Mas o que acontece se o seu objeto for dinâmico? Se o objeto já está sendo controlado pelas regras da física, você também pode interagir com ele nessa instância. As configurações dinâmicas de objeto permitem que você aplique alterações físicas em seu objeto e deixe que ele reaja a elas. Em vez de deslocá-lo algumas unidades de distância, você pode empurrá-lo com alguma força em uma determinada direção. O que impedirá o objeto de se mover nessa direção para sempre? Como no mundo real, a reação de outros objetos produzirá resistência por meio de colisão de superfície (também conhecida como _fricção_). Haverá momentos em que você deseja mover seu objeto, independentemente das malhas físicas dos outros atores do jogo. Para aqueles, você ainda pode contar com as opções Loc e Rot.

![Motion actuator - Dynamic Object Settings](../figures/Chapter3/Fig03-38.png "Motion actuator - Dynamic Object Settings")

Quando seu objeto for dinâmico, você verá novas opções no atuador (consulte a Figura 3.38). Força, Torque, Velocidade Linear e Angular e Amortecimento foram explicados anteriormente. A diferença entre Força, Torque e Velocidade Linear e Angular é simples: quando você usa Força e Torque, você está adicionando o momento físico que será aplicado à massa do objeto e resultará em uma velocidade específica. Quando você configura a velocidade diretamente, você tem o mecanismo de jogo certificando-se de que o momento aplicado resultará nessa velocidade. Também existe uma opção para definir ou adicionar a velocidade linear em cima da existente e especificar os quadros de amortecimento para simular a aceleração; esse é o número de quadros que serão necessários para atingir a velocidade alvo.

>**Local and Global Again**
>
>No Blender, existem dois sistemas principais de coordenadas: Local e Global. Sempre que você se referir a um eixo, deve estar ciente do sistema que deseja usar. O padrão é sempre o Global (também conhecido como _Mundo_) e usará a referência X, Y, Z absoluta de sua cena. Quando você quiser usar o local, que é mostrado como um L na interface, o eixo usado será sempre relativo à orientação atual do seu objeto.

##### Servo Control <a id="Servo_Control"></a>

Este é um método mais complexo e completo para controlar o movimento linear do seu objeto. A opção Servo Control permite que você controle a velocidade com força. Ele aplicará uma força variável para atingir a velocidade desejada. Pode ser usado para simular os mais diversos efeitos, como fricção, voo, deslizamento, etc.

O Servo controle pode (e deve) ser usado para qualquer objeto, independentemente de suas propriedades dinâmicas / físicas (ver Figura 3.39). Ele substitui Local e Velocidade Linear da opção Movimento Simples. O resultado produzido é um movimento mais fluido e contínuo para seu objeto. Isso também não afeta o comportamento de colisão e outras interações físicas [md] em oposição ao uso de Localização no Movimento Simples. Este último faz com que o objeto "salte no espaço", ignorando o que quer que esteja entre sua posição original e final.

![Motion actuator - Servo Control](../figures/Chapter3/Fig03-39.png "Motion actuator - Servo Control")

- **Reference Object** : Albert Einstein disse uma vez que tudo é relativo. Um dos avanços de suas descobertas científicas originou-se da observação de um trem de diferentes pontos de referência (uma estação, o mesmo trem, outro trem). O Reference Object aqui funciona como tal, relativizando a nova velocidade de sua posição e velocidade.

- **Linear Velocity:** The target velocity used in the Servo Control calculation.

- **Force Limit X** , **Y** , **Z** :Ele pode controlar o mínimo e o máximo da força aplicada no objeto. A velocidade alvo será eventualmente alcançada, então esta opção funciona no sentido de acelerar ou desacelerar a aceleração.

>**Advanced Motion Control**
>
>**PID Servo Control System** : As opções a seguir o ajudam a controlar a capacidade de resposta e a reação de seu movimento. Em inglês simples, isso é conhecido como "mecanismo de loopback de controle" e é um procedimento de avaliação constante que molda as características de seu movimento.
>Este é um sistema genérico (não específico do Blender); para obter mais informações, consulte as referências externas, como: http: //en.wikipedia.org/wiki/PID \ _controller

- **Proportional Coefficient** :Você não precisa alterar esse parâmetro, a menos que saiba o que está fazendo. Ele se ajustará para ser 60 vezes o IntegralCoefficient, então se você quiser um valor diferente, lembre-se de atualizá-lo após fazer quaisquer ajustes.

- **Integral Coefficient** : The default value (0.5) will give you a fast response into the system. Values as small as 0.1 will produce very slow responses.

- **Derivate Coefficient** : This parameter is not required and has a direct effect on the stability of the movement. High values can cause instability.

##### Character Motion <a id="Character_Motion"></a>

Last and more recent is the actuator to work with character objects, which is covered in Chapter 6. This actuator will only work if the object physics type is set to Character.

As you can see in Figure 3.40, most of the options are already familiar to us. The only addition is the Jump option, used to simulate a Physic accurate jump from your character.

![Motion actuator - Character Motion](../figures/Chapter3/Fig03-40.png "Motion actuator - Character Motion")

#### Parent <a id="Parent"></a>

Dynamically setting the parent of your objects allows you to make small components behave as a unity. Think of a Rubik's Cube game as a good example of this. Every time you rotate a face of the cube, the small pieces will be linked to a different rotational axis. In terms of implementation, you will reset the parent relation of the individual pieces on every rotation. Now, thanks to the Parent actuator, you only have to worry about the face's movement as a whole, instead of the pieces individually.

![Parent actuator](../figures/Chapter3/Fig03-41.png "Parent actuator")

The ui options are presented in Figure 3.41. If the parent object shape is a compound (set in the Physics panel), you can merge the shapes with the Compound option. From an opposing standpoint, when you don't want your object to interfere with your parent physics geometry, you can check the Ghost option to make it behave as such.

>**If You Go with Physics, Don't Parent It!**
>
>Some of the physic interactions, such as Rigid Body, will behave erratically or not work at all when your object is parented.

#### Property <a id="Property"></a>

There are a few ways of changing your game properties. You can change them through a Python script, a logging option from a Logic Brick (for example, a Keyboard sensor), or by using the Property actuator (see Figure 3.42). Let's take a look at the available options.

![Property actuator](../figures/Chapter3/Fig03-42.png "Property actuator")

- **Add** : Increments or decrements of numbers can be done with this option. Remember to use the minus sign to decrease a number, although when adding a number to a String property, that number will get added to the text, regardless of its signal.

- **Assign** : This option allows you to specify a new value for your property or to copy it from another property of the same object. When your property is a String, you can enclose the new value in single or double quotes.

- **Copy** : Copy a property from a different object. See the note that follows on different data type conversions.

- **Toggle** : When the property is a Boolean, it will toggle from True to False and vice versa. When it's a number (integer, float or timer), it will toggle from 0 to 1 and anything different than 0 to 0.

>**Mixing Types**
>
>When your properties are of different types, Blender will try to accommodate them. Booleans are converted to 0 or 1 when assigned to numbers, and floats are always rounded down.


>**Remember the Expressions?**
>
>Instead of direct values, you can use an expression in the value fields for the Property actuator. Take a look at the Expression controller for more details.

#### Random <a id="Random"></a>

Controlled randomness is one of the keys for a decent AI (artificial intelligence). As you can see in Figure 3.43, the Random actuator has 10 options to generate pseudo-random numbers. They are divided by types[md]Boolean, integer, and float[md]and they use a seed for consistent results over time. A seed allows an algorithm to generate the same random numbers every time you start the interaction.

![Random actuator](../figures/Chapter3/Fig03-43.png "Random actuator")

The generated number is stored in a game property indicated in the Property field. Booleans are converted to 1 or 0 when assigned to a numerical property, and to a TRUE or FALSE text when assigned to a string property. Integers or floats are converted to False when they are zero and are assigned to a Boolean property; they are converted to True otherwise.

#### Sound <a id="Sound"></a>

Soundtracks and sound effects[md]the possibilities are endless and definitively a key aspect of your game. You will use this Sound actuator when you play a "click" sound for the UI (see Figure 3.44). You will also use it to announce steps from surrounding enemies. In fact, the opening music, the main track, and the credit sounds all are musical[md]music, music, and music. You may love music, but if they all play together at the same time, you get the cacophonic experience of an indie garage band. On the other hand, to sync the events of your game with its sounds, you can use these options: Play, Volume, Pitch, and 3D Sound.

![Sound actuator](../figures/Chapter3/Fig03-44.png "Sound actuator")

>**Spatial 3D Sound**
>
>If the sound has only a single channel, you can use it as a 3D sound source. That means the sound will be played using your game object position as reference; it gets louder the closer it gets to the camera, and lower when it's farther away. The 3D options cover the distance range of the volume influence of your sound, the audio cone extension, and its angles.

#### State <a id="State"></a>

The State machine in the game engine works like a layer system on which every controller can belong to one or more state. As with the Blender layers, you can have none, one, or multiple states active at a time. If you disable a state, you will disable the Logic Bricks that are exclusively linked to this state's controllers. You need a way to change the active states and that's what the State actuator is for (see Figure 3.45).

![State actuator](../figures/Chapter3/Fig03-45.png "State actuator")

- **SetState** : Replace the current state mask entirely with the one supplied.

- **AddState** , **RemoveState** : Act on individual states by adding/removing the select ones.

- **ChangeState** : Toggle the selected states reversing their values.

>**States Continued…**
>
>Read more about how to use the states in the "State Machine" section, later in this chapter.

#### Visibility <a id="Visibility"></a>

In the Physics buttons, you can choose the initial visibility of your object and whether or not it's an occluder object. The Visibility actuator allows you to change those properties dynamically during the game, as shown in Figure 3.46. The extra option, Children, replicates the visibility and occlusion recursively for all its children objects.

![Visibility actuator](../figures/Chapter3/Fig03-46.png "Visibility actuator")

#### Scene <a id="Scene"></a>

While most of the actuators act on top of the object, the following actuators[md]Scene, Filter 2D, and the Game actuator[md]work globally, either per scene or per game.

Multiple scenes are a common way to make a user interface (overlay scene), handle different levels (although that can be accomplished with multiple blender files as well), or even preload your game assets in the memory (adding scenes and suspending them before effectively switching between scenes). See Figure 3.47.

![Scene actuator](../figures/Chapter3/Fig03-47.png "Scene actuator")

Multiple scenes are rendered as a stack, the ones in the back first, followed by the ones on top. The Scene actuator allows you to restart your scene, change the current one, add overlay and background scenes, suspend, resume, and remove them.

Also, you can change the current camera of the scene by assigning a new camera object in the Set Camera option.

>**Freeze! New Scene!**
>
>Every time a new scene is set or added, the game engine has to convert all the assets into its internal objects. This is the same process that occurs for your main scene when you first load up your game. Since the game engine is single threaded for most of its operations, the whole game will freeze waiting for the new scene to load.

#### Filter 2D <a id="Filter_2D"></a>

The 2D Filter actuators are post-processing effects applied to the entire screen (see Figure 3.48). They are similar to what can be done with the Composite Nodes in Blender or the filter effects from a graphics software program such as GIMP or Photoshop.

![Filter 2D actuator](../figures/Chapter3/Fig03-48.png "Filter 2D actuator")

>**Old Graphic Cards Support**
>
>Filters 2D require graphic cards with support for GLSL (officially included in OpenGL 2.0 or higher). Otherwise, they will not run and may crash Blender in some cases. Most of today's computers do support it, but you may have trouble running it in some old embedded graphic cards. When not supported, you will see an error report in the Blender console, and it can eventually lead to crashes on Blender. There is no harm for your system, though, so you if you are not sure of the compatibility of your graphic card, you can go ahead and try it.

You may be already familiar with most of the built-in filters. They have similar implementation to traditional filters found in any digital processing software:

- **Blur** : It smudges the whole canvas. Neighboring pixels are blended together, thus existent small details are eventually lost.

- **Sharpen** : It's the opposite of Blur. The details will jump out of the screen becoming crystal clear.

- **Dilation** : While Blur averages neighboring pixels, Dilation will pick the brightest (maximum RGB value) one of the surrounding pixels and use it as the pixel color. The result is a sharper image but with a loss of details; however, it's a good compromise between Blur and Sharpen.

- **Erosion** : It works opposite to the Dilation method. This filter compares the values of all the neighboring pixels and uses the darker (minimum RGB value) one as the pixel color.

- **Laplacian** : This was originally conceived as an edge detection filter. It will produce dark regions where there are not many changes of color and bright zones when the color changes abruptly.

- **Sobel** : This is another simple edge detection formula that detects the spatial frequency of high changes in the image. It will produce images of high contrast with white lines against a solid dark background.

- **Prewitt** : Similar to the Sobel algorithm, this filter also handles edge detection. The difference is that the Prewitt algorithm is more sensitive to vertical and horizontal edges. The Sobel, on the other hand, is isotropic; it's not biased for any particular set of directions.

- **Gray Scale** : This filter discards the color information of your image, keeping the same luminance.

- **Sepia** : This simulates a photography technique to give a warmer tone for a photo and make it last longer. This effect can set an interesting mood for flashbacks or past scenes in your game. The Sepia effect is reached by first converting the image into grayscale and then mixing it with a bright, desaturated yellow.

- **Invert** : Makes a negative of the frame image. What is white becomes black, what is pure red is converter to cyan, and so on. The inversion is made on top of the RGB values of your scene (instead of the HSV, for example).

A filter can be applied on top of another one. In order to combine more than one filter, the filters have to run in a controlled order; otherwise, the effects may vary a lot. To run in the correct order, each Filter 2D Actuator has a Pass Number **,** which will determine which runs first by an ascending order.

There are two extra filters that complement the usage of the other ones:

- **Custom filter** : This is a more advanced option that allows you to write your own filters for your game (see Figure 3.49). There are interesting effects that can be implemented: depth of field, screen-space ambient occlusion, high dynamic range, color balance, vignetting, noise, and so on

![Filter 2D actuator - Custom filter](../figures/Chapter3/Fig03-49.png "Filter 2D actuator - Custom filter")

It's still important to be aware of the Pass Number, just as for the other filters. The Custom Filter can be mixed with the others with no problems. Finally, you can select a Text datablock to use as the filter source. The filter is actually a GLSL shader, which is a whole topic on its own. Chapter 5 covers that in depth along with other graphic topics.

- **Motion Blur** : In a video camera, fast objects appear to be blurred the faster they go. It's quite a popular effect and even in real-time rendering, it can be simulated in an artistic way (a euphemism for a trade-off between quality and performance with tons of compromise).

This filter has its own option to be enabled and disabled. As you can see in Figure 3.50, there is no Pass Number there. The reason is that Motion Blur is always computed before the other filters. Therefore, it will run prior to the first of your filters. You can set the Value to adjust the sensitivity and general effect of the blur[md]small values will produce very little blur.

![Filter 2D actuator - Motion Blur](../figures/Chapter3/Fig03-50.png "Filter 2D actuator - Motion Blur")

##### Enable, Disable, Remove <a id="Enable,_Disable,_Remove"></a>

You can run a Filter 2D just like any other actuator. A positive signal will trigger it once, and the filter will run. However, the filter will keep running, even if the sensor sends some negative signals.

If you want to turn a filter temporally off, you can use the Disable option. To reactivate the filter, you use Enable. If, however, you know that you will no longer need this filter during the game, you should use Remove to remove it instead. For any of these three options, you have to set the Pass Number of the filter you want to deal with.

>**Why Does Filter 2D Not Follow the Rest of the Actuators' Behavior?**
>
>Although it may sound arbitrary, there is a reason behind the enable/disable design of the Filter 2D system. The filters are actually shaders, small programs that must be sent to the graphic card for them to be compiled and accessible to the game. To avoid the overhead of recompiling the shaders every time you call them, the game engine keeps them in its memory from the first moment you enable them until you finish the game, remove the filter, or remove the scene where the filter belongs._To remove the object that called the Filter 2D will not make the filter stop running._

#### Game <a id="Game"></a>

The Game actuator concentrates on top-level functions you can perform on each game. Its options are Start, Restart, and Quit this game, Load and Save GameLogic.globalDict, as shown in Figure 3.51.

![Game actuator](../figures/Chapter3/Fig03-51.png "Game actuator")

Start Game From File will stop the game and start/load the new file. It's used to load new levels or simply to access files with new scenes. Blender will go through the whole process of loading a new file and converting the data. That may produce some waiting time where the whole game (shaders included) seems to be frozen. All the events that happened in the game will be lost with the following exceptions:

- **Global dictionary:** The python dictionary bge.logic.globalDict (explained properly in Chapter 7) is persistent through all your gameplay.

- **Material settings:** If you change the material render mode from Multitexture to GLSL, for example, it will only be valid for the new file you load. This is very useful for loading files that help you to set up the graphic property according to the user profile.

Restart Game will load the opened file again. Since it loads the saved file, any changes made before launching the game engine will not be present.

Quit Game works the same way as if the exit key is pressed (ESC key is the default, this can be changed in the render panel). When combined with the proper sensor and controllers, this option allows the user to quit the game by clicking in a button in the game, for example.

Load and Save bge.logic.globalDict is only relevant if you are using Python scripts. Once you save the global dictionary, it will create a file in the same folder as your blend file with the extension .bgeconf.

>**Please Wait While Loads…**
>
>If the initial scene of your game is too heavy, you may consider implementing a simpler initial scene/file with the game credits, title, and a "please wait while loads" message. This scene will then have an Always sensor linked to a Game actuator set to Start Game From File.

## State Machine <a id="State_Machine"></a>

_"Why did the controller cross the road?[md]to get to the next state."_

A state is a conjunct of actions to be performed by a game character. In our case, it's a set of sensors, controllers, and actuators that together represent a subset of the possible behavior the character will present. Let's say it in a simple way.

Pretend we are creating a triathlon sport game. The triathlete will be able to swim, bike, and run during the course of the game. A real athlete doesn't stop to switch modalities and neither does ours. Therefore, we need to make sure the game inputs (for example, keyboard sensors, collision detection, and so on) will result in different actions and interactions for each modality (for example, diving, jumping, crashing, and so on ). The other thing we must consider is the transition of the states. In our example, each modality/state is exclusive and sequential; they can't happen simultaneously and have a specific order to follow. The player will start swimming, then biking, and finally running. Although they are independent states, they can (and likely will) share sensors and eventually actuators. In Figure 3.52, you can see a pseudo Logic Bricks arrangement for the initial settings of all three modalities. As you can see, the same sensor is linked to different controllers, each one in a respective state and calling different actuators.

![Initial settings of the triathlon state system](../figures/Chapter3/Fig03-52.png "Initial settings of the triathlon state system")

Although all the controllers and actuators are visible, the state 1 (Swim) is the only one that is part of the initial states. Therefore, any controllers from other states (for example, Bike and Run) will be disabled when the game starts. Indeed, sensors and actuators will only be active if the controller they are linked to are currently active. In our pseudo Logic Bricks, the actuator set to make the player float[md]a Location Constraint Actuator[md]will be disabled automatically once the state one (for example, Swim) is demoted.

This is the simplest way of using states. It's not the only one, though. In more complex systems, the states don't need to be exclusive and will work more as individual components that you can turn on and off accordingly. One of the important aspects of this system is that from a controller of any state, you can completely rearrange the status of all the other states, turning them on or off.

>**Artificial Intelligence and the State Machine**
>
>In the artificial intelligence literature, there are multiple techniques to deal with artificial behavior. The State Machine implementation in Blender is flexible enough to be used with your design, whatever you pick. Two of the most popular systems[md]Finite State Machine and Behavior Tree[md]can be implemented with the current features and the other variations might as well. The State system can also be accessed through the Python interface for a pure programming control.

## Sharing and Group Instancing <a id="Sharing_and_Group_Instancing"></a>

The game engine centralizes the logic components at the object level. This is at the same time a curse and a blessing. On the positive side of things, you can set up each object as a unique, independent participant of your game. The down side comes when you need to reproduce a behavior, and when the last thing you need is unique objects. Sure, you can copy over Logic Bricks and properties, but this is hard to maintain and doesn't scale well for more complex files. Note that we are not talking about duplicated objects[md]those indeed share the same Logic Brick. We are looking at game objects that have different individual components but need to share part of each other's functionality. We need a compromise between both systems, and this is possible with group instancing and Logic Bricks cross-linking.

Group instancing support in the game engine was added for the project Yo Frankie[md]a game demo project organized and developed by the Blender Foundation in 2008. For this particular project, they had to share the Logic Bricks between the NPC enemies (sheeps, rats, etc.) and a different set of Logic Bricks for the two main playable characters (Frankie and Momo).

>**To Read More…**
>
>To read about their specific implementation you can look at Campbell Barton's chapter in _The Blender GameKit, 2nd_Edition_: http://wiki.blender.org/index.php/Doc:2.4/Books/GameKit\_2/12.Yo\_Frankie!#Logic\_Sharing.

The first and simplest usage of this feature is to replicate the same set of objects multiple times. Open the file _\Book\Chapter3\group\_instancing\_logic\_1.blend_. As you can see in Figure 3.53, here we have 10 copies of a system compound of balls and fountains. The balls will constantly roll inside the fountain and every once in a while the ball will get more of an impulse at the bottom of the fountain.

![Group Instance first example](../figures/Chapter3/Fig03-53.png "Group Instance first example")

There are three relevant components here: a fountain for the ball to roll in, a ball, and an invisible plane in the bottom of the fountain set to send the balls up when they collide. Since we want the objects to be alike, what we need to do is to group the three elements together and hide them in one of the non-visible layers. Now in our main layer, we can use the Add Menu (Shift+A) and select the newly created group in the Group Instance option. Figure 3.54 shows the option to be selected there.

![Add Menu - Group Instance](../figures/Chapter3/Fig03-54.png "Add Menu - Group Instance")

>**Logic Brick Duplication**
>
>There are other ways to duplicate your Logic Brick object. In fact, the Group Instance option from the Add Menu is simply a shortcut for using an Empty with Group as the Duplication type. Vertices and Faces can also be used there, but this will only duplicate the child object in the geometry, not an entire group.

The most obvious advantage of this is that if you need to change the Logic Bricks, you can at any time edit them in the original elements of the group. This will automatically be replicated to all the instances that share the same Logic Bricks. Group Instance also works for dynamically added objects. In other words, you can add a Group Instance by placing it in the file (as the previous example shows) or by using the Add Object option of the Edit Object actuator.

Now that you understand how Group Instancing works, let's go a step further and see a more advanced (yet still simple) example of sharing Logic Bricks. Please open the file _\Book\Chapter3\group\_instancing\_logic\_2.blend_. In the first example, we were duplicating the same group, but here we have two different groups: Pyramid and Orbit. Both groups share one common object, the DummyMesh, and have a unique object on their own.

Now look closely at the Logic Bricks in Figure 3.55. The sensor and the controller are in the DummyMesh, while the actuators are in the Pyramid and the Orbit objects. This way, a Group Instance that contains the DummyMesh and either the Pyramid or the Orbit will share similarities, allowing for individual effects on top of them. In this example, if you press the spacebar, the Pyramid rotates while the Orbit runs away from the camera.

![Group Instance - second example](../figures/Chapter3/Fig03-55.png "Group Instance - second example")

## To the Infinite and Beyond <a id="To_the_Infinite_and_Beyond"></a>

Now that we have gone over the various possibilities with Logic Bricks, it's time for you to put these skills into practice. Try the sample files and play with them. Rip them apart, disassemble them, and combine them. It's important to look at them creatively and use their diversity and flexibility in your favor.

In the past few years, there have been community organized game engine contests. One of the categories is specifically Logic Bricks-only games. It's really interesting to see what can be done without a single line of code. An online search for "Blender Game Engine Contest" should give you enough inspiration for further experimentation.

Actually, even if you are planning to use Python over plain Logic Bricks, it's important to understand both systems and how they work together. In the end, which tools you use will depend on the project you are working on, your team, and your workflow.

Finally, in one way or another, the next chapters all relate back to this one. You might review some parts of this chapter while learning the game engine aspects of animation, graphics, physics, constraints, and Python.
