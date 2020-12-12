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

Sometimes logic switches don't give you enough control to evaluate your sensors. You may want to compare the value of more than one property at once, or maybe even to check for specific arranges in your sensors, calling the actuator only when some sensors are positive and others negative. Or why not (it's your game after all) do all of this together? As you have guessed, expressions can handle all of those situations and a few others.

Before going into all of the options, let's first take a look at some examples:

First case: We want to eliminate your player when the energy is zero, and there are no lives left. So we create two game properties, named "energy" and "life," and control them with the expression:

energy<=0 AND life==0

Simple, right? But what if you want to finish the game when you type "quit"? Now you need a keyboard sensor with all keys logged to a text property. The expression would be:

text=="quit\n"

>**End of Line**
>
>Here we are using \n to identify a Return (Enter) right after the word. You can see this last technique combined with other actuators and different objects on: _\Book\Chapter3\controller\_expression.blend._
>This is especially powerful for quick prototyping and debugging of your game.


Expressions tend to be as simple as the examples presented. They can grow big, however, and the following parts will show how to combine simple expressions to create more advanced controllers. Keep in mind that expressions are actually used also in the Property sensor and Property actuator. The difference is that for them the result will be directly used as the property value. Therefore, there you will use mostly Values and Arithmetic Operations. For the Expression controller, the expected value is always a Boolean, so you end up using Comparison Test and the Boolean Operations more often.

>**Error Checkpoint**
>
>Always check the console for errors. If the expression is incorrect, the game engine will print an error when you call the controller.

#### Values <a id="Values"></a>

The simplest expression contains no more than a single value. If you want to check if a Boolean property is true, you only need to use its name as a value:

my\_property\_that\_may\_be\_true

For the Controller Expression, you will only use the lonely value when dealing with Booleans; however, for the Property sensor, Property actuator and as part of big expressions, you can also use the following types as values:

- **Boolean** : True, False

- **Number** : 5, [ms]7, 3.5, 40, 3.5[md]integers and floats, positive, negative, and even zero.

- **String** : "text"[md]always around quotation marks.

- **Property** : propertyName[md]gives the property value.

- **Sensor** : sensorName[md]gives True or False according to the sensor status.


A single value is not exactly an expression. Let's move on and see what kind of expressions and operations we can make when combining them together:

>**Sensors in an Expression**
>
>In order to use a sensor name, the sensor has to be linked to the Expression controller. Sensors can't be used in the expressions for the Property sensor and the Property actuator.

#### Comparison Tests <a id="Comparison"></a>

If instead of testing a single variable, you need to compare two values, there are five different comparison tests you can use. The test can be between a variable (property or sensor) and a value, two values, or two variables:

- **Equal** : fruit = "jabuticaba"

- **Greater** : 2.5 > 2.49

- **Lesser** : energy < 37

- **Greater or Equal** : speed >= 100.0

- **Lesser or Equal** : timer <= 2011

The result of a comparison test will always be a Boolean. If you need to return a value other than True or False, then what you are looking for is:

**Condition Statement** : IF (frame < 0, [ms]1, 0)

The syntax is: IF (Condition, ValueWhenTrue, ValueWhenFalse). If you use the above expression as a value for the Add mode in a Property actuator, it will decrease the counter (for example, frame) if the value is greater than zero.

#### Arithmetic Operations <a id="Arithmetic_Operations"></a>

If your value is numeric, you can also manipulate it a bit. This can be used to assign a value based on a variable (for example, speed \* time) or as part of a test (for example, energy + potion > 0). The most basic math operations are supported to operate your value, for the records:

- **Addition** : 1 + 3.8

- **Subtraction** : 10.5 - 5

- **Multiplication** : 23 \* 1000

- **Division** : 37 / 400

- **Modulus** : 10 % 3

#### Boolean Operations <a id="Boolean_Operations"></a>

Finally, you have the capability of combining Boolean tests together. A Boolean test can be a simple Boolean value (for example, a sensor or a property value) or the result of a comparison test. They work as aggregators through which you can compile big expression tests.

- **And** : potionKeyboardSensor AND numberPotions > 0 AND energy + 30 < 60

- **Or** : speed <= 0.0 OR stopKeyboardSensor

- **Not** : jumpKeyboardSensor AND NOT floorCollisionSensor

The Boolean operations are not commutative or associative when grouped together. For example, try to read the following expressions:

1 = 2 AND 3 > 4 OR 5<6

False AND False OR True

They are intentionally ambiguous. Are we testing the AND or the OR first? In order to solve this issue, you can use parentheses to isolate your expressions. The previous expressions are evaluated as:

(1 = 2 AND 3 > 4) OR 5 < 6

(False AND False) OR True

Those expressions will result in true (false or true = true). If the expected result was false, we should have grouped it as:

1 = 2 AND (3 > 4 OR 5 < 6)

False AND (False OR True)

You can find an elegant use of the Boolean operators to create a toggle mechanism on: _\Book\Chapter3\controller\_expression\_toggle.blend._

>**Fake Flipper Animation with Expressions**
>
>In the accompanying material, you can see a simulation of the Flipper animation mode implemented using the Property mode instead. This is done in two different ways: one with a Expression controller, and another with a Nand and And controllers and an Expression in a Property actuator. It shows the flexibility of the system and is a nice way to regulate the speed of your animation: _\Book\Chapter3\controller\_expression\_flipper.blend_ .

#### Python Controller <a id="Python_Controller"></a>

With a Python controller, you can evaluate sensors and activate actuators just as you would do with the other controllers. You can indeed replace any of the tests (logical switches or expressions) by an equivalent in Python. Actually, not only can the other controllers be replaced by this, but also most of your Logic Bricks as well. Chapter 7 is entirely dedicated to how and when to use this controller. Even if you are not into programming, we recommend you read the introduction sections of this chapter to understand its differences and advantages.

There are two types of Python controllers: Script and Module.

- **Script** : This will take an internal Text datablock and run it as a script.

- **Module** : This will call a module from a script file inside or outside your game file. The Module mode has a Debug option that forces the module to be recompiled every time you call it. This is really slow, but allows you to do changes in your script while your game is playing.

>**Which Came First, the Controller or the Controller?**
>
>For scripts, the order in which the controllers is executed matters. In cases where you need a script to run before the others, you can use the Mark option present in the Controller header. This is commonly used for Python controllers running scripts that are responsible for the initialization of your game variables and settings.

### Actuators <a id="Actuators"></a>

Last, but not least, there are the actuators. The trouble you've taken setting up sensors, controllers, and noodle linking will finally pay off. The actuators are grouped per themes (scene, game, object, actions, and so on), and their names and applications may surprise you. (For example, did you know the Camera actuator doesn't have to be used by a camera object?) We recommend that you familiarize yourself with all the options and sub-options and experiment with them as much as you can. While some effects work by themselves (for example, the game actuator), some will be more useful when combined together (for example, motion and action actuators). Have fun!

#### Header <a id="Header"></a>

The header of the actuators is similar to the sensors. Like the sensors, the Name is an essential element when using the actuator with a Python controller. In Figure 3.25, you can also see the Pin, a special option available to be used with controller states.

![Actuator header](../figures/Chapter3/Fig03-25.png "Actuator header")

- **Name** : This can be used to identify your actuator, even when it's not expanded. It's also used from Python scripts to activate it.

- **Pin** : When working with the State Machine system, you can use the State option on top of the actuator list to show only the actuators linked to controllers from visible states. With the Pin option in the actuator header, you can set your actuator to be always visible.

#### Action <a id="Action"></a>

Camera, lights, action! And let the animation begin. Whether you want to animate your Armature or you want to play a pre-recorded Action, you will end up using this actuator. An action can contain different F-Curves, controlling various object properties. If you split your property curves in different actions, you can control them one at a time. For example, leave Size and ObColor in the same action, and you can have a banana that is green when it's still small and turns yellow while growing.

You can also have the same property present in multiple actions and use individual actions to store different animations.

>**Short Actions in the Long Run**
>
>Before the animation system redesign in Blender, it was only possible to have multiple actions for armatures and shape keys. Therefore, for any other animated action, people would create one really long action with different animations in different frame ranges. This still works well, but it's hard to manage if you ever need to change the length of one of the animations[md]you would have to update the start and end of all the actuators that were playing the other subanimations. You may find yourself still using this technique in order to organize your file; however, sometimes a long action can be easier to manage than multiple small ones.

The actuator will let you pick an action, set the frame range, and configure how you want to play it (see Figure 3.26). If you are planning to reuse this actuator[md]for example, for linked/shared Logic Bricks[md]you can leave the action blank and set it through the Python API during the game engine. In Chapter 4, "Animation," we will use this actuator in a series of tutorials.

![Action actuator](../figures/Chapter3/Fig03-26.png "Action actuator")

##### What Can Be Animated <a id="What_Can_Be_Animated"></a>

Some of the animations you create in Blender can be used in the game engine. The same result you see in the viewport when you play them back with Alt+A, you can also get in the game engine. That includes armature poses, shape keys, and some of the properties of object, material, light, and camera as following:

- **Pose** : Any recorded sequence in an Armature object can be played. It's common to have different animated cycles[md]walking, running, jumping, tired walking, taking a break[md]and to alternate between them during an event. When using multiple action actuators, you may have an action currently playing when you start a new one. To make the transition smoothly, you can set the Blend In and Priority to respectively blend the animations for a certain number of frames and to play the new animation on top of the old one.

- **Shape Keys** : Similar to poses, you can play the shape key actions created in the DopeSheet Editor with control over the blending, priority, frames, and so on. There is even a Continue option common to both that allows you to start the animation when you left the last time you activated it. Remember that you don't play the individual shape keys but rather the action that stores their influence on each other over time.

- **Object Properties** : Location, Rotation, Scale, Color, and Physics properties (Location and Rotation Damping, Anisotropic Friction).

- **Material** : Diffuse Color.

- **Light** : Energy, Color, Distance, Attenuation, Spot Size and Spot Blend.

- **Camera** : Start/End Clipping and Focal Length.

##### What Cannot Be Animated <a id="What_Cannot_Be_Animated"></a>

Unfortunately, not everything we can animate inside Blender can be animated in the game engine. More specifically, the following elements can't be animated with the Action actuator:Drivers, Scene, World, remaining Object, Material, Camera, and Light properties.

Be aware that this may change in the near future. And some of these settings behave differently, depending on the render mode (GLSL, MultiTexture).

>**Animating More Elements via Scripting**
>
>Some Scene settings, such as Shading Mode, Mouse Cursor, and Eye Separation, can be set through the Python API. The same is valid for World settings, such as Mist, Background Color, Physics and Logic Maximum Steps, and FPS.

##### Object Settings <a id="Object_Settings"></a>

If you are not animating an Armature Pose or a ShapeKey, there are extra options you can use, as below and highlighted in Figure 3.27.

![Action Actuator - Dynamic Object settings](../figures/Chapter3/Fig03-27.png "Action Actuator - Dynamic Object settings")

- **Force** : If your object is Physical Dynamic, you can apply the transformations (for example, location) as a mechanical force. This avoids the "ghost" effect of having objects trespassing each other when their new location overlaps. With force, they will simply collide.

- **Add** : Evaluate the fcurves as relative values. This way you can add the transformations on top of each other, instead of setting a new position/size/rotation.

- **Local** : Apply the transformations in local or world coordinates.

##### Play Modes <a id="Play_Modes"></a>

The game engine, by default, plays the actions from the start to the end frame, and stop. There are times where you may want to loop the animation, play it backward, or even control the playback speed in a different way. This can be achieved by changing the Action actuator playback type, as you can see in Figure 3.28.

![Action Actuator – Play Mode](../figures/Chapter3/Fig03-28.png "Action Actuator – Play Mode")

- **Play** : Plays the action from start to end frames. If you want it to play again, you have to send a new positive signal to the actuator (for example, a Keyboard sensor with Pulse enabled can have the animation playing interruptedly if a key keeps being pressed).

- **Ping Pong** : Plays the animation from start to end. Next time, it will play it from end to start. Then start to end, and end to start again. And ping, ping, ping, pong.

- **Flipper** : Plays it until you keep it valid. As soon as you stop with the positive signal (for example, you release the key), it plays back to the initial frame. This happens even if the animation was only halfway through the frames.

- **Loop Stop** : Plays the animation while the actuator is valid. If the animation gets to the final frame, it loops back to the start frame. If the actuator is no longer active, it stops right away.

- **Loop End** : Plays the animation continuously going to the initial frame after reaching the final one. If you interrupt the signal in the middle of the action, it will behave like the Play mode and play it all the way until the end frame.

- **Property** : Instead of using a start and final frames, you drive the animation by a game property value. You can use any number, integer or not, as the property value. That way, you can have pretty smooth playbacks. With this option, you can also simulate slow-motion, time-lapse, or even create your own Play mode by controlling the property change as you will.

##### Blendin, Layers, and Priority <a id="Blendin,_Layers,_and_Priority"></a>

If you need to play multiple actions for the same object, you need to configure their transitions and how they will interact. So you need to explore the remaining options in the Action actuator interface: Blendin, Layers, and Priority. Blendin works as a cross fading effect between actions, while Layer allows to have different actions playing at the same time.

- **Blendin** is necessary when you need to switch actions. More specifically, it's vital when you want to smoothly fade from one animation to another. Imagine, for example, that your character is walking and then starts to run. Even if the frames of both animation cycles start and end exactly alike, the effect will be strange. The difference in speed of the actions will make the transition too noticeable and unnatural. Thus, unless you are animating an old car with some engine problems, you don't want the transition to be so abrupt. Therefore, you can Blendin the new action (for example, to run) within the current one (to walk). Blendin works even if the old animation is no longer playing. Note that Blendin only works between Action actuators that are in the same animation Layers.

- **Priority** will determine the execution order of different actions in the same layer. If you have two or more actions playing at the same time, which one will be played? This will be up to the priority to decide. The actuator with the lowest priority will be the one played (so a low priority number equals a high execution priority).

- **Layer** allows you to have concurrently playing animations. In other words, you can stack multiple actions to be played independently. For example, you can have a base layer for the body actions and a top layer for the face animations. While the body can be playing a walking animation, the face can be playing different idle actions. Splitting actions in separate layers (and separate Action actuators) also allows for gradual blending between the actions.

- **Layer Weight** sets the ratio of influence of the previous animation layers to blend into the current Action actuator.

#### Armature <a id="Armature"></a>

The Action actuator is not the only way of moving and controlling your armature. With the help of bone constraints, armatures can perform autonomous interacting with other objects. Together with the Armature sensor, this actuator was originally created for robotic simulations. Nevertheless, these kinds of non-baked/pre-done bone animations can serve multiple purposes. For a proper explanation on when this can be used and how it works, please refer to the iTaSC section in Chapter 4, "Animation."

And for more information, please visit: [http://wiki.blender.org/index.php/Dev:Source/GameEngine/RobotIKSolver](http://wiki.blender.org/index.php/Dev:Source/GameEngine/RobotIKSolver)

![Armature actuator](../figures/Chapter3/Fig03-29.png "Armature actuator")

The actuator modes are the following:

- **Run Armature** : Runs the simulation in this armature.

- **Enable** / **Disable** : Takes a bone and a bone constraint as arguments. It allows you to control when this particular constraint should run.

- **Set Influence** : Sets the influence of a bone constraint dynamically.

- **Set Weight** : Sets the weight of the IK influence in a bone.

- **Set Target** : Sets the targets for a bone constraint. When using the Inverse KinematicConstraint, you can also set the Secondary Target (also known as _polar target_).

>**Dynamic Constraints**
>
This actuator only works for Armature objects. If you want to drive some of the bone parameters (for example a bone constraint influence), you need to have an active Armature actuator with the "Run Armature" option.
You can find an example of Set Influence with Run Armature in the sample file \Book\Chapter3\influence\_dynamic.blend.

#### Camera <a id="Camera"></a>

The Camera actuator will move your object (usually your active camera) behind the specified axis (X or Y) of the camera object (see Figure 3.30). The front part of your object is its Y axis, because this is the one used in the final alignment. It will not act right away, though. The more you activate it, the closer you get from the specified parameters: Min, Max, and Height. After reaching the target, your object will keep "bobbing," while making sure it keeps itself inside the distance determined by the Min and Max range.

![Camera actuator](../figures/Chapter3/Fig03-30.png "Camera actuator")

>**Tips**
>
>If You Are Looking to Change the Active Camera, Keep Looking
>
>If you are trying to change the active camera of the scene, please look at the Scene actuator.

#### Constraint <a id="Constraint"></a>

The Constraint actuator takes control over your object position and orientation. You can use it to make sure that an object is always close to the ground, which is probably the most popular application of it. If you are into physics demos and sci-fi games, you might use it to simulate an anti-gravitational field. What if you want to make a bop bag? A Constraint actuator will make it for you. (Well, you do have to set it up.)

##### Location Constraint <a id="Location_Constraint"></a>

With the Location Constraint option, the actuator will move your object inside the specified range (see Figure 3.31). It doesn't have to happen right away, and this is one of the beauties of it. You can set a Damping factor, which will determine how many frames it will take for the object to get in the right position; this produces very smooth results.

![Constraint actuator – location](../figures/Chapter3/Fig03-31.png "Constraint actuator – location")

The Min and Max are global coordinates and can only restrict one axis at a time. To lock your object into a three-dimensional cage, you need three distinct Constraint actuators. This will give you full control over the range of positions where your object should be.

##### Distance <a id="Distance"></a>

The Distance Constraint option compares and controls the distance between your object and nearby objects (see Figure 3.32). You first have to determine which axis you want to use for the distance check. If you toggle the **L** button, the actuator uses the object axis; otherwise, it uses the global one. The game engine will cast a ray in that direction and try to find a surface that has the game property or the material specified with the M/P option. It uses the Range to determine the maximum length of the casted ray. If the ray hits a face, the following options will be considered:

- **Force Distance** : Sets the new distance between your object and the found/hit surface.

- **Damping** : The number of frames for the repositioning to be complete.

- **N** : Turn it on, and your object will be aligned with the (normal of the) found/hit surface.

- **RotDamping** : The number of frames to complete the alignment rotation.

![Constraint actuator – Distance](../figures/Chapter3/Fig03-32.png "Constraint actuator – Distance")

>**Until a Negative Signal Do Us Part**
>
>This actuator will be active as soon as it is triggered and will remain active until it receives a negative signal or can no longer find a surface (for example, the floor) in the given range. If you want to keep your actuator active even when it doesn't find a surface to be constrained to, you can turn on the Persistency **(PER)** option. If Time is greater than zero, it will set the maximum activation period of the actuator.

#### Orientation Constraint <a id="Orientation_Constraint"></a>

Instead of affecting your object's position, the Orientation Constraint option will restrict its rotation on individual axes (see Figure 3.33). It aligns the specified axis with the reference direction. For example, if you want to make your bop bag stay straight, you can use Z as Direction and 0, 0, 1 as the Referencedirection. As with the other Constraint Actuator options, you can set Min and Max angles, Damping frames, and the Time.

![Constraint actuator – Orientation](../figures/Chapter3/Fig03-33.png "Constraint actuator – Orientation")

#### Force Field Constraint <a id="Force_Field_Constraint"></a>

The Force Field Constraint simulates a spring field underneath your object (see Figure 3.34). The effect is similar to hovering above water or simple buoyancy. Force fields can also be set with the Physics settings in the Material Panel (see Chapter 6 for details).

![Constraint actuator - Force Field](../figures/Chapter3/Fig03-34.png "Constraint actuator - Force Field")

The special options are the following:

- **Force** : Spring force of the force field.

- **Distance** : Height of the force field.

- **RotFh** : Aligns the object axis with the normal of the force field.

- **N** : Adds a horizontal force to (the slopes of) the field.

The rest of the options behave as the ones presented for the other Constraint actuator types **:** Direction, M/P, PER, Time, Damping, and RotDamping.

#### Edit Object <a id="Edit_Object"></a>

There are a few actuators that feel as if they could be split into individual ones. The Edit Object is certainly one of them (see Figure 3.35). With this actuator, you can add more objects into your scene, remove your object out of it, replace its mesh, track its orientation to another object, or eventually alter some of its physics dynamics settings. Let's take a look at them:

![Edit Object actuator](../figures/Chapter3/Fig03-35.png "Edit Object actuator")

- **AddObject** : If you have objects in one of the non-visible layers, you can add them into the game with this option. The added object will be at the position and with the orientation of the object controlling the actuator. The scale, however, will be a combination of both objects. Other than that, the new object is pretty much autonomous[md]actually game property and logic bricks in the new object will be as good as if the object existed since frame one. The only exception is the Timer game properties that start counting only when the object gets added. You can add multiple instances of the same object, and any of them will behave as an independent duplicated copy of it.

Through the options in the interface, you can change the initial linear and angular velocity of the object and its life duration.

>**For More Control Go with Python**
>
>There are so many applications for this feature that it is hard to narrow them down to one example. They run from dynamically populating your game to creating short duration particle effects. You may find yourself looking for more control over added objects, and scripting may address this for you. Through the Python API, you can access the previously added object, get its life span, or even completely replace the actuator by its Python equivalent function KX\_Scene.addObject().

- **EndObject** : Take a deep look at your game object. Now turn away and say bye! Not only will your object be removed from the game, but also any child object parented to it.

- **ReplaceMesh** : If your object is not an Armature, a Camera, an Empty, a Lamp, or a Text, it does have a mesh attached to it. And if it has a mesh, it can have it switched into a different one. There are two options here: to replace the graphic mesh[md]the one you see rendered[md]or to replace the physical mesh[md]the one used for physics interactions, viewed with Show Physics Visualization.

>**But Isn't This Slow? Not Really**
>
>This feature works pretty fast. All meshes in the blender file are preconverted when the game is launched. When the actuator is activated, the game engine simply swaps the current mesh for the new one. This works even if there is no visible object using the mesh you want to replace, or there is no object at all; just make sure to keep the mesh alive with the "fake user" option.

This option can be used to implement what is known as level of detail: you swap your object mesh based on its distance to the camera. Whether the extra stress on your Logic and eventual scripting makes up for the gain in rasterizer performance will be up to your particular game.

- **TrackTo:** Unlike the Camera actuator, this Edit Object option will not move your object but rather change its rotation. Your object will work as a security camera tracking the object specified in the Object field. The 3D tracking option allows for three degrees of freedom in the tracker object. If Time is bigger than zero, it will determine how long a tracking lasts before the actuator is reactivated. To change the tracking axes, go to the Relations Extras options in the Object panel.

- **Dynamics** : Rigid Body and Dynamics can be turned off and back on here. That doesn't make a static object into a Rigid Body or Dynamic. It works to temporarily (or permanently) disable the physics behavior of one. The mass of the object can be changed here as well.

#### Message <a id="Message"></a>

There are different ways to coordinate actions between different objects. As presented earlier, one of them is through linking logic bricks from different objects. That is not only messy, but also limiting; you can only link objects if they are both present in the game altogether (ruling out dynamic added objects); nor you can broadcast an action over multiple objects without linking them manually. A good alternative is to use the Message actuator to send a message for other objects (or for itself). The three optional available fields are: To, Subject, and Body. You can see them in Figure 3.36.

![Message actuator](../figures/Chapter3/Fig03-36.png "Message actuator")

If you don't know which object to send the message to (or want to send it to more than one), you can broadcast it instead. For that you simply have to omit the To parameter. A Message Sensor[md]the other part of the story[md]can filter messages by their Subject. The Body can only be retrieved by a Python script, and it is commonly left blank when you only want to trigger an event, not to pass a value. The Body can be either a text or the value of a property.

> **The Real Thing About Real-Time Is That It Has a Delay**
>
>Be aware that messages are only going to be detected by the Message sensor in the next Logic cycle. Therefore, it's not a full replacement for linked Logic Bricks.

#### Motion <a id="Motion"></a>

_"My body move, move, my body …move!"_[md]hippo dance/pickup line (one of the best moments of DreamWorks' _Madagascar 2_).

It moves, but it does it in distinct ways. For example, an animated character will use an actuator to control the bones and a Motion actuator to control the general movement of the object into the scene[md]its orientation and position. So unless the game character is doing a windmill exercise, your walking cycle will need this actuator. As a matter of fact, any object[md]with or without an action assigned to it[md]may need to rotate and move around. Therefore, this is one of the most important actuators and vastly used for a game. Let's take a deep look at the two available methods: Simple Motion and Servo Control.

>**Rotate It Just a Bit**
>
>Once activated, this actuator will keep playing until it receives a negative signal or until it stops receiving the positive ones. So if you want to rotate your object a few degrees only when you press a key, you must use the Tap option in the Keyboard sensor.

##### Simple Motion <a id="Simple_Motion"></a>

The simplest way of moving an object is by changing its location in a specific direction. You can determine the offset in the X/Y/Z axis and in the next frame, your object will be that far from its original position. You can apply a rotation the same way, by considering the angle you want to rotate each of the axes every time. In Figure 3.37, you can see the barebones for this actuator.

![Motion actuator - Simple Motion](../figures/Chapter3/Fig03-37.png "Motion actuator - Simple Motion")

But what happens if your object is a dynamic one? If the object is already being controlled by the rules of physics, you can interact with it on that instance as well. Dynamic Object Settings allow you to apply physical changes into your object and let it react to them. Instead of displacing it a few units away, you can actually push it with some force into a given direction. What will stop the object from moving in this direction forever? As in the real world, the reaction from the other objects will produce resistance through surface collision (also known as _friction_). There will be times when you want to move your object regardless of the other game actors' physic meshes. For those, you can still rely on the Loc and Rot options.

![Motion actuator - Dynamic Object Settings](../figures/Chapter3/Fig03-38.png "Motion actuator - Dynamic Object Settings")

When your object is a dynamic one, you will see new options in the actuator (see Figure 3.38). Force, Torque, Linear and Angular Velocity, and Damping were all explained earlier. The difference between Force, Torque, and Linear and Angular Velocity is simple: when you use Force and Torque, you are adding physic momentum that will be applied to the object mass and result in a specific velocity. When you set the velocity directly, you have the game engine making sure the applied momentum will result on that velocity. There is also an option to Set or Add the Linear Velocity on top of the existent one and specify the Damping Frames to simulate acceleration; those are the number of frames that it will take to reach the target velocity.

>**Local and Global Again**
>
>In Blender, there are two main coordinate systems: Local and Global. Whenever you refer to an axis, you should be aware of the system you want to use. The default one is always the Global (also known as _World_) and will use the absolute X,Y,Z reference of your scene. When you want to use the Local one, which is shown as an L in the interface, the axis used will always be relative to your object's current orientation.

##### Servo Control <a id="Servo_Control"></a>

This is a more complex and complete method for controlling your object's linear movement. The Servo Control option enables you to control speed with force. It will apply a variable force in order to reach the target specified speed. It can be used to simulate the most varied effects, such as friction, flying, sliding, and so on.

The Servo Control can (and should) be used for any object, regardless of its dynamic/physic properties (see Figure 3.39). It replaces both Location and Linear Velocity from the Simple Motion option. The produced result is a more fluid and continuous movement for your object. This also doesn't affect the behavior of collision and other physics interactions[md]as opposed to using Location in the Simple Motion. The latter makes the object do "jumps into space," ignoring whatever is between its original and final position.

![Motion actuator - Servo Control](../figures/Chapter3/Fig03-39.png "Motion actuator - Servo Control")

- **Reference Object** : Albert Einstein once said that everything is relative. One of the breakthroughs of his scientific findings originated from his observation of a train from different reference points (a station, the same train, another train). The Reference Object here works as such, relativizing the new velocity from its position and velocity.

- **Linear Velocity:** The target velocity used in the Servo Control calculation.

- **Force Limit X** , **Y** , **Z** : It can control the minimum and maximum of the force applied in the object. The target velocity will eventually be reached so this option works toward speeding up or slowing down the acceleration.

>**Advanced Motion Control**
>
>**PID Servo Control System** : The following options help you to control the responsiveness and the reaction of your movement. In simple English, this is known as a "control loopback mechanism," and it is a constant evaluation procedure that shapes the characteristics of your movement.
>This is a generic (non-Blender specific) system; for more information, look at external references such as:http://en.wikipedia.org/wiki/PID\_controller

- **Proportional Coefficient** : You don't need to change this parameter unless you know what you are doing. It will adjust itself to be 60 times the IntegralCoefficient, so if you want a different value, remember to update it after making any adjustments there.

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
