**Table of Contents**

- [Chapter 6: Physics](#Chapter_6_Physics)
	- [What Is Physics?](#What_Is_Physics?)
	- [Overview](#Overview)
	- [World Properties](#World_Properties)
	- [Physics Engine](#Physics_Engine)
		- [Hands-on: World Settings for Multiple Scenes](#Hands-on_World_Settings_for_Multiple_Scenes)
	- [Culling Resolution](#Culling_Resolution)
	- [Physics Substeps](#Physics_Substeps)
	- [On the Issue of Time](#On_the_Issue_of_Time)
	- [Physics Steps](#Physics_Steps)
	- [Logic Steps](#Logic_Steps)
	- [FPS](#FPS)
	- [Physics Deactivation](#Physics_Deactivation)
	- [Physics Panel Settings](#Physics_Panel_Settings)
	- [Physics Types](#Physics_Types)
		- [No Collision](#No_Collision)
		- [Static](#Static)
		- [Dynamic](#Dynamic)
		- [Rigid Body](#Rigid_Body)
		- [Soft Body](#Soft_Body)
		- [Occluder](#Occluder)
		- [Sensor](#Sensor)
		- [Navigation Mesh](#Navigation_Mesh)
			- [Hands-on Tutorial: Navigation](#Hands-on_Tutorial_Navigation)
		- [Characters](#Characters)
	- [Common Settings](#Common_Settings)
		- [Hands-on Tutorial: Creating Compound Objects](#Hands-on_Tutorial_Creating_Compound_Objects)
	- [Material Panel Physics Settings](#Material_Panel_Physics_Settings)
		- [Hands-on Tutorial: Force Field Water Surface](#Hands-on_Tutorial_Force_Field_Water_Surface)
	- [Constraints](#Constraints)
	- [Vehicle Physics](#Vehicle_Physics)
		- [Hands-on Tutorial: Vehicle Physics Using Python](#Hands-on_Tutorial_Vehicle_Physics_Using_Python)
	- [Game Settings](#Game_Settings)
	- [Stabilizing Physics](#Stabilizing_Physics)

# Chapter 6: Physics <a id="Chapter_6:_Physics"></a>

Bem-vindo à Física 101! Vamos ser seus professores neste capítulo. Acompanhe enquanto mergulhamos em um mundo dinâmico de maçãs caindo, corremos ao lado de bolas quicando e voamos voando espaguete (veja a Figura 6.1).

![A physics demo](../figures/Chapter6/Fig06-01.png)

## What Is Physics? <a id="What_Is_Physics?"></a>

No mundo real, as leis da física governam tudo, desde a menor partícula subatômica até a maior galáxia muito, muito distante. Felizmente para nós, não precisamos entender a mecânica quântica, a física newtoniana ou o espaço euclidiano para fazer um jogo divertido. Um mecanismo de física lida com eventos de jogo, como detecção de colisão entre objetos, move objetos de uma forma fisicamente realista e até deforma objetos como se fossem feitos de um material macio.

Um mecanismo de física move as coisas com base em um conjunto de regras predefinidas para que você, o artista, não precise animar manualmente cada interação de objeto. Em comparação com as animações de quadro-chave tradicionais, que são predefinidas, a natureza dinâmica do mecanismo de física significa que é inerentemente não determinístico [md] o movimento do objeto depende da propriedade física do objeto e de seu estado no mundo físico. Esta propriedade única torna os jogos que utilizam a física em tempo real divertidos, se não imprevisíveis às vezes.

Como de costume, este capítulo vem com uma coleção de arquivos de exemplo que mostram o que o mecanismo de física pode fazer. Você pode encontrá-los na pasta/chapters6/demos.

## Overview <a id="Overview"></a>

Como a física é uma parte integrante do motor de jogo do Blender, configurações relacionadas à física são encontradas em muitos lugares diferentes. Por mais dispersos que possam parecer à primeira vista, há um padrão nesse caos.

As configurações de física podem ser divididas nestas seções:

- **World settings:** Contém configurações que afetam toda a cena. Configurações globais, como força da gravidade, podem ser encontradas aqui. A Figura 6.2 mostra o Editor de Propriedades do Mundo.

![World Properties Editor](../figures/Chapter6/Fig06-02.png)

- **Object Physics settings:** Qualquer objeto do motor de jogo (malha, lâmpada, câmera, vazio e texto) pode ser transformado em um objeto físico. Uma vez que a física é habilitada para um objeto, ele começa a obedecer às regras do motor da física, transformando o objeto de um objeto estático em algo que cai, colide, tomba e deforma. A Figura 6.3 mostra o Editor de Propriedades Físicas.

![Physics Properties Editor](../figures/Chapter6/Fig06-03.png)

- **Material Physics settings:** O painel Material não é apenas um lugar onde toda a magia gráfica acontece; ele também contém física adicional que controla como a superfície do objeto se comporta. Configurações como fricção de superfície podem ser encontradas aqui. Como um objeto pode ter vários materiais, as configurações de física dos materiais permitem que o artista atribua diferentes materiais de superfície para diferentes partes de um único objeto. A Figura 6.4 mostra o Editor de Propriedades do Material.

![Material Properties Editor](../figures/Chapter6/Fig06-04.png)

- **Object constraints:** Quando você era jovem, seus pais provavelmente estabeleceram certas regras que você precisava seguir. Se alguma das regras fosse quebrada, coisas ruins aconteceriam. As restrições físicas funcionam aproximadamente da mesma maneira (sem todo o drama e portas fechadas). Eles permitem que você configure regras simples que os objetos seguem, regras como rastrear um objeto para outro ou limitar sua amplitude de movimento. Com restrições, é possível representar de forma realista muitas das estruturas que têm um grau limitado de movimento, como dobradiças, rodas e correntes. A Figura 6.5 mostra o Editor de propriedades de restrições de objeto.

![Object Constraints Properties Editor](../figures/Chapter6/Fig06-05.png)

- **Physics sensors and actuators:** Exceto talvez no caso de uma máquina de Rube Goldberg, onde tudo acontece de uma maneira predeterminada, a maioria dos jogos seria muito chata se não houvesse uma maneira de fazer um objeto se mover ao comando do usuário ou de provocar uma reação quando dois objetos colidem. Atuadores e sensores cumprem essas duas funções, respectivamente. Os atuadores são parte de um tijolo lógico que realiza uma ação (como aplicar uma força ao objeto para fazê-lo se mover). Sensores são gatilhos que detectam quando algo acontece no jogo, como quando dois objetos se tocam. Uma combinação de sensores e atuadores torna o jogo verdadeiramente interativo, dando ao motor de jogo a capacidade de tomar decisões. A Figura 6.6 mostra o Logic Brick Editor. Caso você tenha esquecido, o Capítulo 3 trata de blocos lógicos.

![Logic Brick Editor](../figures/Chapter6/Fig06-06.png)

- **Python:** Além de todas as configurações de física que podem ser acessadas na interface gráfica do usuário, uma extensa API Python está à sua disposição. A API Python oferece controle programável sobre muitos aspectos do mecanismo de física. Com Python, você pode definir dinamicamente muitas das opções físicas enquanto o jogo está sendo executado. Ele ainda permite que você realize algumas coisas que não são possíveis na interface gráfica. Por exemplo, Python pode ser usado para criar física de veículos realista. A Figura 6.7 mostra o Editor de Texto com um script Python aberto.

![Text Editor](../figures/Chapter6/Fig06-07.png)

Portanto, agora que você tem uma visão geral do que é a física e onde encontrar todas as configurações, o restante do capítulo explicará como usar essas configurações em combinação para obter vários efeitos.

## World Properties <a id="World_Properties"></a>

O World Properties Editor é geralmente o primeiro lugar a se visitar ao configurar a física, simplesmente porque as configurações aqui são verdadeiramente globais: elas afetam toda a cena.

No World Properties Editor, existem várias configurações globais de física que afetam como a cena se comporta. Novamente, lembre-se de que as configurações específicas do jogo só são visíveis quando o seletor do motor está definido como Blender Game, conforme mostrado na Figura 6.8.

![Set engine to Blender Game to see the relevant game settings](../figures/Chapter6/Fig06-08.png)

## Physics Engine <a id="Physics_Engine"></a>

Na seção Physics do World Properties Editor, você terá a opção de selecionar um mecanismo de física. Um mecanismo de física é o algoritmo de computador subjacente que conduz todas as simulações de física. O Blender usa Bullet Physics, que é uma biblioteca de física poderosa e de código aberto desenvolvida por Erwin Coumans e outros. O Bullet não é apenas usado no Blender, mas também é usado por outros jogos comerciais, bem como produções de filmes, como parte do pipeline de efeitos visuais.

Quando o seletor do motor é definido como nenhum, todos os cálculos físicos são desabilitados. Os objetos dinâmicos não se movem quando uma força é aplicada e as colisões não são detectadas. A maioria dos jogos usará algum grau de física, então mantenha a física ativada, a menos que você tenha certeza absoluta de que não precisa dela. Se você optar por desabilitar a física, a maioria dos recursos mencionados no restante deste capítulo não funcionará.

A Figura 6.9 mostra as configurações de Física Mundial.

![World Physics settings](../figures/Chapter6/Fig06-09.png)

>**Disabling Physics**
>
>Algumas funções que parecem não estar relacionadas ao mecanismo de física, como os sensores de raycast e mouseover, também usam o mecanismo de física para detectar objetos. Portanto, desativar a física também interromperá essas funções.

Com o mecanismo de física definido como Bullet, você pode definir o valor da gravidade mundial. Quanto maior o número, mais rápido um objeto cai. O valor padrão de 9,8 corresponde à aceleração devido à gravidade na terra; para comparação, Marte tem uma gravidade de 3,7 m / s².

>**World and Scene Gravity Settings**
>
>Existem duas configurações de gravidade separadas no Blender. Um no painel World [md] que controla a gravidade para a física do jogo, e um no painel Scene [md] que controla a gravidade para o aspecto não-jogo da física do Blender (fluido, partículas e simulação de fumaça). Eles são visíveis apenas em seus respectivos engines (Blender Game e Blender Render ou Cycles Render, respectivamente). Ao trabalhar com jogos, certifique-se de ajustar a configuração correta em World.

### Hands-on: World Settings for Multiple Scenes <a id="Hands-on_World_Settings_for_Multiple_Scenes"></a>

Como o Blender suporta múltiplas cenas e cada cena pode ter seu próprio bloco de dados World, as configurações físicas podem ser definidas independentemente por cena. Isso significa que é possível criar vários mundos (ou _níveis_, como são comumente chamados em jogos), cada um com configurações físicas diferentes, todos contidos em um arquivo do Blender. Por exemplo, pode-se criar um jogo com duas cenas, uma ocorrendo na Terra e outra ocorrendo em Marte. Ao alterar as configurações do mundo, como a cor do céu, a profundidade da névoa e a força da gravidade de cada cena, você pode facilmente transmitir a ideia de um planeta estranho.

Para criar um jogo com duas cenas:

1. Abra /Book/Chapter6/earthMars.blend. Quando o jogo está rodando, você está no controle de uma câmera estilo tiro em primeira pessoa, que pode ser movida com as teclas W, A, S e D e girada com o mouse. Os cubos são gerados do nada e caem no solo de acordo com a gravidade.

2. Primeiro, renomeie a cena padrão de "Cena" para algo mais descritivo, como "Terra", clicando no bloco de dados Cena e digitando um novo nome, conforme mostrado na Figura 6.10.

![Renaming the scene](../figures/Chapter6/Fig06-10.png)

3. Vá para o Editor de Propriedades do Mundo; defina a cor do horizonte para azul claro, conforme mostrado na Figura 6.11. Dessa forma, você pode facilmente dizer qual cena é qual.

![Changing the color of the world](../figures/Chapter6/Fig06-11.png)

4. Para fazer outro mundo, você cria uma cópia da cena da Terra clicando no sinal + ao lado do navegador de cena. Na lista suspensa, selecione Full Copy, conforme mostrado na Figura 6.12. Este será o cenário do seu segundo mundo.

![Making a full copy of the scene](../figures/Chapter6/Fig06-12.png)

5. Renomeie a nova cena que você acabou de criar de "Terra.001" para "Marte".

6. Vá para o Editor de Propriedades do Mundo; defina a cor do horizonte para laranja escuro (consulte a Figura 6.13).

!["Mars" world settings](../figures/Chapter6/Fig06-13.png)

7. Abaixe a gravidade de 9,8 para 3,7, que é a gravidade em Marte.

8. Para alternar entre as duas cenas, você precisa adicionar um bloco lógico simples a ambas as cenas, de forma que quando a barra de espaço for pressionada na cena da Terra, ela pule para a cena de Marte e vice-versa. Configure o bloco lógico conforme mostrado na Figura 6.14. Nesse caso, não importa a qual objeto o tijolo lógico está anexado, pois a ação que ele realiza é global. A câmera é usada em nosso exemplo para hospedar o bloco lógico.

![Logic brick setup](../figures/Chapter6/Fig06-14.png)

9. Recrie o tijolo lógico na outra cena também. Configure-o para carregar a cena correspondente.

10. Agora pressione P para jogar. Salte entre as duas cenas usando a barra de espaço. Observe que a gravidade e a cor do céu mudam dependendo da cena em que você está.

11. É isso aí! O jogo finalizado pode ser encontrado com o nome earthMars-ended.blend. Para estender este jogo, você pode brincar com as propriedades físicas do cubo, que estão ocultas na camada 2.

## Culling Resolution <a id="Culling_Resolution"></a>

A seleção de oclusão pula a renderização de objetos que estão fora de vista ou atrás de um objeto Oclusor. Ao não desenhar esses objetos, você pode acelerar o desempenho de exibição do jogo. A seleção de oclusão costumava ser uma opção que poderia ser desativada pelo usuário, mas nas versões mais recentes, a seleção de oclusão está sempre ativada.

Os objetos Occluder devem ser definidos manualmente. Para obter mais informações sobre como configurar a seleção de oclusão, consulte o Capítulo 8, "Fluxo de trabalho e otimização".

A configuração da resolução de eliminação controla a precisão do teste de oclusão. Um valor mais alto leva a um desempenho mais lento, mas fornece uma seleção mais precisa de objetos menores que, de outra forma, poderiam ser perdidos por um buffer de oclusão de baixa resolução. O valor padrão de 128 é ideal para a maioria dos casos.

>**Not Visible but Still There**
>
>A seleção de oclusão apenas ignora a exibição de um objeto. O objeto ainda seria processado pelo mecanismo lógico e físico. Portanto, qualquer interação física, configuração de tijolo lógico ou script Python anexado ao objeto será executado normalmente, mesmo quando o objeto é selecionado da tela.

## Physics Substeps <a id="Physics_Substeps"></a>

As etapas de física e as etapas de lógica são duas configurações que controlam o comportamento do mecanismo de física. Eles são considerados ajustes avançados que geralmente não devem ser modificados. E mesmo se você fizer isso, o efeito pode não ser óbvio a princípio. Esta seção tenta desmistificar essas configurações. Consulte a Figura 6.15 conforme você segue.

Quando a simulação de física não é precisa o suficiente, você pode ver objetos passando uns pelos outros, especialmente quando os objetos se movem muito rápido em relação uns aos outros. Para aumentar a precisão da simulação de física, você pode forçar o Blender a quebrar a simulação de física em um intervalo menor de tempo. Você faz isso aumentando o valor do subconjunto na interface. Essencialmente, uma subetapa é responsável pelo número de iterações físicas que temos por quadro. Portanto, 1 subetapa representa uma interação por quadro, 2 subetapas são duas iterações (isto é o dobro dos cálculos físicos), etc. Um número mais alto faz a simulação de física funcionar com melhor precisão, ao custo de uma diminuição drástica no desempenho para físicos pesados cenas.

Se você se deparar com alguma instabilidade física, pode ficar tentado a aumentar imediatamente o valor da subetapa. Evite este impulso: não confie inteiramente em subetapas para ocultar uma configuração de física mal projetada; o mecanismo de física é projetado para funcionar com uma subetapa de 1 ou 2. Use outras maneiras de estabilizar a física, conforme descrito posteriormente neste capítulo. Apenas aumente o valor da subetapa quando todo o resto falhar.

>**Bottom Line**
>
>De modo geral, o valor 1 é suficiente para jogos lentos; 2 é ideal para jogos de arcade de movimento rápido e jogos de ação com muitas interações físicas; os jogos de direção podem exigir um 3 ou um 4 (bem, dependendo de quão rápido o carro pode ir); não use 5 a menos que seu jogo contenha objetos supersônicos.

## On the Issue of Time <a id="On_the_Issue_of_Time"></a>

Para a discussão a seguir, a palavra _realworld-time_ refere-se ao fluxo do tempo no mundo real, o mundo em que vivemos. Física relativística à parte, o tempo real é sempre constante para o nosso propósito. Não existem dispositivos mágicos, encantamentos fabulosos ou DeLoreans acelerados para alterar o fluxo do tempo.

O termo _game-time_ refere-se ao fluxo do tempo no mundo do jogo virtual. O fluxo do tempo de jogo geralmente também é constante, exceto em casos especiais em que câmera lenta ou lapso de tempo é usado.

Por que isso é importante? Para a maioria dos jogos, o tempo de jogo deve ser diretamente proporcional ao tempo do mundo real e completamente independente da taxa de quadros. Assim, não importa quão alta ou baixa seja a taxa de quadros, o tempo de jogo sempre fluirá a uma taxa constante. Ter o tempo de jogo independente da taxa de quadros tem muitos benefícios. Um jogo executado em um tempo de jogo constante não diminui a velocidade quando a taxa de quadros é baixa, nem acelera quando a taxa de quadros é alta. Isso garante que pessoas com computadores diferentes possam desfrutar do jogo na mesma velocidade. Você não gostaria de jogar um jogo de direção que faz o carro andar mais rápido em um computador rápido, mas diminui a velocidade para um rastreamento em um computador lento!

Acontece que é difícil garantir um tempo de jogo constante apesar das flutuações na taxa de quadros! As configurações a seguir são usadas para controlar como o tempo de jogo é vinculado à taxa de quadros.

## Physics Steps <a id="Physics_Steps"></a>

As etapas máximas de física controlam quantos quadros de simulação física consecutivos o mecanismo de jogo pode rodar para cada quadro renderizado. Um valor alto (5) é fisicamente mais preciso, porque dá ao mecanismo de física tempo suficiente para concluir o cálculo da física, independentemente da taxa de quadros do jogo, resultando, portanto, em um tempo de jogo mais consistente que é independente da taxa de quadros, no custo de ocupar mais tempo de processamento. Um valor baixo (1) pode aumentar a taxa de quadros do jogo ligeiramente, reduzindo o número de quadros de simulação física consecutivos que o motor do jogo tem permissão para executar cada quadro, mas ao custo de um comportamento físico impreciso, porque o tempo de jogo seria vinculado à taxa de quadros.

>**Bottom Line**
>
>Se você ainda estiver confuso, apenas defina Max Physics Steps como 5. Isso garante que o tempo de jogo seja o mais constante possível, não importa qual seja a taxa de quadros.

## Logic Steps <a id="Logic_Steps"></a>

Muito semelhante ao Max Physics Steps, o Max Logic Steps controla quantos tiques lógicos de jogo consecutivos o motor do jogo pode rodar para cada quadro renderizado. Quando a taxa de quadros do jogo é menor do que a configuração de FPS nominal, um valor alto (5) é mais preciso porque garante que a etapa lógica sempre tenha tempo suficiente para terminar todo o cálculo lógico. Por outro lado, um valor baixo (1) renderá um desempenho ligeiramente melhor ao custo de uma flutuação no tempo de jogo. Portanto, isso significa que quando a taxa de quadros é alta, o jogo será executado normalmente, mas se a taxa de quadros cair, o jogo parecerá desacelerar.

>**Bottom Line**
>
>O valor padrão de 5 significa que a lógica sempre tem tempo suficiente para ser executada, não importando a taxa de quadros do jogo. Isso garante que o tempo de jogo não diminua quando a taxa de quadros estiver baixa.

## FPS <a id="FPS"></a>

Quadros por segundo é o Santo Graal do benchmarking de desempenho. Para um videogame, uma alta taxa de quadros é sempre desejada, pois significa uma ação mais suave e uma resposta mais rápida à entrada do usuário. A taxa de quadros é uma função da complexidade da cena e da velocidade do computador. Infelizmente, a configuração aqui age apenas como um limite da taxa de quadros, não a taxa de quadros real que o jogo tem garantia de rodar. O valor padrão de 60fps significa que a cada segundo, o mecanismo de jogo avalia a lógica do jogo 60 vezes. Esse número específico é escolhido porque a maioria dos monitores LCD não atualiza mais rápido do que 60 Hz, portanto, qualquer quadro extra renderizado pelo computador será simplesmente desperdiçado.

Internamente, fps define o número de tiques lógicos e tics físicos nos quais o mecanismo de jogo é executado. Portanto, à medida que você diminui a configuração de fps, o número de tiques lógicos e físicos executados pelo jogo diminui de acordo. Isso tem o efeito de desacelerar o tempo de jogo _._ Em outras palavras, se o fps for definido muito baixo, não apenas o jogo parecerá instável, mas na verdade parecerá estar rodando em câmera lenta.

>**Bottom Line**
>
>The default value of 60 is good for most game applications. Setting this value higher does not give you better performance. It is also customary for some games to set the fps to a lower value such as 30. The idea is that a game running at a constant 30fps feels smoother than a game that is fluctuating between 30fps and 60fps. Additionally, you can set vsync in your graphic card to force a frame rate ceiling. You don't have control over that in the player's computer, though.

## Physics Deactivation <a id="Physics_Deactivation"></a>

The values Linear Threshold, Angular Threshold, and Time all control how aggressively the physics engine puts objects to "sleep" in order to reduce the load on the game.

Setting the deactivation time to 0 effectively disables this optimization. Since sleep can also be disabled per object from the Physics Properties Editor, it's generally not recommended to disable deactivation here.

Lower the Linear Threshold if an object comes to a stop earlier than expected.

Lower the Angular Threshold if an object comes to a stop from spinning earlier than expected.

## Physics Panel Settings <a id="Physics_Panel_Settings"></a>

So now that you are familiar with the World Properties Editor, which contains settings that apply to all physical objects indiscriminately, let's take a look at the Physics Properties Editor. From here, you can alter the physical characteristics of individual objects.

Physics settings apply to all game objects types, including mesh, empty, lamp, and camera.

## Physics Types <a id="Physics_Types"></a>

How do you decide which physics type to pick for an object? That largely depends on the role of the object in the game. Table 6.1 shows all the physics types that are available in Blender and their corresponding characteristics.

|    Type       |    Collision G,F,T    |    Roll Typical Use                      |
| ------------- |:---------------------:|:-----------------------------------------|
| No collision  | No  No  No            | Effects, high-resolution mesh            |
| Static        | Yes  No  No           | Buildings, immovable structures          |
| Dynamic       | Yes  Yes  No          | None                                     |
| Rigid Body    | Yes  Yes  Yes         | Movable barrels, crates, general objects |
| Soft Body     | Yes  Partial  Yes     | Hair, cloth, rubber ducky                |
| Occluder      | No  No  No            | Walls for performance optimization       |
| Sensor        | Yes  No  No           | Event triggers                           |
| Navigation    | No  No  No            | Pathfinding helper                       |
| Character     | Yes  No  No           | Designed specifically for characters     |

Table 6.1: Physics Types
- **Collision**: Whether the object detects collision.

- **G,F,T**: Whether the object can be moved by Gravity, Force, and Torque.

- **Roll**: Whether the objects roll and tumble when they are on an incline.

To familiarize yourself with the different physics types, open the demo file available from /Book/Chapter6/demo/physicsTypes.blend. It shows some of the common physics types and their behavior, as shown in Figure 6.15.

![Different physics types visualized](../figures/Chapter6/Fig06-15.png)

Let's look at the settings in more detail.

### No Collision <a id="No_Collision"></a>

No Collision skips all physics calculation. The objects will be effectively invisible to the physics engine. Other objects will not be able to detect collision with the object, nor collide with it. No Collision objects can still be moved using the Motion actuator. Use this for objects that you don't intend to interact with at all during the game, such as leaves of vegetation.

>**Collision Proxy**
>
>Setting an object to No Collision completely skips collision detection on the object, which can speed up the game considerably on a high-polygon mesh. A common practice is to set the high-polygon mesh to No Collision and then manually create a simplified "collision proxy" mesh object that approximates the shape of the high-polygon mesh. Then attach the high-polygon mesh to the collision proxy using parenting. This way, the low-polygon mesh will be used for all collision calculation, which is fast, and a high-polygon version of the object will be used for display, which is visually nicer. As this is an optimization technique, a step-by-step tutorial on creating a collision proxy is covered in Chapter 8.

### Static <a id="Static"></a>

Static objects are the default physics type for objects. They do not fall due to gravity, nor do they move by external impact, such as another object striking them. By default, the mesh itself is used as the collision mesh, which can be slow if the object has a lot of polygons. Static objects never move on collision with another object. Use this setting for objects that require collision but don't move, such as buildings and fixed structures.

### Dynamic <a id="Dynamic"></a>

Dynamic objects are different from static objects in that they have a defined mass and follow the basic Newtonian law of mass and acceleration. They fall due to gravity and react when another object collides with them. By default, the collision bound for dynamic objects is a sphere for performance reasons. Sometimes this is sufficient, but most of the time, it's better to use another shape as the collision bound. More on collision bounds in Chapter 8. Moreover, because dynamic objects do not roll, their usefulness is limited. If you want to simulate a realistic 3D object, Rigid Body is what you want.

### Rigid Body <a id="Rigid_Body"></a>

Rigid body behaves very similarly to a dynamic object: they have a defined mass, accelerate due to gravity, and react to collisions. On top of that, rigid body objects have the ability to tumble when needed, whereas a dynamic object will slide awkwardly down a ramp without rotating.

If the Suzanne model in the aforementioned sample Blender file is set to Rigid Body, it will behave like a real object, fall toward the ground, and come to rest on one of its ears.

>**Avoid DLoc Movement**
>
>When using a dynamics based object (Dynamic, Rigid Body, and so on), you should use physics-based options, such as force and linear velocity for movement, and not change its location directly by dLoc.

### Soft Body <a id="Soft_Body"></a>

Whereas all the previously described physics types operate on the objects by moving and rotating them around without changing the underlying geometry, Soft Body physics uses a mass-spring system to apply deformations to the actual geometry. With Soft Body, you can create convincing cloth and other soft objects. Although it is very cool to play around with, Soft Body is very computationally intensive compared to the other physics types, and not as stable, so use it sparingly.

As seen in the Suzanne model in the sample file, it will fall due to gravity, and once it hits the ground, it collapses as if it's made of a rubber shell. This is the power of Soft Body physics.

>**Apply Scale**
>
>The physics engine works more reliably when the objects have a scale of 1. Thus, it is highly recommended to Apply Scale by pressing Ctrl+A on most of the objects before you run the game. This will prevent a lot of the strange issues that might crop up later.

### Occluder <a id="Occluder"></a>

Occluder objects do not react to gravity and collision. Their only function is to make any objects behind them invisible. Occluder objects are used to help the game engine decide when to remove objects from view to speed up the rendering performance. Strategically-placed occluders can significantly increase the performance of the game.

Figure 6.16 explains how occluders work.

From left to right, the first image shows the scene setup of /Book/Chapter6/PhysicsOccluder.blend. The second image shows what the camera sees. Notice the monkey head is not visible because the plane is blocking it. The third image is the view from the same camera while in-game, in wireframe mode. Notice that even though the monkey head is behind the wall, it is still being rendered, thus wasting precious computing time. The last image is the same in-game view as the previous image, but with the wall set to Occluder, the monkey head is not displayed.

![Occluder culling](../figures/Chapter6/Fig06-16.png)

### Sensor <a id="Sensor"></a>

Similar to Static Object, a Sensor object detects collision with another object. It is usually used as a replacement for the "radar" or "near" sensor because a Sensor object can be made into any arbitrary shape. Furthermore, Sensors will detect collisions, but they do not register a response. In other words, they behave like ghost objects. Additional logic bricks are needed to utilize a Sensor object effectively.

### Navigation Mesh <a id="Navigation_Mesh"></a>

This setting turns an object into a helper object that is used for pathfinding navigation.

Since Blender 2.6, the game engine has a fully automated AI pathfinding routine. It can be used to direct an AI character through the 3D world, reaching a target, while avoiding obstacles.

#### Hands-on Tutorial: Navigation <a id="Hands-on_Tutorial_Navigation"></a>

1. Open /Book/Chapter6/navigation.blend

2. This scene is set up with four objects (excluding the lamp and the camera).

3. _Monkey_ is our main character; it will be navigating through the maze (the VisualMesh) to get to the Target. To aid its quest, we have created a simple helper geometry that outlines where the character can walk. This object is known as the _NavMesh_. Figure 6.17 shows the initial setup.

![Navigation system](../figures/Chapter6/Fig06-17.png)

4. A navigation mesh is a helper object (invisible while the game is running) that is used to help guide other objects along a path. The NavMesh object is a regular mesh object that defines the shape of the accessible area for the pathfinding routine.

5. There are two ways to create a navigation mesh. One is to manually model a geometry that covers all the areas that are accessible to a character. This is what we have done with NavMesh.

6. Another option is to ask Blender to create a navigation automatically. It might be easier for larger maps, but the result is far less predictable. We will cover this functionality at the end of this hands-on tutorial.

7. Make sure that the NavMesh object is selected and change its physics type to Navigation Mesh. The NavMesh will turn into a colorful grid, but don't be alarmed[md]this is normal. It means the object now can be used to aid in navigation. Navigation meshes becomes invisible when the game is running.

8. Select the Monkey object and add a "steering" Logic Brick actuator to it, as shown in Figure 6.18. Define the target and navigation mesh object, as shown in Figure 6.19.

![Steering actuator setup](../figures/Chapter6/Fig06-18.png)

9. And you are done! Start the game and watch the monkey seek out the cone. The Steering actuator contains additional options that you can explore.

10. Figure 6.19 shows the finished game running in the Blender game engine. You can check out navigation-finished.blend.

![Finished](../figures/Chapter6/Fig06-19.png)

11. As promised, another way to create a navigation mesh is to use the automatic generator. To do this, delete the NavMeshobject first so you can start with a clean slate.

12. Select the object you want to use as the guide in creating the navigation mesh. In this case, you need to select VisualMesh. Blender will build a new navigation mesh based on this mesh.

13. Go to the Scene tab of the Properties Editor, as seen in Figure 6.20. You should see a "Build Navigation Mesh" button, along with a whole slew of settings.

![Automatic navigation mesh generation](../figures/Chapter6/Fig06-20.png)

14. Pressing the aforementioned button will create a navigation mesh automatically from the visual mesh.

15. If the result isn't optimal, play with the settings. Agent Radius is a good place to start.

### Characters <a id="Characters"></a>

This is a specialized physics type that is designed specifically for player-controlled characters. This physics type follows the basic rules of kinematics, while ignoring some of the other physical rules in order to make the object's behavior more predicable. For example, the character object type doesn't bounce off walls or slide on ramps. PhysicsType.blend has an example of a playable character object that walks around. Try to move it with the arrow keys.

## Common Settings <a id="Common_Settings"></a>

Whew. With all the physics types out of the way, let's look at some of the shared settings common to most of the physics types described earlier.

- **Actor:** Makes the object part of the physics evaluation loop. An object not marked as an actor is ignored by the Near and Radar sensors, although it will still obey the laws of physics.

- **Ghost:** Makes an object not react to collisions such that it will pass through another[md]like a ghost. Collisions are still detected for ghost objects, so any sensors that detect collision between two ghost objects will still fire, but the objects will not bounce apart as they normally would.

- **Invisible:** Skips rendering of the object while still calculating all the physics and logic. This is useful for creating invisible walls and edges of maps to prevent players from visiting places you do not want them to go.

- **Mass:** Sets the mass of the object. A heavier object requires more force to move. Contrary to intuition, a heavier object does not fall faster than a lighter object (see note, "Hammer and Feather"). So increasing the mass will not make your object fall faster. To make objects fall faster, lower the damping on the object or increase the gravity in World settings.

>**Hammer and Feather**
>>
>A hammer and a feather fall at the same rate in vacuum! In air, the drag force will slow down a lighter object more than a heavier object, so a heavier object indeed falls faster than a lighter object. But since Blender does not model air friction, object mass does not affect how fast they fall. This is not a bug!

Just as an 18-wheeler truck hitting a bunny won't have a happy ending (for the bunny), the physics engine works best when the objects interacting have masses of a similar magnitude. When an object with a very large mass collides with an object with a very small mass, instability might be created in the physics engine. As a general rule, keep all objects within 2 magnitudes of mass to each other. So, if an object weighs 1.0, it shouldn't interact with an object that is much heavier than 100.0.

- **Radius:** Controls the radius of the collision sphere. If a collision bound other than Sphere is selected, this setting has no effect.

- **No sleeping:** By default, the physics engine automatically suspends the physics calculation for an object when its motion is sufficiently slow. This is known as "sleeping." Putting the object to sleep can free up the CPU cycle and increase game performance until another object interacts with it again. Putting objects to sleep can cause some odd-looking behaviors, such as slow-moving objects coming to a sudden stop. "No sleeping" disables this optimization. The downside is that "no sleeping" might lead to some odd, jittery behavior for objects that are not perfectly stable.

Additionally, there are options for controlling when objects go to sleep in the World properties under the "Physics Deactivation" label. This settings can be used to change the global delay before objects are deactivated.

- **Damping:** Applies a drag force on an object. A damping of 0 corresponds to no friction at all, just like a spherical cow traveling in a vacuum. A damping of 1.0 corresponds to a drag force so strong that the object will be unable to move. Translational damping slows down an object's movement; rotational damping slows down an object's spinning.

- **Anisotropic Friction:** Controls the friction force per axis. You can use this to mimic objects that have different coefficients of friction, depending on the orientation of the object. For example, a skateboard slides easily along its length, but is almost unmovable sideways.

- **Form Factor:** The tooltip says this setting "scales the inertia tensor." Make sense? No? Well, aren't you glad you have this book! Form factor controls the tendency for an object to roll. The bigger the value, the less likely an object will roll and tumble. A smaller value makes the object much more likely to rotate. Set the value too low, and the object will become unstable. The default value is a good balance between physics stability and realism.

- **Collision Bounds:** This is the shape of the object as it appears to the physics engine. This might sound surprising, but the shape of the object used for physics calculation is not always the same as the one that is displayed. The distinction is important because, for performance reasons, a rough proxy shape is often used in place of the actual geometry. This way, the user still sees a fully detailed object on the screen, but the physics engine can run a lot faster using a simplified collision bound. It is important to try to use the simplest collision bounds possible in order to keep the game engine's performance fast.

- **Capsule** , **Box** , **Sphere** , **Cylinder,** and **Cone:** These are some of the basic primitives that can be used to approximate different collision bounds (see Figure 6.21). Their shapes are self-explanatory. To see exactly how the bounding box is applied to your model in-game, turn on "Show Physics Visualization" in the Game Options screen.

When the collision bound is set to Convex Hull, the collision bound takes the shape of the object, but with all the concave areas filled in. Convex Hull can accurately approximate an object of any shape as long as it doesn't have any "negative" space, such as holes. For example, a doughnut-shaped rigid body object set to Convex Hull will be treated as if the hole isn't there.

![Collision bounds visualization: Top row: box, sphere, cylinder; Bottom row: cone, convex hull, triangle mesh](../figures/Chapter6/Fig06-21.png)

- **Triangle Mesh:** This is the most robust collision bound type. It will create a collision bound that is an exact duplicate of the actual mesh. If you want to ensure that the collision bound matches the visual mesh exactly, this is the setting to use. So why don't we use this setting all the time? The reason is performance and stability. The physics engine is far better optimized for simple primitives, such as a box, than an arbitrarily shaped triangle mesh.

>**Visualizing Collision Bounds**
>
>Once the collision bound is set, you should notice that the collision bound is visualized as a dashed lines in the 3D viewport. This helps you visualize the relationship between the collision bounds and the visual mesh.
>To visualize the collision bounds in-game, turn on "Show Physics Visualization" in the Game Options screen and run the game.

- **Collision Margin:** The Bullet Physics Engine SDK Manual explains that the collision margin is an internal setting that improves the performance and stability of the collision detection by giving thickness to each face. It is highly recommended that you do not adjust this setting outside its normal range (0.05). In some cases, too high of a value will result in a tiny air gap between colliding objects. Too small of a value will increase the chance of missed collisions between objects.

- **Compound:** The compound setting makes objects linked together by parent-children relationships behave as if they are a single physics entity.

But, why use compound when you can just join your objects together with Ctrl+J? Apart from the fact that there might be times when you need to control individual objects (so joining them might not be an option), using compound collision bounds made up of simple primitives is actually recommended over using one triangle mesh collision bound. The reason is again that a combination of simple primitives is faster to compute than a triangle meshes.

### Hands-on Tutorial: Creating Compound Objects <a id="Hands-on_Tutorial_Creating_Compound_Objects"></a>

To create a compound physics object (see Figure 6.22):

1. Open /Book/Chapter6/compound.blend.

2. Run the game. Notice that even though the three objects are parented together, they do not react to the ground plane in a convincing way. Only the parent object collides with the ground.

3. To change that, from the Physics Properties Editor, turn on Compound for each of the three objects.

4. Run the game now and notice that all objects contribute to the kinematics of the group.

![Compound objects physics](../figures/Chapter6/Fig06-22.png)

## Material Panel Physics Settings <a id="Material_Panel_Physics_Settings"></a>

By adding a material to the object, you enable additional options that give you finer control over some of the physical properties of the surface. Figure 6.23 shows the physics settings found in the Material panel.

![Material physics settings](../figures/Chapter6/Fig06-23.png)

- **Friction:** Controls the force that slows down a moving object when it comes in contact with another object. The effective friction force between two objects is dependent on the friction settings on both objects. So if one object with a high friction setting comes in contact with another object with low friction, the effective friction force would be somewhere in the middle of the two values.

- **Elasticity:** Controls the "bounciness" of the objects when they collide with another. An object with low elasticity does not bounce away as far after a collision; an object with high elasticity loses almost no momentum in a collision and bounces away at almost the same speed as it came in. The effective elasticity between two colliding objects takes both objects into account. A tennis ball hitting a hardwood floor would be an example of an elastic object colliding with another elastic object. A tennis ball hitting carpet would be an example of an elastic object colliding with a non-elastic object.

- **Force Field:** The next set of settings controls what Blender calls _force field._ When the force and distance are set to non-zero, a force field is generated on all the faces so that any object that comes within range (as specified by the distance setting) is pushed away with a certain force (as specified by the force setting). The result of this is that object that comes close to a force field surface will be repelled. The effect on the object is exactly as the name implies: it mimics a magnetic field. The damping setting slows down the object.

Once Force Field is enabled in the Material panel, you will need to tell individual objects to respect that setting by going into the Physics Properties Editor and turning on Use Material Force Field.

### Hands-on Tutorial: Force Field Water Surface <a id="Hands-on_Tutorial_Force_Field_Water_Surface"></a>

Force field can be used to create a convincing[md]you guessed it![md]force field effect, where an object moving toward a force field seems to be slowed down by invisible energy. This is very different from the usual rigid body interactions, which are always hard collisions.

As you might imagine, the Force Field setting is used to simulate the realistic interaction of floating objects on a calm water surface. To do this:

1. Open /Book/Chapter6/water.blend.

2. Select the _Cube_. You want this object to behave like a basic wooden crate, a crate that bounces, tumbles, and floats in water. So let's add some dynamics to it. Go to the Physics Properties Editor and set the Type from Static to Rigid Body.

3. For extra fun, let's make a lot of these crates! But instead of manually creating them, we'll dynamically add them in-game on the player's command.

4. Select the Camera object in the Logic Editor panel and add a new Keyboard sensor, a new And controller, and an Edit Object actuator, as shown in Figure 6.24.

![Logic bricks](../figures/Chapter6/Fig06-24.png)

5. To make sure that the cube objects get instantiated when you run the game, you need to hide the original cube object. To do this, simply move the Cube to the second layer by pressing M and then 2.

6. With only layer one selected, run the game now. Notice how the cubes all collide with the ground plane, but because the ground plane is hard, the motion is rather jarring. It doesn't look like objects floating on water at all.

7. To make the ground plane have a water-like property, we will turn on Force Field. First, select the object called _WaterPlane._

8. Head to the Material Properties Editor and create a new material. Then simply copy the force field physics setting, as shown in Figure 6.25.

![Material physics settings](../figures/Chapter6/Fig06-25.png)

9. Et voilà! Start the game, press the spacebar, and watch the crates tumble into the ocean.

10. For added realism, create a No-Collision Plane on top of the WaterPlane to act as the water surface.

## Constraints <a id="Constraints"></a>

Constraints are frequently used to create joints and mechanical linkages, indispensible components of many games. The Constraints Properties Editor is shown in Figure 6.26.

![Adding a Rigid Body Joint in the Constraints Properties Editor](../figures/Chapter6/Fig06-26.png)

The only supported object constraint is the Rigid Body Joint. It is used to connect two objects together using a user-defined joint.

Figure 6.27 illustrates the variety of pivot types.

![Constraints illustrated](../figures/Chapter6/Fig06-27.png)

- **Ball:** Joins two objects together using a ball-and-socket joint. This type of constraint is free to rotate around all three axes.

- **Hinge:** Joins two objects together using one axis[md]the hinge axis. This constraint is often used to simulate a door hinge or a wheel on an axle.

- **Cone-twist:** This is an extension of the Ball constraint that supports limiting the angle of rotation. This is especially useful for animating limbs using ragdoll physics. You can set the individual angle limits for each of the three axes.

- **Generic 6 DoF:** If none of the above constraints meet your needs, chances are this generic constraint will give you enough control to accomplish any mechanical linkage you can dream up.

Once you have decided on the pivot type you need, you'll need to set the Targetobject. The Target object is the object that the current object will be linking to.

The rest of the settings should be very self-explanatory. Refer to /Book/Chapter6/demo/constraints.blend to see each constraint's type in action.

- **Extending Constraints:** While one constraint might not be too useful, constraints can be daisy-chained to simulate many different objects. See ConstraintsChain.blend, ConstraintsWaterMill.blend and ConstraintsTrampoline.blend for examples of how to set up multiple constraints.

## Vehicle Physics <a id="Vehicle_Physics"></a>

The Blender physics engine has built-in support for vehicle physics. It is a very stable physics constraints system that provides easy-to-set-up car physics. The result is a fast-performing vehicle physics engine with easily tweakable settings that maps well into a real vehicle (steering, suspension length, suspension stiffness)

Of course, you can also try to create a car physics setup without using the built-in physics constraints; however, it will be far more time-consuming. This section will demonstrate how to set up a playable car object in the game engine using the built-in Bullet engine and a bit of Python scripting.

### Hands-on Tutorial: Vehicle Physics Using Python <a id="Hands-on_Tutorial_Vehicle_Physics_Using_Python"></a>

To get started, open /Book/Chapter6/vehicle/car.blend.

Rather than presenting this as a step-by-step tutorial, we will dissect a fully working, pre-made file.

Our basic car is composed of a body object and four wheel objects. The wheels are separate from the car for now. The physics engine will be responsible for keeping the wheels attached to the body, so the location of the wheel objects does not matter at this point. In this file, they are placed close to the car body for convenience.

Because attaching the wheels to the body will be done by a script, it is crucial for the rotation of the wheel to be correctly set; otherwise, the wheel will be linked to the car in the wrong orientation once the physics engine takes over. In the sample file, notice that the wheel objects all have their rotation set to [0,0,0]. This is important because the local rotation on the objects will interfere with the physics engine and confuse the game engine, resulting in unexpected behavior when you try to attach the wheels to the car. If a wheel needs to have its rotation reset, press Ctrl+A to apply any rotation.

Also notice that the car body is a rigid body object with ghost turned on. This setting is crucial for the car physics to run correctly.

That's pretty much it[md]a car body object and four tires make up the vehicle.

As already mentioned, the actual vehicle physics relies on some Python script to function. Figure 6.28 shows all the logic bricks that are attached to the car body object. Notice that script plays a big part in it.

![Vehicle logic brick setup](../figures/Chapter6/Fig06-28.png)

The script.carInit() functionality is run when the game is started. Here, it initializes the car as a "vehicle constraint," also known as constraint type11, and stores it as a Python object called _vehicle_. The same script then looks for the four wheels by accessing an actuator with specific names (in this case, wheel1, wheel2, etc.), and then the script attaches the wheels to the car body using the settings specified in the script. Variables such as RollInfluence, SuspensionStiffness, and TyreFriction can all be set on a per-tire basis once the vehicle object is created. The job of carInit() is now done. Your car body is now considered to be a vehicle by the game engine, and it will behave like one.

The second most important function, script.carHandler(), is run every frame. This script does the actual moving of the car, and it applies engine force and steering to the vehicle object. But this script gets the user input (keyboard sensor inputs) from another source (see below). The vehicle wrapper has built-in methods such as applyBreaking(), applyEngineForce(), getWheelRotation(), and getNumWheels, which you can call.

Every time a key is pressed, script.keyHandler() is run. It figures out which key is pressed and sets the intermediate variable so that the scripts.carHandler function will know how much throttle to apply, which way to steer, and so on. This script is separated from scripts.carHandler() not because of technical limitations but by design, so that it's easier to manage the code.

With these three Python functions, the car comes alive.

## Game Settings <a id="Game_Settings"></a>

Game settings are global settings that affect the running of the game. These settings are shown in Figure 6.29 and can be found in the Render panel.

![Additional game settings](../figures/Chapter6/Fig06-29.png)

- **Animation Playback Speed:** Closely related to the frame-rate setting is the animation playback speed. This setting controls the speed of the F-Curve and armature animation. By default, the value is set to 24, meaning all F-Curve and actions will be played back as if they are running at a 24fps timebase. This setting can be found in the Render panel.

- **Debug Property:** Shows the value of the Game Properties that are marked with the Debug flag. This can be useful when you want to keep an eye on the values of certain variables while the game is running.

- **Frame Rate and Profile:** Shows the frame rate and other performance statistics in-game. These statistics will be displayed in the top-left corner of the screen in-game.

- **Physics Visualization:** Visualizes the internal computation of the physics engine. This can help you see what the physics engine is really doing when the game is running.

Rigid Body objects are displayed in white, and sleeping objects are drawn in green.

- **Deprecation Warning:** Gives warnings about outdated Python API called in the console (see Chapter 7).

- **Mouse Cursor:** Draws the mouse cursor in-game. This is useful if the game uses mouse-input. Mouse cursor can also be turned on and off via Python.

## Stabilizing Physics <a id="Stabilizing_Physics"></a>

The Bullet physics engine is good. Really good. But as with anything that is powered by a computer, it is still possible to get into a situation where things go haywire.

Okay, so what is unstable physics anyway? When you see objects jitter around when they are not supposed to, or when objects go through each other when they are supposed to collide, you know it's time for a reality check.

Here are some tips to help you regain control of your game. All of the settings here are already covered in the chapter; this list is simply a collection of the most common actions to take to stabilize physics.

- **Avoid Extremes:** Avoid interaction between an extremely heavy object and an exceptionally light object. Avoid interaction between extremely fast objects. Avoid interaction between objects of very different sizes, especially if neither object is static.

- **Physics Substeps**** (World Properties Editor):** Crank it. Higher will be slower but gives much a more accurate physics simulation result.

- **Bounding Box (Physics Properties Editor):** Try to use collision primitives (sphere, cube, cylinder) rather than mesh-based collision boxes (triangle mesh or convex hull). The former will be more stable and perform faster.

- **Form Factor (Physics Properties Editor):** Controls the rotational tendency of an object. Setting this too small will make moving objects extremely unstable. Increasing the form factor usually helps calm down the object, at the cost of making the object feel sluggish on collision.

- **No Sleeping (Physics Properties Editor):** By default, this option is off, meaning objects "freeze" when their movement falls below a certain threshold for a certain time. Keeping the option off improves physics stability and performance.

- **Object Damping (Physics Properties Editor):** For non-static objects, Translational Damping and Rotational Damping can be used to slow objects down. Setting this to a non-zero value ensures that objects eventually will slow down to a stop, which might help with stability.

- **Margin (Physics Properties Editor):** If objects go through each other when they are not supposed to, and you've exhausted the other options listed above, increasing the object collision margin might help.
