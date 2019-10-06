**Índice**

- [Capítulo 1: Introdução](#Chapter_1_Getting_Started)
	- [Uma História da Origem](#An_Origin_Story)
		- [O Blender inicia](#Blender_Begins)
		- [As noites escuras](#The_Dark_Nights)
		- [A Ascenção de Blender](#Blender_Rises)
	- [Sobre o Blender](#About_Blender)
		- [Sobre o Game Engine](#About_the_Game_Engine)
		- [O Futuro da BGE](#Future_of_BGE)
	- [O Básico do 3D](#3D_Basics)
		- [Sistema de Coordenadas](#Coordinate_System)
		- [Pontos, arestas, triângulos e malhas](#Points,_Edges,_Triangles,_and_Meshes)
		- [Transformações básicas](#Basic_Transforms)
		- [Materiais e Texturas](#Materials_and_Textures)
		- [Iluminação](#Lights)
		- [Câmera](#Camera)
		- [Animação](#Animation)
		- [Game](#Game)
	- [Configurando](#Setting_up)
		- [Instalação](#Installation)
		- [Requisitos de sistema](#System_Requirements)
	- [Noções básicas do Blender](#Blender_Basics)
		- [Menu Principal](#Main_Menu)
		- [Vista 3D](#3D_Viewport)
		- [Outliner](#Outliner)
		- [Editor de Propriedades](#Properties_Editor)
		- [Timeline](#Timeline)
		- [Personalização da área de trabalho](#Workspace_Customization)
		- [Mais sobre a vista 3D](#More_on_the_3D_View)
		- [Modos de sombreamento da viewport](#Viewport_Shading_Modes)
		- [Modos de edição](#Editing_Modes)
		- [Teclado e Mouse](#Keyboard_and_Mouse)
		- [Procura](#Search)
		- [Filosofia do Blender](#Blender_Philosophy)
		- [Interface](#Interface)
		- [Teclado](#Keyboard)
		- [Mouse](#Mouse)
		- [Contexto](#Context)
		- [Blocos de dados](#Datablocks)
		- [Parentalidade e Agrupamento](#Parenting_and_Grouping)
		- [Compatibilidade com versões anteriores](#Backward_Compatibility)
	- [Adiante](#Onward)

# Capítulo 1: Introdução <a id="Chapter_1_Getting_Started"></a>
Aqui está algo que você não sabe sobre Mike. Ele leu mais livros sobre Linux do que gostaria de admitir. Infelizmente, Mike raramente passa do capítulo 2. Dado que os dois primeiros capítulos geralmente não contêm nada além de uma introdução calorosa e um histórico do software, essa prática tem duas consequências profundas. A primeira é que Mike pode articular a história do Linux muito melhor do que quase qualquer um. A segunda é que ele ainda não sabe como usar o Linux. É verdade que o primeiro é muito mais útil em uma festa do que saber a diferença entre "tar cvfz" e "lshw".

De acordo com essa tradição de livros sobre tecnologia, este livro não será diferente. Neste capítulo, você aprenderá a rica história do Blender e será apresentado aos princípios básicos deste aplicativo.

## Uma História da Origem <a id="An_Origin_Story"></a>

Era meados da década de 1990, e o computador pessoal estava decolando mais rápido do que se previa. Com isso, surgiu o advento de gráficos animados e jogos em 3D.

### O Blender inicia <a id="Blender_Begins"></a>
Foi nessa época que o Blender surgiu. O Blender começou como um software de animação 3D interno criado por um pequeno estúdio de animação holandês chamado NeoGeo. Talvez fosse por falta de um substituto barato e capaz; talvez fosse por pura ambição, a NeoGeo decidiu criar seu próprio software de animação do zero, em vez de usar o que estava disponível. O principal programador do Blender foi Ton Roosendaal, responsável por escrever grande parte das principais funcionalidades do Blender.

Nos anos seguintes, o Blender permaneceu a ferramenta interna de um estúdio de animação de muito sucesso. O software ficou tão bom que, em 1998, o Blender foi disponibilizado ao público. Uma nova empresa, Not a Number (NaN), foi formada para supervisionar o desenvolvimento e a distribuição do Blender. Em grande parte pela Internet, o Blender foi distribuído em duas versões separadas: uma versão gratuita com funcionalidade limitada e uma versão que não era gratuita (chamada Blender Publisher) que possuía alguns recursos adicionais. Sendo o único pacote completo de animação em 3D e criação de jogos disponível gratuitamente no momento em que a computação gráfica ainda estava em sua infância, o Blender começou a ganhar popularidade, e muitas comunidades online se desenvolveram permitindo que os artistas compartilhassem conhecimento e seu trabalho.

![Left: Blender 1.6. Right: Blender 2.65](../figures/Chapter1/Fig01-01.jpg)

###  As noites escuras <a id="The_Dark_Nights"></a>
Infelizmente, com o colapso da bolha da Internet e outras circunstâncias infelizes, a Not a Number (NaN) entrou em falência em 2002. Como o Blender era propriedade intelectual da empresa na época, dissolver a empresa significava um futuro incerto para o Blender. A comunidade do Blender não queria ver o seu software favorito ficar com o NaN. Então, foi fechado um acordo em que o NaN divulgaria o código fonte do Blender ao público por um pagamento de € 100.000. Uma campanha de arrecadação de fundos "Free the Blender" foi iniciada. A comunidade online respondeu muito generosamente. Alguns meses depois, dinheiro suficiente foi coletado para convencer o NaN a relançar o Blender como um software de código aberto para a recém-criada Fundação Blender. A fundação foi criada especificamente para gerenciar o Blender, agora de código aberto. Ton Roosendaal, o criador original do Blender, lidera a fundação.

### A Ascenção de Blender <a id="Blender_Rises"></a>
Localizada na bela Amsterdã, a Blender Foundation agora supervisiona o desenvolvimento, distribuição e marketing do Blender. Porém, devido à natureza de código aberto do software, seu desenvolvimento foi impulsionado em grande parte por colaboradores voluntários de todo o mundo.

A Blender Foundation também criou o Blender Institute, um estúdio de animação e jogos que se concentra no desenvolvimento de filmes e jogos usando o Blender. O Instituto produziu os filmes _Elephants Dream_, _Big Buck Bunny_, _Sintel_, _Tears of Steel_, Cosmos Laundromat e o jogo _Yo, Frankie! _ Esses projetos atendem a dois objetivos principais: O processo de produção é uma oportunidade de melhorar o Blender em um ambiente de estúdio real, e o resultado final também serve como um anúncio para o próprio software.

![Top: Elephants Dream, Big Buck Bunny, Yo, Frankie!, Bottom:  Sintel, Tears of Steel, Cosmos Laundromat](../figures/Chapter1/Fig01-02.jpg)

Depois veio o Blender 2.5, que mudou muito a aparência e o comportamento do Blender. Essa refatoração, como foi chamada, levou anos de planejamento e codificação. O Blender 2.5 marca um marco significativo na história do Blender. Para usuários provenientes da série Blender 2.4x, toda a interface parece radicalmente diferente: os itens dos menus são reorganizados, os atalhos do teclado são alterados, até o esquema de cores padrão mudou de cinza para um tom de cinza um pouco menos chato. O Blender 2.5 foi projetado para ser mais intuitivo, mais rápido de usar e mais fácil de aprender do que seu antecessor.

O Blender usa a linguagem de programação Python para scripts. Com o Python, você pode personalizar o comportamento do Blender, ampliar sua funcionalidade e, mais importante, controlar o mecanismo do jogo. Saber programar não é um requisito para usar o Blender, mas conhecer o Python fará de você um criador de jogos muito mais capaz.

<img alt="Blender Commit statistics form 2003 to 2012" src="../figures/Chapter1/Fig01-03.png" width="50%" align="left">
O ano de 2012 marcou o décimo aniversário do Blender em código aberto. Durante esses 10 anos de desenvolvimento de código aberto, mais de 150 pessoas contribuíram com algo para o código-fonte, totalizando 50.000 contribuições ("confirmações", no jargão técnico do SVN), com uma média de quase 30 confirmações por dia durante o ano passado. Desnecessário dizer que o programa melhorou muito ao longo dos anos e não mostra sinais de desaceleração. A imagem abaixo mostra as estatísticas de desenvolvimento do Blender coletadas no repositório oficial do SVN, incluindo o tronco do Blender em todas as suas ramificações.

Obviamente, existe software para atender os usuários - é você. Toda vez que um usuário do Blender cria uma obra de arte, justifica, mesmo que um pouco, a enorme quantidade de tempo que foi gasta na criação do software. Esperamos que, ao adquirir este livro, você esteja no caminho de criar algo incrível para compartilhar com o mundo.



---

## Sobre o Blender <a id="About_Blender"></a>

Provavelmente, você já sabe que o Blender é um software 3D de código aberto capaz de modelar, animar, renderizar, compor e produzir um jogo em um único pacote. Mesmo que você não tenha certeza do significado de cada um desses termos, não se preocupe!

Vamos detalhar o termo "software de animação 3D de código aberto".
"Código aberto" significa que o código fonte do Blender está disponível para qualquer pessoa acessar e modificar. A vantagem mais óbvia para o software de código aberto é que, como artista, você pode usar o Blender gratuitamente, para trabalhos não comerciais e comerciais. Como desenvolvedor, você tem permissão para modificar o Blender da maneira que desejar para atender às suas necessidades específicas. Mas o código aberto não significa que qualquer pessoa possa fazer alterações maliciosas no código do Blender sem aprovação. O Blender está licenciado sob a GNU Public License v2 (GPL2). Em poucas palavras, significa que o Blender pode ser copiado, modificado e, se compartilhado novamente, as alterações no código-fonte precisam estar disponíveis e licenciadas em uma licença equivalente.

> **Ressalva**:
>
> Antes de publicar um jogo usando o Blender, você deve entender as limitações da GPL. Este tópico é abordado no capítulo 9, "Publicando e além".

O termo "3D" significa três dimensões. O mundo em que vivemos é 3D porque possui altura, largura e profundidade. Compare isso com os programas de software 2D, como Photoshop, GIMP ou Krita, o processo de criação de conteúdo no Blender é feito em um espaço 3D, não em uma tela 2D.

![2D vs. 3D](../figures/Chapter1/Fig01-04.jpg)

O termo "animação" talvez seja enganoso. Embora tendamos a atribuir o termo "animação por computador" a qualquer filme feito por um computador, devemos lembrar que o Blender não se limita apenas a criar animação. O Blender é capaz de modelar, renderizar, compor e criar jogos da melhor maneira possível.

O termo "software" sugere que o Blender é uma ferramenta - uma ferramenta que permite criar animações e jogos. Portanto, este livro o tratará como tal - apenas um meio para atingir um fim. Nós o ajudaremos a entender cada um dos recursos do Blender, para que você saiba como usar o software para alcançar o que deseja.

Como este é um livro sobre as ferramentas, este não é um livro sobre design de jogos. Tópicos como história, direção de arte e jogabilidade estão além do escopo deste livro. O Blender é apenas uma plataforma que permite fazer arte.

### Sobre o Game Engine <a id="About_the_Game_Engine"></a>

O Blender é uma ferramenta multifacetada. Este livro se concentrará em um aspecto: o processo de criação de jogos. Se você é novo no Blender, aprender o mecanismo do jogo significa que você adquirirá modelagem básica, animação e outras habilidades necessárias ao longo do caminho. Se você já tem experiência com o Blender, ótimo! As habilidades que você já conhece facilitarão muito a transição para o mecanismo de jogo.

Comparado a alguns dos mecanismos de jogos comerciais disponíveis atualmente, o Blender Game Engine (BGE ou GE, abreviado) é relativamente simples. Isso é uma coisa ruim? Não necessariamente. Uma plataforma simples como o Blender é muito fácil de aprender e, no entanto, é flexível o suficiente para fazer muito.

Para ter uma idéia do que o mecanismo de jogo é capaz, o Capítulo 10, "Estudos de Caso", é dedicado a projetos que foram feitos na GE.

### O Futuro da BGE <a id="Future_of_BGE"></a>

Uma desvantagem de escrever sobre software é que ele está melhorando constantemente. Ainda hoje, projetos como o [UPBGE] (https://upbge.org/) prometem melhorar drasticamente os recursos e funcionalidades do Blender Game Engine. Faremos o possível para manter este e-book o mais atualizado possível. O que você deve fazer como leitor é garantir que você esteja sempre usando a versão mais recente do Blender.

> **Construções de Teste**
>
> Se a versão mais recente não for boa o suficiente, você poderá encontrar versões oficiais diárias em [builder.blender.org] (https://builder.blender.org/download/). Além disso, muitas versões de teste não oficiais do Blender estão disponíveis em [graphicall.org] (http://graphicall.org/).

## O Básico do 3D <a id="3D_Basics"></a>

Se você nunca usou um aplicativo 3D antes, os termos modelagem, animação e renderização podem ser estranhos para você. Portanto, antes de criar o jogo espetacular que você sempre quis fazer, vamos relembrar rapidamente o básico da computação gráfica. Você não precisa suportar a seção chata abaixo se já sabe o que significa RGB e a diferença entre Cartesiano e Gaussiano.

O conhecimento nesta seção é universal e se aplica a todos os outros aplicativos 3D. Portanto, mesmo se você vier de um aplicativo diferente, os mesmos conceitos os conduzirão a todos.

### Sistema de Coordenadas <a id="Coordinate_System"></a>

<img alt="The three axes illustrated" src="../figures/Chapter1/Fig01-05.png" width="33%" align="right">
Vivemos em um mundo tridimensional que tem largura, altura e profundidade. Portanto, para representar qualquer coisa que se assemelhe à vida real como um mundo virtual dentro de um computador, precisamos pensar e trabalhar em três dimensões. O sistema mais comum usado é chamado de sistema de coordenadas cartesianas, onde as três dimensões são representadas por X, Y e Z, dispostas como planos de interseção. Onde os três eixos se encontram é chamado de _origin_. Você pode pensar na origem como o centro do seu universo digital. Uma única posição no espaço é representada por um conjunto de números que corresponde à sua posição desde a origem: assim (2, -4, 8) é um ponto no espaço que está a 2 unidades da origem ao longo do eixo X, 4 unidades de a origem ao longo do eixo -Y e 8 unidades acima na direção Z.


### Pontos, Arestas, Triângulos e Malhas <a id="Points,_Edges,_Triangles,_and_Meshes"></a>

Embora possamos definir uma posição no espaço usando as coordenadas XYZ, um único ponto (ou um "vértice", como é mais conhecido em computação gráfica) não é muito útil; afinal, você não pode ver um ponto infinitamente pequeno. Mas você pode associar esse vértice a outro vértice para formar uma linha (também conhecida como "aresta"). Uma aresta por si só ainda não seria muito visível, então você cria outro vértice e une os três vértices com linhas e preenche o meio. De repente, algo muito mais interessante é criado [md] um triângulo (também conhecido como "rosto")! Ao vincular várias faces, você pode criar qualquer forma, cujo resultado é chamado de "malha" ou "modelo". A figura abaixo mostra como uma malha pode ser dividida em faces, arestas e, finalmente, como vértices.

![Bule, cubo, face, borda e vértice.](../figures/Chapter1/Fig01-06.jpg)

Por que o triângulo é tão importante? Acontece que os gráficos de computador modernos usam o triângulo como o elemento básico para quase qualquer formato. Um plano retangular (também conhecido como quadrangular_ ou, mais comumente, quadrangular) é simplesmente dois triângulos dispostos lado a lado. Um cubo é simplesmente seis quadrados juntos. Até uma esfera é feita apenas de pequenas faceletas dispostas em forma de bola.

<img alt="The same cylinder cap can be made up of triangles, quads, or an n-gon." src="../figures/Chapter1/Fig01-07.jpg" width="50%" align="right">

No Blender, uma malha pode ser feita a partir de uma combinação de triângulos, quadrados ou n-gons. O benefício dos n-gons é sua capacidade de manter uma topologia limpa durante a modelagem. Sem n-gons, certas áreas de um modelo (como uma janela na parede) exigiriam um número maior de triângulos ou quadríceps para se aproximar, como mostrado abaixo. Enquanto n-gons facilitam a modelagem em alguns casos, o Blender ainda os converte em triângulos quando você inicia o jogo.

O processo de criação de uma malha reorganizando vértices, arestas e faces é chamado _modeling_. O Blender possui muitas ferramentas que ajudam os artistas a definir a geometria desejada.

Vale ressaltar que, diferentemente do mundo real, os modelos poligonais não possuem volumes. Eles são apenas uma concha feita de faces interconectadas que assumem a forma do objeto, mas a parte interna do objeto é sempre "oca".

<img alt="Surface normals are displayed as cyan lines protruding from the faces." src="../figures/Chapter1/Fig01-08.jpg" width="50%" align="right">

Outro conceito que um modelador provavelmente encontrará são os normais de superfície, ou "normais", para abreviar. Normal é uma propriedade de cada face que indica a direção em que um polígono está voltado. Como os normais são usados para calcular a superfície da sombra, idealmente todos os normais de uma malha devem ser apontados "para fora". Normais mal orientadas podem fazer com que a malha apareça como preta ou invisível. Felizmente, existe uma função Tornar normais consistentes no Blender que geralmente pode resolver o problema. A Figura 1.8 mostra como as normais são apresentadas no Blender.


> **Além dos polígonos**
>
> Tecnicamente, existem outras abordagens para computação gráfica que não dependem de triângulos ou polígonos, como NURBS (spline B racional não uniforme) e voxel (abreviação de VOlumetric piXEL). Mas a modelagem e renderização de polígonos é de longe o mais comum e é o único método suportado no mecanismo de jogo.

### Basic Transforms <a id="Basic_Transforms"></a>

The three basic transforms that you should be familiar with are:

* **Translation:** The moving of an object in any direction, without rotating it.
* **Scaling:** The resizing of an object around a point.
* **Rotation:** The rotating of an object around a point.

These three are the most common manipulations you will encounter. They are illustrated below.

![Translation, scaling, and rotation.](../figures/Chapter1/Fig01-09.jpg)

### Materials and Textures <a id="Materials_and_Textures"></a>

Using polygons, you can define the shape of a mesh. To alter the color and appearance of it, you need to apply materials to the object. Material controls the color, shininess, bumpiness, and even transparency of the object. These variables ultimately all serve to add details to the object.

Often, changing the color is not enough to make a surface look realistic. This is where textures come in. Texturing is a common technique used to add color and detail to a mesh by wrapping the mesh with an image, like a decal. Imagine a toy globe: if you carefully peel off the paper map that is glued onto the plastic ball and lay it out flat on the table, that map would be the texture, and the plastic ball would be the mesh. The projection of the 2D image onto a 3D mesh is called _texture mapping_. Texture mapping can be an automatic process, using one of the predefined projections, or a manual process, which uses a UV layout to map the 2D image onto the 3D mesh. Figure 1.10 illustrates how an image is mapped onto a model.

![Meshes with texture applied.](../figures/Chapter1/Fig01-10.jpg)


Traditionally, a texture changes the color of a surface. But that's not all it can do: textures can also be used to alter other properties of the surface such as its transparency, reflectivity, and even bumpiness to create the illusion of a much more detailed surface.

<img alt="From left to right: diffuse map, normal map, and specular map." src="../figures/Chapter1/Fig01-11.jpg" width="50%" align="right">

A diffuse map controls the base color of the surface. A normal map controls the surface normal of an object, creating a bumpy effect by changing the way the light is reflected off the object. A specular map controls the specular reflection of an object, making it look shiny in certain places and dull in others. A texture map can also have transparent pixels, rendering part of the object transparent.

Generally, textures are image files. But there are also other ways to texture a surface, such as using a procedural texture. Procedural texture differs from an image in that it's generated by an algorithm in real time, rather than from a pre-made image file. The Blender game engine does not support procedural textures yet.

### Lights <a id="Lights"></a>

Everything you see is the result of light hitting your eyes-without lights, the world would be pitch black. Likewise, light is just as important in a virtual world. With light comes shadow as well. Shadow might not be something that you think about every day, but the interplay of shadow and light makes a huge difference in how the scene is presented.

<img alt="From left: Lamp, Sun, Spot lamp, Hemi lamp, and Area lamp." src="../figures/Chapter1/Fig01-12.png" width="50%" align="right">

In most 3D applications, there are several different types of light available to the artist; each type has its advantages and disadvantages. For example, a Spot lamp approximates a lamp with a conical influence; a sun lamp approximates a light source from infinitely far away. Lamps in Blender are treated like regular objects: they can be positioned and rotated just like any other object. Figure 1.12 shows how different lamps look in Blender.

Think of lighting as more than something that makes your scene visible. Good lighting can enhance the purpose of the scene by highlighting details while hiding irrelevant areas in shadow. Skillful placement of lighting also adds drama and realism to the scene, making an otherwise boring scene look visually exciting.

### Camera <a id="Camera"></a>

<img alt="Camera objects" src="../figures/Chapter1/Fig01-13.png" width="50%" align="right">

When you are creating a 3D scene, you are looking at the virtual world from an omniscient view. In this mode, you can view and edit the world from any angle[md]just like a movie director walking around a set in order to adjust things. Once the game starts, the player must view the game through a predetermined camera. Note that a predetermined camera does not mean the camera is fixed; almost all games have a camera that reacts to a player's input. In an action game, the camera tends to follow the character from behind; in a strategy game, the camera might be hovering high above, looking down; in a platformer, the camera is usually looking at the scene from the side.

A camera is also treated as a regular object in Blender, so you can manipulate its location and orientation just as you can with any other object.


> **Drawing and Composition for Visual Storytellers**
>
> Speaking of lights and cameras, this is the part where we point out the wonderful book by Marcos Mateu-Mestre called Framed Ink. The book uses tons of beautiful drawings to illustrate the many key principles in visual storytelling.

### Animation <a id="Animation"></a>

In this context, _animation_ refers to the technique of making things change over time. For example, animation can involve moving an object, deforming it, or changing its color. To set up an animation, you create "keyframes," which are snapshots in time that store specific values pertaining to the animation. The software can then automatically interpolate in between those values to create a smooth transition. The image below shows Blender's Dopesheet Editor. The Dopesheet allows you to see the various properties that change during an animation: the horizontal axis represents time; the vertical axis shows the various properties, such as location or rotation that are keyframed.

![Dopesheet Editor: each diamond shape is a keyframe.](../figures/Chapter1/Fig01-14.png)

<img alt="LocRotScale animation" src="../figures/Chapter1/Fig01-15.png" width="50%" align="right">
<br><br>
The easiest way to animate is to alter the location, rotation, and scaling of an object over time. For example, by altering these variables, you can realistically animate the movement of a bouncing ball. Keep in mind that the curves represent the value of the channels (in this case xyz location) of the ball, not the actual motion path of the ball itself.

<br><br>

<img alt="Armature animation" src="../figures/Chapter1/Fig01-16.png" width="33%" align="left">
<br><br>
To animate something more complicated, such as a human, it's not enough to just move, rotate, and scale the object as a whole. This is where armatures come in. Armatures are skeletons that can be "inserted" into a model to control the model's deformation. Using this system, you can create complex yet organic-looking animations.

<br><br><br><br>
<img alt="Shape keys animation." src="../figures/Chapter1/Fig01-17.jpg" width="50%" align="right">
<br>
A third way to animate is using shape keys. Shape keys are snapshots of the mesh in different shapes. They are often used to animate nuanced changes that cannot be otherwise easily animated with armatures.


<img alt="Procedural physics-based motion." src="../figures/Chapter1/Fig01-18.jpg" width="33%" align="left">
<br>
Finally, keep in mind that making objects move doesn't always have to be a manual process. You can also make objects move by using the physics engine (see Chapter 6).

<br>

### Game <a id="Game"></a>

So far, we have talked about 3D at length. But how does the game engine fit into? Well, a game engine simply takes the existing 3D assets and attaches a "brain" to them so the objects know how to respond to events. The  "brain" can be in the form of logic bricks (which can perform different actions depending on the user input), scripts (which can extend the functionality of logic bricks), or other physical properties of an object (such as rigid body settings to make an object tumble and fall realistically).

![Game = Object + Logic.](../figures/Chapter1/Fig01-19.jpg)

A game engine is made up of many distinct components:

- **Rendering Engine** : Turns the 3D scene you've built (including models, lights, and camera) into an image to be displayed onscreen.
- **Physics** : Handles collisions and physical simulations of objects.
- **Logic/Scripting** : The brain behind a game[md]it reacts to the user input, makes decisions, and keeps track of what's going on in the game.
- **Sound** : Produces the audio events.

The above list is not meant to be exhaustive, but it should give you an idea of what a game engine does. The Blender game engine gives you a lot of control over each of these components, which you will learn one by one in later chapters.

> **Quality vs. Performance**
>
> Making a video game is a constant balancing act between quality and performance. As artists, you want to make the virtual world as rich and detailed as possible; on the other hand, you need to make sure the game can run smoothly for people who might not have top-of-the-line computers. Throughout the process of game-making, you will run into cases where you have to make a decision whether to prioritize the visual quality or the performance of the game. You will also learn tricks to achieve high-quality visual without compromising the performance, as well as how to optimize the game by identifying what is slowing it down.

## Setting up <a id="Setting_up"></a>

It's finally time to dive into Blender! From now on, you may be better off reading the book with the computer at your side. In this section, we will give you a short tour of Blender, just enough to get you familiar with the software.

### Installation <a id="Installation"></a>

Blender runs on Windows, Mac OS X, and Linux, You can find the Blender installer for your operating system from www.blender.org. The complete Blender download size is about 100MB.

Go ahead and install Blender. Start the application once it's installed.

> **Installation Not Required**
>
> Technically, Blender does not need to be installed before it can be used. The installer is available for convenience only. Blender will run from any location. You can even copy it to a USB storage device and carry it with you, so you'll never be apart from your favorite program. Although, by default, Blender saves some user settings to the user directory.

Even though you need Blender to develop the game, Blender games can be packaged as stand-alone applications, so that others playing it don't need to install anything. See Chapter 9, "Publishing and Beyond," for more details.

### System Requirements <a id="System_Requirements"></a>

Blender has no explicit system requirement. The performance of the software is dependent on the complexity of the project. Needless to say, the faster your computer is, the better Blender will run.

## Blender Basics <a id="Blender_Basics"></a>

When you start Blender, you will be greeted with the splash screen.Although you can customize all aspect of Blender, in this book, we will assume you are using the default Blender settings and shortcuts.

Clicking anywhere else to dismiss the splash screen, you are presented with an empty workspace like this:

![Blender default workspace.](../figures/Chapter1/Fig01-20.jpg)

The Blender window is divided into Editors. Each Editor region can be resized, moved, and changed to display a specific set of content. For now, let's focus on the default setup.

#### Main Menu <a id="Main_Menu"></a>

At the top of the screen is the main menu, which offers basic functionalities such as Open, Save, and Help. Furthermore, the main menu controls the view for the rest of the Blender window. The Render Engine option in the middle of the menu controls how the interface is configured.

<img alt="Selecting the Game Engine" src="../figures/Chapter1/Fig01-21.png" width="40%" align="left">
By default, Cycles Render is selected. In this mode, the interface is configured for doing 3D modeling, animation, and rendering with Cycles. But let's switch it to the Blender Game mode. Click the drop-down menu and select Blender Game from the list. This setting will unlock certain features that are not visible normally, and it also hides features that are not available in the Blender game engine.


#### 3D Viewport <a id="3D_Viewport"></a>

Occupying the majority of the screen is a 3D Viewport. Here you can see the 3D world you created and test the game. For now, feel free to explore the 3D Viewport by holding down your middle mouse button over the 3D Viewport and dragging the mouse; the view should rotate with the mouse movement. (Mac users can use the two-finger rotate gesture on the trackpad) The default scene contains three objects: a cube, a camera, and a light. To select one of the objects, right-click on it. The selected object is highlighted in yellow.

>**Basic Navigation Controls**

>Press and hold the middle mouse button to rotate the 3D view. Scroll the mouse wheel to zoom in the 3D view. Right-click to select a 3D object. Selected objects are highlighted in yellow.


<img alt="Number pad keyboard layout." src="../figures/Chapter1/Fig01-23.png" width="25%" align="left">
<br>
Another common setup for the 3D Viewport is to split the view into four quadrants: top view, side view, front view, and a perspective view. You can turn on Quad view by pressing Ctrl+Alt+Q with the mouse over the 3D Viewport (see Figure 1.22). Press the same key combination to go back to the single view.

To quickly snap to one of the predetermined views (side, top, front, and so on), the number pad is the way to go.

<br><br>


#### Outliner <a id="Outliner"></a>

<img alt="Outliner" src="../figures/Chapter1/Fig01-20b.png" width="33%" align="right">

To the right of the screen are two editors. The top portion is the Outliner, which contains a listing of all the data in the current Blender file. For a large project, the Outliner is an indispensable tool for organizing your scene. For now, you can safely ignore it.

#### Properties Editor <a id="Properties_Editor"></a>


<img alt="Properties Editor icons." src="../figures/Chapter1/Fig01-24.png" width="33%" align="right">
Under the Outliner on the right, you have the Properties Editor. Here you can access global settings for the file, as well as settings for individual objects. This is one of the most frequently used panels in Blender, after the 3D view perhaps. The Properties Editor is context sensitive, which means it will automatically display different content, depending on the object that is active. Take a closer look at the row of icons at the top of the Properties Editor, as shown in Figure 1.24. These tabs organize the properties into groups, with the more general settings on the left-most tab, and the more specific settings on the right.


#### Timeline <a id="Timeline"></a>

At the very bottom of the screen is a timeline window, which will be useful when you start making animations.
![Timeline](../figures/Chapter1/Fig01-20c.png)


#### Workspace Customization <a id="Workspace_Customization"></a>

The default screen, as described previously, is set up for general use. At some point, it becomes necessary to change the screen layout to accomplish other tasks. To select a different layout, use the Screens layout drop-down menu from the main menu.

Apart from the predefined screen layouts, you can customize the screen layout however you like. You can either split an existing editor into two or merge two adjacent editors together.

>**Editor, Region, and Area**
>
>A region within the Blender windows is called an _editor_. An editor displays a specific set of content and tools. Common areas include: 3D View, Properties Editor, UV/Image Editor, and Logic Brick Editor.



Figure 1.25 shows one area split into two. You can do it by dragging the top corner of the area to the right or bottom

![Area Splitting](../figures/Chapter1/Fig01-25.png)

To merge two adjacent areas into one is exactly the same as shown in Figure 1.25, but it is done in reverse order. Optionally, you can click with the right mouse button in the edge of the area you want to split or join, and select the option in the Area Options pop-up menu.


<img alt="Editor selection." src="../figures/Chapter1/Fig01-27.png" width="25%" align="left">
<br>
Not only can you change the size and layout of the editor, but the type of editor can also be changed. As you can see in Figure 1.27, the left-most icon in the header can be used to change the editor type.

<img alt="Dopesheet, Image Editor, and Logic Brick Editor." src="../figures/Chapter1/Fig01-28.png" width="45%" align="right">
Almost everything a studio needs to create the game is integrated into a single interface: you can create the game, test the game, and play the game all from the same program. This means that, as an artist, you can create a game in the shortest time possible, without having to worry about importing and exporting files between different applications. As a programmer, you won't have to switch back and forth between different software just to test your code. Figure 1.28 shows some screenshots of different editors that you will be using throughout the book.


### More on the 3D View <a id="More_on_the_3D_View"></a>

The 3D view is where you will spend most of your time, so let's take a look at it in a bit more detail. You've already learned a few ways to navigate around the scene earlier in this chapter, using both the mouse and the keyboard.

#### Viewport Shading Modes <a id="Viewport_Shading_Modes"></a>

<img alt="Drawing Modes" src="../figures/Chapter1/Fig01-29.png" width="25%" align="right">
Let's look at the four different Viewport Shading modes available in the 3D view. They are used to change the way the scene is displayed onscreen. The four modes are:

- **Bounding Box** : Represents all objects as a wireframe boundary. Useful for when the scene gets really complex.
- **Wireframe** : Draws all objects as wireframe, which allows you to see through objects.
- **Solid** : Draws all objects as solid faces, which is commonly used when modeling.
- **Textured** : Draws all objects as solid faces, also with texture and accurate lighting. This is useful for previewing the scene.

The two most commonly used Shading modes are Wireframe and Solid. Therefore, they are assigned to a keyboard toggle for easy access. Press the Z key to toggle between Wireframe and Solid View modes. Additionally, you can Press Alt+Z to toggle between Solid and Textured view modes.

> **Standing Out**
>
> Individual objects can also override the Viewport Shading mode via a setting under the Properties Editor > Object > Display > Type.



### Editing Modes <a id="Editing_Modes"></a>

To the left of the Shading mode selector is the Editing Mode selector.

- **Object Mode** : The default mode, which allows the manipulation of objects in the scene as a whole. From this mode, you can select any of the objects in the scene, and move, rotate, and scale them. In fact, almost everything apart from modeling can be done from Object mode.
- **Edit Mode**: This mode can be seen as the counterpart to Object mode. It allows you to edit the underlying geometry of the object. If you are modeling, you'll probably want to be in Edit mode. For this reason, Edit mode is not available when a non-editable object is selected (for example, a camera or lamp).

To switch between Object mode and Edit mode, press the tab key.

In addition to the two editing modes we just discussed, there are a few other modes that are less commonly used.

- **Sculpt Mode** : Only available for Mesh objects. Allows modifications to the mesh as if it were clay.
- **Vertex** , **Weight,** and **Texture Paint Mode** : Only available for Mesh objects. These modes allow the assignment of color or weight to the mesh.
- **Pose Mode** : Is used to animate bones in an armature.

Edit mode and Object mode are by far the most commonly used editing modes, so we will refrain from diving too deeply into the other modes for now.

### Keyboard and Mouse <a id="Keyboard_and_Mouse"></a>

The joke is that to move an object in Blender, you have to press the G key, which stands for "movinG." This gag stems from the fact that to a beginner, many of the shortcuts in Blender seem counterintuitive. However, there is a very good reason why "G" is preferred over "M." In this case, the G key can be easily accessed on the keyboard by the left hand while the right hand is on the mouse. Also, officially, G stands for Grab.



> **Think Different**
>
> By default, the Mac keyboard uses Command instead of Control as the default modifier key. So whenever you see Ctrl+Something in this book, mentally map it to Cmd if you are using a Jobsian product.
>
> Additionally, Blender has good support for multi-touch gestures on OS X. You can pinch to zoom, rotate to orbit around, and pan around.



Let's start with some shortcuts that work the way you would expect:

* **Ctrl + S:** Save File
* **Ctrl + O:** Open File
* **Ctrl + N:** New File
* **Ctrl + Z:** Undo
* **Ctrl + Shift + Z:** Redo
* **Ctrl + Q:** Close(Quit) Application

The above shortcuts work anywhere within Blender: they are effectively global. Unfortunately, the familiarity ends here.

To manipulate an object in the 3D view, generally you have to select it at first:

- **Right-click:** Select object
- **Shift + Right-click:** Extend selection to multiple objects
- **A:** Select all

All of the actions above are "reversible." If something is already selected, right-clicking on it will deselect it. If all the objects are already selected, pressing A will deselect all.

Once an object is selected, you can start manipulating it. The keyboard shortcuts below correspond to the three most basic transforms:

- **G:** Start Grabbing
- **S:** Start Scaling
- **R:** Start Rotating
- **Move mouse:** Carry out transform action
- **Left-click:** Confirm transformation
- **Enter:** Confirm transformation

Pressing one of the keys will start the transformation, and then you can move your mouse to control the degree of the effect. To finalize the transformation, left-click the mouse or press Enter.

### Search <a id="Search"></a>

<img alt="The Search Box" src="../figures/Chapter1/Fig01-30.png" width="30%" align="right">

The final tip that you will learn is the search functionality in Blender. If you are unable to recall how to invoke a certain operation, whether through a button or a keyboard shortcut, a quick way to find it is by using the search functionality. Key in a few letters of what you are looking for, and the result should appear as shown in Figure 1.30.

Tapping on the spacebar from anywhere will bring out a search box that contains a list of actions.



A word of caution, though: the current implementation of the search is not very context-aware, so sometimes operations that are not permitted in the active context might show up.

### Blender Philosophy <a id="Blender_Philosophy"></a>

Blender is designed with certain philosophies in mind. Understanding these will allow you to use Blender the way it is intended, which allows you to navigate around Blender faster and work more efficiently.

Let the brainwashing begin!

### Interface <a id="Interface"></a>

Because Blender was originally created as an in-house software, its interface is designed to maximize speed and efficiency for users who have mastered it. Since Blender 2.5, a lot of work has been done to make the interface more user-friendly. That said, Blender is probably unlike any other program you've used before, including other kinds of 3D software. Luckily, the Blender interface is very consistent within the application. This means that once you learn to do something, you'll be able to use it in another part of the program.

### Keyboard <a id="Keyboard"></a>

Because of the large number of commands Blender is capable of performing, invoking a function through a quick tap on the keyboard is generally faster than using the mouse to find the menu entry. As you follow through the rest of this section, pay special attention to the shortcut keys that are used, because Blender is designed to let you work fast once you learn the shortcuts.


Blender's keyboard shortcuts are optimized for a full-sized English QWERTY keyboard. The number pad (which, unfortunately, is not present on many laptops) is used to quickly navigate around the 3D scene. Laptop users usually have to press extra keys on their keyboard (such as the Fn key or a toggle) in order to simulate a number pad key. As a solution, go to File > User Preferences (Ctrl + Alt + U), then switch to Input tab and enable "Emulate Numpad" option to use main 1 to 0 keys instead of Numpad keys. If you want this setting remain permanently, click on the "Save User Settings" button.
![Emulate Numpad](../figures/Chapter1/Fig01-30-1.png)

<img alt="3D Navigator." src="../figures/Chapter1/Fig01-31.png" width="20%" align="right">
Alternatively, Blender also has an add-on called "3D Navigation" that provides an easier way to navigate around the world for people without a number pad. To enable the 3D navigation plug-in to help you navigate around the 3D Viewport quickly, go to File > User Preferences > Add-Ons, and turn on 3D Views: 3D Navigation. Then you can switch views quickly from the 3D view's Toolshelf.

### Mouse <a id="Mouse"></a>

Blender is designed for a three-button mouse: a mouse with two buttons and a scroll wheel. Although there is an option to emulate the middle-mouse button (when you click on the scroll wheel), this book will assume that you are working with a three-button mouse for convenience.

> **How to Emulate a Three-Button Mouse**
>
> If you don't have a three-button mouse, you can use the Alt+Left mouse button combination to emulate the middle mouse button. To enable this feature, go to File > User Preferences > Input and turn on Emulate 3 Button Mouse.

### Context <a id="Context"></a>

In Blender, the actions you can perform at any given time are limited to the current state of Blender, also known collectively as the " context." For example, certain operations can only be invoked when you have an object selected; the Property Editors change, depending on which object is selected; the effect of the keyboard shortcuts even changes, depending on where your mouse is positioned. This context-sensitive nature lets you focus on the task at hand by only providing you with options that makes sense at the time. This is Blender's way of preventing the interface from getting too cluttered.

The "context" usually refers to one or a combination of the following:

- **Active rendering engine:** Blender Render, Blender Games, and Cycles Render are the default three.
- **Active editor:** The active editor is defined as the window subdivision that the mouse cursor is hovering over. Shortcut keys often have different effects, depending on which editor the mouse is over.
- **Active object:** The active object is defined as the object that is most recently selected.
- **Selected object:** All the objects that have been selected (highlighted). Keep in mind that there can be more than one selected object, but only one active object.
- **Editing mode:** Blender has six different modes of editing. Two of the most commonly used are the Edit mode and the Object mode. In Object mode, you can manipulate objects as a whole. In Edit mode, you can change the shape of a mesh. In each mode, there is a unique set of tools and options at your disposal. You will learn about the other four modes (Sculpt, Vertex Paint, Texture Paint, Weight Paint) in later chapters.

### Datablocks <a id="Datablocks"></a>

Often, a single Blender file contains hundreds of objects, each with different colors, textures, and animations. How is all this organized?

Blender uses "data blocks" to represent content stored within a Blender file. Each data block represents a collection of data or settings. Some common datablock types you will encounter are Object datablock, Mesh datablock, Material datablock, Texture datablock, and Image datablock.


<img alt="Datablock hierarchy" src="../figures/Chapter1/Fig01-32.png" width="30%" align="right">

In order to reduce the apparent complexity of the program, Blender further organizes data blocks into hierarchies. At the top level are scenes, which can have a number of worlds, each of which can have any number of objects (objects can be a mesh, a lamp, a camera, and so on). If the object is a mesh, then a Mesh datablock is attached to it. If the object is a lamp, then a Lamp datablock is attached to the object.

An example of a datablock hierarchy chain is shown in Figure 1.32: Scene > Object > Mesh > Material > Texture > Image


Throughout the Blender interface, you will run into many datablock managers. They all look like Figure 1.33.


<img alt="Datablock Sharing" src="../figures/Chapter1/Fig01-33.png" width="30%" align="left">

Because datablocks can be shared, copied, and reused, large scenes can be managed efficiently through the use of shared datablocks. Figure 1.33 shows a datablock that has been shared by three "users," as denoted by the number next to its name.

### Parenting and Grouping <a id="Parenting_and_Grouping"></a>

Grouping and parenting both allow you to introduce some form of order to the scene by setting up arbitrary relationships between different objects. But grouping and parenting work in different ways.

Parenting is used to establish links between multiple objects so that basic transformations like location, rotation, and scaling are propagated from the parent to its children. This way, any transformation applied to the parent is automatically applied to all the children. Parenting is a useful way to "glue" different objects together so they behave as one.

To parent one object to another, simply select the object you want to be the child first.  If more than one object is to be a child, select all of them now. Lastly, select the object that you want to be the parent. Then press Ctrl+P to set parent.

An object can only have one parent object, but a parent object can have many children.

Grouping can also be used to logically link objects in the scene together without any transformation constraints to the objects. Unlike parenting, grouping does not have a parent-child relationship; objects are simply members of a group.

Select all the objects you want to group. Then press Ctrl+G to add them to a new group. You can also manage group membership from the Object Properties Editor.

Grouping, by itself, it not very useful. But groups can be quickly "instanced" as group instances. Group Instance is a very useful way to create multiple copies of objects without making actual copies of the objects. Grouping will also come in handy for asset management, which will be discussed in the next chapter.

A single object can be in multiple groups. A group can have multiple objects.

### Backward Compatibility <a id="Backward_Compatibility"></a>

Blender is designed so that older files can be opened with newer versions of Blender. But due to the rate that Blender matures, some unexpected behaviors are to be expected when you least expect them.

Due to the Blender Python API change in Blender 2.5, old scripts written for 2.4x will be broken in later versions of Blender. But by the time you are reading this, there should be enough new content available for you to find.

## Onward <a id="Onward"></a>

This concludes the crash course on Blender and the game engine. By now, you should have a cursory understanding of the function of a game engine and be familiar with the Blender interface. In the next chapter, you will get your hands dirty and build a simple game by following the step-by-step tutorial.
