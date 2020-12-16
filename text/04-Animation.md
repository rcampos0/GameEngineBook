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

If the fast zooming of the lens still doesn't make everyone dizzy, it's time to animate the camera rotation. It's good to remember that while the rotation is a property of the camera object, the focal length is part of the camera datablock. As such, these transformations are stored in independent actions. Thus, we will need to create a new action (through keyframing the camera rotation) and set up a new Action actuator.

1. Change the current frame to 1.

2. Select the camera object.

3. With the mouse over the 3D viewport, invoke the Keyframe menu (I key) and select Rotation.

4. Advance 5 frames.

5. Change camera rotation along its local Z axis by 60 degrees so it keeps looking forward but spinning (press R + Z + Z + 60).

6. Keyframe the rotation again.

7. Repeat the previous steps until you get (and keyframe) frame 30,which will complete a full loop of 360 degrees.

8. Create an Action actuator. Change frame range from 1 to 30.

9. Set CameraAction.001 as the actuator Action. (This is the new action we created.)

10. Link the And controller with this Action actuator.

You can get this final file on _\Book\Chapter04\tutorials\pretutorial\_camera\_actions.blend_.

This effect is a bit annoying if you play the file multiple times to test the animation (as you will soon). So this spinning camera is not included in the base file you will use for the actual tutorial. If, however, you want to bring the camera along, you can append it into your other files. All the logic bricks and actions linked to the camera object and camera datablock will follow the Blender object.

### Animation Cycle Tutorial <a id="Animation_Cycle_Tutorial"></a>

To start, let's open the Momo file and look at the armature. Open the book file _\Book\Chapter4\tutorial\_walk\_1.begin.blend._

We will create a walking cycle for Momo, following these steps:

1. Armature setup

2. Extreme poses

3. Moving forward

4. Between poses

5. Play time

In this tutorial, we will not cover animation extensively. This topic alone could fill a whole book. Instead, we will focus on the workflow of integrating your animation skills with the game engine tools. You'll get some tips you can apply to both Blender and the game engine animations. Both platforms work in a similar fashion.

#### Armature Setup <a id="Armature_Setup"></a>

The armature is already created, but not yet ready to animate the character. If you go to the Pose Mode, you can move the individual bones, as shown in Figure 4.33. As you might already know, bones constraints are useful in posing the armature, so let's create some.

![Select and move individual bones](../figures/Chapter4/Fig04-33.png)

For Momo, there are two sets of bone constraints that will help your posing. The Inverse Kinematics, IK, for controlling the bone chains from their extreme bones, and Track To for the eyes.

##### Inverse Kinematics Bone Constraints <a id="Inverse_Kinematics_Bone_Constraints"></a>

First, let's take a look at the IK bone constraints. IK can be used to pose arms and legs by moving only the hands and feet. The position of the arm and leg bones will be automatically calculated to accommodate the hand/feet position. Not only Momo's human counterparts (arms, legs, etc.) benefit from it, but also Momo's tail is perfect to demonstrate the usage of IK, so let's start with it. With the file open, follow these steps to get to the configuration shown in Figure 4.34.

![Set an IK bone constraint in Momo's tail](../figures/Chapter4/Fig04-34.png)

1. Select the armature object.

2. Change to Pose mode.

3. Select the last tail bone (RigMomo.tail.001).

4. Select Bone Constraints in the Property Editor.

5. Add an Inverse Kinematics bone constraint.

Now the setup is almost done. Before we finish, try to move the tail bone around. This results in all sorts of twists and revolving poses just by moving only a single control bone. You can see this early iteration in Figure 4.35, which went a bit too far, however. All you need is to control the chain of bones that this bone belongs to; in this case, all six bones from the tail bone group.

![IK bone constraint with no limit](../figures/Chapter4/Fig04-35.png)

In order to constraint the Influence of the bone control, you need to set the chain length in the IK Bone Constraint panel. The default value, zero, makes the chain of influenced bones as long as possible. For the tail, you can set the chain length to be five bones.

There are other IK bone constraints that we want to set. So far we have been seeing only the bones from the first bone layer. Bone layers work like the object layers in Blender. A bone can be in more than one layer, and you can choose which layer to set at a time. The bone layers can be found in the armature Object Data panel in the Property Editor, as seen in Figure 4.36.

![Bone layers](../figures/Chapter4/Fig04-36.png)

If you can turn on the second bone layer, you will see only the hand, foot, and tail bones. They all need IK bone constraints as well. Try copying the steps for the tail bone. To mimic the original file, you need to set the chain length to be two bones for the forearm and the shin bones, and three bones for the feet. These numbers correspond to how many bones are left in the chain of bones. At this point, your file should be like the one on _\Book\Chapter4\tutorial\_walk\_2.ik.blend._

>**Targetless Constraints**
>
>Those IK bone constraints are targetless. As explained previously in the bone constraints section, they are a fake IK. They are used only to help in posing and can be removed from the final file once the animation is done.

##### Track To Bone Constraints <a id="Track_To_Bone_Constraints"></a>

Well, if you haven't looked at the hidden third bone layer, now is a good time to do so. As you see in Figure 4.37, in this layer, we have the eye bones and two other bones to be used as trackers. Sure, you could move the eye bones directly, but again, this is not the ideal workflow.

![Track To bone system](../figures/Chapter4/Fig04-37.png)

The two bones in front of the eyes are the tracker bones. Each eye bone will need a Track To bone constraint with those bones set as the targets. Think of the bone trackers as the direction in which Momo is looking. For example, if there is a banana on the floor, you can place the trackers right on the fruit. This will make the eyes converge there.

Setting the Track To bone constraint is not much different than setting the other bone constraints. If you follow the steps in the list below, you should see the settings shown in Figure 4.38:

1. Select the armature object.

2. Change to Pose mode.

3. Select the left eye bone.

4. Select Bone Constraints in the Property Editor.

5. Add a Track To bone constraint.

![Track To Bone Constraint panel](../figures/Chapter4/Fig04-38.png)

To finish the setup, select the RigMomo as the target object and eyes.target.L as the target bone. Do the same for the right eye, and you are ready to move the target bones around. The armature is now ready for the first animation. If you just want to have fun animating the character, you can check the current file status at _\Book\Chapter4\tutorial\_walk\_3.trackto.blend._

#### Extreme Poses <a id="Extreme_Poses"></a>

The first thing you need for your animation is the start position of the walking cycle. A good cycle shouldn't have a clear beginning or end, so we'll start with the extreme poses. In general, an extreme pose shows a moment when the animation hits a peak, before it changes direction. For the walking cycle, an extreme pose is when one leg is in its maximum stretch and the other is slightly bent, waiting to transfer its weight to the leg in front of it. We will start from there.

It helps to be able to view images and videos when animating. If you want to spare yourself from a visit to the nearest circus, a drawing or video of a person walking will do just fine.

On the book files, you can find an image of Momo walking in _\Book\Chapter4\ ExtremePoseSide.png_ and _ExtremePoseFront.png._

In Figure 4.39, you can see those images being used as background in a file ready for posing. This Blender file is the same one we built in the previous section with additional reference images as background. Find it in _\Book\Chapter4\tutorial\_walk\_4.extreme\_reference.blend_.

![Reference image as background](../figures/Chapter4/Fig04-39.png)

>**Reference Images**
>
>The reference images are used here in the background. If you prefer to see them on top of the view, you have two options. You can use the "Front" option in the Background Images panel. Or you can use empties instead. Add empties with the Display type set to Image. Place them in the desired location and lock their selection in the Outliner.

Try to match your armature to the reference image. In the Pose mode, move and rotate the bones around. (You don't want to change the armature in Edit mode.) Pay special attention to the feet bones to make sure they are well planted in the ground.

After you are done with the initial pose, you can go for a bit of monkey see-monkey do. Follow the steps below. The explanation follows.

1. Change current frame to 1.

2. Select all bones.

3. Keyframe Loc/Sca/Rot (I key)

4. Change frame to 41[md]this will be the end frame of our animation.

5. Keyframe Loc/Sca/Rot again (with the bones still selected).

6. Change frame to 21[md]the half of the animation where the second stride begins.

7. Copy all the bone transformations (Ctrl + C or the icon in the 3D View header).

8. Paste them mirrored (Shift + Ctrl + V or the last icon in the 3D View header).

9. Keyframe Loc/Sca/Rot yet again.

10. In the F-Curve Editor, select all bones and change Extrapolation Mode to Constant (Shift + E or Channel Menu > Extrapolation Mode).

What we just did was first define the animation length for 40 frames (1.3 seconds at 30 fps for one complete set of two strides). The first and last frames need to match; so we copied the transformation of the bones over frame 1 to 41. (You can copy them in the Dopesheet Editor as well.) We copied to frame 41 and not to frame 40 because we don't want a duplicated frame in the animation. We want the transition from the last frame (40) to the first frame (1) to be the same as from the last frame (40) to the next frame (41), which is outside the loop range.

The extreme poses for the left and the right strides are flipped copies of each other. If you named your bones properly (as we did, using .L and .R for symmetric left and right bones respectively), you can mirror copy/paste them. Therefore, in the middle of our animation (frame 20), we place a copy of the poses.

Finally, the change in the Extrapolation mode ensures that the frames behave as if they were copied over and over in the Dopesheet. The handlers of the initial keyframes change with the handlers of the final frames and vice versa.

In the Render panel in the Properties Editor, you can set the speed (30fps). The playback range (1 to 40) can be changed in the Timeline Editor or in the same Render panel If you switch the render engine to Blender Render. With this set, you can play back (Alt + A) your file to see the two extreme poses alternating over time. Before finishing, go to the Dopesheet Editor, switch from Dopesheet to Action Editor and rename the previously created action from ArmatureAction to Walking. You can see the panel in Figure 4.40.

The final file can be found in _\Book\Chapter4\tutorial\_walk\_5.extremeposes.blend._

![Action Editor - first poses ready](../figures/Chapter4/Fig04-40.png)

#### Moving Forward <a id="Moving_Forward"></a>

The final walking cycle will have no real forward movement: the character stays in the same place. It's similar to those old Looney Tunes cartoons when the coyote runs past the cliff and keeps running without going anywhere. Then he falls. Nevertheless, you still need to set up a system where you can see the character walking as if you had a Motion Actuator attached to it. To help with this, we will look at two methods: using the central bone or moving the environment.

##### Root Bone <a id="Root_Bone"></a>

The simplest way to make Momo move is by keyframing the root bone along the way. The root bone is the parent of all the bones. Thus, if it moves, the rest of the armature will follow it. To set the root bone to move, go to Pose mode and do the following:

1. Select the bone. In RigMomo you will find the Bone.main on the floor level.

2. Insert a Location keyframe. This will be the initial position of the bone and armature.

3. Advance from frame 1 to 41.

4. Move the bone forward the distance of one stride[md]0.23 (see the note below).

5. Keyframe the new bone position.

6. Change the Channel Extrapolation mode of the root bone to Linear Extrapolation.

In the book files, you can see Momo setup with the root bone steps at _\Book\Chapter4\tutorial\_walk\_6.rootbone.blend_.

>**How Big Is a Stride?**
>
>If your character is walking, eventually you will need to find where its feet will land after each stride. This varies from person to person, and is a function of the leg's size, the speed of the movement (walking, running, jumping), and other factors such as the environment (for example, snow). For this walking cycle, you can use 23cm (or 0.23 Blender units) for the complete two strides.

After you are done with all the animation (past the polishing stage), you then can clean the bone location F-Curve. During the production of your game, you may need to come back for tweaks in your animation cycle. Therefore, instead of cleaning the bone curve you can simply disable the root bone channel in the Graph Editor. In Figure 4.41, you can see the speaker icon you use for that.

![Graph Editor - disabling individual bone channels](../figures/Chapter4/Fig04-41.png)

The downside of this method comes when you need to change the root bone as part of your animation. For example, sometimes you don't want your animation cycle to be uniformly moving forward. Even for Momo's walk, it's better if there is a break every time he rests one of the feet as he gets ready for the next step. As you know, the movement of the character will be decoupled from the animation cycle. And, no, we don't get tired of repeating that. So, in this case, if you look at the character from a constantly moving point of reference, it will seem as if Momo is moving forward, then backward, and then forward again to the original position. To move all the bones at once, nothing is better than the root bone. It's not a good idea to rely on a bone that you plan to disable though.

A work-around for that is to have one root bone to control the external position, and another bone (parented to the root bone) to control the internal position, relative to the object location. To avoid this surplus of global control bones, let's look at our second method.

##### If Mohamed Won't Go to the Mountain… <a id="If_Mohamed_Won't_Go_to_the_Mountain…"></a>

…he goes to the beach. Our dear monkey, however, is suntanned enough and might as well stay put. In other words, in this method, Momo never moves. We will instead animate the environment around him.

This method is based on the principle that perception is always relative. For example, on your computer screen, there is no way to distinguish between moving the camera away from the character and moving the character away from the camera. The result will be exactly the same. We will be adding moving placeholders that you can use as a guide to position the feet. Figure 4.42 shows the setup.

![Animation feet place holders](../figures/Chapter4/Fig04-42.png)

This file is on _\Book\Chapter4\tutorial\_walk\_7.placehold.blend_. You can't tell from the picture, but if you play back the animation, you will see the placeholders moving against Momo (or would it be the other way around?). In fact, the camera is static so Momo doesn't really move.

1. Create a simple, easy-to-spot object.

2. Create an Array modifier[md]set the constant offset to be equivalent to one stride and set enough copies to fill the screen.

3. Move the Array object to be aligned with Momo. The feet from your extreme pose should match the position of the array elements.

4. Insert a location keyframe.

5. Advance from frames 1 to 41.

6. Move the array object forward the distance of two strides[md]0.46. (See the note on root bone.)

7. Keyframe the new array object position.

8. In the Graph Editor, change the array object Extrapolation mode to linear extrapolation.

This method requires a bit more setup than the previous one, but it has a big advantage. To work in the between poses (the next step of this tutorial), you will need to keep track of the foot position while the character moves forward. While the body is constantly moving, the feet are planted on the ground until it's their time to get up and get smashed on the floor again. This will prevent the undesirable effect known as _sliding feet_. This problem will be revisited next when we create the poses between the extremes. Figure 4.43 shows the complete walking cycle in different moments; note that the feet are always in the same place relative to the placeholders.

![Animation feet placeholders](../figures/Chapter4/Fig04-43.png)

#### Between Poses <a id="Between_Poses"></a>

So far we have only two poses, the extreme left and the extreme right stride poses. By default, Blender interpolates the keyframed poses, creating a smooth transition between them. This mathematic interpolation is of no use for the final animation. That leaves us with 20 frames to fill between those extreme poses.

From traditional animation literature, you can use two main techniques to create those in-between frames: straight-ahead action and pose-to-pose.

Regardless of the advantages of one or another method (you can learn more about them in the material in the reference section of this chapter), we should attend to the differences in their workflows. In straight-ahead action, you animate frames one-by-one as you go. In pose-to-pose, you create sub-extreme poses and fill in the intervals systematically.

In both cases, you need to ensure that the feet are not sliding while you pose them. Use the technique presented in the previous section to prevent this. Sliding feet and feet going under the ground are hallmarks of not enough frames and automatic interpolation. Avoid them at all costs.

Also, although you can create the animation by posing and keyframing the bones in the 3D view, you might want to tweak them in the Graph Editor. That can spare you from creating too many frames and using the handlers for fine-tuning your transitions. The fewer frames you have, the easier it is to change your animation. In Figure 4.44, you can see the current F-Curves edited for this walking cycle.

![F-Curve tweaks](../figures/Chapter4/Fig04-44.png)

This is no different from the traditional workflow of animation in Blender. It's not even much different from the animation workflow in other 3D software. From the vast amount of techniques and tools available, I used the following for this cycle:

- **IK bone constraints:** Use the IK constrained bones as guides, but remember to keyframe the affected bones as well.

- **AutoKey:** Automatic keyframe insertion in the Timeline Editor header, especially for the straight-ahead action will spare you from a lot of manual keyframing.

- **Show/Hide Handlers (Ctrl+H):** My personal favorite shortcut in the Graph Editor.

- **UV grid:** In the floor to spot feet sliding.

In Figure 4.45, you can see the final result of our take on this. This file is in _\Book\Chapter4\tutorial\_walk\_8.pose\_to\_pose.blend_. Play it back to see it animated. From here, you can either keep working out of your file, take it from the book file, or merge both together. An action, as any other data block in Blender, can be imported and saved over different files (as long as the armature bones don't change their names).

![Walking cycle complete](../figures/Chapter4/Fig04-45.png)

#### Play Time <a id="Play_Time"></a>

Now that the animation cycle is done, it's time to bring it from Blender into the game. You need to set an Action actuator to play the walking action and a Motion Actuator to make it move accordingly.

Let's start by creating the Logic Bricks for the armature. With RigMomo selected, follow the steps in order. In Figure 4.46, you can see how the Logic Editor will look.

1. Add an Always sensor and set Positive Pulse on.

2. Add an Action actuator. Set the action created (for example, Walk), the Play mode to Loop End, and the Start and End Frames to 1 and 40 respectively.

3. Link the Action actuator with the Always sensor; this will automatically create an And controller.

4. Add a Motion actuator and leave the values blank for now.

5. Link the Motion actuator with the same And controller.

![Logic Bricks for animation playback](../figures/Chapter4/Fig04-46.png)

To set the value in the Motion actuator, you need to calculate the object speed in Blender and convert it to the game engine. The calculation is simple and is going to give you the precise speed. If, however, you don't feel like doing math today, let trial and error be your guide.

The speed-in Blender units by seconds-is equal to two strides (0.23 x 2) divided by the number of cycles per second - the frame range of your animation cycle (40) divided by the Blender fps playback value. The game engine uses the same frame rate as Blender, to be set in the Render panel to 30fps. So for Momo, the speed we are working with is 0.35 Blender units per second: 0.46 / (40/30).

The value to use in the Motion actuator is the object speed times the frequency on which the Motion actuator is activated. Since we are using an Always sensor triggering every logic tic, the frequency is 1/60 or 0.017. If you change your game to run at 30 logic tics per second, the frequency would be double (2/60 or 0.033). The multiplication of the speed times the frequency is the value you will add to the component of the actuator. The final Loc is [0, -0.0059, 0] X, Y, and Z respectively (see Figure 4.47).

![Walking Momo](../figures/Chapter4/Fig04-47.png)

In the end, you might want to set the camera to track Momo during the walk. In the sample file, you will see the camera is parented to an empty with an Edit Object > Track To Actuator to follow Momo. Also, the zoom and rotate camera intro effect was brought back from the pretutorial. A checkerboard pattern on the floor will also help to follow the pace of his progression. The final file is shown in Figure 4.47 and can be found on _\Book\Chapter4\tutorial\_walk\_9.playtime.blend_.

### Idle Animation <a id="Idle_Animation"></a>

In the latest file, we set up Momo to walk. We never set it up for him to stop walking, though[md]the Always sensor will play the animation in an infinite loop until you quit the game. To push our animation exercises further, let's create an idle animation for Momo. We will then set up Momo to walk, stop, and walk again. Idle animations are played when the character is waiting for you to make a decision (whether to keep walking, to run, to turn, etc.). So as soon as we stop walking, we will set the character to act accordingly.

Start off by opening the file _\Book\Chapter4\tutorial\_idle\_1.begin.blend_. This is the same file we made in the previous tutorial, duplicated here for convenience (the spinning camera effect was removed again). Select RigMomo and create a new action in the Action Editor inside the Dopesheet. You actually have two options here: you can either create a new blank action or use the Walk action as reference (duplicate it and make changes on top of it). To duplicate the existing action into a new one, you have to click in the number by the action name, as shown in Figure 4.48. This is useful when you are creating variations of the same action (different walking styles, different jumps, and so on).

![Insert a new action](../figures/Chapter4/Fig04-48.png)

In this case, since the actions are very different, there is not much to recycle from the walking cycle to the idle animation. You want to keep only the first and final frames to guarantee a smoother transition between the two animations. If you don't want to bother deleting keyframes, you can create a new action from scratch, maintaining the initial pose by following these steps:

1. Go to frame 1.

2. Unlink the Walk action from the armature (click the X button).

3. Create a new action (click in the + or New button).

4. Rename your new action "Idle."

5. Select all the bones of the armature and keyframe them.

6. Go to a later frame, which will be the final frame for your idle animation. For example, to make an idle animation of 4 seconds, go to frame 121.

7. Set a keyframe for all the bones again.

Now you have a new, blank action to play with. The only rule you need to follow is to avoid animations that require Momo to move around. The reason is that you may need to interrupt the idle animation at any moment as soon as you get back to walking.

The transition between the walking animation and the idle one can be seamless. In the Logic Brick section next, we will explain how to make the walk finish its complete cycle before starting the idle animation. Also, this will have to rely on the blend between poses from both actions for a few frames. This will work only if the pose in the current frame of the idle animation is not very distinct from the pose at the initial frame of the walking action. If the poses are extremely different (for example, Momo is facing opposite directions), the automatic calculated in-between poses will be mathematically correct but artistically awful. This is similar to our reasons for making the between poses in the previous tutorial.

As long as your poses are inside the range of the initial and final frames, the idle animation will play fine. Since you want to avoid moving Momo around, it's a good time to learn how to enhance his facial expressions.

Before you finish the idle animation, you need to set up drivers for your shape keys. You can find the current snapshot file at the end of the next section.

### Making a Face <a id="Making_a_Face"></a>

Do you know the difference between television and a live performance? In television the director has full control of the framing of the shots. It's common to use and abuse close-ups and strong facial expressions as a replacement for expressive body language. In the live theater, the audience may be sitting close or far away from the stage, and they all need to be pleased. (Sure, people fight over a front seat, but the show still has to make sense to everyone.)

Good artists do fine in both mediums. But a pretty face on your HD television screen can be a very boring, disappointing I-want-my-ticket-back experience in a live theater (been there, done that, and slept).

In a game, we have the best and the worst of both worlds. You still can use directed framing for cut scenes. But for most of the game, you must be prepared to produce good, effective animations for close and far distances.

In the previous tutorial, we covered the techniques for a good, full body-language posing. Add some more classic animation techniques (for example, strong silhouettes, lines of action, and exaggeration), and you are good to go. For facial expression, however, we will look at something new. If you have not been reading these chapters in order, now is a good time to go back and read about the shape keys.

#### Shape Keys and Bone Drivers <a id="Shape_Keys_and_Bone_Drivers"></a>

A shape key is like an individual piece of grammar. You need to build a library of poses to use in your animation. Momo already has a few poses previously created. We will use them in our animation posing with the bone-driven technique.

Open the file _\Book\Chapter4\tutorial\_idle\_2.shapekeys\_ui.blend_. This is the initial file with the UI rearranged to work better with the shape keys.

In Figure 4.49, you can see all the poses in the Mesh data panel in the Property Editor for the MeshMomo object. The different poses were created in pairs: smile and ooh; eyebrowsUP and eyebrowsDOWN; eyelidUP and eyelidDOWN. They are all relative to the basis shape. To see the poses change the value by their names in the shape keys slot[md]set the influence value to 1.0 and all the other poses to 0.0. If you want to tweak any of the poses, you need to select the shape and go to the Edit mode. You will no longer be working in the basis shape, so any changes will only be applied to this particular shape.

![Shape smile - Edit mode](../figures/Chapter4/Fig04-49.png)

The shapes are not exclusive. Often, you will have more than one pose active at the same time. Therefore, each shape has very isolated changes. For Momo, you could have a single pose with both the eyelid up and the eyebrow up shapes. However, this would give you no way to play with their influence individually in different actions. Unlike armatures, you have no way to mask out the shapes by using only a few "bones" (or part of the mesh).

Now you can integrate the shape keys into your idle animation. The first thing you need to do is to set bones to drive the shapes. The idea is to use shape keys as "pose libraries" inside your armature animation workflow. Therefore, you will be using control bones from RigMomo to control the influence of each individual shape.

Select RigMomo and switch to the Pose mode. In the walking tutorial, we looked at the bones in the bone layers 1 to 3. Now you can finally turn on layer 4 to see the last bones of Momo's armature. The bones in this layer are all detached from the main armature, as you can see in Figure 4.50.

![Shape key control bones](../figures/Chapter4/Fig04-50.png)

To hook up the control bones with the shape keys, you need to follow the steps. The final driver in the Graph Editor will look like Figure 4.51.

1. Select the MeshMomo object.

2. Select a shape key (for example, smile).

3. Click with the right mouse button in the Influence value.

4. Select Add Driver.

5. Open the Graph Editor.

6. Switch the Edit mode from F-Curve Editor to Drivers.

7. Inside the "Key" channel, select the curve to edit (for example, Value(smile)).

8. Open the Property panel (N).

9. Change Type from Script Expression into Averaged Value.

10. Delete the F-Curve modifier (created by default).

11. In the Object/Bone panel, set RigMomo and the bone to use as controller (for example, Mouth).

![Shape key driver](../figures/Chapter4/Fig04-51.png)

By default, Blender sets the global X coordinate of the bone to drive the shape influence. In the Pose mode, you can move the mouth bone sideways to see the shape influence increasing and decreasing respectively. As with any other bone, you can keyframe the position of this bone controller (mouth) to animate this shape key influence over time.

This is not an effective setup, though. First, it's more intuitive to use the vertical position of the bone to drive this particular shape. Second, it's better if you don't need to move the bone as much as you do now to have significant changes. Sure, these are not deal breakers, but we are here to learn, aren't we?

First, in the Driver panel, change the Transform channel influence from X Location to Z Location and change Space to Local Space. Optionally, you can lock the transformation of X, Y and rotation of the bone[md]we will be using only its Z movements.

Second, you need to map the bone transformations to shape influence. To keep the bone positions not far away for the rest of the armature, we will use the short distance of a tenth Blender unit to control all the shape influences. That creates a curve with two points, [0.0, 0.0] and [0.1, 1.0]. This will map the shape influence to 0.0 when the bone Z pose location is 0.0, and 1.0 when the location is 0.1.

To move the bone up and down will now drive the shape influence as you want. Your file now should match the book file: _\Book\Chapter4\tutorial\_idle\_3.smile\_shapekeydriver.blend_.

For the second pose, "ooh," you will use the same bone controller but with a different mapping. We want to set the "ooh" pose when the bone is in -0.1 and "smile" when it's 0.1, as we have. This will allow a smooth transition between those two extreme poses. Repeat the previous steps all the way to the creation of the F-Curve.

This time the curve will be the reverse of the smile, with two points: [-0.1, 1.0] and [0.0, 0.0]. Figure 4.52 illustrates the final arrangement.

![F-Curves of shape driver influence](../figures/Chapter4/Fig04-52.png)

Additionally, you can add a bone constraint to make sure the bone controller is moving only vertically and that it's always inside the range you are using (-0.1 to 0.1).

Finally, you need to set up the remaining poses[md]eyelid up and down and eyebrow up and down. The setup is the same as for the pair ooh and smile. This time, we will leave them for you, but you can check the final setup file in _\Book\Chapter4\tutorial\_idle\_4.shapekeysdriver.blend_.

### Get Your Hands Dirty <a id="Get_Your_Hands_Dirty"></a>

With the armature ready to pose, you can complete the idle animation. Once things are set, there is no need to worry about anything but the armature poses. Take the previous file and create the complete cycle.

Our attempt of a fun idle animation can be seen on the book file _\Book\Chapter4\tutorial\_idle\_5.action.blend_. The animation is not (yet) set to play in the game engine, but you can play it back in the 3D view. Also remember to change the end frame in your render panel to match the playback of your animation cycle. This will not affect the game engine, but it will help you preview your work in Blender.

After the tutorial section, you can check out the idle and walking animation made by Moraes Júnior especially for this book. In the meantime, enjoy our take on Momo, the happiest monkey in the world (see Figure 4.53).

![Momo idle animation](../figures/Chapter4/Fig04-53.png)

### Wiring Up the Logic Bricks <a id="Wiring_Up_the_Logic_Bricks"></a>

There is only one thing missing. We need to alternate between the two animations: the walking and the idle one. With the latest file open, select RigMomo and in the Logic Editor, make the following changes:

1. Change the Always sensor to a Keyboard sensor with Key set to W.

2. Add a Property Sensor to check whether the frame property is between 39 and 40. Set Invert and turn on Positive and Negative Pulse modes.

3. Connect the Property Sensor to the Motion actuator (Move Forward).

These changes can be seen in Figure 4.54. What you are doing here first is to set the action to play when the W key is pressed. Since the Action Actuator is set to Loop End, the animation will still play for a few more frames. In order to make Momo keep moving forward, you need to keep the Motion Actuator active until the frame played is not the final (40). That way when you release the key, you ensure that the Momo animation is in the beginning of its animation cycle, ready to blend with the idle action.

![Logic Brick, Part 1 - keep walking](../figures/Chapter4/Fig04-54.png)

Now all that is left to be done is to play the idle action when Momo is not walking. Add a Nor Controller connected to the Keyboard and the Property and connect it to a new Action Actuator. The Nor Controller will play this actuator only when both sensors are false. The Action Actuator and the final logic bricks can be seen in Figure 4.55. The explanation for the parameters follows.

![Logic Brick, Part 2 - idle](../figures/Chapter4/Fig04-55.png)

- **Playback type** : Loop Stop will make the action loop until the Keyboard Sensor is active. It will stop immediately after.

- **Priority** : 2[md]it has to be higher than the walking Action Actuator. Lower priority actions have precedence over higher ones.

- **Start/End Frame** : 1 and 160[md]the range of your animation.

- **Blendin** : 11[md]If the pose of the initial frame of the idle animation is the same as the walking, you don't need to blend them (Blendin = 0). Otherwise, this parameter will make the transition smooth.

- **Continue** : False[md]ye want the animation to start over from frame 1 every time you stop walking.

The final file is on _\Book\Chapter4\tutorial\_idle\_6.idlewalkforward.blend_.

### How Many Bricks Does It Take to Turn Momo? <a id="How_Many_Bricks_Does_It_Take_to_Turn_Momo?"></a>

Momo can walk and stop. Now, if only we had a jump, we would be set for a side-scroller platform game (due to copyright restrictions, you will not see a figure of Momo running after a spinning-spiked hedgehog). For a 3D game, however, you need to be able to freely navigate into the levels. And there is no better way than allowing the character to turn around.

The simplest way to make Momo turn is by adding new Motion Actuators responding to a new set of Keyboard Sensors. Let's use the key A to turn left and D to turn right. To make it turn left, follow these instructions:

1. Add Keyboard sensor[md]key A.

2. Add Motion actuator with Rot Z 2.5 degrees.

3. Connect Sensor with Actuator, which creates a new And controller.

4. Change the original cWalk controller from And to Or.

5. Connect the new sensor to this controller as well.

6. Connect the new sensor to the Nor controller.

Now do the same for the right rotation, and you will have the logic bricks shown in Figure 4.56. You may notice that I'm using three States for the controllers here. They are always turned on, thus the main purpose is purely for organization.

![Logic Brick, Part 3 turning](../figures/Chapter4/Fig04-56.png)

Source: Blender Foundation.

The final file is on _\Book\Chapter4\tutorial\_idle\_7.turning.blend_.

>**The Dilemma of the Sweet Miso Soup
>
>Once when I was younger, my hand slipped while seasoning the miso soup and, brilliantly, I thought it was a good idea to compensate for the salt by sweetening it. Guess what, it didn't work (and yes, I had to eat it all).
>The same goes for animation. No one needs to turn right and left the same way. It can be because of a soccer injury, a shorter leg, you name it.
>So sometimes (not always, not now), you need more control over the turning. For the _Yo Frankie_ project, they had specific animations for each side Momo would be turning. Those subanimations make for both good transitions between actions and for more artistic control. It's always a matter of compromising between what you can afford to do and what you can't, which is addressed between the technical and artistic teams. Thus, even though a programmer may insist it is so, an animation for "getting up" is not the same as a "sitting down" animation played backward. For our simple walking cycle, this will do.
>Bottomline: a miso soup with sugar is not a break-even[md]it's bad cooking.

### Hats Off to Momo and Vice-Versa <a id="Hats_Off_to_Momo_and_Vice-Versa"></a>

Momo is a classy monkey, often seen at parties of the animal kingdom's high society. However, when with his inner circle of friends, Momo is actually a very casual monkey[md]not much to show, nothing to hide. One character[md]two quite distinct moments. This is the theme of our animation.

In this tutorial, we will show how to make Momo switch between two kinds of hats: a bouncing hat and a hat that fits tight on its head. We will not only use two different Blender objects, but also animate them differently when worn. To make an object external to the armature follow it, we need two things: a bone and a parented empty.

The bone, which can be animated as any other bone, will indicate Momo's head location and rotation for every frame. The empty, external to the armature, is parented to the bone, and copies the bone transformations automatically during the game. In this tutorial, this empty, working as a placeholder, will be used to place the hat Momo will be wearing.

Start by opening a variation of the latest walking Momo on the book file _\Book\Chapter4\tutorial\_hat\_1.begin.blend_.

If you want to carry these changes to your own working file, you need to append the Hats group into your local file. This also includes the camera object and an empty where we are running the script to control the hat switch. You can see the hats in Figure 4.57.

![Hats for Momo](../figures/Chapter4/Fig04-57.png)

Source: Blender Foundation.

This is a simple tutorial, focusing on illustrating the bone parenting technique. Thus, most of the components are ready for you to hook up with your file (for example, the scripts). Let's first set up one of the hats.

1. Select the armature and go to Edit mode.

2. Create one bone in the middle of the head named Head.Hat.Steady.

3. Parent the bone to the head bone.

4. Change Armature mode to Pose mode.

5. Go to Object mode and create an empty with the same position/rotation as the Head.Hat.Steady bone. Name the empty Head.PH.Hat.Steady.

6. With the empty selected, select the bone you just created and make it the parent of the empty (Ctrl+P  Set Parent To  Bone).

With those changes, you can already animate the bone Head.Hat.Steady, and the empty placeholder will follow along. The hat will be placed exactly where the empty is. In the current file, both hats are parented to empties/placeholders close to the camera. In order to animate the hat bones, you need to temporarily bring the hat to the position it will be during the game. For that to work with the Head.Hat.Steady bone, you need to bring the Hat.Cap Blender object to the same position/rotation as the empty placeholder and parent the hat object to it (select the hat, select the empty, in the Transform panel in the 3D view, right-mouse click in the values to "Copy To Selected," Ctrl+P to parent). Now you can go to the armature Edit mode and move the bone to make the hat fit the head properly. Figure 4.58 shows the arrangement of Bone + Empty + Hat. The current snapshot can be found _in \Book\Chapter4\tutorial\_hat\_2.capsetup.blend_.

![Hat + empty placeholder + hat bone](../figures/Chapter4/Fig04-58.png)

Once the bone is in the right place, you can go over the walking and the idle animations and do some tweaks on its position/rotation over time. For this hat, you don't need to move much. In our case, we only tilted it a bit in the middle of the idle animation to follow the eyebrow raising and some subtle bouncing during the walk. When you now run the game, you will see the hat always in the right place during the animations. To make sure you can follow closely, the file with the animated Hat.Cap can be seen in Figure 4.59 and the book file _\Book\Chapter4\tutorial\_hat\_3.animatedcap.blend_.

![Momo walking in the game with the cap on his head](../figures/Chapter4/Fig04-59.png)

So far so good. Let's now set up the second hat. For this one, you will create a new bone and a new placeholder. The reason is that you will make a different animation for this hat. The classy top hat will be a bit looser, so it should bounce more during the animations.

Start by moving/rotating the Hat.Cap back to its original placeholder by the camera and re-parent it to the empty (Camera.PH.Hat.Cap). Now repeat the same steps you did for the other hat. This time name the bone Head.Hat.Bouncy and the empty Head.PH.Hat.Bouncy. For the animation, make it more exaggerated, with the hat slipping during the walk and the idle actions. Figure 4.60 illustrates one of the moments the hat almost fell off. After moving the Hat.Top object back to its original placeholder (Camera.PH.Hat.Top), your file should be ready for the final adjustments.

![Classy top hat is too big for Momo's head](../figures/Chapter4/Fig04-60.png)

>**Copy Menu Attributes Add-on**
>
>As soon as you start parenting your objects, you will see that it's not so easy to copy over transformations. Blender built-in copy tools work only on top of the local transformations, and this is not enough when you want to copy the visual or world transformations. The difference is that the visual transformations (what you see) are an accumulated result from the different local transformations of the chain of parents.
>Blender comes with an add-on that allows you to do all sorts of advanced copy operations. Go to the User Preferences, Add-Ons and enable the Copy Attributes Menu add-on.
>This add-on was originally intended only to bring over the copy menu (Ctrl+C) from Blender 2.49. Bassam Kurdali, its original developer and maintainer, was kind enough to expand it to help with this tutorial. Kudos to him.
>If you don't want to use add-ons, you can go old school with Blender 2.49 work-arounds. Duplicate your empty and do a Clear Parent  Clear and Keep Transformation in the new empty. Now you can use this object to copy the transformations from, delete it, and parent the hat to the original empty.

Now that the animations are done and the armature set up, we can move on to look to the implementation of hats switching on the fly.

Take the final file _\Book\Chapter4\tutorial\_hat\_4.animatedhats.blend_.

The interaction is simple: click on a hat to switch to it; click anywhere else to bring it back close to the camera. When you pick a hat, the game engine will have to do as you did to tweak the animations: take the selected hat, move it to the head placeholder position, match their rotations, and parent it to this placeholder.

This is done by a script that is already hooked up for the camera. This Python script is very simple, and you should be able to understand it after the Chapter 7, "Python Scripting." The script accesses the objects[md]hats and empty placeholders[md]by their names. Therefore, for your local changes, it's important to follow the names as presented here or tweak the script accordingly.

### Mango Jambo Special Animation <a id="Mango_Jambo_Special_Animation"></a>

The walking cycle you've seen so far is technically correct, and it follows the workflow you can count on, regardless of your animation skills. The bottom line is: with a good method and the understanding of the techniques, although you may not be brilliant, you can't go wrong either.

Now, as the icing on the cake, I've asked the animator Moraes Júnior to do the same thing we did together[md]a new walking cycle and idle animation using the same base file. For reference, he created Momo for the _Yo Frankie_ project and its original animations. After our using and abusing of Momo in the previous pages, it's only fair to see what his "father" would have done instead. Here you can see and study his work and the final contribution: \Book\Chapter4\mangojambo.blend

## To Learn More <a id="To_Learn_More"></a>

Finally, dedicate the proper time to mastering the ways of animation. Learning how to make animation work in Blender is still not the same thing as knowing what to do. Here is a list of classic materials for learning animation[md]modern references for animation and character control in games and Blender-specific reading.

- _Drawn to Life_ by Walt Stanchfield

- _The Animator's Survival__Kit_ by Richard Williams

- _Cartoon Animation_ by Preston Blair

- _3rd Person Action Platformer Hero Animation Graph_ by Rune Vendler

- [_http://altdevblogaday.org/2011/04/14/3rd-person-action-platformer-hero-animation-graph_](http://altdevblogaday.org/2011/04/14/3rd-person-action-platformer-hero-animation-graph)

- _Character Animation DVD_ by William Reynish

- Blender 2.5 Character Animation Cookbook by Virgilio Vasconcelos
