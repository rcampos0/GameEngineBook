**Índice**

- [Capítulo 2: Primeiro Jogo](#Chapter_2_First_Game)
	- [Ideia de Jogo](#Game_Idea)
	- [Elementos do Jogo](#Game_Elements)
	- [Organização do Arquivo, Dados do bloco, e ligação](#File_Organization,_Datablocks,_and_Linking)
	- [Dados do bloco](#Datablocks)
	- [Ligando e Anexando](#Linking_and_Appending)
	- [Como usar o Capítulo de Arquivos](#How_to_Use_the_Chapter_Files)
	- [Modelando](#Modeling)
	- [Texturizando](#Texturing)
	- [Rigging](#Rigging)
	- [Animação](#Animation)
	- [Câmera e teclado](#Camera_and_Keyboard)
	- [Mundo e Ambiente](#World_and_Environment)
	- [Inteligência Artificial](#Artificial_Intelligence)
	- [Tudo voce pode comer](#All_You_Can_Eat)
	- [Sistema de pontuação](#Scoring_System)
	- [Música para seus ouvidos](#Music_for_Your_Ears)
	- [Onde vou daqui](#Where_to_Go_from_Here)

# Capítulo 2: Primeiro Jogo <a id="Chapter_2_First_Game"></a>

Neste capítulo, vamos seguir as etapas de criação de um jogo simples, do começo ao fim. O primeiro objetivo é manter o seu conhecimento do Blender atualizado. Segundo, esta é uma chance de apresentar uma visão geral do fluxo de trabalho do jogo. Desse ponto em diante, você poderá ler os capítulos deste livro em qualquer ordem, de acordo com suas necessidades.

Bem-vindo ao _Feed The Shark, _ o jogo.## Game Idea <a id="Game_Idea"></a>

_A população de tubarões está esgotada em todo o mundo. Estudos sugerem que a pesca excessiva e a comercialização ilegal de barbatanas de tubarão impactaram não apenas o principal predador dos oceanos, mas também trouxeram desequilíbrio para todo o ecossistema.

_É hora da vingança! _

Embora sejamos tentados, não podemos realmente fazer um jogo sangrento aqui. Devido ao risco de perder nosso público adolescente, precisamos fazer alguns compromissos no desenvolvimento da linha da história:

_ Lutando pela sobrevivência, os tubarões precisam comer o máximo possível para escapar dos riscos de extinção.

Claro, quem não gosta de sashimi? Simplificando, precisaremos de um tubarão nadador que coma peixe e seja controlado pelo jogador (como mostrado na Figura 2.1). Toda vez que o tubarão come um peixe, ele se torna cada vez maior.

Para torná-lo mais parecido com um jogo, o envolveremos com um sistema de pontuação e um onipresente relógio de contagem regressiva.

![Alimente o tubarão, o jogo.](../figures/Chapter2/Fig02-01.png)


## Elementos do Jogo <a id="Game_Elements"></a>

Este jogo minimalista consistirá em:

1. Tubarão animado controlado pelo teclado
2. Ambiente subaquático
3. Cardumes de peixes controlados pela IA
4. Interface

Não estamos cobrindo todos os tópicos extensivamente. No entanto, mostraremos algumas das noções básicas de modelagem, animação e outras tarefas específicas do Blender.

Se você já conhece o Blender como uma ferramenta de criação de ativos, pode pular algumas dessas etapas. Você encontrará instantâneos incrementais para todas as partes individuais aqui neste site.

## Organização de arquivos, blocos de dados e vinculação <a id="File_Organization,_Datablocks,_and_Linking"></a>

_Iniciando com a nadadeira direita… _

É importante planejar com antecedência e saber como organizar os arquivos que criaremos. Para este projeto, tentaremos tornar os arquivos o mais independentes possível. Você deve poder abrir o arquivo do tubarão e testar a animação da natação - sem ter que se preocupar com os outros peixes, o terreno ou a interface.

Ter arquivos independentes permite que uma grande equipe trabalhe em conjunto em ativos separados. Também ajuda no controle de versão individual. Pode parecer um exagero para um projeto pequeno, mas é uma boa prática que aumenta bastante.

> **Controle de versão**
>> Controle de versão é qualquer sistema que você pode encontrar para organizar a versão dos seus arquivos. Se você mantiver backups diários de seus arquivos de produção em uma pasta separada, estará executando o controle de versão. Em termos práticos, existem maneiras mais modernas de fazer isso, sem ter que lidar com a renomeação de arquivos e os arquivos de log preenchidos manualmente, como SVN, Git e Bazaar.
>
> Os arquivos do Blender não são ideais quando se trata de mesclagem. (Como são binários, você reverte um arquivo inteiramente ou o faz manualmente.) Portanto, trabalhar com componentes individuais pode ajudá-lo a superar isso.

## Blocos de dados <a id="Datablocks"></a>

No capítulo anterior, apresentamos o conceito de blocos de dados. Blocos de dados vinculados (por exemplo, um bloco de dados de textura usado por um bloco de dados de material) nem precisam fazer parte do mesmo arquivo. Em nosso projeto, vamos usá-lo até certo ponto. Quais são os critérios aqui?

Tomando o material e as texturas como exemplo, você precisa considerar como os usará no seu fluxo de trabalho. Esses dois são frequentemente editados juntos: você ajusta a influência de um canal de textura em seu material, ajusta a cor difusa do material e volta à textura. Nesse caso, é melhor ter os dois blocos de dados no mesmo arquivo.

Agora vamos olhar para armaduras e ações. Somente depois de terminar o seu equipamento, você inicia a animação. Mesmo que você altere sua armadura depois de iniciar a animação, convém mantê-las separadas. Se você precisar voltar para uma versão anterior da armadura, mas quiser manter as novas animações, arquivos separados são o caminho a seguir. Dito isto, poderíamos manter as ações separadas dos principais arquivos de armadura. Poderíamos, mas por uma questão de simplicidade, não o faremos.

Mas como os mantemos vinculados enquanto em arquivos separados?

## Vinculando e anexando <a id="Linking_and_Appending"></a>

Existem quatro maneiras de adicionar novos objetos e outros blocos de dados ao seu arquivo Blender:
- Você pode construí-los do zero.
- Você pode importá-los de um formato diferente (Collada ou FBX, por exemplo).
- Você pode vinculá-los a partir de outro arquivo do Blender.
- Você pode anexá-los de outro arquivo do Blender.

Para vincular parte de outro arquivo do liquidificador, clique em Arquivo> Link (Ctrl + A + O). Em seguida, navegue no seu sistema e encontre o arquivo de origem. Clique nele e você verá algumas pastas que categorizam os blocos de dados. Selecione o (s) bloco (s) de dados pretendidos, configure as opções de vinculação na seção "Link da biblioteca". Por fim, clique em "Link from Library".

![Vinculando blocos de dados](../figures/Chapter2/Fig02-02-1.png  "Linking data blocks")

Para anexar parte de outro arquivo do liquidificador, clique em Arquivo> Anexar (Shift + F1). Em seguida, navegue no seu sistema e encontre o arquivo de origem. Clique nele e você verá algumas pastas que categorizam os blocos de dados. Selecione o (s) bloco (s) de dados pretendido (s), configure as opções anexadas na seção "Anexar da Biblioteca". Por fim, clique em "Anexar da Biblioteca".

![Anexando blocos de dados](../figures/Chapter2/Fig02-02-2.png  "Appending data blocks")

>**Dicas**
>
>- Nos arquivos grandes e complexos do liquidificador, existem muitos arquivos (blocos de dados) e você pode ter problemas para encontrar o arquivo pretendido. Você pode pesquisar itens através da caixa de pesquisa no canto superior direito da caixa de diálogo (mesmo com caracteres curinga). Além disso, você pode filtrar blocos de dados e itens na guia Filtro.
><img alt="Animação de teclas de forma." src="../figures/Chapter2/Fig02-02-3.png" align="center">
>
>- Você pode usar miniaturas para encontrar alguns tipos de blocos de dados mais fáceis. Antes de usar esse recurso, use os comandos Arquivo> Pré-visualizações de dados para gerar miniaturas para blocos de dados (como materiais, texturas, ...).
><img alt="Animação de teclas de forma." src="../figures/Chapter2/Fig02-02-4.png" align="center">

A diferença entre vincular e anexar é o que acontece depois que você traz os novos dados para o seu arquivo. Se você anexar um arquivo - vamos chamá-lo _library_ - os novos elementos não farão referência ao arquivo original da biblioteca. Você pode literalmente excluir o arquivo da biblioteca e não resultará em alterações no seu arquivo de trabalho. Isso também significa que qualquer alteração feita no arquivo da biblioteca não será sincronizada novamente no arquivo de trabalho.

Se você deseja manter os arquivos sincronizados (e o faz na maioria das vezes), é necessário definir "Link" ao importar o arquivo da biblioteca. Ao fazer isso, você não poderá editar o arquivo no seu arquivo de trabalho do Blender. Em vez disso, você precisa voltar ao seu arquivo de biblioteca, alterá-lo, salvá-lo e, em seguida, abrir o arquivo de trabalho novamente.

Como você verá em nossa estrutura de arquivos (explicada a seguir), usaremos principalmente a vinculação entre os arquivos.

Você não despeja simplesmente todo o arquivo do Blender dentro do seu. Em vez disso, você pode navegar dentro da estrutura do arquivo e trazer apenas um objeto ou grupo, material ou mesmo uma cena inteira. Estaremos vinculando o tubarão, a interface, o ambiente e outros peixes no arquivo principal. Também poderíamos fazer links aninhados, fazendo com que um dos arquivos da biblioteca vinculasse outro arquivo dentro dele (por exemplo, as ações poderiam ser vinculadas nos arquivos de armadura).

## Como usar os arquivos de capítulos <a id="How_to_Use_the_Chapter_Files"></a>

Nos arquivos do livro, você encontra o jogo completo (exercício) na pasta Livro / Capítulo02 / jogo / _final /.

Por uma questão de simplicidade, usaremos a sintaxe do caminho relativo do Blender para se referir aos arquivos dentro desta pasta. Nesse caso, // refere-se à pasta base e //interface/score.blend significa Livro / Capítulo02 / jogo / _final / interface / score.blend.

Para jogar dentro do Blender, abra o arquivo game.blend. Este arquivo é apenas uma parte do jogo e depende dos arquivos externos organizados como:

** // ** game.blend

**//** assets **/** shark.blend

**//** assets **/** school.blend

**//** level **/** seabed.blend

**//** interface **/** score.blend

Para acompanhar o andamento das etapas da instrução, temos outras pastas. Copie a pasta inteira no seu computador para trabalhar a partir daí. Estas são as pastas que usaremos:


- ** livro / Capítulo02 / game \ _my ** - A estrutura da pasta semi-vazia a ser preenchida à medida que você avança no capítulo.

- **Livro/Capítulo02/game\_progress** A mesma estrutura de pastas, mas cheia de arquivos de snapshots diferentes. Cada arquivo é nomeado após o nome original mais um número de progresso - por exemplo, game.1.blend, game.1.blend, //assets/shark.8.blend. Para usá-los, você precisa renomear o arquivo para o nome original e copiar para a pasta correta na pasta "game \ _my".

- **Livro/Capítulo02/game\_final** - A final no final deste exercício; use para referência.

- **Livro/Capítulo02/references**  - Arquivos para apoiar a criação do jogo.

No restante do capítulo, vamos nos referir aos arquivos da sua pasta // game \ _my / top.


## Modelando <a id="Modeling"></a>

Abra o Blender e salve o aquivo padrão como //assets/shark.blend.

Nós iremos modelar o outline do tubarão baseado nas imagens de referência. Para configurar seu ambiente de trabalho, siga estes passos:

1. Divida sua vista3d em quatro visões (Ctrl+Alt+Q).

2. Abra o painel de propriedades da vista 3d (N) - lembre que o mouse precisa estar sobre a vista 3d paraenviar o comando para  o painel.

3. No botão do painel, você irá ver a opção de Imagem de fundo. Deixe ativo.

4. Adicione três imagens para os Eixos/Visões: Topo, Frente, e Direita. Eles podem ser encontrados na pasta de referência nomeados shark-top.png, shark-front.png, e shark-right.png.

5. Mude seu tamanho para 3.00.

![Configuração da imagem de Fundo(Blender Foundation).](../figures/Chapter2/Fig02-03.png "Redo last menu.")

O arquivo atual pode ser encontrado sob o nome //assets/shark.1.blend.

Para iniciar o modelo, remova o cubo inicial (X) e adicione um cilindro à cena (Shift + A> Malha> Cilindro). Novos objetos sempre são adicionados à localização do cursor 3D, portanto, verifique se ele está no centro da cena [0,0,0] (Shift + S> Cursor para o centro). O cilindro padrão não corresponde às dimensões ou à orientação do modelo de referência. A maneira rápida de mudar isso é acessar o menu refazer último (F6) e ajustar os parâmetros do cilindro. Como você pode ver na Figura 2.4, usamos 12 vértices, raio de 0,4, profundidade de 1,0, localização Y 0,5 e rotação X 90 graus.

![Refazer o último menu (Blender Foundation).](../figures/Chapter2/Fig02-04.png "Redo last menu.")

Esta será a base para o tubarão. Modelaremos aproximadamente as vistas frontal e lateral, tentando combinar a imagem. Para trabalhar com mais liberdade, vamos personalizar a tela. Como modelaremos apenas as referências de vista lateral e frontal, ajuda a desativar a "visualização em quadruplo" no painel Propriedades na visualização 3D. Em vez disso, dividiremos a tela ao meio (arrastando o triângulo a partir da borda inferior esquerda do editor de vistas em 3D).

Entre no modo de edição e, na vista superior, remova metade da malha (deixando os vértices do meio). Como o tubarão é simétrico, não precisamos modelar suas duas metades. Volte ao modo Objeto e, no painel Propriedades, adicione um Modificador de Espelho. Ative o recorte como ativado e verifique se o eixo do espelho é X. As outras opções padrão estão corretas.

![Modificador de espelho](../figures/Chapter2/Fig02-04-1.png "Mirror Modifier")

Graças ao modificador, você deve ver o cilindro completo novamente. De volta ao modo Editar, qualquer alteração que você fizer será espelhada automaticamente na outra metade, como você pode ver na Figura 2.5.

![Modificador de espelho (Blender Foundation.Cengage Learning).](../figures/Chapter2/Fig02-05.png "Mirror Modifier")

Não podemos fazer muito com a malha atual. Precisamos de mais vértices para modelar o tubarão, e usaremos a ferramenta Loop Cut para isso. No modo de edição, pressione Ctrl + R. Isso mostrará uma borda roxa na parte superior do cilindro. Se você mover o mouse sobre a malha, poderá escolher onde cortá-la. No nosso caso, queremos um corte paralelo à base da geometria. Para confirmar o comando, clique com o botão direito do mouse na janela e mova o mouse para deslizar o novo loop de aresta ou pressione Esc para cortar o meio do cilindro. Se você rolar a roda do mouse antes de confirmar (clique), poderá fazer várias fatias ao mesmo tempo, como mostra a Figura 2.6.

![Corte de loop (Cengage Learning).](../figures/Chapter2/Fig02-06.png "Loop cut")

Cortaremos o cilindro em todas as seções em que o contorno do tubarão tenha uma mudança significativa em sua inclinação. Lembre-se de salvar o arquivo e, se você quiser comparar seu progresso, verifique o arquivo //assets/shark.2.blend.

Como este é um tubarão e não uma salsicha, precisamos acomodar os novos arcos de malha para seguir a imagem de referência. A tecla B ativa a seleção da caixa e permite selecionar um ou mais vértices de uma só vez. Outro atalho útil é Alt + RMB (no linux: Alt + Shift + RMB) em uma das arestas dos loops para selecionar rapidamente o loop da aresta.

![Edge loop](../figures/Chapter2/Fig02-06-1.png "Edge loop")

Com os arcos selecionados, você pode agarrá-los e mover-se (G). Quando necessário, você pode usar a tecla S para dimensioná-los em torno deles. As transformações (rotação, redimensionamento e até mesmo agarrar) sempre acontecem em relação a / ao redor de um pivô. Por padrão, o pivô é o Cursor 3D. Você pode alterá-lo, por exemplo, para girar em torno do centro dos vértices selecionados. Para alterar o pivô, use os atalhos vírgula e ponto (seleção atual e cursor 3D respectivamente) ou o menu no modo Sombreamento. De fato, muitas outras opções no cabeçalho da Visualização 3D são importantes para modelagem (como snap, edição proporcional, seleção de vértice / aresta / face) e podem ser encontradas na Figura 2.7.

![3D View header(Blender Foundation)](../figures/Chapter2/Fig02-07.png "3D View header")

Nesse ponto, você também pode começar a explorar a vista superior. Para alternar rapidamente para a vista superior, use o NumPad7 ou ative ou desative a visualização em quad. Às vezes, você precisa transformar a geometria apenas em um eixo. Na Figura 2.8, você pode usar o manipulador para puxar se desejar mover uma aresta em um eixo específico. Você também pode usar o teclado para isso. Para restringir a transformação, pressione X, Y ou Z após o comando e deslize no eixo especificado. Shift + X, Y ou Z funciona da maneira oposta. Ele bloqueia a transformação para o eixo oposto (para que você só possa mover / dimensionar / girar em um plano). Isso é realmente útil - usamos G com Shift + Z o tempo todo.

![Eixo de transformação travado(Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-08.png "Locked axis transformation")

Você também pode usar a ferramenta Edição proporcional, como mostra a Figura 2.9. Às vezes, você não deseja mover vértices / arestas / faces individuais, e os loops de arestas e as áreas selecionadas pela caixa são grandes demais para serem transformados como um único bloco unificado. Para usar a edição proporcional, pressione O (ou vá para o ícone no cabeçalho da Vista 3D) para ativar e desativar. Agora, se você mover um vértice, todos os vértices vizinhos serão marcados. A influência da ferramenta é determinada pelo círculo ao redor do pivô. (Mais uma vez, veja a importância do pivô?) Você pode aumentar o tamanho do círculo de influência rolando a roda do mouse para cima e para baixo.

![Ferramenta de Edição Proporcional(Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-09.png "Proportional Editing tool")

Com essas ferramentas, você pode chegar ao estágio do arquivo //assets/shark.3.blend. Também neste arquivo, existem algumas linhas de esboço na parte superior da vista 3D; estes são feitos com a ferramenta Lápis de graxa para ajudar a bloquear a forma antes da modelagem. São marcadores temporários e nada mais. Portanto, eles foram removidos assim que o modelo foi finalizado em shark4.blend. Embora já possamos adicionar uma cauda ao tubarão, este pobre tubarão ainda não sabe nadar. Para finalizar as instruções de modelagem, extrudaremos esses bits ausentes. Nesse contexto, extrudar significa retirar uma peça da geometria base, mantendo-a conectada. É mais fácil mostrar do que dizer. No modo de edição, selecione a face na lateral do tubarão e faça a extrusão pressionando E, como mostra a Figura 2.10.

![Extruding(Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-10.png "Extruding")

Depois de inserir o comando de extrusão, uma nova face é criada. Esta face está conectada a na mesma posição da face original. Além disso, ele coloca voce automaticamente no comando Agarrag com o movimento travado no eixo normal (não mais o X, Y ou Z, mas a face normal). Puxe a face o quanto for ncessário (no nosso caso, a imagem de referência frontal deve ser o guia) e clique para finalizá-lo. Se você pressionar Esc, cancelará a parte "Grab" do comando, mas ainda terá a nova face.

>**Transform Orientation**
>
>Se um objeto ou suas partes forem rotacionadas em relação ao eixo global, vocẽ irá encontrar o bloqueio do eixo padrão pouco útil. Portanto, o Blender permite que você defina rapidamente um modo de alinhamento diferente no cabeçho da Visualização 3D (o padrão é Global). Para alternar para ele, insira o eixo desejado duas vezes (por exemplo, X + X). Ao alterar a orientação global, você está, na verdade, alterando a orientação dos controladores Transform (translação, rotação, escala). Uma exceção a este sistema (e amplamente usado) é que quando Global é definido como a orientação global, você obtém transformações locais ao digitar duas vezes seu eixo de bloqueio.
Além disso, um recurso avançado é adicionar Orientações de tranformação personalizadas. Isso pode ser acessado no final do painel Propriedades da Vista 3D.

Como o Modificador Mirror tem as opções "Merge" e "clipping" ativadas, a extrusão não será simplesmente restringida ao normal (o eixo perpendicular à face) inicialmente. Em vez disso, a face extrudada será travada na normal, mas metade dela será travada no plano do espelho. Portanto, ela se comportará como se estivesse travado verticalmente (eixo Z).

Para economiar tempo com a modelagem, iremos adicionar uma cabeça das malhas embutidas no Blender. No modo edit, vá ao menu Add Mesh (Shift + A) e escolha Monkey. você precisará escalar (S), rotacionar (R) e agarrar (G) para que corresponda à imagem de referência. E eles combinam perfeitamente - que feliz coincidẽncia.

Você precisará remover algumas faces do pescoço para conectá-lo à parte superior do corpo. Para excluir faces, use a tecla X.Isso abrirá o menu mostrado na Figura 2.11 - escolha sua opção com sabedoria. Para conectar vértices e arestas, use a tecla F. (Eles precisam ser selecionados, e não mais do que o que pode caber em uma face.)

![Delete menu(Blender Foundation)](../figures/Chapter2/Fig02-11.png "Delete menu")

Para finalizar o modelo, você pode adicionar as nadadeiras nas laterais. Comece selecionando uma face na laterial da malha e extrudando até qeu seja necessário. Como fizemos para o corpo principal do tubarão, devemos adicionar mais seções a nadadeira com a ferramenta Loop Cut.

Você pode refinar seu modelo o quanto quiser. O modelo atual está em // assets/shark.4.blend.

## Texturizando <a id="Texturing"></a>

A pŕoxima etapa não deve levar muito tempo. Para adicionar a pele do tubarão, usaremos uma imagem projetada nas faces. As imagens são bidimensionais. Para combinar os dois, precisamos fazer o equivalente a descascar uma laranja e achatar a casca em uma superfície plana. A casca no plano será a nossa imagem da casca da laranja, permitindo-nos usar uma imagem 2D para o nosso modelo 3D. Outro exemplo é a representação do mapa-múndi onde uma esfera é projetada em um plano, como voce pode ver na Figura 2.12. O processo de mapear a geometria 3D para um plano 2D é chamado de _UV texturing._

![World Map: a superfície 2D equivalente de uma geometria 3D(NASA)](../figures/Chapter2/Fig02-12.png "World Map: 2D surface equivalent of a 3D geometry")

Antes de começar, vá para o painel Modificadores (Modifiers) e aplique o Modificador Espelho (Mirror Modifier). Se você não fizer isso, o tubarão não pode ter uma textura diferente para cada um de seus lados - em vez disso, ele usaria a mesma textura invertida no modelo. Além disso, vocẽ não precisará mais das imagens de fundo. Vocẽ pode desativá-las ou removê-las do arquivo - ambas as opções podem ser encontradas no painel Imagens de Fundo (Background Images) no menu Propriedades de Visualização 3D (3D View Properties Menu).

Para começar a criar uma textura UV, você precisa alternar para o modo Editar e chamar o menu Mapeamento UV (U) (UV Mapping menu). Este menu possui diferentes opções de mapeamento. Estaremos usando o primeiro, Desempacote (Unwrap), que é uma forma semiautomática de calcular o alongamento ideal para a textura 2D. O resultado pode ser visto e editado no Editor de Imagem/UV (UV/Image Editor).

No menu Editor, clique em Imagem > Nova Imagem (Image > New Image), e no menu pop-up, defina o Tipo Gerado (Generate Type) como Grade UV (UV Grid) e confirme. Isso produzirá uma imagem de amostra onde você pode verificar no modelo 3D o quão esticada a imagem do mapa (textura) (texture) será, uma vez que ela for re-projetada no modelo de tubarão. Se você olhar a Figura 2.13, verá um problema com o desempacotamento padrão: a imagem na laeral do tubarão está muito esticada e não tem resolução suficiente. Embora a cauda do tubarão tenha alta resolução, isso não corresponde à sua necessidade (afinal, a cauda é pequena) - quanto menores os quadrados da grade de teste UV, maior a proporção pixel por face.

![Desempacotamento padrão incorreto (Cengage Learning)](../figures/Chapter2/Fig02-13.png "Bad default unwrapping")
Para resolver esse problema, vá para a visualização 3D (3D View) e selecione o loop de borda (edge loop) que separa o nadador lateral do corpo. Com este "anel" selecionado, vá ao menu Borda (Edge) (Ctral + E) e selecione Marcar Costura (Mark Seam). Agora refaça o Mapeamento UV (UV Mapping)  Desempacotamento (Unwrapping), e voce terá um alongamento mais distribuido ao longo da malha. Isso pode ser visto na Figura 2.14 e no arquivo //assets/shark.5.blend.

![Final UV mapping(Blender Foundation-Cengage Learning)](../figures/Chapter2/Fig02-14.png "Final UV mapping")
Seu modelo agora está pronto para a texturização adequada. Na visualização 3D, mude para o Modo de Pintura de Textura e divirta-se. Assim que terminar de pintar, salve a imagem do Editor de Imagem / UV em seu computador em //assets/shark.png.

>**Não Pintar,Não dor**
>
>Há mais na pintura de textura do que podemos cobrir aqui. Mas é importante saber que o recurso está lá e funciona muito bem para retocar a pintura 3D das texturas do jogo. 

Assim, se você não quiser pintar o modelo, pode usar a imagem de referência como textura. Volte para a visão lateral e no menu Mapeamento UV (U) (UV Mapping), defina Visão de Projeto (Project from View). No UV/Editor de Imagem, (UV/Image Editor), selecione a imagem que você usou como referência. Para as nadadeiras laterais, vá para a vista superior e, selecionando apenas elas, repita >O procedimento e escolha a imagem de referẽncia superior.

Outra opção é usar a textura simples de "tatuagem de tubarão" que pintei para o arquivo final do jogo. Este peixe é uma pequena parte da textura, porque a textura corresponde ao layout UV de toda a malha. Se a imagem parecer estranha em seu tubarão, você terá que editar seu layout de UV para torná-lo compatível com o UV do //assets/shark.6.blend. Você encontrará a textura em \Book\Capítulo02\game\_final\assets\textures\shader.png.

A textura precisa fazer parte de um material. Selecione o objeto e, no Editor de Propriedades, abra o painel Material. Crie dois materiais - um para os olhos e outro para o resto do tubarão. No modo de edição, você pode atribuir um material para as faces selecionadas. O material para os olhos não tem sombra e usa o branco como cor difusa. O material do corpo também não tem sombra, mas precisa de uma textura para as informações de cor. Como o material de corpo selecionado,mude para o painel Textura e adicione uma nova textura. O tipo de textura precisa ser "Imagem" ou "Filme" e você precisa escolher a imagem que preparou como textura. Finalmente, vá para a aba Mapping e selecione UV como Coordenada. Desta forma, a textura será mapeada de acordo com o UV que você acabou de criar.

Se vocẽ não está familiarizado com os materiais do Blender, consulte o Capítulo 5, "Gráficos". Você também pode importar os materiais Shark e SharkEyes do arquivo atual em //assets/shark.6.blend.

## Rigging <a id="Rigging"></a>

_Animate the shark…_

Para fazer o tubarão nadar, precisamos de uma armadura com ossos. Semelhante aos ossos reais, os ossos do Blender irão deformar a malha, produzindo a animação do nosso jogo.

A base do arquivo está aqui: //assets/shark.6.blend

A primeira coisa a fazer é adicionar um objeto Armature (Shift + A  Armadura (armature)). É importante ter o centro da armadura no "centro de massa" do tubarão, que por acaso também é o lugar certo para a origem da malha do tubarão. (No nosso caso, está no centro da cena nas coordenadas [0, 0, 0]). Para ter certeza de que entendeu direito, na visualização 3D, olhe para o grande ponto que representa o centro do tubarão ou tente girá-lo usando seu centro como pivô. Se o centro estiver ligeiramente acima das nadadeiras laterais e centralizado no lado mais curto do tubarão, você está pronto para ir (prosseguir adiante). Caso contrário, vocẽ precisa redefinir sua origem com a opção Shift + Ctrl + Alt + C:

1. Mova o cursor 3D para a localização aproximada (ou para pular a próxima etapa, coloque-o em [ 0, 0, 0 ], ou use Shift + C ).

2. Defina sua coordenada X para 0 - o painel de Propriedade mostra a localização exata do cursor 3D.

3. Defina Origem > Origem para o cursor 3D.

Com o cursor 3D no centro do objeto, adicione a armadura ( Shift + A ). No modo Editar da armadura, selecione este osso ( A ou RMB no osso ) e mova-o [nd] 1 unidade em Z. Agora, a cauda do osso está no centro. A cauda é a pequena extremidade do osso, oposto à sua cabeça. este será nosso osso raíz, o osso que controla todos os outros.

Com o cursor 3D ainda no centro, adicione um novo osso ( Shift + A ). Seleciona esta cauda de osso e mova-a (G) até que corresponda à localização da boca, como você pode ver na Figura 2.15. Agora selecione este osso e osso raiz e os parente eles sem vincula-los (Ctrl + P  Manter Offset). Dessa forma, o osso ainda pode se mover livremente, embora seja pai do osso raiz.

![Editando o Osso (Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-15.png "Bone editing")

De volta ao osso raiz: selecione sua cauda e extrude-o. (E). Esta é outra maneira de adicionar ossos, conectando-os automaticamente. Mova o osso extrudado para o início da cauda do tubarão. Agora repita o procedimento parao novo osso, extrudando-o até o final da cuda do tubarão. A figura 2.16 mostra os ossos atuais conforme vistos em //assets/shark.7.blend.

![Armature Bones(Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-16.png "Armature Bones")

Before animating the shark, we need to link the armature with the mesh. This is done with the Set Parent To operator:

In the Object mode, select the shark mesh and then the shark armature and Ctrl+P  Armature Deform  With Automatic Weights. This will try to automatically set the influence of each bone in the mesh. For fine-tuning, select the armature, set it to Pose Mode, and then select the mesh and set it to Weight Paint mode. Now you can select the bones individually and paint their influence over the vertices as shown in Figure 2.17.

![Weight painting(Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-17.png "Weight painting")


>**X-Ray and Auto-Normalize**
>
>With the armature selected, go to the Properties Data panel and set X-Ray on in the armature display-this will make the bones always be visible. Also, while weight painting, you can set Auto Normalize in the Tool panel-this ensures that all bone-deforming vertex groups don't add up to 1.0 while weight painting.


To test the bone weighting, move the bones around (in the Pose not Edit Mode) and see if the mesh goes with it. The file is ready for animation and can be found here: //assets/shark.8.blend.

## Animation <a id="Animation"></a>

To create an animation, you need to define the individual poses that will build up the illusion of movement. As an artist, you can define the poses frame by frame or work in a few moments of the animation. For example, you can define just a few frames, and Blender will automatically calculate the missing frames for the animation. It depends on how much control you want.


>**When 206 Bones Are Too Many**
>
>The animation complexity is also directly related to the number of bones created in your rig. For this game, we are not using many bones for simplicity's sake. In Chapter 4, "Animation," you will find more robust examples.


We will create a swimming cycle-an animation where the first and the last poses are the same and can be played seamlessly in a loop. Let's start by the following these steps:


1. Set the current frame to the initial one (Shift+Left).

2. Select the armature.

3. Change to the Pose mode.


Rotate the tailbone 50 degrees clockwise in the Z axis. Rotate the head bone 5 degrees counter-clockwise in the same axis. Select all bones (A) and insert a keyframe (ILocRot). This will be our pose for the first frame. The current file is at //assets/shark.9.blend and is shown in Figure 2.18.

![Initial pose(Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-18.png "Initial pose")

To create a cycle, you need the beginning and end frames to match. Move to frame 31 (through the Timeline or Shift+Up six times) and add a new keyframe for the same pose.

There are different ways to see your animation in Blender. Change your current screen to Animation (in the header menu where you see Default). This screen shows the three animation editors: Dopesheet, Graph Editor, and Timeline, as you can see in Figure 2.19.

![Animation screen(Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-19.png "Animation screen")

In the Dopesheet, you can see where we have added keyframes so far. The two points and the line connecting them mean that there is no change between the two poses. The other way of adding a new pose is by selecting the keyframes in the Dopesheet and duplicating them. As with the other editors in Blender, you can grab (G), scale (S), copy (Shift+D), and toggle all selection (A) using the same shortcuts you are used to.

The middle pose of the animation cycle should be opposite to the initial (and final) pose. Blender has a simple way to flip poses. In Figure 2.20, you can see the Paste Flipped option in the 3D View header.


1. Change to the Pose Mode.

2. Select all bones (A).

3. Click on Copy Pose in the 3D View header.

4. Go to frame 15.

5. Click on Paste Flipped Pose.

6. Store the keyframes (I).


![Copy and paste Flipped Pose buttons(Blender Foundation)](../figures/Chapter2/Fig02-20.png "Copy and paste Flipped Pose buttons")


>**Bones Mirroring**
>
>If your rigs have bones bifurcating from the main bone chain, there is a special way to make them mirror. By default, Blender will try to paste the pose of the same bone mirrored relative to the Y axis. Sometimes, however, you want to swap the transformations between two bones-a left and right. The classic example is walking animations when you need to animate only half of the strides.
>To have Blender interpret the bones as two sides of the same bone, you need to name them L (for left bones) and R (for right bones). This way, the bone Swimmer.001.L will be treated as the pair of Swimmer.001.R, and their poses will be swapped and mirrored when using the Pose Flip Paste option. To learn more about this, refer to the walking cycle tutorial in the Chapter 4.


The swimming animation is now finished. In the Timeline, set the final playback frame to 30. Playing back the animation (Alt+A) will reveal our lovely and clumsy swimming cycle. In the Dopesheet, switch the Display mode to Action Editor. There you can change the name of the current action to "SharkSwimming," as shown in Figure 2.21.

![Action Editor header(Blender Foundation)](../figures/Chapter2/Fig02-21.png "Action Editor header")

The current snapshot of this file is //assets/shark.10.blend.

You can also do a "SharkAttack" animation. For a smooth transition, make the new action with the same initial and final poses as the "SharkSwimming." If you go with that, use the attack animation when the shark eats a fish.

## Camera and Keyboard <a id="Camera_and_Keyboard"></a>

After all the hard work of setting up your main character, it's time to bring in the game. If you play (P) the game now, you will see nothing but the shark standing still.


>**Playing and Quitting the Game**
>
>Every time you need to test the current status of the game, you can launch it from the Game menu (available when the Engine is set to Game Engine) or by using the shortcut P. To quit the running game and go back to the regular Blender environment, use the Exit key set in the game Render panel (Esc by default).


We will now set up the logic bricks. You'll learn more about logic bricks in the next chapter. They are the visual components of the logic and interaction of the game. The shark animation and movement will be controlled with logic bricks. We will also set up the camera control and motion.

The shark will always be swimming. Thus, we will be playing the swimming animation constantly:


1. Change your screen from animation to game logic.

2. In the Logic Editor, add an Always sensor (Shift+ASensorAlways).

3. Add an Action actuator and connect it with the sensor.

4. In the Action actuator: mode Loop Stop, action SharkSwimming, start frame 1 and end frame 30.


Now that the shark can swim, you want it to move around. The controls of the game are simple: use the spacebar to swim forward; left and right to rotate; up and down to emerge and submerge. You have to add a Keyboard sensor for each of those keys and connect them as such:


- Left key => Motion actuator: RotZ = 1° and disable L for rotation

- Right key => Motion actuator: RotZ = -1° and disable L for rotation

- Up key => Motion actuator: RotX = 1°

- Down key => Motion actuator: RotX = -1°

- Space key => Motion actuator: LocY = -0.05


Test your progress inside the game (P) and remember to always save. If your file is showing a different result than the file at //assets/shark.11.blend, check the logic bricks in Figure 2.22.

![Motion actuators(Blender Foundation)](../figures/Chapter2/Fig02-22.png "Motion actuators")

This simple setup allows the shark to swim freely away from the camera. To have the camera following the shark, select the camera and do the following:


1. Add an Always sensor.

2. Add a Camera actuator and connect it with the sensor.

3. In the Camera actuator, set SharkArmature as object, height 5.0, axis [nd]Y, min 5.0, max 20.0, damping 0.10.


This camera will be behind the shark, always trying to stay inside the specified distance (from 5 to 20 Blender units). The damping will set how fast you want the camera to adjust to the new position while the shark swims away.

If you are modeling everything from scratch, you should tweak the speed and angle of the shark Motion actuator and the damping and distance of the camera to better accommodate the scale of your work.

With the shark alone in the scene, it's hard to tell how it is moving. It's time to add other objects to the scene so you can make sure that the camera settings and the shark motion are well adjusted. Thus, the next step is to add the world (the SeaBed et al). In the meantime, you can compare the status of your file with: //assets/shark.12.blend.

## World and Environment <a id="World_and_Environment"></a>

We will leave the shark file for now and put the game pieces together. Open the file //game.1.blend. This empty file will be the main file of the game. If you want to start a file from scratch, open the Blender default file, delete everything from it (press A to select all and then X to delete), and change engine to Blender Game and Shading mode to GLSL.

You need to bring the shark model into this file. Start by linking in the SharkMesh and the SharkArmature objects from the shark asset file. Go to the menu File > Link, navigate to the shark blend file, and once in it, navigate inside "Object," select the SharkArmature and SharkMesh objects, and press OK. A screen capture of the linking options is shown in Figure 2.23. The defaults options are good for now.

![Linking options(Blender Foundation)](../figures/Chapter2/Fig02-23.png "Linking options")

It's important to save your file first; otherwise, the Relative Path option will have no effect. Linking keeps your shark file as an external asset. Any changes you make in the shark.blend file will be transferred over to the game.blend file, once you save it. That also means you cannot make changes in the asset objects through the game.blend file. If you linked before you saved the file, no worries. You can change all the file paths going to the menu File > External Data > Make All Paths Absolute.

The camera doesn't need to be linked. In fact, it's better to keep it as a local object, given that you will certainly adjust its parameters later. To append (not link) the camera, use the menu File  Append and use the default options to import the camera. This will be the main camera for the game. Select the camera and in the 3D View header, choose View > Cameras > Set Active Object as Camera. If everything went right, you can now play your game, and it should behave just as in the shark.blend file.

Good news. The SeaBed was already prepared and is ready for the game (and in your game\_my asset folder). Repeat the linking steps once again for the SeaBed group inside the //level/seabed.blend. You now have the shark, the camera, and the set prepared for the game. The progress shown in Figure 2.24 can be checked at //game.2.blend.

![Shark, camera, and SeaBed(Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-24.png "Shark, camera, and SeaBed")

To simulate the water, we will add a blue mist effect. This produces an effect similar to fog and gives a nice water attenuation effect (where everything eventually fades to blue). Follow these steps:


1. Switch to the World panel in the Properties Editor.

2. Create a new World.

3. Set Horizon Color to Hex: 264A6B.

4. Turn Mist on and set Start 0.0 and Depth 50.0


In order to preview the color and the mist effect in the 3D Viewport, you need to set Viewport Shading to Texture (Alt+Z), as shown in Figure 2.25. The World is now finished and part of the //game3.blend file.

![Mist effect-preview in 3D View(Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-25.png "Mist effect-preview in 3D View")

Play your game and swim around with the shark. However, there is one basic element missing in our survival shark game: the food.

## Artificial Intelligence <a id="Artificial_Intelligence"></a>

While the shark is 100 percent interactive, controlled by the player, the fish will be controlled through a simple AI (artificial intelligence) mechanic. The principles are simple: the fish's swimming cycle is handled by logic bricks, while the fish's constant spawning inflow is controlled by an individual "program" (a script) responsible for the following components:


- Populating the game with fish schools.

- Making the fish follow a "fish leader."

- Killing some fish when the shark attacks.



>**Speaking of Scripts**
>
>Scripts can also be used to complement the functionality of a component of the game. The score scene is using logic bricks to handle the score, but it needs a script to handle the time out, the game over, and to change the resolution of all the text objects. We'll explain more about that in the "Scoring System" section of this chapter.


Once again, we will take advantage of a system with linkable assets. Instead of creating the fish school yourself, you will bring it inside your game, ready to use.

Start by reopening the current version of the file //game.blend. Now you need to link the group FishSchool from the file //assets/school.blend. (This time, instead of navigating in the Object subfolder, go to Group.) If you link a group in with the "Instance Groups"  option enabled, you will end up with an instance of this group added to the scene. This "group instance" is nothing more than an empty object that is used to place a Blender group in the scene. The group is linked from the original file, thus changes made there are kept in sync with your game file.

In Figure 2.26, you can see the game with the school of fish around the shark. If you open the file school.blend, you can see an empty (FishLeader) in the visible layer and an object (Fish) in the second layer (which is and has to be hidden by default). The empty is always rotating and adding more of the fish model into the scene. A fish is added every second or so until the limit specified in the FishLeader game property, maxFish, is reached. Change this number from 30 to 100 and fish will flood you. Decrease to 5, and you make the game even harder. Select the FishLeader, and you will see some new logic bricks. Pay particular attention to the Python controllers.

![School of fish(Cengage Learning)](../figures/Chapter2/Fig02-26.png "School of fish")

The script allows for more direct manipulation of your game elements, complex math computations, and a denser logic for your game play. If you look at the scripts in this file (in the text editor), you'll see you have nothing to be scared of. This is a simple textual way to describe interactive behaviors for your game. And it's far simpler than the hardcore task of programming an entire game engine. Cheers for the compromise. In Figure 2.27, you can look at the game property and logic bricks (including the script controllers) of the FishLeader.


>**Art Versus Math**
>
>"But I'm an artist and don't understand math." Sure, we get that a lot. But bear in mind that here you only need to understand the mechanics of when to rely on a script and what you can do with it. For a more in-depth overview of this topic, see Chapter 7, "Python Scripting," later in the book. Also, the math you need for Python scripting is more accessible than most people assume. Unless, of course, you are planning to run for Miss U.S.A. [http://youtu.be/9QBv2CFTSWU](http://youtu.be/9QBv2CFTSWU)


If you want to do your own customizations, try to animate the fish with bones. You can follow all the steps we did for the shark. Additionally, remember to change the object being added by the FishLeader "AddFish" actuator (see Figure 2.27). Instead of adding the fish, you will have to add the fish parent (the FishArmature object you will create). The armature child (the fish itself) will be added together automatically.

![Logic bricks and Game Property of the FishLeader(Blender Foundation)](../figures/Chapter2/Fig02-27.png "Logic bricks and Game Property of the FishLeader")

The current checkpoint is at //game.4.blend. If you changed your //assets/school.blend file, you need only replace the one in the sources with yours. As we mentioned (three times already, anyone counting?), the new data will be automatically synced in the game. Play your game, and get ready to wrap up the shark feeding.

## All You Can Eat <a id="All_You_Can_Eat"></a>

If you try to catch the fish with the shark, you will see that the shark pushes the fish away. For the game, we need three things to happen: (1) the fish needs to die, (2) the shark needs to get bigger, (3) a score on the screen needs to tell how many fish we caught and how much time we have left.

The score system will be made in the next section. For now, we will focus on making the shark and the little fish interact.

The school of fish is, in fact, already set up. But let's look at what we have there. Open the file //assets/school.blend. In the second layer, select the fish and look at the logic bricks, shown in Figure 2.28.

![Fish school logic bricks(Blender Foundation)](../figures/Chapter2/Fig02-28.png "Fish school logic bricks")

We have a Collision sensor that will only be active when touching an object that has a "shark" property. We don't want to know when one fish collides with another or with the seabed, for that matter. This filter addresses that. The sensor is connected to a Python controller "killMe.py" that takes care of some housekeeping. It tells the FishLeader that we will need a new fish soon. The controller also activates two actuators: one to kill the fish, and the second to send a message indicating a fish went down.

This message is like spam mail. It doesn't matter if you have a mail-only sign in your mailbox. It doesn't even matter if you don't have a mailbox. You will receive the McDonald's coupon you never asked for. (And you will end up eating there-damned spammers!)

And so will the shark. Once the shark receives a message, it can act accordingly. In our case, we want to make the shark big. To do so, open the file shark.12.blend again. Until now, we have been adding all the logic bricks to the armature. Now let's put the armature aside and use the mesh:


1. Select the SharkMesh object.

2. Add a keyframe to the size (IScaling).

3. Go to frame 100, scale up the shark, and repeat the previous step.

4. Open the Logic Editor.

5. Create a Boolean game property named "shark."

6. Create an Integer game property named "size."

7. Add a Message sensor with the subject "Sharked"

8. Add a Property actuator: mode Add, property "size," and value 1.

9. Add an Action actuator: mode Property, action SharkMeshAction, and property "size."

10. Connect the sensor with both actuators.


The final shark file is at //assets/shark.13.blend. In Figure 2.29, we have a screen of the logic bricks setup.

![Shark ready to grow(Blender Foundation)](../figures/Chapter2/Fig02-29.png "Shark ready to grow")

We started by creating an animation for the shark. This animation is played according to a game property (size) that will increase every time a message is received. The message gets to the shark every time a fish is eaten (for example, collides with the shark). Thus, we have a good synchronization between fish disappearing and the shark getting bigger.

Apart from that, the shark needs the "shark" game property to be detected by the fish school. This will trigger the collision. The collision sensor simply checks if the object has a property with a given name, so the type and value of the property are arbitrary (in our case, we are using a Boolean property, but it could be any other property type). Now one by one, we can eat the fish. And it's time to count sheep.

## Scoring System <a id="Scoring_System"></a>

The score system of the game is part of its interface built on top of the 3D view. In Figure 2.30, you can see the main elements of the interface: the score on the top left, the time countdown on the top right, and the title of the game on the bottom right.

![Interface elements(Blender Foundation)](../figures/Chapter2/Fig02-30.png "Interface elements")

The user interface is independent from the game file, objects, and events. Thanks to the messaging system of the game engine (the combination message actuator and message sensors), you can implement the interface as a separate file with its own logic. Open the interface file in //interface/score.blend. The diagram in Figure 2.31 illustrates the dynamic of its elements and the message flow.

![Message system diagram(Cengage Learning)](../figures/Chapter2/Fig02-31.png "Message system diagram")

Now you have two sets of independent and concurrent events. On the one hand, you can  update the score every time a message comes from a fish saying it got "sharked" (a fish collided with the shark). This is pretty straightforward and happens for as long as the game is not over.

The game is over when you run out of time, which is part of the second set of events. The time system is an independent countdown timer (using a timer game property). It updates the time in the interface and sends a message to all the game elements when the time is up, and the game is over. This message is used to freeze the fish-counting and trigger an action to move the score to its final position, as you can see in Figure 2.32.

![Game over interface(Cengage Learning)](../figures/Chapter2/Fig02-32.png "Game over interface")

This scene will be imported without changes into your game file. Once again, the linking system of Blender allow you to keep components separated and synced. Open //game.4.blend and link (not append) the "Score" scene from the //interface/score.blend file. Although the scene is now in the Blender file, you still need to load it into the game:


1. Add an empty object (Shift+AEmpty).

2. Select the object and open the Logic Editor.

3. Add an Always sensor.

4. Add a Scene actuator: mode Add Overlay Scene, scene "Score."

5. Connect the sensor with the actuator.


Now the game is a combination of two scenes that work as separate layers. The file is at //game.5.blend. In Figures 2.33 and 2.34, you can see the user interface integrated within the game.

![Game start(Cengage Learning)](../figures/Chapter2/Fig02-33.png "Game start")

![Game over(Cengage Learning)](../figures/Chapter2/Fig02-34.png "Game over")

## Music for Your Ears <a id="Music_for_Your_Ears"></a>

A game is not complete without sound effects. There are three sounds under // sounds/: the ambient sound (water.m4a), the eating-fish effect (sharked.m4a), and the ending sound (gameover.m4a). This is the farewell set of instructions for this chapter and a prelude for the following chapter (entirely on logic bricks). Speaking of the lack of images, those are sound samples. Feel free to whistle along.

- **Ambient sound** : Add a Sound actuator; load the sound file (water.m4a). Mode: Loop End, Volume: 2. Connect it to the Always sensor you created to load the UI. This will play the ambient sound through the whole game in an eternal loop.

- **Eating-fish sound** : Add a Message sensor with subject: "Sharked" and a Sound actuator; load the sound file (sharked.m4a). Mode: Play End, Volume: 2. Connect the sensor with the actuator. Every time a fish is eaten, the sound effect will be played.

- **Ending game sound** : Add a Message sensor with subject: "GameOver" and connect it to a new Sound actuator; load the sound file (gameover.m4a). Mode: Play End, Volume: 0.3.

There is a catch here. You are sending the GameOver message not once but continuously. That would make the GameOver sound play in loop, which you don't want. You can fix this in the score.blend scene file (by sending the message only once). Or else you can do it here, as follows:

You need a Boolean game property that tells you what the status of the game is: when gameover is False the game is running; if gameover is True the game is over. When you receive a message with the subject "GameOver," you need to change the value of this property. You do this by connecting the Message sensor with a new Property actuator -Mode: Assign, Property: "gameover," Value: True.

Next you add a Property sensor named GameIsNotOver to detect if the game is running (if the gameover game property is True or False). Set Evaluation Type to Equal, property to "gameover," and Value as False.

Connect this sensor to the And controller of the game over Sound actuator. Optionally, you can also link this sensor to the And controller of the eating-fish Sound actuator. This will make the sound effects stop after the game is over. The ambient sound should still play; thus, there is no need to connect the GameIsNotOver sensor with the And controller of the ambient Sound. The final logic bricks can be seen in Figure 2.35

![Sound logic bricks(Blender Foundation)](../figures/Chapter2/Fig02-35.png "Sound logic bricks")

The final file is at //game.6.blend.

## Where to Go from Here <a id="Where_to_Go_from_Here"></a>

The game is complete: the final files are in \Book\Chapter02\game\_final\game.blend.

The modular approach we took allows for easy customization of the individual elements of the game. As you advance in the book, you should try to keep evolving the games files. Create a new user interface. Create multiple shark animations. Change all your assets.

If you want to share your version of the Feed the Shark the game, please host it online and send us a link. If there are enough contributions, we will make them available on the book's home page.
