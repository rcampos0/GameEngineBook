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

A primeira coisa a fazer é adicionar um objeto Armature (Shift + A  Armadura (armature)). É importante ter o centro da armadura no "centro de massa" do tubarão, que por acaso também é o lugar certo para a origem da malha do tubarão. (No nosso caso, está no centro da cena nas coordenadas [0, 0, 0]). Para ter certeza de que entendeu direito, na visualização 3D, olhe para o grande ponto que representa o centro do tubarão ou tente girá-lo usando seu centro de pivô. Se o centro estiver ligeiramente acima das nadadeiras laterais e centralizado no lado curto do tubarão, você está pronto para prosseguir. Caso contrário, você precisa redefinir sua origem com a opção Shift + Ctrl + Alt + C:

1. Mova o cursor 3D para a localização aproximada (ou para pular a próxima etapa, coloque-o em [0, 0, 0] ou use Shift + C).

2. Defina sua coordenada X como 0 - o painel de Propriedades mostra a localização exata do cursor 3D.

3. Defina Origem > Origem para o cursor 3D.

Com o cursor 3D no centro do objeto, adicione a armadura (Shift + A). No modo Editar da armadura, selecione esse osso (A ou RMB nele) e mova-o [nd] 1 unidade em Z. Agora, a cauda do osso está no centro. A cauda é a pequena extremidade do osso, opostá à sua cabeça. Este será o nosso osso raiz, o osso que controla todos os outros.

Com o cursor 3D ainda no centro, adicione um novo osso (Shift + A). Selecione esta cauda de osso e mova-a (G) até que corresponda à localização da boca, como você pode ver na Figura 2.15. Agora selecione este osso e o osso raiz e os parente sem vinculá-los (Ctrl + P  Manter Offset). Dessa forma, o osso ainda pode se mover livremente, embora seja pai do osso raiz.

![Editando o Osso(Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-15.png "Bone editing")

De volta ao osso raiz: selecione sua cauda e extrude-o (E). Esta é outra maneira de adicionar ossos, conectando-os automaticamente. Mova o osso extrudado para o início da cauda do tubarão. Agora repita o procedimento para o novo osso, extrudando-o até o final da cauda do tubarão. A Figura 2.16 mostra os ossos atuais conforme vistos em //assets/shark.7.blend.

![Armadura de Osso (Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-16.png "Armature Bones")

Antes de animar o tubarão, precisamos vincular a armadura à malha. Isso é feito o comando Set Parent To Operator:

No modo Objeto, selecione a malha de tubarão e, em seguida, a armadura de tubarão e Ctrl + P  Deformar Armadura  Com Pesos automáticos. Isso tentará definir automaticamente a influência de cada osso na malha. Para fazer o ajuste fino, selecione a armadura, defina-a para o modo de pose e, a seguir, selecione a malha e defina-a para o modo de pintura de peso. Agora você pode selecionar os ossos individualmente e pintar sua influência sobre os vértices, conforme mostrado na Figura 2.17.

![Pintando os pesos (Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-17.png "Weight painting")


>**X-Ray and Auto-Normalize**
>
>Com a armadura selecionada, vá para o painel Propriedades de Dados e ative o X-Ray no visor da armadura - isso fará com que os ossos estejam sempre visíveis. Além disso, durante a pintura de peso, você pode definir a normalização automática no painel Ferramentas - isso garante que todos os grupos de vértices de deformação óssea não totalizem 1,0 durante a pintura de peso.


Para testar o peso do osso, mova os ossos ao redor (no modo Pose não Edit) e veja se a malha vai junto. O arquivo está pronto para animação e pode ser encontrado aqui: //assets/shark.8.blend.

## Animação <a id="Animation"></a>

Para criar uma animação, você precisa definir as poses individuais que criarão a ilusão de movimento. Como artista, você pode definir as poses quadro a quadro ou trabalhar em alguns momentos da animação. Por exemplo, você pode definir apenas alguns frames, e o Blender irá calcular automaticamente os frames que faltam para a animação. Depende de quanto controle você deseja.

>**Quando 206 ossos são muitos**
>
>A complexidade da animação também está diretamente relacionada ao número de bones criados em seu rig. Para este jogo, não estamos usando muitos ossos por uma questão de simplicidade. No Capítulo 4, "Animação", você encontrará exemplos mais robustos.

Vamos criar um ciclo de natação - uma animação em que a primeira e a última poses são iguais e podem ser reproduzidas continuamente em um loop. Vamos começar seguindo estas etapas:
1. Defina o quadro atual para o inicial (Shift + Esquerda).

2. Selecione a armadura.

3. Mude para o modo Pose.


Gire o cóccix 50 graus no sentido horário no eixo Z. Gire o osso da cabeça 5 graus no sentido anti-horário no mesmo eixo. Selecione todos os ossos (A) e insira um quadro-chave (ILocRot). Essa será nossa pose para o primeiro frame. O arquivo atual está em //assets/shark.9.blend e é mostrado na Figura 2.18.

![Pose Inicial(Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-18.png "Initial pose")

Para criar um ciclo, você precisa dos quadros inicial e final correspondentes. Vá para o frame 31 (por meio da Linha do tempo ou Shift + Up seis vezes) e adicione um novo quadro-chave para a mesma pose.
Existem diferentes maneiras de ver sua animação no Blender. Mude sua tela atual para Animação (no menu do cabeçalho, onde você vê Padrão). Essa tela mostra os três editores de animação: Dopesheet, Graph Editor e Timeline, como você pode ver na Figura 2.19.

![Animation screen(Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-19.png "Animation screen")

No Dopesheet, você pode ver onde adicionamos frames-chave até agora. Os dois pontos e a linha que os conecta significam que não há mudança entre as duas poses. A outra maneira de adicionar uma nova pose é selecionar os quadros-chave no Dopesheet e duplicá-los. Como com os outros editores no Blender, você pode pegar (G), dimensionar (S), copiar (Shift + D), e alternar todas as seleções (A) usando os mesmos atalhos que você está acostumado.

A pose do meio do ciclo de animação deve ser oposta à pose inicial (e final). O Blender tem uma maneira simples de virar poses. Na Figura 2.20, você pode ver a opção Colar invertido no cabeçalho da visualização 3D.


1. Mude para o modo de pose.

2. Selecione todos os ossos (A).

3. Clique em Copy Pose no cabeçalho da vista 3D.

4. Vá para o frame 15.

5. Clique em Colar posição invertida.

6. Armazene os quadros-chave (I).


![Copia e Cola Flipped Pose buttons(Blender Foundation)](../figures/Chapter2/Fig02-20.png "Copy and paste Flipped Pose buttons")


>**Espelhando Ossos**
>
>Se suas plataformas têm ossos bifurcando da cadeia de ossos principal, há uma maneira especial de fazê-los espelhar. Por padrão, o Blender tentará colar a pose do mesmo osso espelhado em relação ao eixo Y. Às vezes, no entanto, você deseja trocar as transformações entre dois ossos - um esquerdo e um direito. O exemplo clássico são as animações de caminhada, quando você precisa animar apenas metade das passadas.
>Para que o Blender interprete os ossos como dois lados do mesmo osso, você precisa nomeá-los L (para ossos esquerdos) e R (para ossos direitos). Desta forma, o osso Swimmer.001.L será tratado como o par de Swimmer.001.R, e suas poses serão trocadas e espelhadas ao usar a opção Pose Flip Paste. Para saber mais sobre isso, consulte o tutorial de ciclismo de caminhada no Capítulo 4.

A animação de natação está concluída. Na linha de tempo, defina o quadro de reprodução final para 30. Reproduzir a animação (Alt + A) revelará nosso adorável e desajeitado ciclo de natação. No Dopesheet, mude o modo Display para Action Editor. Lá você pode alterar o nome da ação atual para "SharkSwimming", conforme mostrado na Figura 2.21.

![Action Editor header(Blender Foundation)](../figures/Chapter2/Fig02-21.png "Action Editor header")

O instantâneo atual deste arquivo é //assets/shark.10.blend.

Você também pode fazer uma animação "SharkAttack". Para uma transição suave, faça a nova ação com as mesmas poses inicial e final do "SharkSwimming". Se você continuar, use a animação de ataque quando o tubarão comer um peixe.

## Camera e Keyboard <a id="Camera_and_Keyboard"></a>

Depois de todo o trabalho árduo de configurar seu personagem principal, é hora de entrar no jogo. Se você jogar (P) o jogo agora, não verá nada além do tubarão parado.


>**Jogando e Saindo do Jogo**
>
>Toda vez que você precisar testar o status atual do jogo, pode iniciá-lo a partir do menu Jogo (disponível quando o Motor está configurado como Game Engine) ou usando o atalho P. Para sair do jogo em execução e voltar ao normal No ambiente do Blender, use a tecla Exit definida no painel Render do jogo (Esc por padrão).


Agora vamos configurar os blocos lógicos. Você aprenderá mais sobre tijolos lógicos no próximo capítulo. Eles são os componentes visuais da lógica e da interação do jogo. A animação e o movimento do tubarão serão controlados com tijolos lógicos. Também configuraremos o controle e o movimento da câmera.

O tubarão sempre estará nadando. Assim, reproduziremos a animação de natação constantemente:


1. Mude sua tela de animação para lógica de jogo.

2. No Logic Editor, adicione um sensor Always (Shift + ASensorSempre).

3. Adicione um atuador Action e conecte-o ao sensor.

4. No atuador de ação: modo Loop Stop, ação SharkSwimming, start frame 1 e end frame 30.


Agora que o tubarão pode nadar, você quer que ele se mova. Os controles do jogo são simples: use a barra de espaço para nadar para a frente; esquerda e direita para girar; para cima e para baixo para emergir e submergir. Você deve adicionar um sensor de teclado para cada uma dessas teclas e conectá-las da seguinte forma:


- Tecla esquerda => Atuador de movimento: RotZ = 1 ° e desabilitar L para rotação

- Tecla direita => Atuador de movimento: RotZ = -1 ° e desabilitar L para rotação

- Tecla para cima => Atuador de movimento: RotX = 1 °

- Tecla para baixo => Atuador de movimento: RotX = -1 °

- Tecla de espaço => Atuador de movimento: LocY = -0,05


Teste seu progresso dentro do jogo (P) e lembre-se de sempre salvar. Se o seu arquivo estiver mostrando um resultado diferente do arquivo em //assets/shark.11.blend, verifique os blocos lógicos na Figura 2.22.

![Atuadores de movimento(Blender Foundation)](../figures/Chapter2/Fig02-22.png "Motion actuators")

Essa configuração simples permite que o tubarão nade livremente para longe da câmera. Para que a câmera siga o tubarão, selecione a câmera e faça o seguinte:
1. Adicione um sensor Always.

2. Adicione um atuador de câmera e conecte-o ao sensor.

3. No atuador da câmera, defina SharkArmature como objeto, altura 5.0, eixo [nd] Y, mín 5,0, máx 20,0, amortecimento 0,10.


Esta câmera ficará atrás do tubarão, sempre tentando ficar dentro da distância especificada (de 5 a 20 unidades do Blender). O amortecimento definirá a velocidade com que você deseja que a câmera se ajuste à nova posição enquanto o tubarão se afasta.

Se você está modelando tudo do zero, deve ajustar a velocidade e o ângulo do atuador Shark Motion e o amortecimento e a distância da câmera para acomodar melhor a escala de seu trabalho.

Com o tubarão sozinho na cena, é difícil dizer como ele está se movendo. É hora de adicionar outros objetos à cena para que você possa ter certeza de que as configurações da câmera e o movimento do tubarão estão bem ajustados. Assim, o próximo passo é adicionar o mundo (o SeaBed et al). Enquanto isso, você pode comparar o status do seu arquivo com: //assets/shark.12.blend.

## Mundo e Ambiente <a id="World_and_Environment"></a>

Vamos deixar o arquivo shark por enquanto e juntar as peças do jogo. Abra o arquivo //game.1.blend. Este arquivo vazio será o arquivo principal do jogo. Se você deseja iniciar um arquivo do zero, abra o arquivo padrão do Blender, exclua tudo dele (pressione A para selecionar tudo e então X para excluir), e mude o motor para o Blender Game e o modo Shading para GLSL.

Você precisa trazer o modelo de tubarão para este arquivo. Comece vinculando os objetos SharkMesh e SharkArmature do arquivo shark asset. Vá para o menu Arquivo > Link, navegue até o arquivo de mistura de tubarões e, uma vez nele, navegue dentro de "Objeto", selecione os objetos SharkArmature e SharkMesh e pressione OK. Uma captura de tela das opções de vinculação é mostrada na Figura 2.23. As opções padrão são boas por enquanto.

![Opções de vinculação(Blender Foundation)](../figures/Chapter2/Fig02-23.png "Linking options")

É importante salvar seu arquivo primeiro; caso contrário, a opção Caminho Relativo não terá efeito. A vinculação mantém seu arquivo de tubarão como um ativo externo. Todas as alterações feitas no arquivo shark.blend serão transferidas para o arquivo game.blend assim que você salvá-lo. Isso também significa que você não pode fazer alterações nos objetos de ativo por meio do arquivo game.blend. Se você vinculou antes de salvar o arquivo, não se preocupe. Você pode alterar todos os caminhos de arquivo indo para o menu Arquivo> Dados externos> Tornar todos os caminhos absolutos.

A câmera não precisa estar conectada. Na verdade, é melhor mantê-lo como um objeto local, visto que você certamente ajustará seus parâmetros posteriormente. Para anexar (não vincular) a câmera, use o menu Arquivo  Anexar e use as opções padrão para importar a câmera. Esta será a câmera principal do jogo. Selecione a câmera e no cabeçalho Visualização 3D, escolha Exibir> Câmeras> Definir objeto ativo como câmera. Se tudo deu certo, agora você pode jogar seu jogo, e ele deve se comportar como no arquivo shark.blend.

Boas notícias. A SeaBed já estava preparada e pronta para o jogo (e na pasta do seu jogo \ _minha ativos). Repita as etapas de vinculação mais uma vez para o grupo SeaBed dentro do //level/seabed.blend. Agora você tem o tubarão, a câmera e o conjunto preparados para o jogo. O progresso mostrado na Figura 2.24 pode ser verificado em //game.2.blend.

![Shark, camera, e SeaBed(Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-24.png "Shark, camera, and SeaBed")

Para simular a água, adicionaremos um efeito de névoa azul. Isso produz um efeito semelhante à névoa e dá um bom efeito de atenuação da água (onde tudo eventualmente desbota para o azul). Siga esses passos:


1. Alterne para o painel Mundo no Editor de propriedades.

2. Crie um novo mundo.

3. Defina Horizon Color como Hex: 264A6B.

4. Ligue a névoa e defina o início 0,0 e a profundidade 50,0


Para visualizar a cor e o efeito de névoa no Viewport 3D, você precisa definir Viewport Shading para Texture (Alt + Z), conforme mostrado na Figura 2.25. O mundo agora está concluído e faz parte do arquivo //game3.blend.

![Pré-visualização do efeito de névoa na visualização 3D(Blender Foundation-Art Cengage Learning)](../figures/Chapter2/Fig02-25.png "Mist effect-preview in 3D View")

Jogue o seu jogo e nade com o tubarão. No entanto, falta um elemento básico em nosso jogo de sobrevivência do tubarão: a comida.

## Inteligência Artificial <a id="Artificial_Intelligence"></a>

Enquanto o tubarão é 100 por cento interativo, controlado pelo jogador, o peixe será controlado por meio de uma mecânica simples de IA (inteligência artificial). Os princípios são simples: o ciclo de natação do peixe é feito por tijolos lógicos, enquanto o fluxo constante de desova do peixe é controlado por um "programa" individual (um script) responsável pelos seguintes componentes:


- Preenchendo o jogo com cardumes de peixes.

- Fazer com que os peixes sigam um "líder dos peixes".

- Matar alguns peixes quando o tubarão ataca.


>**Falando de Scripts**
>
>Os scripts também podem ser usados para complementar a funcionalidade de um componente do jogo. A cena da pontuação está usando tijolos lógicos para controlar a pontuação, mas precisa de um script para lidar com o tempo limite, o jogo acabado e para alterar a resolução de todos os objetos de texto. Explicaremos mais sobre isso na seção "Sistema de pontuação" deste capítulo.

Mais uma vez, tiraremos vantagem de um sistema com ativos vinculáveis. Em vez de criar você mesmo o cardume de peixes, você o trará para dentro do jogo, pronto para usar.

Comece reabrindo a versão atual do arquivo //game.blend. Agora você precisa vincular o grupo FishSchool do arquivo //assets/school.blend. (Desta vez, ao invés de navegar na subpasta Objeto, vá para Grupo.) Se você vincular um grupo com a opção "Grupos de Instâncias" habilitada, você terminará com uma instância desse grupo adicionada à cena. Esta "instância de grupo" nada mais é do que um objeto vazio que é usado para colocar um grupo do Blender na cena. O grupo está vinculado ao arquivo original, portanto, as alterações feitas nele são mantidas em sincronia com o arquivo do jogo.

Na Figura 2.26, você pode ver o jogo com o cardume de peixes ao redor do tubarão. Se você abrir o arquivo school.blend, poderá ver um vazio (FishLeader) na camada visível e um objeto (Fish) na segunda camada (que está e deve estar oculto por padrão). O vazio está sempre girando e adicionando mais do modelo de peixe à cena. Um peixe é adicionado a cada segundo ou mais até que o limite especificado na propriedade do jogo FishLeader, maxFish, seja atingido. Mude este número de 30 para 100 e os peixes o inundarão. Diminua para 5 e tornará o jogo ainda mais difícil. Selecione o FishLeader e você verá alguns novos blocos lógicos. Preste atenção especial aos controladores Python.

![School of fish(Cengage Learning)](../figures/Chapter2/Fig02-26.png "School of fish")

O script permite uma manipulação mais direta dos elementos do seu jogo, cálculos matemáticos complexos e uma lógica mais densa para o seu jogo. Se você olhar os scripts neste arquivo (no editor de texto), verá que não tem nada a temer. Esta é uma forma textual simples de descrever comportamentos interativos para seu jogo. E é muito mais simples do que a tarefa pesada de programar um motor de jogo inteiro. Felicidades pelo compromisso. Na Figura 2.27, você pode observar as propriedades do jogo e as peças lógicas (incluindo os controladores de script) do FishLeader.


>**Arte Versus Matemática**
>
>"Mas eu sou um artista e não entendo matemática." Claro, recebemos muito isso. Mas tenha em mente que aqui você só precisa entender a mecânica de quando confiar em um script e o que pode fazer com ele. Para uma visão geral mais aprofundada deste tópico, consulte o Capítulo 7, "Script do Python", posteriormente neste livro. Além disso, a matemática necessária para o script Python é mais acessível do que a maioria das pessoas supõe. A menos, é claro, que você esteja planejando concorrer para a Miss EUA. [Http://youtu.be/9QBv2CFTSWU](http://youtu.be/9QBv2CFTSWU)


Se você quiser fazer suas próprias personalizações, tente animar os peixes com ossos. Você pode seguir todas as etapas que fizemos para o tubarão. Além disso, lembre-se de alterar o objeto que está sendo adicionado pelo atuador FishLeader "AddFish" (consulte a Figura 2.27). Em vez de adicionar o peixe, você terá que adicionar o pai peixe (o objeto FishArmature que você criará). O filho da armadura (o próprio peixe) será adicionado automaticamente.

![Logic bricks e Game Property of the FishLeader(Blender Foundation)](../figures/Chapter2/Fig02-27.png "Logic bricks and Game Property of the FishLeader")

O ponto de verificação atual está em //game.4.blend. Se você alterou seu arquivo //assets/school.blend, você só precisa substituir o que está nas fontes pelo seu. Como mencionamos (já três vezes, alguém contando?), Os novos dados serão sincronizados automaticamente no jogo. Jogue o seu jogo e prepare-se para encerrar a alimentação dos tubarões.

## Tudo o que conseguires comer <a id="All_You_Can_Eat"></a>

Se você tentar pegar o peixe com o tubarão, verá que o tubarão empurra o peixe para longe. Para o jogo, precisamos que três coisas aconteçam: (1) o peixe precisa morrer, (2) o tubarão precisa ficar maior, (3) uma pontuação na tela precisa dizer quantos peixes pescamos e quanto tempo nós saimos.

O sistema de pontuação será feito na próxima seção. Por enquanto, vamos nos concentrar em fazer o tubarão e os peixinhos interagirem.

O cardume, de fato, já está montado. Mas vamos dar uma olhada no que temos lá. Abra o arquivo //assets/school.blend. Na segunda camada, selecione o peixe e observe os tijolos lógicos, mostrados na Figura 2.28.

![Fish school logic bricks(Blender Foundation)](../figures/Chapter2/Fig02-28.png "Fish school logic bricks")

Temos um sensor de Colisão que só estará ativo ao tocar em um objeto que possui a propriedade "tubarão". Não queremos saber quando um peixe colide com outro ou com o fundo do mar, aliás. Este filtro trata disso. O sensor é conectado a um controlador Python "killMe.py" que cuida de algumas tarefas domésticas. Diz ao FishLeader que precisaremos de um novo peixe em breve. O controlador também ativa dois atuadores: um para matar os peixes e o segundo para enviar uma mensagem indicando que um peixe caiu.

Esta mensagem é como um e-mail de spam. Não importa se você tem um sinal somente para correio em sua caixa de correio. Nem importa se você não tem uma caixa de correio. Você receberá o cupom do McDonald's que nunca solicitou. (E você vai acabar comendo spammers malditos!)

E o tubarão também. Depois que o tubarão recebe uma mensagem, ele pode agir de acordo. No nosso caso, queremos tornar o tubarão grande. Para fazer isso, abra o arquivo shark.12.blend novamente. Até agora, estivemos adicionando todos os blocos lógicos à armadura. Agora vamos colocar a armadura de lado e usar a malha:


1. Selecione o objeto SharkMesh.

2. Adicione um quadro-chave ao tamanho (IScaling).

3. Vá para o quadro 100, amplie o tubarão e repita a etapa anterior.

4. Abra o Logic Editor.

5. Crie uma propriedade de jogo booleana chamada "shark".

6. Crie uma propriedade de jogo Integer chamada "size".

7. Adicione um sensor de mensagem com o assunto "Sharked"

8. Adicione um atuador de propriedade: modo Adicionar, propriedade "tamanho" e valor 1.

9. Adicione um atuador Action: mode Property, action SharkMeshAction e propriedade "size".

10. Conecte o sensor com ambos os atuadores.


O arquivo shark final está em //assets/shark.13.blend. Na Figura 2.29, temos uma tela de configuração dos blocos lógicos.

![Shark pronto para crescer(Blender Foundation)](../figures/Chapter2/Fig02-29.png "Shark ready to grow")

Começamos criando uma animação para o tubarão. Esta animação é reproduzida de acordo com uma propriedade do jogo (tamanho) que aumentará cada vez que uma mensagem for recebida. A mensagem chega ao tubarão toda vez que um peixe é comido (por exemplo, colide com o tubarão). Assim, temos uma boa sincronização entre o desaparecimento dos peixes e o aumento do tamanho do tubarão.

Além disso, o tubarão precisa da propriedade de jogo "tubarão" para ser detectado pelo cardume. Isso irá desencadear a colisão. O sensor de colisão simplesmente verifica se o objeto possui uma propriedade com um determinado nome, portanto, o tipo e o valor da propriedade são arbitrários (no nosso caso, estamos usando uma propriedade booleana, mas poderia ser qualquer outro tipo de propriedade). Agora, um a um, podemos comer os peixes. E é hora de contar ovelhas.

## Sistema de Pontuação <a id="Scoring_System"></a>

O sistema de pontuação do jogo faz parte de sua interface construída sobre a visualização 3D. Na Figura 2.30, você pode ver os principais elementos da interface: a pontuação no canto superior esquerdo, a contagem regressiva do tempo no canto superior direito e o título do jogo no canto inferior direito.

![Elementos da Inteface(Blender Foundation)](../figures/Chapter2/Fig02-30.png "Interface elements")

A interface do usuário é independente do arquivo, objetos e eventos do jogo. Graças ao sistema de mensagens do mecanismo de jogo (a combinação do atuador de mensagens e dos sensores de mensagens), você pode implementar a interface como um arquivo separado com sua própria lógica. Abra o arquivo de interface em //interface/score.blend. O diagrama da Figura 2.31 ilustra a dinâmica de seus elementos e o fluxo de mensagens.

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
