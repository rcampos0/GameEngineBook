**Table of Contents**

- [Chapter 6: Physics](#Chapter_6_Physics)
	- [O que é Física?](#What_Is_Physics?)
	- [Overview](#Overview)
	- [Propriedades do Mundo](#World_Properties)
	- [Engine da Física](#Physics_Engine)
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
>O valor padrão de 60 é bom para a maioria dos aplicativos de jogos. Definir esse valor mais alto não oferece melhor desempenho. Também é comum para alguns jogos definir os fps para um valor mais baixo, como 30. A ideia é que um jogo rodando em 30fps constantes seja mais suave do que um jogo que flutua entre 30fps e 60fps. Além disso, você pode definir o vsync em sua placa gráfica para forçar um teto de taxa de quadros. Você não tem controle sobre isso no computador do jogador, no entanto.

## Physics Deactivation <a id="Physics_Deactivation"></a>

Os valores Limiar Linear, Limiar Angular e Tempo controlam a agressividade com que o mecanismo de física coloca os objetos "hibernando" para reduzir a carga no jogo.

Definir o tempo de desativação como 0 desativa efetivamente esta otimização. Como o sono também pode ser desabilitado por objeto no Editor de Propriedades de Física, geralmente não é recomendado desabilitar aqui.
Lower the Linear Threshold if an object comes to a stop earlier than expected.

Abaixe o limite angular se um objeto parar de girar antes do esperado.

## Physics Panel Settings <a id="Physics_Panel_Settings"></a>

Agora que você está familiarizado com o World Properties Editor, que contém configurações que se aplicam a todos os objetos físicos indiscriminadamente, vamos dar uma olhada no Physics Properties Editor. A partir daqui, você pode alterar as características físicas de objetos individuais.

As configurações físicas se aplicam a todos os tipos de objetos do jogo, incluindo malha, vazio, lâmpada e câmera.

## Physics Types <a id="Physics_Types"></a>

Como você decide que tipo de física escolher para um objeto? Isso depende muito do papel do objeto no jogo. A Tabela 6.1 mostra todos os tipos de física que estão disponíveis no Blender e suas características correspondentes.

|    Tipo         |    Colisão G,F,T      |    Rolo de uso típico                      |
| ----------------|:---------------------:|:-------------------------------------------|
| Nenhuma colisão | Não  Não  Não         | Efeitos, malha de alta resolução           |
| Estático        | Sim  Não  Não         | Edifícios, estruturas imóveis              |
| Dinamico        | Sim  Sim  Não         | Nenhum                                     |
| Corpo Rígido    | Sim  Sim  Sim         | Barris móveis, engradados, objetos gerais  |
| Corpo Macio     | Sim  Parcial  Sim     | Cabelo, pano, patinho de borracha          |
| Oclusor         | Não  Não  Não         | Paredes para otimização de desempenho      |
| Sensor          | Sim  Não  Não         | Gatilhos de Evento                         |
| Navigação       | Não  Não  Não         | Ajudante de Pathfinding                    |
| Personagem      | Sim  Não  Não         | Projetado especificamente para personagens |

Tabela 6.1: Tipos de Física
- **Collision**: Se o objeto detecta colisão.

- **G,F,T**: Se o objeto pode ser movido por gravidade, força e torque.

- **Roll**: Se os objetos rolam e tombam quando estão em uma inclinação.

Para se familiarizar com os diferentes tipos de física, abra o arquivo de demonstração disponível em /Book/Chapter6/demo/physicsTypes.blend. Mostra alguns dos tipos comuns de física e seu comportamento, conforme mostrado na Figura 6.15.

![Diferentes tipos de física visualizados](../figures/Chapter6/Fig06-15.png)

Vejamos as configurações com mais detalhes.

### No Collision <a id="No_Collision"></a>

No Collision pula todos os cálculos físicos. Os objetos serão efetivamente invisíveis para o mecanismo de física. Outros objetos não serão capazes de detectar a colisão com o objeto, nem colidir com ele. Nenhum objeto de colisão ainda pode ser movido usando o atuador de movimento. Use isso para objetos com os quais você não pretende interagir durante o jogo, como folhas de vegetação.

>**Collision Proxy**
>
>Definir um objeto como Sem Colisão pula completamente a detecção de colisão no objeto, o que pode acelerar o jogo consideravelmente em uma malha de polígono alto. Uma prática comum é definir a malha de polígono alto como Sem colisão e então criar manualmente um objeto de malha "proxy de colisão" simplificado que se aproxima da forma da malha de polígono alto. Em seguida, anexe a malha de polígono alto ao proxy de colisão usando os pais. Desta forma, a malha de polígono baixo será usada para todos os cálculos de colisão, que é rápido, e uma versão de polígono alto do objeto será usada para exibição, que é visualmente melhor. Como esta é uma técnica de otimização, um tutorial passo a passo sobre como criar um proxy de colisão é abordado no Capítulo 8.

### Static <a id="Static"></a>

Objetos estáticos são o tipo de física padrão para objetos. Eles não caem devido à gravidade, nem se movem por impacto externo, como outro objeto os atingindo. Por padrão, a própria malha é usada como malha de colisão, que pode ser lenta se o objeto tiver muitos polígonos. Objetos estáticos nunca se movem em colisão com outro objeto. Use esta configuração para objetos que requerem colisão, mas não se movem, como edifícios e estruturas fixas.

### Dynamic <a id="Dynamic"></a>

Os objetos dinâmicos são diferentes dos objetos estáticos porque têm uma massa definida e seguem a lei newtoniana básica de massa e aceleração. Eles caem devido à gravidade e reagem quando outro objeto colide com eles. Por padrão, o limite de colisão para objetos dinâmicos é uma esfera por motivos de desempenho. Às vezes, isso é suficiente, mas na maioria das vezes, é melhor usar outra forma como limite de colisão. Mais sobre limites de colisão no Capítulo 8. Além disso, como os objetos dinâmicos não rolam, sua utilidade é limitada. Se você deseja simular um objeto 3D realista, Rigid Body é o que você deseja.

### Rigid Body <a id="Rigid_Body"></a>

O corpo rígido se comporta de maneira muito semelhante a um objeto dinâmico: eles têm uma massa definida, aceleram devido à gravidade e reagem a colisões. Além disso, objetos de corpo rígido têm a capacidade de rolar quando necessário, enquanto um objeto dinâmico desliza desajeitadamente por uma rampa sem girar.

Se o modelo Suzanne no arquivo de amostra do Blender mencionado acima for definido como Corpo Rígido, ele se comportará como um objeto real, cairá em direção ao solo e parará em uma de suas orelhas.

>**Avoid DLoc Movement**
>
>Ao usar um objeto baseado em dinâmica (Dynamic, Rigid Body e assim por diante), você deve usar opções baseadas em física, como força e velocidade linear para movimento, e não alterar sua localização diretamente por dLoc.

### Soft Body <a id="Soft_Body"></a>

Enquanto todos os tipos de física descritos anteriormente operam nos objetos movendo-os e girando-os sem alterar a geometria subjacente, a física Soft Body usa um sistema de massa-mola para aplicar deformações à geometria real. Com Soft Body, você pode criar tecidos convincentes e outros objetos macios. Embora seja muito legal para brincar, Soft Body é muito computacionalmente intensivo em comparação com os outros tipos de física, e não é tão estável, então use-o com moderação.

Conforme visto no modelo Suzanne no arquivo de amostra, ele cairá devido à gravidade e, quando atingir o solo, desmorona como se fosse feito de uma casca de borracha. Este é o poder da física do Soft Body.

>**Apply Scale**
>
>O mecanismo de física funciona de forma mais confiável quando os objetos têm uma escala de 1. Portanto, é altamente recomendável Aplicar escala pressionando Ctrl + A na maioria dos objetos antes de executar o jogo. Isso evitará muitos dos problemas estranhos que podem surgir mais tarde.

### Occluder <a id="Occluder"></a>

Objetos oclusores não reagem à gravidade e à colisão. Sua única função é tornar invisíveis todos os objetos atrás deles. Os objetos Occluder são usados para ajudar o mecanismo de jogo a decidir quando remover objetos da vista para acelerar o desempenho de renderização. Os oclusores estrategicamente posicionados podem aumentar significativamente o desempenho do jogo.

A Figura 6.16 explica como funcionam os oclusores.

Da esquerda para a direita, a primeira imagem mostra a configuração da cena de /Book/Chapter6/PhysicsOccluder.blend. A segunda imagem mostra o que a câmera vê. Observe que a cabeça do macaco não está visível porque o avião a está bloqueando. A terceira imagem é a vista da mesma câmera durante o jogo, no modo wireframe. Observe que, embora a cabeça do macaco esteja atrás da parede, ela ainda está sendo renderizada, desperdiçando um precioso tempo de computação. A última imagem é a mesma visualização do jogo que a imagem anterior, mas com a parede configurada para Occluder, a cabeça do macaco não é exibida.

![Occluder culling](../figures/Chapter6/Fig06-16.png)

### Sensor <a id="Sensor"></a>

Semelhante ao objeto estático, um objeto Sensor detecta a colisão com outro objeto. É geralmente usado como um substituto para o sensor "radar" ou "próximo" porque um objeto Sensor pode ser feito em qualquer forma arbitrária. Além disso, os sensores detectam colisões, mas não registram uma resposta. Em outras palavras, eles se comportam como objetos fantasmas. Tijolos lógicos adicionais são necessários para utilizar um objeto Sensor com eficácia.

### Navigation Mesh <a id="Navigation_Mesh"></a>

Esta configuração transforma um objeto em um objeto auxiliar que é usado para navegação de pathfinding.

Desde o Blender 2.6, o motor de jogo tem uma rotina de pathfinding AI totalmente automatizada. Ele pode ser usado para direcionar um personagem de IA através do mundo 3D, alcançando um alvo, enquanto evita destruir.

#### Hands-on Tutorial: Navigation <a id="Hands-on_Tutorial_Navigation"></a>

1. Abra /Book/Chapter6/navigation.blend

2. Esta cena é configurada com quatro objetos (excluindo a lâmpada e a câmera).

3. _Monkey_ é nosso personagem principal; ele estará navegando pelo labirinto (o VisualMesh) para chegar ao alvo. Para ajudar em sua busca, criamos uma geometria auxiliar simples que descreve por onde o personagem pode andar. Este objeto é conhecido como _NavMesh_. A Figura 6.17 mostra a configuração inicial.

![Navigation system](../figures/Chapter6/Fig06-17.png)

4. Uma malha de navegação é um objeto auxiliar (invisível enquanto o jogo está em execução) que é usado para ajudar a guiar outros objetos ao longo de um caminho. O objeto NavMesh é um objeto de malha regular que define a forma da área acessível para a rotina de pathfinding.

5. Existem duas maneiras de criar uma malha de navegação. Uma é modelar manualmente uma geometria que cobre todas as áreas acessíveis a um personagem. Isso é o que fizemos com NavMesh.

6. Outra opção é pedir ao Blender para criar uma navegação automaticamente. Pode ser mais fácil para mapas maiores, mas o resultado é muito menos previsível. Abordaremos essa funcionalidade no final deste tutorial prático.

7. Certifique-se de que o objeto NavMesh esteja selecionado e altere seu tipo de física para Navigation Mesh. O NavMesh se transformará em uma grade colorida, mas não se assuste [md], isso é normal. Isso significa que o objeto agora pode ser usado para auxiliar na navegação. As malhas de navegação ficam invisíveis durante o jogo.

8. Selecione o objeto Monkey e adicione um atuador Logic Brick de "direção" a ele, conforme mostrado na Figura 6.18. Defina o alvo e o objeto de malha de navegação, conforme mostrado na Figura 6.19.

![Steering actuator setup](../figures/Chapter6/Fig06-18.png)

9. E pronto! Comece o jogo e observe o macaco procurar o cone. O Atuador de direção contém opções adicionais que você pode explorar.

10. A Figura 6.19 mostra o jogo finalizado rodando no motor de jogo do Blender. Você pode verificar navigation-ended.blend.

![Finished](../figures/Chapter6/Fig06-19.png)

11. Como prometido, outra maneira de criar uma malha de navegação é usar o gerador automático. Para fazer isso, exclua o NavMeshobject primeiro para que você possa começar do zero.

12. Selecione o objeto que deseja usar como guia na criação da malha de navegação. Nesse caso, você precisa selecionar VisualMesh. O Blender irá construir uma nova malha de navegação baseada nesta malha.

13. Vá para a guia Scene do Properties Editor, conforme mostrado na Figura 6.20. Você deve ver um botão "Build Navigation Mesh", junto com uma série de configurações.

![Automatic navigation mesh generation](../figures/Chapter6/Fig06-20.png)

14. Pressionar o botão mencionado criará uma malha de navegação automaticamente a partir da malha visual.

15. Se o resultado não for o ideal, brinque com as configurações. O agente Radius é um bom lugar para começar.

### Characters <a id="Characters"></a>

Este é um tipo de física especializado projetado especificamente para personagens controlados pelo jogador. Este tipo de física segue as regras básicas da cinemática, enquanto ignora algumas das outras regras físicas para tornar o comportamento do objeto mais previsível. Por exemplo, o tipo de objeto de personagem não ricocheteia nas paredes ou desliza nas rampas. PhysicsType.blend tem um exemplo de um objeto de personagem jogável que anda por aí. Tente movê-lo com as setas do teclado.

## Common Settings <a id="Common_Settings"></a>

Uau. Com todos os tipos de física fora do caminho, vamos dar uma olhada em algumas das configurações compartilhadas comuns à maioria dos tipos de física descritos anteriormente.

- **Actor:** Torna o objeto parte do ciclo de avaliação física. Um objeto não marcado como ator é ignorado pelos sensores Near e Radar, embora ainda obedeça às leis da física.

- **Ghost:** Faz com que um objeto não reaja a colisões de forma que passe por outro [md] como um fantasma. As colisões ainda são detectadas para objetos fantasmas, então quaisquer sensores que detectem a colisão entre dois objetos fantasmas ainda irão disparar, mas os objetos não irão se separar como normalmente fariam.

- **Invisible:** Pula a renderização do objeto enquanto ainda calcula toda a física e lógica. Isso é útil para criar paredes e bordas invisíveis de mapas para evitar que os jogadores visitem lugares que você não quer que eles vão.

- **Mass:** Define a massa do objeto. Um objeto mais pesado requer mais força para se mover. Ao contrário da intuição, um objeto mais pesado não cai mais rápido do que um objeto mais leve (veja a nota, "Martelo e Pena"). Portanto, aumentar a massa não fará seu objeto cair mais rápido. Para fazer os objetos caírem mais rápido, diminua o amortecimento no objeto ou aumente a gravidade nas configurações do mundo.

>**Hammer and Feather**
>>
>Um martelo e uma pena caem na mesma proporção no vácuo! No ar, a força de arrasto vai desacelerar um objeto mais leve mais do que um objeto mais pesado, então um objeto mais pesado realmente cai mais rápido do que um objeto mais leve. Porém, como o Blender não modela o atrito do ar, a massa do objeto não afeta a velocidade com que eles caem. Isso não é um bug!

Assim como um caminhão de 18 rodas batendo em um coelho não terá um final feliz (para o coelho), o mecanismo de física funciona melhor quando os objetos interagindo têm massas de magnitude semelhante. Quando um objeto com uma massa muito grande colide com um objeto com uma massa muito pequena, pode ser criada instabilidade no mecanismo de física. Como regra geral, mantenha todos os objetos dentro de 2 magnitudes de massa entre si. Portanto, se um objeto pesa 1,0, ele não deve interagir com um objeto muito mais pesado do que 100,0.

- **Radius:** Controla o raio da esfera de colisão. Se um limite de colisão diferente de Sphere for selecionado, esta configuração não terá efeito.

- **No sleeping:** Por padrão, o mecanismo de física suspende automaticamente o cálculo da física para um objeto quando seu movimento é suficientemente lento. Isso é conhecido como "dormir". Colocar o objeto para dormir pode liberar o ciclo da CPU e aumentar o desempenho do jogo até que outro objeto interaja com ele novamente. Colocar objetos para dormir pode causar alguns comportamentos estranhos, como objetos que se movem lentamente e param repentinamente. "Sem dormir" desativa esta otimização. A desvantagem é que "não dormir" pode levar a um comportamento estranho e nervoso para objetos que não são perfeitamente estáveis.

Além disso, existem opções para controlar quando os objetos vão dormir nas propriedades do mundo sob o rótulo "Desativação física". Essas configurações podem ser usadas para alterar o atraso global antes que os objetos sejam desativados.

- **Damping:** Aplica uma força de arrasto em um objeto. Um amortecimento de 0 corresponde a nenhum atrito, assim como uma vaca esférica viajando no vácuo. Um amortecimento de 1,0 corresponde a uma força de arrasto tão forte que o objeto será incapaz de se mover. O amortecimento translacional retarda o movimento de um objeto; o amortecimento rotacional diminui a rotação de um objeto.

- **Anisotropic Friction:** Controla a força de atrito por eixo. Você pode usar isso para imitar objetos que possuem coeficientes de atrito diferentes, dependendo da orientação do objeto. Por exemplo, um skate desliza facilmente ao longo de seu comprimento, mas é quase imóvel de lado.

- **Form Factor:** A dica de ferramenta diz que essa configuração "dimensiona o tensor de inércia". Faz sentido? Não? Bem, você não está feliz por ter este livro! O fator de forma controla a tendência de um objeto rolar. Quanto maior o valor, menor a probabilidade de um objeto rolar e tombar. Um valor menor torna o objeto muito mais provável de girar. Defina o valor muito baixo e o objeto se tornará instável. O valor padrão é um bom equilíbrio entre estabilidade física e realismo.

- **Collision Bounds:** Esta é a forma do objeto conforme aparece para o motor de física. Isso pode parecer surpreendente, mas a forma do objeto usado para cálculos físicos nem sempre é a mesma que é exibida. A distinção é importante porque, por motivos de desempenho, uma forma aproximada de proxy é freqüentemente usada no lugar da geometria real. Dessa forma, o usuário ainda vê um objeto totalmente detalhado na tela, mas o mecanismo de física pode funcionar muito mais rápido usando um limite de colisão simplificado. É importante tentar usar os limites de colisão mais simples possíveis para manter o desempenho do motor de jogo rápido.

- **Capsule** , **Box** , **Sphere** , **Cylinder,** e **Cone:** Essas são algumas das primitivas básicas que podem ser usadas para aproximar diferentes limites de colisão (consulte a Figura 6.21). Suas formas são autoexplicativas. Para ver exatamente como a caixa delimitadora é aplicada ao seu modelo no jogo, ative "Mostrar Visualização Física" na tela Opções do Jogo.

Quando o limite de colisão é definido como Convex Hull, o limite de colisão assume a forma do objeto, mas com todas as áreas côncavas preenchidas. Convex Hull pode aproximar com precisão um objeto de qualquer forma, desde que não tenha nenhum "negativo "espaço, como orifícios. Por exemplo, um objeto de corpo rígido em forma de rosca definido como Convex Hull será tratado como se o furo não existisse.

![Visualização de limites de colisão: Linha superior: caixa, esfera, cilindro; Linha inferior: cone, casco convexo, malha triangular](../figures/Chapter6/Fig06-21.png)

- **Triangle Mesh:** Este é o tipo de limite de colisão mais robusto. Isso criará um limite de colisão que é uma duplicata exata da malha real. Se você quiser garantir que o limite de colisão corresponda exatamente à malha visual, esta é a configuração a ser usada. Então, por que não usamos essa configuração o tempo todo? O motivo é desempenho e estabilidade. O mecanismo de física é muito melhor otimizado para primitivos simples, como uma caixa, do que uma malha de triângulo de forma arbitrária.

>**Visualizing Collision Bounds**
>
>Uma vez que o limite de colisão é definido, você deve notar que o limite de colisão é visualizado como linhas tracejadas na janela de exibição 3D. Isso ajuda a visualizar a relação entre os limites de colisão e a malha visual.
> Para visualizar os limites da colisão no jogo, ative "Mostrar Visualização Física" na tela Opções do Jogo e execute o jogo.

- **Collision Margin:** O Manual do Bullet Physics Engine SDK explica que a margem de colisão é uma configuração interna que melhora o desempenho e a estabilidade da detecção de colisão, dando espessura a cada face. É altamente recomendável que você não ajuste esta configuração fora de sua faixa normal (0,05). Em alguns casos, um valor muito alto resultará em um pequeno intervalo de ar entre os objetos em colisão. Um valor muito pequeno aumentará a chance de colisões perdidas entre objetos.

- **Compound:** A configuração composta faz com que os objetos vinculados por relacionamentos pai-filhos se comportem como se fossem uma única entidade física.

Mas, por que usar compostos quando você pode simplesmente unir seus objetos com Ctrl + J? Além do fato de que pode haver momentos em que você precisa controlar objetos individuais (então juntá-los pode não ser uma opção), usar limites de colisão compostos feitos de primitivas simples é realmente recomendado em vez de usar um limite de colisão de malha de triângulo. A razão é novamente que uma combinação de primitivas simples é mais rápida de calcular do que malhas de triângulo.

### Hands-on Tutorial: Creating Compound Objects <a id="Hands-on_Tutorial_Creating_Compound_Objects"></a>

Para criar um objeto de física composta (ver Figura 6.22):

1. Abra /Book/Chapter6/compound.blend.

2. Execute o jogo. Observe que, embora os três objetos sejam parentes, eles não reagem ao plano do solo de maneira convincente. Apenas o objeto pai colide com o solo.

3. Para mudar isso, no Editor de Propriedades de Física, ative Composto para cada um dos três objetos.

4. Execute o jogo agora e observe que todos os objetos contribuem para a cinemática do grupo.

![Física de objetos compostos](../figures/Chapter6/Fig06-22.png)

## Material Panel Physics Settings <a id="Material_Panel_Physics_Settings"></a>

Ao adicionar um material ao objeto, você ativa opções adicionais que fornecem um controle mais preciso sobre algumas das propriedades físicas da superfície. A Figura 6.23 mostra as configurações físicas encontradas no painel Material.

![Configurações de física de materiais](../figures/Chapter6/Fig06-23.png)

- **Friction:** Controla a força que desacelera um objeto em movimento quando ele entra em contato com outro objeto. A força de atrito efetiva entre dois objetos depende das configurações de atrito em ambos os objetos. Portanto, se um objeto com uma configuração de alto atrito entrar em contato com outro objeto com baixo atrito, a força de atrito efetiva estaria em algum lugar no meio dos dois valores.

- **Elasticity:** Controla o "salto" dos objetos quando eles colidem com outro. Um objeto com baixa elasticidade não rebate tanto após uma colisão; um objeto com alta elasticidade quase não perde impulso em uma colisão e salta quase na mesma velocidade em que entrou. A elasticidade efetiva entre dois objetos em colisão leva os dois objetos em consideração. Uma bola de tênis batendo em um piso de madeira seria um exemplo de um objeto elástico colidindo com outro objeto elástico. Uma bola de tênis atingindo o tapete seria um exemplo de um objeto elástico colidindo com um objeto não elástico.

- **Force Field:** O próximo conjunto de configurações controla o que o Blender chama de _ campo de força._ Quando a força e a distância são definidas como diferentes de zero, um campo de força é gerado em todas as faces para que qualquer objeto que esteja dentro do alcance (conforme especificado pela configuração de distância) é empurrado para longe com uma certa força (conforme especificado pela configuração de força). O resultado disso é que o objeto que se aproxima de uma superfície de campo de força será repelido. O efeito no objeto é exatamente o que o nome indica: ele imita um campo magnético. A configuração de amortecimento torna o objeto mais lento.

Depois que Force Field estiver habilitado no painel Material, você precisará dizer a objetos individuais para respeitar essa configuração acessando o Editor de Propriedades de Física e ativando Use Material Force Field.

### Hands-on Tutorial: Force Field Water Surface <a id="Hands-on_Tutorial_Force_Field_Water_Surface"></a>

O campo de força pode ser usado para criar um efeito de campo de força convincente [md] você adivinhou! [Md], onde um objeto se movendo em direção a um campo de força parece ser retardado por uma energia invisível. Isso é muito diferente das interações usuais de corpos rígidos, que são sempre colisões fortes.

Como você pode imaginar, a configuração Campo de força é usada para simular a interação realista de objetos flutuantes em uma superfície de água calma. Para fazer isso:

1. Abra /Book/Chapter6/water.blend.

2. Selecione o _Cube_. Você deseja que esse objeto se comporte como uma caixa de madeira básica, uma caixa que salta, tomba e flutua na água. Então, vamos adicionar alguma dinâmica a ele. Vá para o Editor de Propriedades de Física e defina o Tipo de Estático para Corpo Rígido.

3. Para diversão extra, vamos fazer muitos desses caixotes! Mas, em vez de criá-los manualmente, nós os adicionaremos dinamicamente no jogo sob o comando do jogador.

4. Selecione o objeto Camera no painel Logic Editor e adicione um novo sensor de teclado, um novo controlador And e um atuador Edit Object, conforme mostrado na Figura 6.24.

![Logic bricks](../figures/Chapter6/Fig06-24.png)

5. Para certificar-se de que os objetos de cubo sejam instanciados ao executar o jogo, você precisa ocultar o objeto de cubo original. Para fazer isso, basta mover o cubo para a segunda camada pressionando M e, em seguida, 2.

6. Com apenas a camada um selecionada, execute o jogo agora. Observe como todos os cubos colidem com o plano do solo, mas como o plano do solo é duro, o movimento é um tanto chocante. Não se parece com objetos flutuando na água.

7. Para fazer com que o plano terrestre tenha uma propriedade semelhante à da água, ligaremos o Campo de Força. Primeiro, selecione o objeto chamado _WaterPlane._

8. Vá para o Editor de Propriedades de Material e crie um novo material. Em seguida, simplesmente copie a configuração da física do campo de força, conforme mostrado na Figura 6.25.

![Configurações de física de materiais](../figures/Chapter6/Fig06-25.png)

9. Et voilà! Comece o jogo, pressione a barra de espaço e veja as caixas caírem no oceano.

10. Para adicionar realismo, crie um plano sem colisão no topo do WaterPlane para atuar como a superfície da água.

## Constraints <a id="Constraints"></a>

Restrições são freqüentemente usadas para criar juntas e ligações mecânicas, componentes indispensáveis de muitos jogos. O Editor de Propriedades de Restrições é mostrado na Figura 6.26.

![Adicionando uma junta de corpo rígido no Editor de propriedades de restrições](../figures/Chapter6/Fig06-26.png)

A única restrição de objeto suportada é a junta de corpo rígido. É usado para conectar dois objetos juntos usando uma junta definida pelo usuário.

A Figura 6.27 ilustra a variedade de tipos de pivô.

![Restrições ilustradas](../figures/Chapter6/Fig06-27.png)

- **Ball:** Une dois objetos usando uma articulação esférica. Este tipo de restrição pode girar livremente em torno dos três eixos.

- **Hinge:** Une dois objetos usando um eixo [md] o eixo da dobradiça. Essa restrição é freqüentemente usada para simular uma dobradiça de porta ou uma roda em um eixo.

- **Cone-twist:** Esta é uma extensão da restrição Ball que suporta a limitação do ângulo de rotação. Isso é especialmente útil para animar membros usando a física ragdoll. Você pode definir os limites de ângulo individuais para cada um dos três eixos.

- **Generic 6 DoF:** Se nenhuma das restrições acima atender às suas necessidades, é provável que essa restrição genérica lhe dê controle suficiente para realizar qualquer ligação mecânica que você possa imaginar.

Depois de decidir o tipo de pivô necessário, você precisará definir o objeto-alvo. O objeto Destino é o objeto ao qual o objeto atual será vinculado.

O restante das configurações deve ser autoexplicativo. Consulte /Book/Chapter6/demo/constraints.blend para ver cada tipo de restrição em ação.

- **Extending Constraints:** Embora uma restrição possa não ser muito útil, as restrições podem ser encadeadas para simular muitos objetos diferentes. Consulte ConstraintsChain.blend, ConstraintsWaterMill.blend e ConstraintsTrampoline.blend para exemplos de como configurar várias restrições.

## Vehicle Physics <a id="Vehicle_Physics"></a>

O mecanismo de física do Blender possui suporte integrado para a física do veículo. É um sistema de restrições físicas muito estável que fornece uma física de carro fácil de configurar. O resultado é um motor de física de veículo de desempenho rápido com configurações facilmente ajustáveis que mapeiam bem em um veículo real (direção, comprimento da suspensão, rigidez da suspensão)

Claro, você também pode tentar criar uma configuração de física do carro sem usar as restrições físicas integradas; no entanto, será muito mais demorado. Esta seção demonstrará como configurar um objeto de carro jogável no motor de jogo usando o motor Bullet integrado e um pouco de script Python.

### Hands-on Tutorial: Vehicle Physics Using Python <a id="Hands-on_Tutorial_Vehicle_Physics_Using_Python"></a>

Para começar, abra /Book/Chapter6/vehicle/car.blend.

Em vez de apresentar isso como um tutorial passo a passo, dissecaremos um arquivo pré-fabricado totalmente funcional.

Nosso carro básico é composto de um objeto de corpo e objetos de quatro rodas. As rodas estão separadas do carro por enquanto. O motor de física será responsável por manter as rodas presas ao corpo, portanto, a localização dos objetos da roda não importa neste momento. Nesse arquivo, eles são colocados próximos à carroceria do carro por conveniência.

Como a fixação das rodas ao corpo será feita por um script, é fundamental que a rotação da roda seja ajustada corretamente; caso contrário, a roda será ligada ao carro na orientação errada assim que o motor físico assumir. No arquivo de amostra, observe que todos os objetos de roda têm sua rotação definida para [0,0,0]. Isso é importante porque a rotação local nos objetos irá interferir com o motor de física e confundir o motor do jogo, resultando em um comportamento inesperado quando você tenta prender as rodas no carro. Se uma roda precisar ter sua rotação redefinida, pressione Ctrl + A para aplicar qualquer rotação.

Observe também que o corpo do carro é um objeto de corpo rígido com o fantasma ativado. Essa configuração é crucial para que a física do carro funcione corretamente.

É basicamente um objeto de corpo de carro e quatro pneus compõem o veículo.

Como já mencionado, a física real do veículo depende de algum script Python para funcionar. A Figura 6.28 mostra todos os blocos lógicos que estão anexados ao objeto da carroceria. Observe que o script desempenha um grande papel nisso.

![Vehicle logic brick setup](../figures/Chapter6/Fig06-28.png)

A funcionalidade script.carInit () é executada quando o jogo é iniciado. Aqui, ele inicializa o carro como uma "restrição de veículo", também conhecido como tipo de restrição 11, e o armazena como um objeto Python chamado _vehicle_. O mesmo script procura as quatro rodas acessando um atuador com nomes específicos (neste caso, wheel1, wheel2, etc.), e então o script anexa as rodas à carroceria do carro usando as configurações especificadas no script. Variáveis ​​como RollInfluence, SuspensionStiffness e TyreFriction podem ser definidas em uma base por pneu, uma vez que o objeto de veículo é criado. O trabalho de carInit () está concluído. A carroceria do seu carro agora é considerada um veículo pelo motor do jogo e se comportará como tal.

A segunda função mais importante, script.carHandler (), é executada a cada quadro. Este script faz o movimento real do carro e aplica a força do motor e direção ao objeto do veículo. Mas este script obtém a entrada do usuário (entradas do sensor do teclado) de outra fonte (veja abaixo). O wrapper do veículo possui métodos integrados, como applyBreaking (), applyEngineForce (), getWheelRotation () e getNumWheels, que você pode chamar.

Cada vez que uma tecla é pressionada, script.keyHandler () é executado. Ele descobre qual tecla é pressionada e define a variável intermediária para que a função scripts.carHandler saiba quanto acelerador aplicar, que direção dirigir e assim por diante. Este script é separado de scripts.carHandler () não por causa de limitações técnicas, mas por design, para que seja mais fácil gerenciar o código.

Com essas três funções Python, o carro ganha vida.

## Game Settings <a id="Game_Settings"></a>

As configurações do jogo são configurações globais que afetam o funcionamento do jogo. Essas configurações são mostradas na Figura 6.29 e podem ser encontradas no painel Render.

![Additional game settings](../figures/Chapter6/Fig06-29.png)

- **Animation Playback Speed:** Intimamente relacionada à configuração da taxa de quadros está a velocidade de reprodução da animação. Esta configuração controla a velocidade da curva F e da animação da armadura. Por padrão, o valor é definido como 24, o que significa que todas as curvas F e ações serão reproduzidas como se estivessem em execução em uma base de tempo de 24 fps. Essa configuração pode ser encontrada no painel Render.

- **Debug Property:** Mostra o valor das propriedades do jogo marcadas com o sinalizador Debug. Isso pode ser útil quando você deseja ficar de olho nos valores de certas variáveis enquanto o jogo está em execução.

- **Frame Rate and Profile:** Mostra a taxa de quadros e outras estatísticas de desempenho no jogo. Essas estatísticas serão exibidas no canto superior esquerdo da tela do jogo.

- **Physics Visualization:** Visualiza a computação interna do motor de física. Isso pode ajudá-lo a ver o que o mecanismo de física realmente está fazendo quando o jogo está rodando.

Os objetos de corpo rígido são exibidos em branco e os objetos adormecidos são desenhados em verde.

- **Deprecation Warning:** Dá avisos sobre API Python desatualizada chamada no console (consulte o Capítulo 7).

- **Mouse Cursor:** Desenha o cursor do mouse no jogo. Isso é útil se o jogo usa entrada do mouse. O cursor do mouse também pode ser ligado e desligado via Python.

## Stabilizing Physics <a id="Stabilizing_Physics"></a>

O motor de física do Bullet é bom. Muito bom. Mas, como com qualquer coisa que é alimentada por um computador, ainda é possível entrar em uma situação em que as coisas dão errado.

Ok, então o que é física instável, afinal? Quando você vê objetos se agitando quando não deveriam, ou quando objetos passam uns pelos outros quando deveriam colidir, você sabe que é hora de verificar a realidade.

Aqui estão algumas dicas para ajudá-lo a recuperar o controle do jogo. Todas as configurações aqui já foram abordadas no capítulo; esta lista é simplesmente uma coleção das ações mais comuns para estabilizar a física.

- **Avoid Extremes:** Evite a interação entre um objeto extremamente pesado e um objeto excepcionalmente leve. Evite a interação entre objetos extremamente rápidos. Evite a interação entre objetos de tamanhos muito diferentes, especialmente se nenhum dos objetos for estático.

- **Physics Substeps**** (Editor de propriedades do mundo): ** Ponha em marcha. Maior será mais lento, mas fornece um resultado de simulação de física muito mais preciso.

- **Bounding Box (Physics Properties Editor):** Tente usar primitivas de colisão (esfera, cubo, cilindro) em vez de caixas de colisão baseadas em malha (malha triangular ou casco convexo). O primeiro será mais estável e terá um desempenho mais rápido.

- **Form Factor (Physics Properties Editor):** Controla a tendência rotacional de um objeto. Definir muito pequeno tornará os objetos em movimento extremamente instáveis. Aumentar o fator de forma geralmente ajuda a acalmar o objeto, ao custo de torná-lo lento na colisão.

- **No Sleeping (Physics Properties Editor):** Por padrão, esta opção está desligada, o que significa que os objetos "congelam" quando seu movimento cai abaixo de um certo limite por um certo tempo. Manter a opção desativada melhora a estabilidade física e o desempenho.

- **Object Damping (Physics Properties Editor):** Para objetos não estáticos, o amortecimento translacional e o amortecimento rotacional podem ser usados para desacelerar os objetos. Definir isso para um valor diferente de zero garante que os objetos eventualmente irão desacelerar até parar, o que pode ajudar na estabilidade.
- **Margin (Physics Properties Editor):** Se os objetos passarem uns pelos outros quando não deveriam, e você tiver esgotado as outras opções listadas acima, aumentar a margem de colisão do objeto pode ajudar.
