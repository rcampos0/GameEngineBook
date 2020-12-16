**Table of Contents**

- [Chapter 4: Animation](#Chapter_4_Animation)
	- [Every Pot Has a Cover](#Every_Pot_Has_a_Cover)
	- [Animation Cycles](#Animation_Cycles)
	- [Moving Animation Cycles](#Moving_Animation_Cycles)
	- [Still Animation Cycles](#Still_Animation_Cycles)
	- [Actions and F-Curves](#Actions_and_F-Curves)
	- [Armature and Poses](#Armature_and_Poses)
		- [When to Use Pose Actions](#When_to_Use_Pose_Actions)
	- [Graphic Mesh vs. Physic Shape](#Graphic_Mesh_vs._Physic_Shape)
	- [Bone Constraints](#Bone_Constraints)
		- [Bone Constraints Not Supported](#Bone_Constraints_Not_Supported)
		- [Bone Constraints Supported](#Bone_Constraints_Supported)
			- [Transform](#Transform)
				- [Copy Location, Rotation, Scale](#Copy_Location,_Rotation,_Scale)
				- [Copy Transforms](#Copy_Transforms)
				- [Limit Distance, Limit Rotation, Limit Scale](#Limit_Distance,_Limit_Rotation,_Limit_Scale)
				- [Maintain Volume](#Maintain_Volume)
				- [Transformation](#Transformation)
			- [Tracking](#Tracking)
				- [Clamp To](#Clamp_To)
				- [Damped Track, Locked Track, and Track To](#Damped_Track,_Locked_Track,_and_Track_To)
				- [Inverse Kinematics](#Inverse_Kinematics)
					- [Legacy Solver](#Legacy_Solver)
					- [iTaSC Solver](#iTaSC_Solver)
				- [Stretch To](#Stretch_To)
			- [Relationship](#Relationship)
				- [Action](#Action)
				- [Child Of](#Child_Of)
				- [Floor](#Floor)
				- [Pivot](#Pivot)
	- [Bone Parenting](#Bone_Parenting)
	- [Shape Keys](#Shape_Keys)
		- [When to Use Shape Keys](#When_to_Use_Shape_Keys)
	- [Tutorials](#Tutorials)
		- [Pre-Tutorial](#Pre-Tutorial)
		- [Animation Cycle Tutorial](#Animation_Cycle_Tutorial)
			- [Armature Setup](#Armature_Setup)
				- [Inverse Kinematics Bone Constraints](#Inverse_Kinematics_Bone_Constraints)
				- [Track To Bone Constraints](#Track_To_Bone_Constraints)
			- [Extreme Poses](#Extreme_Poses)
			- [Moving Forward](#Moving_Forward)
				- [Root Bone](#Root_Bone)
				- [If Mohamed Won't Go to the Mountain…](#If_Mohamed_Won't_Go_to_the_Mountain…)
			- [Between Poses](#Between_Poses)
			- [Play Time](#Play_Time)
		- [Idle Animation](#Idle_Animation)
		- [Making a Face](#Making_a_Face)
			- [Shape Keys and Bone Drivers](#Shape_Keys_and_Bone_Drivers)
		- [Get Your Hands Dirty](#Get_Your_Hands_Dirty)
		- [Wiring Up the Logic Bricks](#Wiring_Up_the_Logic_Bricks)
		- [How Many Bricks Does It Take to Turn Momo?](#How_Many_Bricks_Does_It_Take_to_Turn_Momo?)
		- [Hats Off to Momo and Vice-Versa](#Hats_Off_to_Momo_and_Vice-Versa)
		- [Mango Jambo Special Animation](#Mango_Jambo_Special_Animation)
	- [To Learn More](#To_Learn_More)

# Capítulo 4: Animação <a id="Chapter_4_Animation"></a>

_Escrito em colaboração com Moraes Júnior - Mango Jambo para amigos [md] conhecido por seu trabalho como o animador do personagem principal no projeto de jogo aberto da Blender Foundation Yo Frankie._

A animação é o sopro da vida. É a alma de seus personagens. E juramos que não estamos inventando isso. Dê uma olhada na origem etimológica da palavra, e você verá que animação vem de _anima_, que significa _soul_ em latim. Tente se lembrar disso. Se por nada mais, ele pode ajudá-lo a parecer inteligente para a próxima pessoa que se pergunta por que você é pago para jogar videogame. A Figura 4.1 destaca o que a animação pode ser.

![Este capítulo é sobre o quê? Hmmm? Eu não consigo ver!](../figures/Chapter4/Fig04-01.png)

De volta ao caminho certo, neste capítulo você notará uma estrutura diferente dos capítulos anteriores.

Vamos primeiro falar sobre as principais ferramentas de animação e técnicas disponíveis. Esta parte será naturalmente densa, focando em quando e por que usar recursos de animação específicos. Mesmo para os animadores experientes do Blender, existem aspectos importantes do sistema de mecanismo de jogo que você precisa aprender porque nem todos os recursos disponíveis no Blender são traduzidos diretamente para o mecanismo de jogo.

A segunda parte é organizada como um tutorial. Trabalhei com o artista Moraes Júnior para expor seu fluxo de trabalho de animação. Nesta parte, revisitaremos os recursos de animação do motor de jogo e aprenderemos como um artista os integra em um ambiente de produção. Para esta parte, é especialmente importante que você siga as etapas nos arquivos do livro.

>**Keyframing a Keyframe**
>
>_Keyframe_ é usado como verbo e substantivo neste capítulo. O último (substantivo) refere-se aos quadros de animação que você criará manualmente. O primeiro (verbo) é a ação de criar esses quadros (por meio do atalho da tecla "I" ou do sistema de Gravação automática).

Para usar o sistema de animação corretamente, será útil saber como produzir animações surpreendentes. Para isso existe uma boa literatura disponível, seja ela específica do Blender ou não. Este livro não vai te ensinar como fazer belas animações. No entanto, queremos que você, o artista, entenda como animar para o motor de jogo.

>**Antes que você comece**
>
>Se esta é sua primeira vez trabalhando com animação no Blender, certifique-se de não pular o primeiro capítulo. A engine do jogo usa as animações criadas no Blender com Keyframes, F-Curves, interpolações e assim por diante. Para aprender a dominar a animação, você terá um melhor momento consultando um livro específico do Blender. No entanto, não custa refrescar sua mente em relação aos conceitos básicos e tópicos de navegação de interface cobertos no Capítulo 1.

## Cada panela tem uma tampa <a id="Every_Pot_Has_a_Cover"></a>

_Todo pote animado tem uma curva F._

Onde usamos animações em um jogo? O lugar mais óbvio é para a animação de personagens; por exemplo, sempre que o jogador anda, pula ou voa, você verá as animações do jogo em execução. Essa não é a única vez, porém, em que você verá animações. Você também os verá em cutscenes, elementos de fundo, a interface do usuário e assim por diante [md] a lista é interminável. Para cobrir uma ampla variedade de usos, existem três mecanismos que o motor do jogo fornece para animar os elementos do jogo: transformações de objetos, poses de armadura e chaves de forma.

- **Transformações de objeto** permitem que você altere transformações de objeto, como tamanho, rotação e localização.

- **Armatures** permitem trabalhar com uma estrutura de osso, malha deformada e configurações especiais de osso, como restrição de osso e parentesco de osso.

- **Shape keys** fornecem controle completo de transformação de malha.

Esses são sistemas diferentes, mas há muitas sobreposições entre eles. Mais importante, você frequentemente os usará juntos. Nas próximas páginas, falaremos sobre esses mecanismos individualmente e também veremos como eles se complementam. Nos aspectos práticos de como usá-los de forma eficaz, vamos nos concentrar na animação de personagens, que é a forma mais complexa de animação que você pode ter em seu jogo. Depois de compreender os conceitos de animação de personagens, você não terá dificuldade em dar vida aos elementos do seu menu, agitar seus ambientes e dirigir suas cutscenes.

Uma leitura estimulante espera por você. E que comece a diversão. Primeiro, vamos examinar um conceito fundamental para a animação de jogos [md] o ciclo de animação.

## Animation Cycles <a id="Animation_Cycles"></a>

Um ciclo de animação é geralmente uma ação curta que, quando repetida, produz a ilusão de um longo movimento contínuo. Um exemplo clássico é a animação ambulante de um personagem. Você não precisa animar o passo esquerdo, depois o passo direito, depois a esquerda, depois a direita ... ad infinitum. Uma ação com um passo para a esquerda e para a direita pode produzir o mesmo resultado. Apenas certifique-se de que a ação comece e termine na mesma pose, e você pode continuar reproduzindo em um loop.

Os ciclos de animação estão no centro da animação do personagem em um jogo. Uma biblioteca de várias animações pode fornecer um comportamento diversificado e rico para o personagem do jogo. Como referência, em um projeto de jogo como _Yo Frankie_, os personagens principais [md] Frankie e Momo [md] têm 87 e 70 ações únicas individuais, respectivamente. Algumas das ações que você pode encontrar são: Andar, Andar para trás, Andar mais rápido, Vire à esquerda, Vire à direita, Pule, Escolha, Jogue, Pule, Sono ocioso, Ocioso, Demonstração ociosa e muitas outras.

## Ciclos de animação em movimento <a id="Moving_Animation_Cycles"></a>

Muitas das ações básicas de um jogo podem ser expressas como ciclos de animação em movimento: andar, correr, girar, voar, rolar e nadar. Você deve ter notado que todos esses exemplos de ações também expressam a ideia de movimento no espaço. Entretanto, um ciclo de animação não tem nenhuma influência no deslocamento do objeto animado. Em vez disso, você obtém a aparência final da animação por meio de uma combinação de controle de movimento externo (por exemplo, um atuador de movimento) e a reprodução de um ciclo de animação. Na verdade, se você reproduzir apenas a ação de animação sozinha, verá que se parece mais com um exercício de esteira.

>**Ainda não está convencido?**
>
>O que estamos fazendo aqui é dividir a animação da pose do osso da animação do objeto. Poderíamos de fato fazer o personagem avançar movendo todos os ossos naquela direção. Embora isso tornasse a exibição da malha do objeto no lugar certo, não moveria o centro do objeto, o que resultaria em erros para os cálculos físicos e, eventualmente, para a exibição do próprio objeto. A caixa delimitadora da física é calculada em torno do centro do objeto, assim como o teste de seleção da câmera [md] a rotina que garante que os objetos fora do alcance da câmera não sejam renderizados.

## Ciclos de animação fixa <a id="Still_Animation_Cycles"></a>

Há casos em que você não precisa deslocar seu objeto enquanto reproduz suas animações, e nós os chamamos de _ ciclos de animação._ Um ciclo de animação sem o componente de deslocamento é como um cachorro perseguindo seu próprio rabo. E se é isso que você deseja animar, você precisa do ciclo de animação e nada mais. Na verdade, qualquer animação ociosa ou secundária pode ser usada diretamente sem a necessidade de um atuador de movimento. Por exemplo, se você estiver fazendo um ciclo de animação de respiração ou fazendo seu personagem bater os pés enquanto espera impacientemente por você fazer um movimento, toda a animação é controlada pelas poses da armadura. Mesmo que seu personagem precise se mover um pouco, você não usaria um atuador de movimento aqui. Nesses casos, certifique-se de que a pose final esteja na mesma posição da inicial.

## Ações e curvas F <a id="Actions_and_F-Curves"></a>

Uma ação no Blender é algo especial para animação. Por sua definição, uma ação é uma coleção de canais de Curvas F. Ele permite que uma propriedade (tamanho do objeto, posição do osso, etc.) tenha um valor diferente ao longo de quadros diferentes.

Mas o que são curvas F? Curvas funcionais são curvas criadas por pontos de controle (as posições do quadro-chave) e interpoladas para preencher o vazio. Como no Blender, no motor de jogo você não precisa definir um quadro-chave para cada quadro da sua animação. As partes da curva entre os quadros-chave serão calculadas com base nas configurações de interpolação e nos manipuladores de cada um dos quadros-chave.

Quando falamos sobre a ação de um objeto, estamos nos referindo à ação atual ligada a ele. Esta é a animação que será reproduzida quando você reproduzir a animação no viewport, ou se você renderizar a animação do Blender. Esta é também a ação na qual os quadros-chave são armazenados. Para jogar esta ação no motor do jogo, você precisa obter o nome da ação a ser usado no atuador de ação [md] selecione o objeto e você encontrará a ação na Folha de Dope quando definido para Action Editor.

>**Não perca sua ação**
>
>Se você quiser jogar ações diferentes para o mesmo objeto durante um jogo, você precisa criá-las no Blender. Uma ação é um bloco de dados que pode ser nomeado, removido, importado e vinculado como qualquer outro bloco de dados do Blender.
>É importante definir a opção Usuário falso (no cabeçalho da Planilha de Dope definida como Editor de ação) se você planeja desvincular uma ação de um objeto e criar um novo. Caso contrário, o software presumirá que você não precisa mais dessa ação e a removerá na próxima vez que você salvar e reabrir o arquivo.
>Além disso, você pode usar uma ação criada por um objeto em outro objeto, comprovando que eles são compatíveis. Para a maioria dos objetos, tudo o que eles precisam é ser do mesmo tipo. Para armaduras, eles também devem ter a mesma quantidade de ossos com os mesmos nomes. Para malhas com ações de chave de forma, os canais de chave de forma precisam ter o mesmo nome.

No início, não editamos uma curva diretamente no editor F-Curve. O fluxo de trabalho normal é primeiro enquadrar alguns parâmetros (por exemplo, posição e rotação) na visualização 3D. Depois de bloquear a chave e as posturas intermediárias, você pode fazer pequenos ajustes na curva. Este é o momento em que você pode ir para o editor da Curva F e fazer alterações diretamente nas curvas. Com alguma prática, você pode até olhar para o caos como na Figura 4.2 e ver bolas quicando e suaves fade-ins e fade-outs.

![Caos F-Curve](../figures/Chapter4/Fig04-02.png)

Mesmo quando estiver usando o atuador Action, você estará manipulando internamente as Curvas F (por meio do Dope Sheet ou, felizmente, da visualização 3D). As únicas ações que irão alterar a geometria do seu objeto são a ação de pose do osso e as ações-chave da forma. O primeiro executará a ação de pose de osso para sua armadura, enquanto o último desempenha uma ação chave de forma que afeta toda a malha.

Outras ações podem ser usadas para animar seu objeto como um todo, sem afetar sua geometria interna. Você pode mover o objeto, alterar seu tamanho, girá-lo e animar seus parâmetros de tipo específicos. Por exemplo, você pode animar uma câmera para seguir um caminho predeterminado ou animar uma lâmpada para piscar uma luz dinâmica de cor fraca. Sua câmera precisa trocar as lentes durante o jogo? Uma ação pode facilmente fazer isso por você.

## Armadura e Poses <a id="Armature_and_Poses"></a>

O sistema de animação do Bone funciona na engine do jogo de forma muito parecida com a do Blender. Você criará um objeto Mesh e um objeto Armature para deformar o primeiro.

>**Malha e Armadura**
>
>Ambos os objetos Armature e Mesh precisam estar presentes no jogo para que funcionem. Na verdade, se você estiver adicionando o objeto animado dinamicamente (por exemplo, por meio de um atuador Adicionar objeto), você se referirá ao objeto Armadura para trazer o conjunto animado.
>Como no Blender, o objeto Armature é o pai do objeto Mesh. Portanto, a armadura será o objeto do jogo executando a maioria dos sensores e atuadores de animação. Assim, você também pode despejar todos os blocos lógicos de seu objeto na armadura. Uma exceção é a opção Replace Mesh no Edit Object Actuator. Nesse caso, você precisa executar o Atuador no próprio objeto Mesh.

O fluxo de trabalho para Armadura e Bones se assemelha ao Editor NLA (Non-Linear Animation) no Blender. Você cria ações de animação individuais que deseja reproduzir em um determinado momento. Essas são as ações às quais nos referimos quando falamos sobre os ciclos de animação, no início deste capítulo.

A primeira diferença é que você não precisa predefinir a ordem e a duração de todas as ações que deseja jogar. Por exemplo, no Editor de NLA, se você deseja animar a curva de um tubarão, criará uma ação para "Natação em linha reta" e outra para "Curva". Você vai alternar entre eles com base em seu script: talvez o tubarão vire ao mesmo tempo que você joga a isca por perto.

>**Falando de NLA**
>
>Mesmo que a animação NLA não seja suportada no mecanismo de jogo, você ainda pode usar o Editor NLA para fazer suas sequências de animação. Cenas cortadas ou cenas de diálogo complexas podem se beneficiar muito de um fluxo de trabalho baseado em NLA.
>Por exemplo, você pode combinar ações de diálogo de um sistema MoCap (captura de movimento) com ciclos de animação de corpo ocioso pré-gerados. Uma vez que a edição da animação é feita, você precisa combinar as ações em uma única ação com o operador Bake Action, disponível através do Menu de Pesquisa (barra de espaço).

Ao contrário do NLA Editor, temos a chance de jogar ações com base nas decisões do jogador ou nas interações de IA predefinidas. Em nosso exemplo do tubarão, podemos ter o jogador controlando o tubarão e girando-o quando ele se cansar de nadar em linha reta. Talvez este tubarão goste de perseguir o rabo sem descanso. De qualquer maneira, podemos reproduzir e parar de reproduzir as animações individuais ("Straight_Swimming" e "Turning") a qualquer momento. A Figura 4.3 ilustra isso.

![Tubarão preso na ação de virada](../figures/Chapter4/Fig04-03.png)

A segunda diferença é com relação às restrições ósseas. Abordaremos isso com mais detalhes posteriormente. É importante saber que nem todas as Restrições de osso que funcionam no Blender funcionarão no motor de jogo. A maioria deles faz isso, então não deve ser muito incômodo. Além disso, o bone restrito e o bone alvo devem fazer parte da mesma armadura.

A terceira diferença é a simplicidade geral da armadura e do sistema ósseo. Em geral, os jogos têm rigging mais simples (como a armadura e o sistema ósseo são conhecidos) do que nos filmes de animação. Para jogos AAA, isso não é tão verdadeiro [md] que seus rigs estão mais próximos do filme do que os rigs de jogos tradicionais. No final das contas, a complexidade do rig também está diretamente relacionada à quantidade de polígonos que sua malha possui. Portanto, como os objetos do jogo naturalmente têm menos faces do que seus equivalentes em filmes de animação, o aparelhamento reflete isso.

Um bom exemplo é Frankie the Flying Squirrel no curta de animação _Big Buck Bunny_ e no jogo _Yo Frankie! _. Como você pode ver na Figura 4.4, o modelo original tinha 11.777 faces e 388 bones, enquanto o modelo refeito para o jogo tinha apenas 2.509 faces e 52 bones. Mesmo que o papel de Frankie tenha passado de personagem do filme paralelo para personagem principal do jogo, a complexidade do arquivo do jogo é muito mais simples. (A contagem de faces do arquivo de filme vai para 128.404 quando você aplica os modificadores de Superfície de subdivisão.)

![_Big Buck Bunny_ (left) and _Yo Frankie_ (right) rigging comparison](../figures/Chapter4/Fig04-04.png)

### Quando usar ações de pose <a id="When_to_Use_Pose_Actions"></a>

Sempre! O principal uso das ações de pose é aquele explicado anteriormente quando falamos sobre ciclos de animação. Ciclos de animação completos não serão os únicos em seu repertório de personagens.

Você não precisa ter todos os ossos colocados em todas as ações que deseja jogar. Imagine que você deseja ter uma animação de caminhada regular e permitir que o personagem olhe para trás enquanto caminha. Para esse tipo de situação, você pode animar os ossos da parte superior do corpo com uma ação diferente da das pernas e do quadril. Se as animações estiverem em ações separadas, você pode ativar e desativar as ações individuais (andar, olhar para trás) individualmente. Isso o poupará de fazer uma ação de animação para cada combinação possível de movimentos individuais (piscar, pular, andar, coçar a cabeça e assim por diante). Também torna mais simples controlar essas ações. Eles não precisam ter o mesmo comprimento ou ser chamados do mesmo atuador.

Personagens animados não são os únicos objetos do jogo que podem usar o sistema de animação de armadura. Você pode usar armaduras sempre que precisar de mais controle do que o atuador de movimento pode fornecer. Até mesmo um objeto simples como uma porta pode usar uma armadura para ajudar a abri-la e fechá-la. O problema com uma porta é que muitas vezes você precisa usar a porta como um objeto de colisão [md] para manter os três porquinhos protegidos do lobo. Isso nos leva ao nosso próximo tópico.

## Malha gráfica vs. forma física <a id="Graphic_Mesh_vs._Physic_Shape"></a>

Animar uma malha com ossos é uma tarefa relativamente cara para o computador. Portanto, quando você define um objeto para executar uma ação de pose, está alterando apenas a malha gráfica do objeto [md] a malha usada para a renderização do jogo. Todos os cálculos de física, no entanto, são feitos em outra instância dessa malha e não são atualizados com a animação. Na Figura 4.5 você pode ver a tela quando a opção Show Physics Visualization está ligada e o jogo tem uma armadura de objeto animada. A pose original de descanso da armadura é usada para a malha de física / colisão. Esta é a malha com os braços parados. Embora possamos ver a postura correta acima disso, esta não é a usada para os cálculos de física.

![Malha física não atualizada para malhas de armações](../figures/Chapter4/Fig04-05.png)

## Restrições ósseas <a id="Bone_Constraints"></a>

As restrições são um conjunto útil de ferramentas para facilitar o processo de animação. Eles são mais familiares aos riggers do que aos animadores, já que são usados ​​para construir armaduras mais fáceis de animar. Graças às restrições ósseas, podemos construir controladores ósseos para facilitar o trabalho com armaduras de jogo complexas. Devido a restrições como IK (Cinemática Inversa), podemos criar poses de maneiras muito simplificadas. Resumindo, as restrições de ossos pouparão você de animar todos os ossos individualmente, definindo relações entre eles.

A forma como as restrições ósseas funcionam no motor de jogo é bastante semelhante ao próprio Blender. Existem algumas diferenças, no entanto. Quando você define uma restrição de osso [md] por exemplo, a rotação de cópia [md], você define um osso a ser restringido a outro osso, o osso alvo. Nesse caso, o bone restrito copiará a rotação do bone alvo para cada pose, cada quadro. Ao contrário do Blender, no motor de jogo, o osso alvo e o osso restrito precisam fazer parte da mesma armadura.

No Blender, as restrições de ossos podem ser usadas de duas maneiras. A primeira e mais simples maneira é usá-los para ajudar na pose. Por exemplo, a restrição Track To bone ajuda a animar indiretamente as rotações dos olhos, animando o alvo para o qual os olhos estão olhando. Nesse caso, mesmo que você não esteja animando diretamente os ossos dos olhos, o processo de animação é muito mais intuitivo. É assim que você faz no Blender, e é assim que você vai fazer para o motor de jogo. Outra maneira de usá-los é configurando as restrições e animando seus valores de influência. Cada restrição óssea tem uma influência que varia de zero a um.

>**Influência da restrição óssea**
>
>Quando você inicia um jogo, a influência atual das restrições ósseas determinará o comportamento inicial da armadura. Se precisar alterá-lo durante o jogo, você pode usar um atuador de armadura com a opção Definir influência.

### Restrições ósseas não suportadas <a id="Bone_Constraints_Not_Supported"></a>

Como o bone restrito e o bone alvo precisam estar na mesma armadura, algumas restrições que dependem de curvas externas, dobradiças e objetos são incompatíveis com o mecanismo de jogo. Na versão atual do Blender, as restrições de osso não suportadas são: Spline IK, Follow Path, Rigid Body Joint, Script, Shrinkwrap e, parcialmente, ChildOf.

>**Articulação do corpo rígido parcialmente suportada**
>
>A junta rígida do corpo é suportada como uma restrição de objeto, mas não como uma restrição óssea. Você aprenderá como usá-lo no capítulo 6, Física.

### Suporta restrições ósseas <a id="Bone_Constraints_Supported"></a>

Todas as restrições de bone Transform, Tracking e Relationship que não foram mencionadas anteriormente podem ser usadas como você faria no Blender.

Na Figura 4.6, você pode ver o menu com todas as restrições ósseas compatíveis com o motor de jogo em destaque.

![Restrições ósseas suportadas](../figures/Chapter4/Fig04-06.png)

Se você não está familiarizado com as restrições ósseas, a seguir há uma breve visão geral delas e de suas funcionalidades. Como acontece com quase todos os outros recursos do motor de jogo, os usos sugeridos ilustram, mas não limitam sua aplicação potencial.

#### Transformar <a id="Transform"></a>

As restrições de osso de transformação ajudam a construir um sistema de controle de osso. Esta armadura de controle é uma armadura de alto nível, com apenas alguns ossos afetando diretamente a armadura real.

##### Copiar localização, rotação, escala <a id="Copy_Location,_Rotation,_Scale"></a>

Eles permitem que você copie parte da transformação e defina um deslocamento para a cópia. O osso não fica travado, permitindo ajustes adicionais da transformação do osso (ver Figuras 4.7a-c).

Um uso simples seria construir armaduras de controle com ossos duplicados entre as armaduras. Essas restrições ósseas permitem a sincronização das cadeias ósseas.

Um exemplo artístico de seu uso seria roupas ou armaduras. As cadeias de osso externas (para roupas) podem copiar a cadeia de osso de base (para o corpo) para usar como uma transformação de base. Como não há bloqueio, você pode animar os ossos externos independentemente da animação do corpo. O deslocamento pode ser usado para corresponder à separação real entre as geometrias do corpo e do tecido.

![Copiar restrição óssea de localização](../figures/Chapter4/Fig04-07a.png)

![Rotação de cópia, restrição óssea](../figures/Chapter4/Fig04-07b.png)

![Copiar restrição óssea de escala](../figures/Chapter4/Fig04-07c.png)

##### Copiar transformações <a id="Copy_Transforms"></a>

Diferente das restrições de bone anteriores, você não pode definir o deslocamento de bone nesta restrição, então com influência 1.0, o bone restrito e o bone de destino estarão exatamente no mesmo lugar (veja a Figura 4.8).

Como regra geral, uma influência diferente de 1.0 produz comportamentos mais interessantes.

![Copiar transforma a restrição óssea](../figures/Chapter4/Fig04-08.png)

##### Limite de distância, limite de rotação, limite de escala <a id="Limit_Distance,_Limit_Rotation,_Limit_Scale"></a>

Quando você usa uma transformação de osso para influenciar outro osso (por exemplo, controles deslizantes de osso ou drivers de osso), você está mapeando um intervalo de transformação (a posição de [0,0,0] a [0,1,0] no osso restrito [md] veja a restrição de osso de transformação). As restrições de limite de osso restringem o osso a transformações dentro do intervalo esperado a partir do qual estão sendo mapeados (veja as Figuras 4.9a-c).

Eles também podem ser usados para complementar as restrições de localização / rotação / escala do osso copiando a transformação, mas limitando alguns dos parâmetros (por exemplo, copiar o local, mas não permitir que Z fique abaixo de zero [md] sob o osso usado como referência de base )

![Limite de restrição óssea de distância](../figures/Chapter4/Fig04-09a.png)

![Limite de restrição óssea de rotação](../figures/Chapter4/Fig04-09b.png)

![Limi Scale bone constraint](../figures/Chapter4/Fig04-09c.png)

##### Manter o Volume <a id="Maintain_Volume"></a>

Esta restrição óssea não usa um alvo (veja a Figura 4.10). A transformação acontece apenas dependendo do próprio osso (e dentro do eixo oposto ao eixo Livre selecionado).

É usado para squash e stretch, o efeito clássico de desenho animado para apertar bolas quicando.

![Manter restrição óssea de volume](../figures/Chapter4/Fig04-10.png)

##### Transformação <a id="Transformation"></a>

Esta é a melhor restrição óssea para controles deslizantes. Ele permite que você mapeie a transformação do bone alvo em uma transformação completamente diferente do bone restrito. Por exemplo, você pode mapear a faixa de localização de um bone alvo (slider) de [0, -1,0] a [0,1,0] na rotação do bone restrito de -90 graus a 90 graus (ver Figura 4,11).

Nos arquivos do livro, você pode ver este exemplo de um controle deslizante de osso em que usamos Limite de localização, Transformação, Rotação de cópia e uma Restrição de limite de rotação de osso para configurar um braço simples. Não é o uso ideal dessas restrições ósseas, mas mostra como elas podem ser configuradas juntas.

![Restrição óssea de transformação](../figures/Chapter4/Fig04-11.png)

Você pode encontrar o arquivo em _\Book\Chapter04\1\_constraints\_transform.blend_ (consulte a Figura 4.12).

![Controle deslizante de osso](../figures/Chapter4/Fig04-12.png)

#### Rastreando <a id="Tracking"></a>

Uma restrição de bone rastreada pode fazer parte de sua armadura principal ou de seus bones de controle. Por exemplo, é comum ter a restrição de bone Inverse Kinematics em um bone que faz parte da cadeia. Ao mesmo tempo, o Track To freqüentemente usa um osso não conectado à corrente e não deformando nenhuma malha diretamente.

##### Grampo para <a id="Clamp_To"></a>

A restrição Clamp To bone força o bone ao longo de um objeto de curva (veja a Figura 4.13). O osso precisa ser desconectado da corrente do osso para restringir adequadamente sua localização na curva.

É muito útil para animação de ambiente cíclico de ativos de seu jogo. Por exemplo, você pode fazer pássaros voando no céu tendo uma curva predefinida para os ossos seguirem. Carros dirigindo ou mesmo pessoas andando em segundo plano também podem ser realizados com essa técnica.

![Restrição de grampo para osso](../figures/Chapter4/Fig04-13.png)

##### Pista Amortecida, Pista Bloqueada e Pista Para <a id="Damped_Track,_Locked_Track,_and_Track_To"></a>

Essas três restrições ósseas funcionam de maneira semelhante. Você seleciona um osso alvo [md] onde o osso restrito estará voltado para [md] e um eixo indicando a direção interna para apontar para aquele alvo. A diferença é quanto controle manual sobre a rotação do osso você precisa após configurar a restrição do osso. Enquanto o Track To bloqueia completamente a rotação do osso restrito, o Damped Track o mantém completamente livre para transformações no topo da influência da restrição do osso.

O Damped Track oferece mais liberdade entre eles e é o mais simples de configurar. Você só precisa selecionar o eixo a ser travado, e isso permite ajustar a rotação de qualquer eixo do osso restrito (veja a Figura 4.14). Você pode ver um exemplo disso usado em olhos robóticos. O efeito básico é rastrear um objeto alvo. Mas você ainda pode girar os olhos para um efeito extravagante, quero dizer, clássico "alvo de andróide bloqueado".

![Restrição óssea de trilha amortecida](../figures/Chapter4/Fig04-14.png)

Trilha bloqueada funcionará como um meio-termo entre os outros dois rastreadores. Ele permite que você ajuste a rotação do eixo não rastreado (consulte a Figura 4.15). Uma câmera de segurança pode ser simulada com essa restrição óssea. Um eixo principal é rastreado pela câmera (por exemplo, fazendo uma rotina de rotação horizontal), enquanto os outros eixos são controlados / animados independentemente.

![Restrição de osso de trilha bloqueada](../figures/Chapter4/Fig04-15.png)

Track To bloqueia o osso restrito para qualquer ajuste de rotação, deixando sua rotação ser controlada inteiramente pela restrição do osso (consulte a Figura 4.16). Por padrão, ele gira apenas um eixo. No entanto, você pode rastrear o outro eixo do osso definindo Target Z neste painel de restrição de osso. O uso clássico disso é para os olhos. Em vez de girar os ossos do olho diretamente, você pode configurá-los para rastrear um osso-alvo para o qual os olhos estarão fixos.

![Restrição de faixa para osso](../figures/Chapter4/Fig04-16.png)

##### Cinemática Inversa <a id="Inverse_Kinematics"></a>

A restrição de bone IK (cinemática inversa) ajuda a ignorar a arquitetura FK (Cinemática direta) dos bones de armadura. FK é projetado para mudanças individuais de rotação ao longo da cadeia óssea (do pai para os filhos). Para alterar a localização de um osso, você precisa girar todos os ossos que levam a ele e certificar-se de que a rotação resultante coloque o osso no local desejado (consulte a Figura 4.17).

É muito fácil perder-se indo e voltando para ajustar a posição dos ossos. Vejamos um braço rig como exemplo. Uma armadura simples teria um osso do ombro como pai e o braço, antebraço e mão como filhos. Se quiser colocar a mão em um lugar específico, você precisa girar o ombro, girar o braço e, finalmente, girar a mão. Se você calculou mal a extensão do braço e seu raio de extensão, você precisa voltar e girar a mão novamente, fazendo o ajuste fino.

Com IK, você só precisa mover a mão para o local de destino. A rotação do antebraço, braço e ombro será calculada automaticamente pelo Blender.

![Restrição óssea de cinemática inversa](../figures/Chapter4/Fig04-17.png)

O osso alvo não pode ser pai ou filho de qualquer osso restringido por esta restrição óssea [md], isso produz efeitos cíclicos imprevisíveis. Isso inclui não apenas o osso onde você adicionou o IK, mas também quantos ossos você definir no comprimento da sua corrente. (Deixar como zero influencia toda a cadeia óssea.)

###### Legacy Solver <a id="Legacy_Solver"></a>

Por padrão, o Blender usa o solver Legacy para os cálculos da Cinemática Inversa. É assim que a maior parte do software de animação funciona e como os animadores costumam trabalhar.

Quando um osso está sob a influência de uma restrição IK Bone, você pode definir configurações específicas de IK no painel Bone, como você pode ver na Figura 4.18.

![Inverse Kinematics Bone panel](../figures/Chapter4/Fig04-18.png)

Esses parâmetros permitem adicionar algum controle sobre os cálculos IK, de outra forma automáticos.

- **Limit** : No braço, você precisa ter certeza de que os ossos se comportam como os ossos reais. Por exemplo, na vida real você não pode torcer o cotovelo acima de certos limites. Para imitar esse comportamento, você pode forçar a rotação de um osso dentro de um determinado intervalo. Em nosso caso, os limites seriam definidos: X: 5 graus a 180 graus; Y: -90 graus a 90 graus; Z: 0 graus a 0 graus.

- **Stiffness:** Este parâmetro define o quão difícil é girar o osso. Valores altos fazem um osso girar menos. A rigidez articular pode ser um dos primeiros sintomas da artrite. Portanto, cuide de seus personagens.

- **Stretch:** Os braços dos desenhos animados geralmente precisam se esticar além de seus tamanhos originais. O fator de alongamento deve ser definido por osso. (O alongamento também precisa ser ativado na restrição óssea, mas está ativado por padrão.)

Ao contrário da restrição Esticar até o osso, o volume do osso não é totalmente preservado ao usar o alongamento IK. Em outras palavras, o braço parece gordo quando esticado. Para usar o alongamento IK e a restrição Stretch To bone, você precisa configurar duas cadeias de osso separadamente: uma para IK e a outra [md] com Stretch To [md] para deformar a malha. O Stretch To é o que preserva o volume correto para os ossos. Você pode ver um arquivo de amostra na seção Esticar para mais adiante neste capítulo.

>**Target-less Bone Constraint**
>
>Se você não selecionar um destino para a restrição de osso, ainda poderá usar o IK de uma maneira especial. Nesse caso, o osso restrito é o alvo próprio e, como tal, pode ser colocado em qualquer lugar. Essa técnica, conhecida como _fake IK, _ é muito leve em termos de computação. No IK tradicional, você define o quadro-chave apenas o osso alvo, portanto, o cálculo de IK deve ser executado toda vez que você reproduz a animação. Com IK falso, o cálculo é válido durante a transformação (quando você está movendo o osso alvo). Você tem que definir o quadro-chave de todos os bones restritos individuais para que isso funcione. (Isso é feito automaticamente quando AutoKey é habilitado no editor de linha de tempo.) Como não há IK acontecendo quando você reproduz a animação, o cálculo de IK falso é muito superior ao IK real.

###### iTaSC Solver <a id="iTaSC_Solver"></a>

Além disso, você pode alterar o solucionador IK no painel Armadura para usar o iTaSC. Este nome significa _Instantaneous Task Specification using Constraints._ Este solver IK foi desenvolvido especialmente para robótica, mas pode ser usado como um substituto mais avançado para o antigo solver IK (Legacy).

O cálculo ou a estrutura da armadura são calculados em tempo real, com base em restrições predefinidas e um alvo dinâmico. É um sistema muito poderoso, mas não está diretamente relacionado ao paradigma mais tradicional de armadura, ossos e pose de animação. Nenhum quadro-chave é necessário aqui.

O solucionador iTaSC é mais rápido do que o Legacy e definitivamente melhor no tratamento de restrições dinâmicas reais (consulte a Figura 4.19).

![iTaSC Bone panel](../figures/Chapter4/Fig04-19.png)

As outras restrições ósseas são ótimas para ajudá-lo a animar sua armadura, mas não são tão eficientes em lidar com as mudanças em tempo real na armadura para produzir movimentos dinamicamente plausíveis. Se você gosta de robótica ou simplesmente deseja explorar configurações mais avançadas neste solucionador, consulte a documentação oficial:

_http: //wiki.blender.org/index.php/Dev: Source/GameEngine/RobotIKSolver_

##### Stretch To <a id="Stretch_To"></a>

Um osso alongado permite que você produza transformações corporais de desenho animado (consulte a Figura 4.20). Diferente de um osso escamado, um alongado mantém seu volume. O osso alvo precisa ser completamente isolado e não conectado ao osso restrito. Não pode ser filho ou pai.

Nos arquivos do livro, você pode encontrar um exemplo de uma técnica mais avançada que integra as restrições de bone Stretch To, IK e Copy Rotation. Estude-o cuidadosamente; mais instruções estão dentro do arquivo _\Book\Chapter04\2\_cartoon\_arm.blend_.

![Stretch To bone constraint](../figures/Chapter4/Fig04-20.png)

#### Relationship <a id="Relationship"></a>

A seguir estão as restrições ósseas que são menos suportadas. Ironicamente, além do nome da categoria, não há muita relação entre eles.

Uma restrição de bone que vale a pena mencionar é a restrição de bone de ação. Com ele, você pode executar ações completas na armadura movendo um único osso. Dada a complexidade dessa restrição, a parte de exemplo deste texto evoluiu como um pseudo-tutorial. Digo _pseudo-tutorial_ porque não estamos trabalhando em nenhum arquivo, embora você deva ser capaz de seguir as instruções e reproduzir o efeito sozinho.

##### Action <a id="Action"></a>

Com a restrição Action bone, você pode reproduzir uma ação inteira controlando um único bone (veja a Figura 4.21). Certifique-se de que o osso alvo não seja animado na ação que você está jogando; caso contrário, isso produzirá resultados imprevisíveis. Como essa é uma restrição de osso mais complicada, a melhor maneira de mostrar os possíveis usos é por meio de um pseudo-mini-tutorial, como você verá a seguir.

![Action bone constraint](../figures/Chapter4/Fig04-21.png)

Um exemplo de uso é para animações do tipo Transformers. Digamos que você precise criar um personagem semelhante ao Optimus Prime. A armadura tem duas poses básicas muito distintas: um carro normal e um robô durão. Alguns de seus ciclos de animação acontecerão na forma de carro e outros no robô.

Você primeiro cria uma ação separada com dois extremos [md] a conformação do carro e dos ossos do robô. A própria ação contém a transformação entre essas duas formas.

Agora você cria um bone [md] desconectado da cadeia principal [md] para controlar a influência desta ação sobre a pose do bone. Este osso será usado como um alvo nas restrições de osso de ação que você precisa criar para todos os ossos (e com isso quero dizer criar uma restrição de osso, configurá-la corretamente e copiar para os outros ossos).

>**Slider-like Controllers**
>
>Este é realmente um uso clássico de um controlador de osso como um controle deslizante. Uma vez que apenas uma das transformações do osso (Localização X) será usada para influenciar a ação jogada, você pode até mesmo bloquear as outras transformações de pose (Localização YZ, Rotação XYZ, Escala XYZ) e criar uma restrição de localização limite para este osso . Na Figura 4.22 você pode ver um exemplo dessa configuração.

![Bone constraint slider](../figures/Chapter4/Fig04-22.png)

Depois que toda a configuração estiver feita, você só precisa se preocupar com o osso alvo quando precisar alternar entre as poses. Mova o osso para a esquerda e você terá um carro. Mova-o para a direita e você terá um robô. Anime o osso indo da esquerda para a direita e você poderá integrar a animação "Transformers" como parte de qualquer outra ação.

Outro uso para essa restrição de bone é reproduzir duas ações que influenciam os mesmos bones ao mesmo tempo. Esta é uma solução para a limitação do motor de jogo de ser capaz de jogar apenas uma ação que influencia um osso por vez. Nos arquivos do livro, você pode ver uma amostra disso em _\Book\Chapter04\3\_action\_constraint.blend_. Observe no arquivo que cada atuador de ação é definido em sua própria camada, para que possam ser empilhados juntos para o mesmo objeto.

##### Child Of <a id="Child_Of"></a>

_É apenas parcialmente suportado._

A capacidade de definir relações parentais dinamicamente para bones durante o jogo é essencial para algumas animações. Imagine que você está construindo um jogo de samurai. Nos momentos sem luta, a espada estará dentro de uma bainha e, portanto, deve ser dada como pai a ela. Durante o combate, a espada se moverá da bainha para as mãos do samurai. A partir desse ponto, a espada deve ser direcionada às mãos para que siga sua posição e rotação durante a animação das cabeças de corte.

O osso para ser pai dinâmico (por exemplo, o osso da espada) não precisa ter nenhuma transformação no modo Pose (ele precisa estar em sua origem local [0,0,0] e com rotação zero). Também não pode ter um pai, a não ser os definidos dinamicamente pela restrição.

No Blender, você pode ter várias restrições de osso filho de e alternar entre o pai atual para um osso. No motor de jogo, entretanto, como você não pode animar a restrição de influência do osso, o uso não é tão flexível. No final, você o usará como se fossem as restrições ósseas Copy Transformations. A diferença é que o Filho de permite que você selecione quais transformações copiar (por exemplo, Localização e Rotação), e sua opção Definir Inverso é semelhante à opção Deslocamento das restrições ósseas de Copiar Localização, Rotação e Escala (ver Figura 4,23).

![Child Of bone constraint](../figures/Chapter4/Fig04-23.png)

Outra opção para este tipo de animação é usar parentalidade óssea. Com isso, a espada pode até ser um objeto da Física e interagir com outros elementos do jogo. Isso é abordado no último tutorial deste capítulo, intitulado "Tiremos o chapéu para Momo e vice-versa".

>**Not Supported Yet Useful**
>
>Tal como acontece com as outras restrições ósseas não suportadas adequadamente no motor de jogo, você ainda pode usá-lo totalmente para ajudar a animar no Blender. No entanto, você precisará preparar as transformações ósseas restritas para ver as mudanças no mecanismo de jogo. Este tópico é abordado posteriormente no Capítulo 8, "Fluxo de Trabalho e Otimização, Capítulo 8."

##### Floor <a id="Floor"></a>

O piso permite que você crie um plano imaginário ao qual restringir suas transformações ósseas. Ele cria o equivalente a um piso, teto ou parede que não pode ser transposto. O local da pose do osso restrito deve ser limpo para que a fixação ao plano funcione (Alt + G). Veja a Figura 4.24.

![Floor bone constraint](../figures/Chapter4/Fig04-24.png)

##### Pivot <a id="Pivot"></a>

Essa restrição de osso ajuda a girar os ossos em torno de um osso específico. Um exemplo seria criar uma animação de chave de fenda. A posição do parafuso seria representada por um osso usado como pivô (o osso alvo nesta restrição de osso). A mão com a chave de fenda teria sua rotação travada no pivô. Para fazer a influência se propagar através da cadeia óssea, você precisaria que o osso da mão tivesse uma restrição óssea IK (consulte a Figura 4.25).

Dado que muitas vezes o parafuso não fará parte da malha diretamente deformada pela armadura (a menos que você esteja animando Frankenstein se preparando para um teste de QI), o osso Pivot pode ser o pai de um objeto externo que você usa como um espaço reservado para o parafuso . Mais sobre isso na próxima seção.

![Pivot bone constraint](../figures/Chapter4/Fig04-25.png)

## Bone Parenting <a id="Bone_Parenting"></a>

Não é Vegas, mas o que acontece na armadura permanece na armadura. Então, como você faz sua animação afetar outros objetos? A armadura afeta a malha deformada, mas não é tudo.

A paternidade óssea permite que você sincronize eventos externos com a animação interna. É um recurso muito simples, semelhante à parentalidade objeto a objeto. A diferença aqui é que você atribui um objeto a um osso. Sempre que você anima a armadura, a posição do bone será copiada para o objeto filho. Este objeto filho realmente atua como um pai para outros objetos. Ele funciona como uma extensão integrada da armadura para o mundo do jogo.

Anteriormente, ao falar sobre armadura e poses, mencionamos que a malha física de sua malha deformada não é deformada. No entanto, você ainda pode usar a paternidade óssea para interagir fisicamente com o seu mundo.

Vejamos um exemplo. Imagine que você precisa pegar um elemento (uma chave, uma moeda) em seu jogo com a mão de seu personagem. Você começa animando a armadura do braço e as malhas do braço como faria normalmente. Em seguida, você precisa de um objeto vazio ligado ao osso da sua mão e colocado bem em cima dele. Este vazio será seu objeto. Ele se moverá automaticamente com sua mão e pode ser usado com qualquer Logic Brick que você quiser.

Depois que sua mão pegar a chave, você precisa se certificar de que a chave não caia no chão ou caia em um ralo e encontre seu fim ao lado de moedas enferrujadas, baratas e meu velho yoyo.

Assim que o objeto Collision (nosso vazio pai) toca o objeto alvo, você pode definir este objeto para ser temporariamente pai deste vazio (que então é pai do osso da mão). Agora, se você continuar reproduzindo a animação "pegando a chave", terá o elemento de destino sempre "à mão". Para obter mais detalhes e instruções, consulte o tutorial "Tiramos o chapéu para Momo e vice-versa".

No jogo _Yo Frankie! _, Eles usam esse recurso de maneira semelhante. Ambos os personagens principais [md] Frankie e Momo [md] têm um parente vazio até o osso do pulso. Quando o jogador tenta pegar algumas nozes ou ovelhas, o jogo chama um script Python para controlar essa interação. Internamente, um sensor de colisão verifica se o objeto escolhido está perto do jogador e o direciona para o "Lançamento do Carregador de Lugar", o vazio parental ósseo. Na Figura 4.26, você pode ver o "Throw Place Carry" de Momo vazio no meio da animação de arremesso.

![Momo bone-parenting system](../figures/Chapter4/Fig04-26.png)

## Shape Keys <a id="Shape_Keys"></a>
Às vezes, a animação do osso pode não fornecer controle suficiente sobre a deformação da malha. Nesses casos, você pode animar a malha diretamente por meio das teclas de forma. Assim como no Blender, você pode definir múltiplas formas de teclas representando diferentes poses para seu personagem. Cada pose mantém a posição de todos os vértices de sua malha.

O fluxo de trabalho com chaves de forma é diferente das animações de armadura. Você começa a definir sua pose base e, além disso, cria variações de pose. Se você alterar sua geometria posteriormente, será um processo doloroso mesclar a alteração de volta a todas as poses criadas anteriormente, portanto, certifique-se de que sua malha esteja pronta antes de criar suas formas.

>**Shape Keys Performance**
>
>O nível de controle que você obtém com as Shape Keys tem um preço. O desempenho necessário para o cálculo por vértice é consideravelmente mais pesado do que o controle de armadura regular. Portanto, você não deve abusar dessa técnica.

### When to Use Shape Keys <a id="When_to_Use_Shape_Keys"></a>

Use as teclas de forma sempre que a animação for muito complexa para animações de armadura. Essa não é toda a história, no entanto. As animações de chave de forma são frequentemente integradas às animações de armadura tradicionais, não como algo separado. Eles podem funcionar como animações independentes, é claro; há de fato um atuador dedicado apenas a isso. No entanto, a maior aplicação das chaves de forma não é substituir a animação do osso, mas complementá-la.

O uso mais popular é para animação facial de personagens. Você pode criar uma pose de rosto para cada posição extrema de suas expressões e contar com interpolações básicas entre as poses para simular a animação. Isso pode ser usado para aplicações específicas, como sincronização labial, para animação geral, como expressão de estados de espírito (felicidade, tristeza, segunda-feira).

No jogo _Yo Frankie_, ambos os personagens principais usaram animações chave de forma junto com armaduras. Momo usou seis poses de forma para ajudar em suas animações. Os mais simples ajudam a piscar os olhos. O que seria o nosso macaco fofo se não pudesse piscar para seus companheiros? Na Figura 4.27, você pode ver a pose da base Momo e variações dela criadas mudando apenas a influência das quatro posturas dos olhos [md] pálpebras para cima, para baixo, sobrancelha para cima e sobrancelha para baixo.

![Momo blinking shape key poses](../figures/Chapter4/Fig04-27.png)

>**Isn't This Overkill?**
>
>Você pode estar se perguntando se essas poses poderiam ter sido criadas com poses regulares de ossos. Pode apostar que sim. No entanto, o projeto _Yo Frankie_ tem uma importante missão educacional. Um dos objetivos do projeto era demonstrar os múltiplos recursos do motor de jogo. Na verdade, o suporte para chaves de forma na engine do jogo foi implementado especificamente para este projeto. Assim, esses arquivos são a primeira referência que os animadores estudaram sobre como usá-los.

As poses restantes [md] Smile e Ooh [md] são um pouco mais complexas. Eles são extremos opostos da mesma animação de chave de forma com a pose Natural entre eles. Momo pode ser sorridente, natural ou ooh'ing. Como o último não é um verbo real, dê uma olhada na Figura 4.28 para apreciar melhor todo o apelo sexual do macaco. Seria difícil obter esses resultados sem adicionar muitos ossos, o que criaria um sistema difícil de animar. Portanto, as teclas de formato são uma solução muito mais elegante.
![Momo shape keys poses: ooh, basis, and smile](../figures/Chapter4/Fig04-28.png)

Frankie, o esquilo voador, também usa formas para algumas expressões faciais e para controlar suas asas. Como Momo, seria muito difícil controlar a deformação das asas usando apenas ossos. Portanto, uma pose de forma foi criada para mostrar como a malha deve ser quando a asa está dobrada. Na Figura 4.29, você pode ver Frankie em uma pose natural e com as asas ativas.

![Frankie - Ready to fly (left) and a natural pose (right)](../figures/Chapter4/Fig04-29.png)

Essas teclas de forma não são usadas isoladas como uma ação. Em vez disso, eles são usados como parte de uma pose de armadura, impulsionados por um bone, como todos os outros bones de animação. Este osso é usado como um direcionador para a ação da forma que pretende controlar. Como os outros controles osso sobre osso com restrições (que veremos a seguir), o osso condutor em si não está ciente de sua função como controlador de chave de forma. A Figura 4.30 mostra a configuração regular da ação da forma para um osso de controle. Você aprenderá mais sobre isso posteriormente na seção do tutorial.

![Shape key driven by a control bone](../figures/Chapter4/Fig04-30.png)

>**Action Actuator**
>
>As teclas de forma também podem ser usadas diretamente pelo atuador Action. Isso é útil quando você precisa animar toda a sua malha exclusivamente por meio da manipulação de vértices. Embora você provavelmente não vá usá-lo para seu personagem principal, você pode fazer bons efeitos inovadores com isso.

## Tutorials <a id="Tutorials"></a>

_Nenhum quadro-chave foi prejudicado durante a criação desses tutoriais._

Nas páginas seguintes, vamos fazer um personagem andar, interagir com objetos e ter algumas expressões faciais legais para você brincar. Para o modelo, usaremos o macaco, Momo (consulte a Figura 4.31). Limpei o arquivo original, removendo as chaves de forma e os ciclos de animação criados anteriormente. Você pode obter o Momo em seu novo estado em _ \ Book \ Chapter04 \ tutorials \ __ tutorials \ _momobase.blend_.

![Dear Momo, get ready for rock 'n' roll!](../figures/Chapter4/Fig04-31.png)

### Pre-Tutorial <a id="Pre-Tutorial"></a>

Neste pequeno pré-tutorial, vamos animar a rotação da câmera e a distância focal da câmera como um efeito de abertura para o jogo.

Todo o tutorial é baseado no uso de atuadores de ação para controlar as animações Momo. Como explicamos anteriormente, existem diferentes tipos de ação que podem ser usados. Independentemente do tipo de ação, a forma de usar o atuador é a mesma. Portanto, começaremos com uma ação muito simples e passaremos progressivamente por tópicos mais complexos, como animações-chave de ossos e formas.

Abra o arquivo base em _ \ Book \ Chapter04 \ tutorials \ tutorials \ _momobase.blend_.

1. Altere o quadro atual para 1.

2. Selecione o objeto da câmera.

3. No painel Câmera no Editor de propriedades, defina a distância focal para 10,0.

4. Com o mouse sobre o valor, pressione I para atribuir o quadro-chave ao quadro 1.

5. Vá para o quadro 30.

6. Altere a distância focal para 100,0.

7. Keyframe o novo valor para este quadro.

Neste pequeno pré-tutorial, vamos animar a rotação da câmera e a distância focal da câmera como um efeito de abertura para o jogo.

Todo o tutorial é baseado no uso de atuadores de ação para controlar as animações Momo. Como explicamos anteriormente, existem diferentes tipos de ação que podem ser usados. Independentemente do tipo de ação, a forma de usar o atuador é a mesma. Portanto, começaremos com uma ação muito simples e passaremos progressivamente por tópicos mais complexos, como animações-chave de ossos e formas.

Abra o arquivo base em _ \ Book \ Chapter04 \ tutorials \ tutorials \ _momobase.blend_.

1. Altere o quadro atual para 1.

2. Selecione o objeto da câmera.

3. No painel Câmera no Editor de propriedades, defina a distância focal para 10,0.

4. Com o mouse sobre o valor, pressione I para atribuir o quadro-chave ao quadro 1.

5. Vá para o quadro 30.

6. Altere a distância focal para 100,0.

7. Keyframe o novo valor para este quadro.

![Setting up an Action actuator](../figures/Chapter4/Fig04-32.png)

Se o zoom rápido da lente ainda não deixa todo mundo tonto, é hora de animar a rotação da câmera. É bom lembrar que enquanto a rotação é uma propriedade do objeto da câmera, a distância focal faz parte do bloco de dados da câmera. Como tal, essas transformações são armazenadas em ações independentes. Assim, precisaremos criar uma nova ação (por meio de keyframing a rotação da câmera) e configurar um novo atuador de ação.

1. Altere o quadro atual para 1.

2. Selecione o objeto da câmera.

3. Com o mouse sobre a janela de exibição 3D, abra o menu Keyframe (tecla I) e selecione Rotation.

4. Avance 5 frames.

5. Altere a rotação da câmera ao longo de seu eixo Z local em 60 graus para que ela continue olhando para frente, mas girando (pressione R + Z + Z + 60).

6. Crie um quadro-chave para a rotação novamente.

7. Repita as etapas anteriores até obter (e o quadro-chave) o quadro 30, que completará um loop completo de 360 ​​graus.

8. Crie um atuador de ação. Altere o intervalo de quadros de 1 a 30.

9. Defina CameraAction.001 como a ação do atuador. (Esta é a nova ação que criamos.)

10. Vincule o controlador E a este atuador de ação.

Você pode obter este arquivo final em _\Book\Chapter04\tutorials\pretutorial\_camera\_actions.blend_.

Este efeito é um pouco irritante se você reproduzir o arquivo várias vezes para testar a animação (como você fará em breve). Portanto, esta câmera giratória não está incluída no arquivo base que você usará para o tutorial real. Se, no entanto, quiser levar a câmera, você pode anexá-la aos outros arquivos. Todos os tijolos lógicos e ações vinculadas ao objeto da câmera e ao bloco de dados da câmera seguirão o objeto do Blender.

### Animation Cycle Tutorial <a id="Animation_Cycle_Tutorial"></a>

Para começar, vamos abrir o arquivo Momo e olhar a armadura. Abra o arquivo do livro _\Book\Chapter4\tutorial\_walk\_1.begin.blend._

Vamos criar uma bicicleta de caminhada para Momo, seguindo estas etapas:

1. Configuração da armadura

2. Posturas extremas

3. Seguindo em frente

4. Entre as poses

5. Tempo de jogo

Neste tutorial, não cobriremos a animação extensivamente. Este tópico sozinho poderia preencher um livro inteiro. Em vez disso, vamos nos concentrar no fluxo de trabalho de integração de suas habilidades de animação com as ferramentas do motor de jogo. Você obterá algumas dicas que pode aplicar às animações do Blender e do motor de jogo. Ambas as plataformas funcionam de maneira semelhante.

#### Armature Setup <a id="Armature_Setup"></a>

A armadura já foi criada, mas ainda não está pronta para animar o personagem. Se você for para o Modo de postura, poderá mover os ossos individuais, conforme mostrado na Figura 4.33. Como você já deve saber, as restrições de bones são úteis para posicionar a armadura, então vamos criar algumas.

![Select and move individual bones](../figures/Chapter4/Fig04-33.png)

Para Momo, existem dois conjuntos de restrições ósseas que ajudarão na sua pose. The Inverse Kinematics, IK, para controlar as cadeias de ossos de seus ossos extremos, e Track To para os olhos.

##### Inverse Kinematics Bone Constraints <a id="Inverse_Kinematics_Bone_Constraints"></a>

Primeiro, vamos dar uma olhada nas restrições de osso IK. IK pode ser usado para colocar braços e pernas movendo apenas as mãos e os pés. A posição dos ossos do braço e da perna será calculada automaticamente para acomodar a posição das mãos / pés. Não apenas as contrapartes humanas de Momo (braços, pernas, etc.) se beneficiam disso, mas também a cauda de Momo é perfeita para demonstrar o uso de IK, então vamos começar com isso. Com o arquivo aberto, siga estas etapas para chegar à configuração mostrada na Figura 4.34.

![Set an IK bone constraint in Momo's tail](../figures/Chapter4/Fig04-34.png)

1. Selecione o objeto de armadura.

2. Mude para o modo Pose.

3. Selecione o último osso da cauda (RigMomo.tail.001).

4. Selecione Restrições de osso no Editor de propriedades.

5. Adicione uma restrição de osso Inverse Kinematics.

Agora a configuração está quase concluída. Antes de terminar, tente mover o cóccix. Isso resulta em todos os tipos de torções e poses giratórias apenas movendo apenas um único osso de controle. Você pode ver essa iteração inicial na Figura 4.35, que foi um pouco longe demais, entretanto. Tudo que você precisa é controlar a cadeia de ossos à qual esse osso pertence; neste caso, todos os seis ossos do grupo cóccix.

![IK bone constraint with no limit](../figures/Chapter4/Fig04-35.png)

Para restringir a influência do controle do osso, você precisa definir o comprimento da cadeia no painel Restrição do osso IK. O valor padrão, zero, torna a cadeia de ossos influenciados o mais longa possível. Para a cauda, você pode definir o comprimento da corrente em cinco ossos.

Existem outras restrições de osso IK que desejamos definir. Até agora, vimos apenas os ossos da primeira camada óssea. Camadas de osso funcionam como camadas de objetos no Blender. Um osso pode estar em mais de uma camada e você pode escolher qual camada definir de cada vez. As camadas de osso podem ser encontradas no painel Armature Object Data no Property Editor, como visto na Figura 4.36.

![Bone layers](../figures/Chapter4/Fig04-36.png)

Se você puder ativar a segunda camada óssea, verá apenas os ossos da mão, do pé e da cauda. Todos eles precisam de restrições ósseas IK também. Tente copiar as etapas para o cóccix. Para imitar o arquivo original, você precisa definir o comprimento da corrente como dois ossos para o antebraço e os ossos da canela e três ossos para os pés. Esses números correspondem a quantos ossos sobraram na cadeia de ossos. Neste ponto, seu arquivo deve ser como o de _\Book\Chapter4\tutorial\_walk\_2.ik.blend._

>**Targetless Constraints**
>
>Essas restrições ósseas IK não têm objetivo. Conforme explicado anteriormente na seção de restrições ósseas, eles são um IK falso. Eles são usados apenas para ajudar na pose e podem ser removidos do arquivo final assim que a animação for concluída.

##### Track To Bone Constraints <a id="Track_To_Bone_Constraints"></a>

Bem, se você não olhou para a terceira camada óssea oculta, agora é um bom momento para fazê-lo. Como você pode ver na Figura 4.37, nesta camada, temos os ossos do olho e dois outros ossos para serem usados como rastreadores. Claro, você pode mover os ossos do olho diretamente, mas, novamente, esse não é o fluxo de trabalho ideal.

![Track To bone system](../figures/Chapter4/Fig04-37.png)

Os dois ossos na frente dos olhos são os ossos rastreadores. Cada osso do olho precisará de uma restrição Track To bone com esses ossos definidos como alvos. Pense nos rastreadores de ossos como a direção para a qual Momo está olhando. Por exemplo, se houver uma banana no chão, você pode colocar os rastreadores bem na fruta. Isso fará os olhos convergirem para lá.

Definir a restrição Track to bone não é muito diferente do que definir outras restrições de bone. Se você seguir as etapas na lista abaixo, deverá ver as configurações mostradas na Figura 4.38:

1. Selecione o objeto de armadura.

2. Mude para o modo Pose.

3. Selecione o osso do olho esquerdo.

4. Selecione Restrições de osso no Editor de propriedades.

5. Adicione uma restrição Track to bone.

![Track To Bone Constraint panel](../figures/Chapter4/Fig04-38.png)

Para terminar a configuração, selecione o RigMomo como o objeto alvo e eyes.target.L como o osso alvo. Faça o mesmo para o olho direito e você estará pronto para mover os ossos alvo. A armadura agora está pronta para a primeira animação. Se você apenas deseja se divertir animando o personagem, pode verificar o status do arquivo atual em _ \ Book \ Chapter4 \ tutorial \ _walk \ _3.trackto.blend._

#### Extreme Poses <a id="Extreme_Poses"></a>

A primeira coisa que você precisa para sua animação é a posição inicial da bicicleta de caminhada. Um bom ciclo não deve ter um começo ou um fim claros, então vamos começar com as poses extremas. Em geral, uma pose extrema mostra um momento em que a animação atinge o pico, antes de mudar de direção. Para o ciclo de caminhada, uma postura extrema é quando uma perna está em seu alongamento máximo e a outra ligeiramente dobrada, esperando para transferir seu peso para a perna à sua frente. Vamos começar a partir daí.

Ajuda poder ver imagens e vídeos durante a animação. Se você quiser se livrar de uma visita ao circo mais próximo, um desenho ou vídeo de uma pessoa caminhando bastará.

Nos arquivos do livro, você pode encontrar uma imagem de Momo caminhando em _ \ Book \ Chapter4 \ ExtremePoseSide.png_ e _ExtremePoseFront.png._

Na Figura 4.39, você pode ver essas imagens sendo usadas como fundo em um arquivo pronto para posar. Este arquivo do Blender é o mesmo que construímos na seção anterior com imagens de referência adicionais como fundo. Encontre-o em _ \ Book \ Chapter4 \ tutorial \ _walk \ _4.extreme \ _reference.blend_.

![Reference image as background](../figures/Chapter4/Fig04-39.png)

>**Reference Images**
>
>As imagens de referência são usadas aqui em segundo plano. Se você preferir vê-los no topo da visualização, você tem duas opções. Você pode usar a opção "Frontal" no painel Imagens de fundo. Ou você pode usar vasilhames. Adicione vasilhames com o tipo de exibição definido como Imagem. Coloque-os no local desejado e bloqueie sua seleção no Outliner.

Tente combinar sua armadura com a imagem de referência. No modo Pose, mova e gire os ossos. (Você não deseja alterar a armadura no modo Editar.) Preste atenção especial aos ossos dos pés para se certificar de que estão bem plantados no solo.

Depois de fazer a pose inicial, você pode fazer um pouco de ver macaco fazer. Siga os passos abaixo. A explicação segue.

1. Altere o quadro atual para 1.

2. Selecione todos os ossos.

3. Loc / Sca / Rot do quadro-chave (chave I)

4. Mude o quadro para 41 [md], este será o quadro final de nossa animação.

5. Keyframe Loc / Sca / Rot novamente (com os bones ainda selecionados).

6. Mude o quadro para 21 [md] a metade da animação onde a segunda passada começa.

7. Copie todas as transformações ósseas (Ctrl + C ou o ícone no cabeçalho da visualização 3D).

8. Cole-os espelhados (Shift + Ctrl + V ou o último ícone no cabeçalho da visualização 3D).

9. Loc / Sca / Rot do quadro-chave novamente.

10. No Editor da Curva F, selecione todos os ossos e altere o Modo de Extrapolação para Constante (Shift + E ou Menu do Canal> Modo de Extrapolação).

O que acabamos de fazer foi primeiro definir a duração da animação para 40 quadros (1,3 segundos a 30 fps para um conjunto completo de duas passadas). O primeiro e o último quadros precisam ser iguais; portanto, copiamos a transformação dos ossos do quadro 1 ao 41. (Você também pode copiá-los no Editor de Dopesheet.) Copiamos o quadro 41 e não o quadro 40 porque não queremos um quadro duplicado na animação. Queremos que a transição do último quadro (40) para o primeiro quadro (1) seja a mesma do último quadro (40) para o próximo quadro (41), que está fora do intervalo do loop.

As poses extremas para os passos esquerdo e direito são cópias invertidas uma da outra. Se você nomeou seus ossos corretamente (como fizemos, usando .L e .R para ossos esquerdo e direito simétricos, respectivamente), você pode copiar / colar os mesmos. Portanto, no meio de nossa animação (quadro 20), colocamos uma cópia das poses.

Por fim, a alteração no modo de extrapolação garante que os quadros se comportem como se tivessem sido copiados continuamente no Dopesheet. Os manipuladores dos quadros-chave iniciais mudam com os manipuladores dos quadros finais e vice-versa.

No painel Render do Editor de Propriedades, você pode definir a velocidade (30fps). O intervalo de reprodução (1 a 40) pode ser alterado no Editor de Linha de Tempo ou no mesmo painel Render Se você mudar o mecanismo de renderização para Renderização do Blender. Com este conjunto, você pode reproduzir (Alt + A) seu arquivo para ver as duas poses extremas alternando ao longo do tempo. Antes de terminar, vá para o Editor de Dopesheet, mude de Dopesheet para Action Editor e renomeie a ação criada anteriormente de ArmatureAction para Walking. Você pode ver o painel na Figura 4.40.

O arquivo final pode ser encontrado em _\Book\Chapter4\tutorial\_walk\_5.extremeposes.blend._

![Action Editor - first poses ready](../figures/Chapter4/Fig04-40.png)

#### Moving Forward <a id="Moving_Forward"></a>

O ciclo final de caminhada não terá nenhum movimento real para a frente: o personagem permanece no mesmo lugar. É semelhante àqueles antigos desenhos do Looney Tunes quando o coiote passa correndo pelo penhasco e continua correndo sem ir a lugar nenhum. Então ele cai. No entanto, você ainda precisa configurar um sistema onde possa ver o personagem andando como se você tivesse um atuador de movimento conectado a ele. Para ajudar nisso, examinaremos dois métodos: usando o osso central ou movendo o ambiente.

##### Root Bone <a id="Root_Bone"></a>

A maneira mais simples de fazer o Momo se mover é enquadrar o osso raiz ao longo do caminho. O osso da raiz é o pai de todos os ossos. Portanto, se ele se mover, o resto da armadura o seguirá. Para definir o osso da raiz para se mover, vá para o modo Pose e faça o seguinte:

1. Selecione o osso. No RigMomo você encontrará o Bone.main no nível do chão.

2. Insira um quadro-chave de localização. Esta será a posição inicial do osso e da armadura.

3. Avance do quadro 1 para o 41.

4. Mova o osso para frente a distância de uma passada [md] 0,23 (veja a nota abaixo).

5. Crie um quadro-chave para a posição do novo osso.

6. Altere o modo de extrapolação do canal do osso da raiz para extrapolação linear.

Nos arquivos do livro, você pode ver a configuração do Momo com as etapas do osso raiz em _\Book\Chapter4\tutorial\_walk\_6.rootbone.blend_.

>**How Big Is a Stride?**
>
>Se seu personagem estiver caminhando, eventualmente você precisará descobrir onde seus pés pousarão após cada passada. Isso varia de pessoa para pessoa e depende do tamanho da perna, da velocidade do movimento (caminhar, correr, pular) e de outros fatores, como o ambiente (por exemplo, neve). Para este ciclo de caminhada, você pode usar 23 cm (ou 0,23 unidades do Blender) para as duas passadas completas.

Depois de concluir toda a animação (após o estágio de polimento), você pode limpar a Curva F de localização do osso. Durante a produção do seu jogo, você pode precisar voltar para ajustes no seu ciclo de animação. Portanto, em vez de limpar a curva óssea, você pode simplesmente desativar o canal ósseo da raiz no Editor de gráfico. Na Figura 4.41 você pode ver o ícone de alto-falante que usa para isso.

![Graph Editor - disabling individual bone channels](../figures/Chapter4/Fig04-41.png)

A desvantagem desse método surge quando você precisa alterar o osso da raiz como parte de sua animação. Por exemplo, às vezes você não quer que seu ciclo de animação avance uniformemente. Mesmo para a caminhada de Momo, é melhor se houver uma pausa toda vez que ele descansar um dos pés enquanto se prepara para o próximo passo. Como você sabe, o movimento do personagem será desacoplado do ciclo de animação. E, não, não nos cansamos de repetir isso. Portanto, neste caso, se você olhar para o personagem de um ponto de referência em constante movimento, parecerá que Momo está se movendo para a frente, depois para trás e, em seguida, para a frente novamente para a posição original. Para mover todos os ossos de uma vez, nada é melhor do que o osso da raiz. Não é uma boa idéia confiar em um osso que você planeja desativar.

Uma solução alternativa para isso é ter um osso raiz para controlar a posição externa e outro osso (parente ao osso raiz) para controlar a posição interna, em relação à localização do objeto. Para evitar esse excesso de ossos de controle global, vamos examinar nosso segundo método.

##### If Mohamed Won't Go to the Mountain… <a id="If_Mohamed_Won't_Go_to_the_Mountain…"></a>

… ele vai para a praia. Nosso querido macaco, porém, está bastante bronzeado e pode muito bem ficar parado. Em outras palavras, neste método, Momo nunca se move. Em vez disso, vamos animar o ambiente ao seu redor.

Este método é baseado no princípio de que a percepção é sempre relativa. Por exemplo, na tela do computador, não há como distinguir entre mover a câmera para longe do personagem e mover o personagem para longe da câmera. O resultado será exatamente o mesmo. Adicionaremos marcadores de posição móveis que podem ser usados como guia para posicionar os pés. A Figura 4.42 mostra a configuração.

![Animation feet place holders](../figures/Chapter4/Fig04-42.png)

Este arquivo está em _\Book\Chapter4\tutorial\_walk\_7.placehold.blend_. Você não pode dizer pela imagem, mas se você reproduzir a animação, verá os marcadores se movendo contra o Momo (ou seria o contrário?). Na verdade, a câmera é estática, então Momo realmente não se move.

1. Crie um objeto simples e fácil de localizar.

2. Crie um modificador Array [md] defina o deslocamento constante para ser equivalente a uma passada e defina cópias suficientes para preencher a tela.

3. Mova o objeto Array para ser alinhado com Momo. Os pés de sua pose extrema devem corresponder à posição dos elementos da matriz.

4. Insira um quadro-chave de localização.

5. Avance dos frames 1 ao 41.

6. Mova o objeto de matriz para frente a distância de duas passadas [md] 0,46. (Veja a nota sobre osso da raiz.)

7. Crie um quadro-chave para a nova posição do objeto array.

8. No Editor de gráfico, altere o modo de extrapolação do objeto de matriz para extrapolação linear.

Este método requer um pouco mais de configuração do que o anterior, mas tem uma grande vantagem. Para trabalhar entre as poses (a próxima etapa deste tutorial), você precisará controlar a posição do pé enquanto o personagem se move para frente. Enquanto o corpo está em constante movimento, os pés ficam plantados no chão até que seja a hora de se levantarem e serem esmagados no chão novamente. Isso evitará o efeito indesejável conhecido como _pés deslizantes_. Esse problema será revisitado a seguir, quando criarmos as poses entre os extremos. A Figura 4.43 mostra o ciclo completo de caminhada em diferentes momentos; observe que os pés estão sempre no mesmo lugar em relação aos espaços reservados.
![Animation feet placeholders](../figures/Chapter4/Fig04-43.png)

#### Between Poses <a id="Between_Poses"></a>

Até agora, temos apenas duas poses, a extrema esquerda e a extrema direita. Por padrão, o Blender interpola as poses do quadro-chave, criando uma transição suave entre elas. Esta interpolação matemática não tem utilidade para a animação final. Isso nos deixa com 20 quadros para preencher entre essas poses extremas.

Da literatura de animação tradicional, você pode usar duas técnicas principais para criar esses quadros intermediários: ação direta e pose a pose.

Independentemente das vantagens de um ou outro método (você pode aprender mais sobre eles no material da seção de referência deste capítulo), devemos atentar para as diferenças em seus fluxos de trabalho. Na ação direta, você anima os quadros um a um conforme avança. Em pose a pose, você cria poses sub-extremas e preenche os intervalos sistematicamente.

Em ambos os casos, você precisa se certificar de que os pés não deslizem ao colocá-los. Use a técnica apresentada na seção anterior para evitar isso. Pés deslizantes e pés sob o solo são marcas de quadros insuficientes e interpolação automática. Evite-os a todo custo.

Além disso, embora você possa criar a animação posicionando e enquadrando os bones na visualização 3D, você pode querer ajustá-los no Editor de gráfico. Isso pode evitar que você crie muitos quadros e use os manipuladores para ajustar suas transições. Quanto menos quadros você tiver, mais fácil será alterar sua animação. Na Figura 4.44, você pode ver as curvas F atuais editadas para este ciclo de caminhada.

![F-Curve tweaks](../figures/Chapter4/Fig04-44.png)

Isso não é diferente do fluxo de trabalho tradicional de animação no Blender. Não é nem muito diferente do fluxo de trabalho de animação em outro software 3D. Da vasta quantidade de técnicas e ferramentas disponíveis, usei o seguinte para este ciclo:

- **IK bone constraints:** Use os ossos restritos IK como guias, mas lembre-se de enquadrar os ossos afetados também.

- **AutoKey:** A inserção automática de quadros-chave no cabeçalho do Editor de linha de tempo, especialmente para a ação direta, o poupará de muitos quadros-chave manuais.

- **Show/Hide Handlers (Ctrl+H):** Meu atalho pessoal favorito no Editor de gráfico.

- **UV grid:** No chão para detectar pés escorregando.

Na Figura 4.45, você pode ver o resultado final de nossa opinião sobre isso. Este arquivo está em _ \ Book \ Chapter4 \ tutorial \ _walk \ _8.pose \ _to \ _pose.blend_. Reproduza-o para vê-lo animado. A partir daqui, você pode continuar trabalhando no seu arquivo, retirá-lo do arquivo do livro ou mesclar os dois. Uma ação, como qualquer outro bloco de dados no Blender, pode ser importada e salva em arquivos diferentes (contanto que os ossos da armadura não mudem seus nomes).

![Walking cycle complete](../figures/Chapter4/Fig04-45.png)

#### Play Time <a id="Play_Time"></a>
Agora que o ciclo de animação está concluído, é hora de trazê-lo do Blender para o jogo. Você precisa definir um atuador de ação para executar a ação de caminhada e um atuador de movimento para fazê-lo se mover de acordo.

Vamos começar criando os blocos lógicos para a armadura. Com o RigMomo selecionado, siga as etapas em ordem. Na Figura 4.46, você pode ver a aparência do Logic Editor.

1. Adicione um sensor Always e ative o pulso positivo.

2. Adicione um atuador de ação. Defina a ação criada (por exemplo, Walk), o modo Play para Loop End e os frames inicial e final como 1 e 40 respectivamente.

3. Vincule o atuador Action ao sensor Always; isso criará automaticamente um controlador And.

4. Adicione um atuador de movimento e deixe os valores em branco por enquanto.

5. Vincule o atuador de movimento ao mesmo controlador E.

![Logic Bricks for animation playback](../figures/Chapter4/Fig04-46.png)

Para definir o valor no atuador de movimento, você precisa calcular a velocidade do objeto no Blender e convertê-lo para o motor de jogo. O cálculo é simples e vai te dar a velocidade precisa. Se, no entanto, você não sentir vontade de fazer matemática hoje, deixe a tentativa e o erro ser seu guia.

A velocidade - em unidades do Blender em segundos - é igual a duas passadas (0,23 x 2) divididas pelo número de ciclos por segundo - o intervalo de quadros do seu ciclo de animação (40) dividido pelo valor de reprodução de fps do Blender. O motor do jogo usa a mesma taxa de quadros do Blender, a ser definida no painel Render para 30fps. Então, para Momo, a velocidade com a qual estamos trabalhando é de 0,35 unidades do Blender por segundo: 0,46 / (40/30).

O valor a ser usado no atuador de movimento é a velocidade do objeto vezes a frequência na qual o atuador de movimento é ativado. Como estamos usando um sensor Always disparando todos os tiques lógicos, a frequência é 1/60 ou 0,017. Se você mudar seu jogo para rodar a 30 tiques lógicos por segundo, a frequência será o dobro (2/60 ou 0,033). A multiplicação da velocidade pela frequência é o valor que você adicionará ao componente do atuador. O Loc final é [0, -0,0059, 0] X, Y e Z respectivamente (consulte a Figura 4.47).

![Walking Momo](../figures/Chapter4/Fig04-47.png)

No final, você pode querer configurar a câmera para rastrear Momo durante a caminhada. No arquivo de amostra, você verá que a câmera está direcionada a um vazio com Editar objeto> Faixa para atuador para seguir Momo. Além disso, o efeito de introdução de zoom e rotação da câmera foi trazido do pré-tutorial. Um padrão xadrez no chão também ajudará a acompanhar o ritmo de sua progressão. O arquivo final é mostrado na Figura 4.47 e pode ser encontrado em _\Book\Chapter4\tutorial\_walk\_9.playtime.blend_.

### Idle Animation <a id="Idle_Animation"></a>

No arquivo mais recente, configuramos o Momo para andar. Nunca configuramos para que ele pare de andar, embora [md] o sensor Always reproduza a animação em um loop infinito até que você saia do jogo. Para levar nossos exercícios de animação adiante, vamos criar uma animação inativa para Momo. Em seguida, configuraremos Momo para andar, parar e andar novamente. Animações inativas são reproduzidas quando o personagem está esperando por você para tomar uma decisão (se deve continuar caminhando, correr, virar, etc.). Portanto, assim que pararmos de andar, definiremos o personagem para agir de acordo.

Comece abrindo o arquivo _\Book\Chapter4\tutorial\_idle\_1.begin.blend_. Este é o mesmo arquivo que fizemos no tutorial anterior, duplicado aqui por conveniência (o efeito de câmera giratória foi removido novamente). Selecione RigMomo e crie uma nova ação no Action Editor dentro do Dopesheet. Na verdade, você tem duas opções aqui: você pode criar uma nova ação em branco ou usar a ação Walk como referência (duplique-a e faça alterações em cima dela). Para duplicar a ação existente em uma nova, você deve clicar no número ao lado do nome da ação, conforme mostrado na Figura 4.48. Isso é útil quando você está criando variações da mesma ação (diferentes estilos de caminhada, diferentes saltos e assim por diante).

![Insert a new action](../figures/Chapter4/Fig04-48.png)

Nesse caso, como as ações são muito diferentes, não há muito o que reciclar desde o ciclo de caminhada até a animação ociosa. Você deseja manter apenas o primeiro e o último quadros para garantir uma transição mais suave entre as duas animações. Se você não quiser se preocupar em excluir quadros-chave, pode criar uma nova ação do zero, mantendo a pose inicial seguindo estas etapas:

1. Vá para o frame 1.

2. Desvincule a ação Walk da armadura (clique no botão X).

3. Crie uma nova ação (clique no botão + ou Novo).

4. Renomeie sua nova ação como "Ocioso".

5. Selecione todos os bones da armadura e crie um quadro-chave para eles.

6. Vá para um quadro posterior, que será o quadro final da animação inativa. Por exemplo, para fazer uma animação inativa de 4 segundos, vá para o quadro 121.

7. Defina um quadro-chave para todos os ossos novamente.

Agora você tem uma nova ação em branco para jogar. A única regra que você precisa seguir é evitar animações que exijam que o Momo se mova. O motivo é que você pode precisar interromper a animação inativa a qualquer momento, assim que voltar a andar.

A transição entre a animação de caminhada e a de inatividade pode ser perfeita. Na seção Logic Brick a seguir, explicaremos como fazer a caminhada terminar seu ciclo completo antes de iniciar a animação inativa. Além disso, isso terá que depender da combinação entre as poses de ambas as ações por alguns quadros. Isso funcionará apenas se a pose no quadro atual da animação inativa não for muito distinta da pose no quadro inicial da ação de caminhar. Se as poses forem extremamente diferentes (por exemplo, Momo está voltado para direções opostas), o cálculo automático entre as poses será matematicamente correto, mas artisticamente horrível. Isso é semelhante às nossas razões para fazer as poses entre no tutorial anterior.

Contanto que suas poses estejam dentro da faixa dos quadros inicial e final, a animação ociosa será reproduzida bem. Já que você deseja evitar mover Momo, é um bom momento para aprender como melhorar suas expressões faciais.

Antes de terminar a animação inativa, você precisa configurar os drivers para suas chaves de forma. Você pode encontrar o arquivo de instantâneo atual no final da próxima seção.

### Making a Face <a id="Making_a_Face"></a>

Você sabe a diferença entre televisão e uma performance ao vivo? Na televisão, o diretor tem total controle do enquadramento das tomadas. É comum usar e abusar de closes e expressões faciais fortes como substitutos para uma linguagem corporal expressiva. No teatro ao vivo, o público pode estar sentado perto ou longe do palco, e todos precisam estar satisfeitos. (Claro, as pessoas brigam por um assento dianteiro, mas o show ainda precisa fazer sentido para todos.)

Bons artistas se dão bem em ambos os meios. Mas um rosto bonito na tela da sua televisão HD pode ser uma experiência muito enfadonha e decepcionante de quero meu ingresso de volta em um teatro ao vivo (estive lá, fiz aquilo e dormi).

Em um jogo, temos o melhor e o pior dos dois mundos. Você ainda pode usar o enquadramento direcionado para cut scenes. Mas, na maior parte do jogo, você deve estar preparado para produzir animações boas e eficazes para distâncias curtas e longas.

No tutorial anterior, cobrimos as técnicas para uma boa pose de linguagem corporal completa. Adicione algumas técnicas de animação mais clássicas (por exemplo, silhuetas fortes, linhas de ação e exagero) e você está pronto para ir. Para a expressão facial, entretanto, veremos algo novo. Se você não leu esses capítulos na ordem, agora é um bom momento para voltar e ler sobre as chaves de forma.

#### Shape Keys and Bone Drivers <a id="Shape_Keys_and_Bone_Drivers"></a>

Uma chave de forma é como uma parte individual da gramática. Você precisa construir uma biblioteca de poses para usar em sua animação. Momo já tem algumas poses criadas anteriormente. Iremos usá-los em nossa animação posando com a técnica bone-driven.

Abra o arquivo _\Book\Chapter4\tutorial\_idle\_2.shapekeys\_ui.blend_. Este é o arquivo inicial com a IU reorganizada para funcionar melhor com as teclas de forma.

Na Figura 4.49, você pode ver todas as poses no painel de dados Mesh no Editor de Propriedades para o objeto MeshMomo. As diferentes poses foram criadas em pares: sorriso e ooh; sobrancelhas UP e sobrancelhasDOWN; eyelidUP e eyelidDOWN. Eles são todos relativos à forma de base. Para ver as poses, altere o valor por seus nomes no slot das teclas de forma [md], defina o valor de influência como 1.0 e todas as outras poses como 0.0. Se você quiser ajustar qualquer uma das poses, você precisa selecionar a forma e ir para o modo Editar. Você não estará mais trabalhando na forma de base, portanto, quaisquer alterações serão aplicadas apenas a esta forma específica.

![Shape smile - Edit mode](../figures/Chapter4/Fig04-49.png)

As formas não são exclusivas. Freqüentemente, você terá mais de uma pose ativa ao mesmo tempo. Portanto, cada forma tem mudanças muito isoladas. Para Momo, você pode ter uma única pose com as formas das pálpebras e sobrancelhas para cima. No entanto, isso não lhe daria nenhuma maneira de brincar com a influência deles individualmente em ações diferentes. Ao contrário das armaduras, você não tem como mascarar as formas usando apenas alguns "ossos" (ou parte da malha).

Agora você pode integrar as chaves de forma em sua animação inativa. A primeira coisa que você precisa fazer é definir os ossos para direcionar as formas. A ideia é usar chaves de forma como "bibliotecas de pose" dentro do fluxo de trabalho de animação de armadura. Portanto, você usará ossos de controle do RigMomo para controlar a influência de cada forma individual.

Selecione RigMomo e mude para o modo Pose. No tutorial de caminhada, vimos os ossos nas camadas de osso 1 a 3. Agora você pode finalmente ativar a camada 4 para ver os últimos ossos da armadura de Momo. Os ossos nesta camada são todos destacados da armadura principal, como você pode ver na Figura 4.50.

![Shape key control bones](../figures/Chapter4/Fig04-50.png)

Para conectar os bones de controle com as teclas de forma, você precisa seguir as etapas. O driver final no Editor de gráfico será semelhante à Figura 4.51.

1. Selecione o objeto MeshMomo.

2. Selecione uma chave de forma (por exemplo, sorriso).

3. Clique com o botão direito do mouse no valor de Influência.

4. Selecione Adicionar driver.

5. Abra o editor de gráfico.

6. Mude o modo de edição de F-Curve Editor para Drivers.

7. Dentro do canal "Key", selecione a curva a ser editada (por exemplo, Value (smile)).

8. Abra o painel Propriedade (N).

9. Altere o tipo de Expressão de script para Valor médio.

10. Exclua o modificador F-Curve (criado por padrão).

11. No painel Object / Bone, defina RigMomo e o bone para usar como controlador (por exemplo, Mouth).

![Shape key driver](../figures/Chapter4/Fig04-51.png)

Por padrão, o Blender define a coordenada X global do osso para direcionar a influência da forma. No modo Pose, você pode mover o osso da boca para os lados para ver a influência da forma aumentando e diminuindo respectivamente. Como com qualquer outro osso, você pode definir o quadro-chave da posição desse controlador de osso (boca) para animar a influência dessa forma ao longo do tempo.

No entanto, esta não é uma configuração eficaz. Primeiro, é mais intuitivo usar a posição vertical do osso para direcionar essa forma particular. Em segundo lugar, é melhor se você não precisar mover o osso tanto quanto precisa agora para ter mudanças significativas. Claro, estes não são obstáculos, mas estamos aqui para aprender, não estamos?

Primeiro, no painel Driver, altere a influência do canal Transform de X Location para Z Location e altere Space para Local Space. Opcionalmente, você pode bloquear a transformação de X, Y e a rotação do osso [md], usaremos apenas seus movimentos Z.

Em segundo lugar, você precisa mapear as transformações ósseas para influenciar a forma. Para manter as posições dos ossos não muito longe para o resto da armadura, usaremos a curta distância de uma décima unidade do Blender para controlar todas as influências de forma. Isso cria uma curva com dois pontos, [0,0, 0,0] e [0,1, 1,0]. Isso mapeará a influência da forma para 0,0 quando o local da pose Z do osso for 0,0 e 1,0 quando o local for 0,1.

Mover o osso para cima e para baixo agora irá direcionar a influência da forma como você deseja. Seu arquivo agora deve corresponder ao arquivo de livro: _ \ Book \ Chapter4 \ tutorial \ _idle \ _3.smile \ _shapekeydriver.blend_.

Para a segunda pose, "ooh", você usará o mesmo controlador de osso, mas com um mapeamento diferente. Queremos definir a pose "ooh" quando o osso estiver em -0,1 e "sorrir" quando estiver 0,1, como fizemos. Isso permitirá uma transição suave entre essas duas poses extremas. Repita as etapas anteriores até a criação da Curva-F.

Desta vez, a curva será o reverso do sorriso, com dois pontos: [-0,1, 1,0] e [0,0, 0,0]. A Figura 4.52 ilustra o arranjo final.

![F-Curves of shape driver influence](../figures/Chapter4/Fig04-52.png)

Além disso, você pode adicionar uma restrição de osso para garantir que o controlador de osso esteja se movendo apenas verticalmente e que esteja sempre dentro do intervalo que você está usando (-0,1 a 0,1).

Finalmente, você precisa configurar as poses restantes [md] pálpebra para cima e para baixo e sobrancelha para cima e para baixo. A configuração é a mesma do par ooh e sorriso. Desta vez, vamos deixá-los para você, mas você pode verificar o arquivo de configuração final em _ \ Book \ Chapter4 \ tutorial \ _idle \ _4.shapekeysdriver.blend_.

### Get Your Hands Dirty <a id="Get_Your_Hands_Dirty"></a>

Com a armadura pronta para posar, você pode completar a animação ociosa. Depois que as coisas estiverem definidas, não há necessidade de se preocupar com nada além das poses da armadura. Pegue o arquivo anterior e crie o ciclo completo.

Nossa tentativa de uma animação ociosa divertida pode ser vista no arquivo do livro _ \ Book \ Chapter4 \ tutorial \ _idle \ _5.action.blend_. A animação (ainda) não está configurada para ser reproduzida no mecanismo de jogo, mas você pode reproduzi-la na visualização 3D. Lembre-se também de alterar o quadro final em seu painel de renderização para corresponder à reprodução de seu ciclo de animação. Isso não afetará o mecanismo de jogo, mas ajudará você a visualizar seu trabalho no Blender.

Após a seção tutorial, você pode conferir a animação ociosa e ambulante feita por Moraes Júnior especialmente para este livro. Enquanto isso, aproveite nossa opinião sobre Momo, o macaco mais feliz do mundo (consulte a Figura 4.53).

![Momo idle animation](../figures/Chapter4/Fig04-53.png)

### Wiring Up the Logic Bricks <a id="Wiring_Up_the_Logic_Bricks"></a>

Só falta uma coisa. Precisamos alternar entre as duas animações: a pé e a ociosa. Com o arquivo mais recente aberto, selecione RigMomo e, no Logic Editor, faça as seguintes alterações:

1. Altere o sensor Always para um sensor de teclado com a chave definida para W.

2. Adicione um sensor de propriedade para verificar se a propriedade do quadro está entre 39 e 40. Defina Inverter e ative os modos de pulso positivo e negativo.

3. Conecte o sensor de propriedade ao atuador de movimento (mover para frente).

Essas mudanças podem ser vistas na Figura 4.54. O que você está fazendo aqui primeiro é definir a ação a ser executada quando a tecla W for pressionada. Como o Action Actuator está definido como Loop End, a animação ainda será reproduzida por mais alguns quadros. Para fazer o Momo continuar avançando, você precisa manter o atuador de movimento ativo até que o quadro reproduzido não seja o final (40). Dessa forma, ao soltar a tecla, você garante que a animação Momo está no início de seu ciclo de animação, pronta para se misturar com a ação ociosa.

![Logic Brick, Part 1 - keep walking](../figures/Chapter4/Fig04-54.png)

Agora tudo o que falta fazer é jogar a ação ociosa quando Momo não está andando. Adicione um Nor Controller conectado ao teclado e à propriedade e conecte-o a um novo Action Actuator. O Nor Controller jogará este atuador apenas quando ambos os sensores forem falsos. O Action Actuator e os blocos lógicos finais podem ser vistos na Figura 4.55. A explicação para os parâmetros segue.

![Logic Brick, Part 2 - idle](../figures/Chapter4/Fig04-55.png)

- **Playback type** : Loop Stop fará com que a ação seja repetida até que o Sensor do Teclado esteja ativo. Ele vai parar imediatamente depois.

- **Priority** : 2 [md] deve ser mais alto do que o atuador de ação ambulante. As ações de prioridade mais baixa têm precedência sobre as mais altas.

- **Start/End Frame** : 1 e 160 [md] o intervalo de sua animação.

- **Blendin** : 11 [md] Se a pose do quadro inicial da animação inativa for a mesma que a de caminhar, você não precisa misturá-los (Blendin = 0). Caso contrário, este parâmetro tornará a transição suave.

- **Continue** : Falso [md], você deseja que a animação comece do quadro 1 toda vez que você parar de andar.

O arquivo final está em _\Book\Chapter4\tutorial\_idle\_6.idlewalkforward.blend_.

### How Many Bricks Does It Take to Turn Momo? <a id="How_Many_Bricks_Does_It_Take_to_Turn_Momo?"></a>

Momo pode andar e parar. Agora, se pelo menos tivéssemos um salto, estaríamos prontos para um jogo de plataforma side-scroller (devido a restrições de direitos autorais, você não verá uma figura de Momo correndo atrás de um ouriço com espinhos giratórios). Para um jogo 3D, no entanto, você precisa ser capaz de navegar livremente pelos níveis. E não há maneira melhor do que permitir que o personagem se vire.

A maneira mais simples de fazer o Momo girar é adicionando novos Atuadores de Movimento que respondem a um novo conjunto de Sensores de Teclado. Vamos usar a chave A para virar à esquerda e D para virar à direita. Para virar à esquerda, siga estas instruções:

1. Adicionar sensor de teclado [md] tecla A.

2. Adicione o atuador de movimento com Rot Z 2,5 graus.

3. Conecte o sensor ao atuador, o que cria um novo controlador E.

4. Altere o controlador cWalk original de E para Ou.

5. Conecte o novo sensor a este controlador também.

6. Conecte o novo sensor ao controlador Nor.

Agora faça o mesmo para a rotação correta e você terá os blocos lógicos mostrados na Figura 4.56. Você pode notar que estou usando três estados para os controladores aqui. Eles estão sempre ativados, portanto, o objetivo principal é puramente de organização.

![Logic Brick, Part 3 turning](../figures/Chapter4/Fig04-56.png)

Fonte: Fundação Blender.

O arquivo final está em _\Book\Chapter4\tutorial\_idle\_7.turning.blend_.

>**The Dilemma of the Sweet Miso Soup
>
>Uma vez, quando eu era mais jovem, minha mão escorregou enquanto temperava a sopa de missô e, de maneira brilhante, achei uma boa ideia compensar o sal adoçando-o. Adivinha, não funcionou (e sim, tive que comer tudo).
>O mesmo se aplica à animação. Ninguém precisa virar à direita e à esquerda da mesma maneira. Pode ser por causa de uma lesão no futebol, uma perna mais curta, etc.
>Portanto, às vezes (nem sempre, não agora), você precisa de mais controle sobre as curvas. Para o projeto _Yo Frankie_, eles tinham animações específicas para cada lado que Momo giraria. Essas subanimações proporcionam boas transições entre as ações e um controle mais artístico. É sempre uma questão de compromisso entre o que você pode fazer e o que não pode, o que é feito entre as equipes técnica e artística. Assim, mesmo que um programador possa insistir nisso, uma animação para "levantar" não é o mesmo que uma animação para "sentar" reproduzida ao contrário. Para o nosso ciclo de caminhada simples, isso bastará.
> Conclusão: uma sopa de missô com açúcar não é um ponto de equilíbrio [md], é um cozimento ruim.

### Hats Off to Momo and Vice-Versa <a id="Hats_Off_to_Momo_and_Vice-Versa"></a>

Momo é um macaco elegante, frequentemente visto em festas da alta sociedade do reino animal. No entanto, quando está com seu círculo íntimo de amigos, Momo é na verdade um macaco muito casual [md] não há muito a mostrar, nada a esconder. Um personagem [md] dois momentos bem distintos. Este é o tema da nossa animação.

Neste tutorial, mostraremos como fazer o Momo alternar entre dois tipos de chapéu: um chapéu saltitante e um chapéu que se ajusta bem em sua cabeça. Não usaremos apenas dois objetos Blender diferentes, mas também os animaremos de forma diferente quando usados. Para fazer um objeto externo à armadura segui-lo, precisamos de duas coisas: um bone e um parented empty.

O bone, que pode ser animado como qualquer outro bone, indicará a localização da cabeça de Momo e a rotação para cada quadro. O vazio, externo à armadura, é pai do osso e copia as transformações do osso automaticamente durante o jogo. Neste tutorial, este vazio, funcionando como um espaço reservado, será usado para colocar o chapéu que Momo usará.

Comece abrindo uma variação do último Momo ambulante no arquivo do livro _ \ Book \ Chapter4 \ tutorial \ _hat \ _1.begin.blend_.

Se você deseja transportar essas alterações para seu próprio arquivo de trabalho, é necessário anexar o grupo Hats em seu arquivo local. Isso também inclui o objeto de câmera e um vazio onde estamos executando o script para controlar o switch hat. Você pode ver os chapéus na Figura 4.57.

![Hats for Momo](../figures/Chapter4/Fig04-57.png)

Fonte: Fundação Blender.

Este é um tutorial simples, com foco em ilustrar a técnica de paternidade óssea. Portanto, a maioria dos componentes está pronta para você conectar com seu arquivo (por exemplo, os scripts). Vamos primeiro configurar um dos chapéus.

1. Selecione a armadura e vá para o modo Editar.

2. Crie um osso no meio da cabeça denominado Head.Hat.Steady.

3. Parente o osso com o osso da cabeça.

4. Mude o modo Armature para o modo Pose.

5. Vá para o modo Objeto e crie um vazio com a mesma posição/rotação do osso Head.Hat.Steady. Nomeie o vazio Head.PH.Hat.Steady.

6. Com o vazio selecionado, selecione o osso que você acabou de criar e torne-o o pai do vazio (Ctrl + P  Definir pai para  Osso).

Com essas alterações, você já pode animar o bone Head.Hat.Steady, e o espaço reservado vazio seguirá. O chapéu será colocado exatamente onde está o vazio. No arquivo atual, ambos os chapéus são parentais para vazios / espaços reservados próximos à câmera. Para animar os ossos do chapéu, você precisa trazê-lo temporariamente para a posição que ficará durante o jogo. Para que funcione com o osso Head.Hat.Steady, você precisa trazer o objeto Hat.Cap Blender para a mesma posição/rotação que o espaço reservado vazio e pai do objeto chapéu para ele (selecione o chapéu, selecione o vazio, em o painel Transformar na visualização 3D, clique com o botão direito do mouse nos valores para "Copiar para selecionado," Ctrl + P para o pai). Agora você pode ir para o modo de edição de armadura e mover o osso para fazer o chapéu caber na cabeça corretamente. A Figura 4.58 mostra a disposição de Bone + Vazio + Chapéu. O instantâneo atual pode ser encontrado _in\Book\Chapter4\tutorial\_hat\_2.capsetup.blend_.

![Hat + empty placeholder + hat bone](../figures/Chapter4/Fig04-58.png)

Assim que o osso estiver no lugar certo, você pode revisar as animações de caminhada e ociosidade e fazer alguns ajustes em sua posição/rotação ao longo do tempo. Para este chapéu, você não precisa se mover muito. Em nosso caso, apenas inclinamos um pouco no meio da animação ociosa para acompanhar o levantar de sobrancelhas e alguns saltos sutis durante a caminhada. Ao executar o jogo agora, você verá o chapéu sempre no lugar certo durante as animações. Para ter certeza de que você pode acompanhar de perto, o arquivo com o Hat.Cap animado pode ser visto na Figura 4.59 e o arquivo do livro _\Book\Chapter4\tutorial\_hat\_3.animatedcap.blend_.

![Momo walking in the game with the cap on his head](../figures/Chapter4/Fig04-59.png)

Por enquanto, tudo bem. Vamos agora configurar o segundo chapéu. Para este, você criará um novo osso e um novo espaço reservado. A razão é que você fará uma animação diferente para este chapéu. A cartola elegante ficará um pouco mais solta, então deve pular mais durante as animações.

Comece movendo / girando o Hat.Cap de volta ao seu espaço reservado original pela câmera e redirecione-o para o vazio (Camera.PH.Hat.Cap). Agora repita os mesmos passos que você fez para o outro chapéu. Desta vez, nomeie o osso Head.Hat.Bouncy e o vazio Head.PH.Hat.Bouncy. Para a animação, deixe-a mais exagerada, com o chapéu escorregando durante a caminhada e as ações ociosas. A Figura 4.60 ilustra um dos momentos em que o chapéu quase caiu. Depois de mover o objeto Hat.Top de volta para seu espaço reservado original (Camera.PH.Hat.Top), seu arquivo deve estar pronto para os ajustes finais.

![Classy top hat is too big for Momo's head](../figures/Chapter4/Fig04-60.png)

>**Copy Menu Attributes Add-on**
>
>Assim que você começar a criar seus objetos, verá que não é tão fácil copiar transformações. As ferramentas de cópia integradas do Blender funcionam apenas em cima das transformações locais, e isso não é suficiente quando você deseja copiar as transformações visuais ou mundiais. A diferença é que as transformações visuais (o que você vê) são um resultado acumulado das diferentes transformações locais da cadeia de pais.
> O Blender vem com um add-on que permite que você faça todos os tipos de operações de cópia avançadas. Vá para Preferências do usuário, Add-Ons e habilite o add-on Copy Attributes Menu.
> Este add-on foi originalmente planejado apenas para trazer o menu de cópia (Ctrl + C) do Blender 2.49. Bassam Kurdali, seu desenvolvedor e mantenedor original, teve a gentileza de expandi-lo para ajudar neste tutorial. Parabéns a ele.
> Se você não quiser usar add-ons, você pode ir à velha escola com as soluções alternativas do Blender 2.49. Duplique seu vazio e faça um Clear Parent  Clear and Keep Transformation no novo empty. Agora você pode usar este objeto para copiar as transformações, excluí-lo e pai do chapéu para o vazio original.

Agora que as animações estão concluídas e a armadura configurada, podemos prosseguir para examinar a implementação da troca de chapéus em tempo real.

Pegue o arquivo final _ \ Book \ Chapter4 \ tutorial \ _hat \ _4.animatedhats.blend_.

A interação é simples: clique em um chapéu para alternar para ele; clique em qualquer outro lugar para trazê-lo de volta para perto da câmera. Quando você escolhe um chapéu, o mecanismo de jogo terá que fazer como você fez para ajustar as animações: pegue o chapéu selecionado, mova-o para a posição do marcador de posição da cabeça, combine suas rotações e pare-o com este marcador.

Isso é feito por um script que já está conectado à câmera. Este script Python é muito simples e você deve ser capaz de entendê-lo após o Capítulo 7, "Script Python". O script acessa os objetos [md] chapéus e espaços reservados vazios [md] por seus nomes. Portanto, para suas alterações locais, é importante seguir os nomes conforme apresentados aqui ou ajustar o script de acordo.
### Mango Jambo Special Animation <a id="Mango_Jambo_Special_Animation"></a>

O ciclo de caminhada que você viu até agora é tecnicamente correto e segue o fluxo de trabalho com o qual você pode contar, independentemente de suas habilidades de animação. O ponto principal é: com um bom método e o entendimento das técnicas, embora você possa não ser brilhante, você também não pode errar.

Agora, como a cereja do bolo, pedi ao animador Moraes Júnior que fizesse a mesma coisa que fizemos juntos [md] um novo ciclo de caminhada e animação ociosa usando o mesmo arquivo base. Para referência, ele criou Momo para o projeto _Yo Frankie_ e suas animações originais. Depois de usarmos e abusarmos de Momo nas páginas anteriores, é justo ver o que seu "pai" teria feito em vez disso. Aqui você pode ver e estudar seu trabalho e a contribuição final: \Book\Chapter4\mangojambo.blend

## To Learn More <a id="To_Learn_More"></a>

Por fim, dedique o tempo adequado para dominar as formas de animação. Aprender como fazer animação funcionar no Blender ainda não é a mesma coisa que saber o que fazer. Aqui está uma lista de materiais clássicos para o aprendizado de animação [md], referências modernas para animação e controle de personagens em jogos e leitura específica do Blender.

- _Drawn to Life_ por Walt Stanchfield

- _The Animator's Survival__Kit_ por Richard Williams

- _Cartoon Animation_ por Preston Blair

- _3ª pessoa Action Platformer Hero Animation Graph_ por Rune Vendler

- [_http://altdevblogaday.org/2011/04/14/3rd-person-action-platformer-hero-animation-graph_](http://altdevblogaday.org/2011/04/14/3rd-person-action-platformer-hero-animation-graph)

- _Dvd de animação de personagens_ por William Reynish

- Livro de receitas de animação de personagens do Blender 2.5 por Virgilio Vasconcelos
