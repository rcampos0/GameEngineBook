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

### Transformações Básicas <a id="Basic_Transforms"></a>

As três transformações básicas com as quais você deve se familiarizar são:

* ** Translação: ** O movimento de um objeto em qualquer direção, sem girá-lo.
* ** Dimensionamento: ** O redimensionamento de um objeto em torno de um ponto.
* ** Rotação: ** A rotação de um objeto em torno de um ponto.

Essas três são as manipulações mais comuns que você encontrará. Eles são ilustrados abaixo.

![Translação, dimensionamento, e rotação.](../figures/Chapter1/Fig01-09.jpg)

### Materiais e Texturas <a id="Materials_and_Textures"></a>

Usando polígonos, você pode definir a forma de uma malha. Para alterar a cor e a aparência, é necessário aplicar materiais ao objeto. O material controla a cor, o brilho, o relevo e até a transparência do objeto. No fim, todas essas variáveis servem para adicionar detalhes ao objeto.

Muitas vezes, alterar a cor não é suficiente para fazer com que uma superfície pareça realista. É aqui que as texturas entram. A texturização é uma técnica comum usada para adicionar cor e detalhes a uma malha, envolvendo a malha com uma imagem, como um decalque. Imagine um globo de brinquedo: se você cuidadosamente retira o mapa de papel colado na bola de plástico e o coloca sobre a mesa, esse mapa seria a textura e a bola de plástico seria a malha. A projeção da imagem 2D em uma malha 3D é denominada _texture mapping_. O mapeamento de textura pode ser um processo automático, usando uma das projeções predefinidas, ou um processo manual, que usa um layout UV para mapear a imagem 2D na malha 3D. A Figura 1.10 ilustra como uma imagem é mapeada em um modelo.

![Malhas com textura aplicada.](../figures/Chapter1/Fig01-10.jpg)


Tradicionalmente, uma textura muda a cor de uma superfície. Mas isso não é tudo o que pode fazer: as texturas também podem ser usadas para alterar outras propriedades da superfície, como sua transparência, refletividade e até irregularidade, para criar a ilusão de uma superfície muito mais detalhada.

<img alt="From left to right: diffuse map, normal map, and specular map." src="../figures/Chapter1/Fig01-11.jpg" width="50%" align="right">

Um mapa difuso controla a cor base da superfície. Um mapa normal controla a superfície normal de um objeto, criando um efeito irregular alterando a maneira como a luz é refletida no objeto. Um mapa especular controla a reflexão especular de um objeto, fazendo com que pareça brilhante em certos lugares e opaco em outros. Um mapa de textura também pode ter pixels transparentes, tornando parte do objeto transparente.

Geralmente, as texturas são arquivos de imagem. Mas também existem outras maneiras de texturizar uma superfície, como o uso de uma textura processual. A textura processual difere de uma imagem, pois é gerada por um algoritmo em tempo real, e não de um arquivo de imagem pré-criado. O mecanismo de jogo do Blender ainda não suporta texturas processuais.

### Luzes <a id="Lights"></a>

Tudo o que você vê é o resultado da luz atingindo seus olhos - sem luzes, o mundo seria totalmente escuro. Da mesma forma, a luz é igualmente importante em um mundo virtual. Com a luz vem a sombra também. A sombra pode não ser algo que você pensa todos os dias, mas a interação de sombra e luz faz uma enorme diferença na forma como a cena é apresentada.

<img alt="From left: Lamp, Sun, Spot lamp, Hemi lamp, and Area lamp." src="../figures/Chapter1/Fig01-12.png" width="50%" align="right">

Na maioria das aplicações 3D, existem vários tipos diferentes de luz disponíveis para o artista; cada tipo tem suas vantagens e desvantagens. Por exemplo, uma lâmpada Spot aproxima-se de uma lâmpada com influência cônica; uma lâmpada solar aproxima-se de uma fonte de luz infinitamente distante. As lâmpadas no Blender são tratadas como objetos comuns: elas podem ser posicionadas e giradas como qualquer outro objeto. A Figura 1.12 mostra a aparência de diferentes lâmpadas no Blender.

Pense na iluminação como algo que torna sua cena visível. Uma boa iluminação pode aprimorar o objetivo da cena destacando os detalhes enquanto oculta áreas irrelevantes na sombra. A colocação hábil da iluminação também adiciona drama e realismo à cena, fazendo com que uma cena chata pareça visualmente emocionante.

### Câmera <a id="Camera"></a>

<img alt="Camera objects" src="../figures/Chapter1/Fig01-13.png" width="50%" align="right">

Ao criar uma cena 3D, você está olhando o mundo virtual de uma visão onisciente. Nesse modo, você pode visualizar e editar o mundo de qualquer ângulo [md], como um diretor de cinema andando em um set para ajustar as coisas. Uma vez iniciado o jogo, o jogador deve vê-lo através de uma câmera pré-determinada. Observe que uma câmera predeterminada não significa que a câmera está fixa; quase todos os jogos têm uma câmera que reage à entrada do jogador. Em um jogo de ação, a câmera tende a seguir o personagem por trás; em um jogo de estratégia, a câmera pode estar pairando acima, olhando para baixo; em um jogo de plataformas, a câmera geralmente olha a cena de lado.

Uma câmera também é tratada como um objeto comum no Blender, para que você possa manipular sua localização e orientação da mesma forma que em qualquer outro objeto.


> **Desenhando e compondo para contadores de histórias visuais**
>
> Por falar em luzes e câmeras, é nessa parte que destacamos o maravilhoso livro de Marcos Mateu-Mestre, chamado Framed Ink. O livro usa toneladas de belos desenhos para ilustrar os muitos princípios-chave da narrativa visual.

### Animação <a id="Animation"></a>

Nesse contexto, _animação_ refere-se à técnica de fazer as coisas mudarem com o tempo. Por exemplo, a animação pode envolver mover um objeto, deformar ou alterar sua cor. Para configurar uma animação, crie "quadros-chave", que são instantâneos no tempo que armazenam valores específicos pertencentes à animação. O software pode interpolar automaticamente entre esses valores para criar uma transição suave. A imagem abaixo mostra o Editor de Dopesheet do Blender. Um Dopesheet permite ver as várias propriedades que mudam durante uma animação: o eixo horizontal representa o tempo; o eixo vertical mostra as várias propriedades, como localização ou rotação, que são os quadros principais.

![Editor de Dopesheet: cada forma de diamante é um quadro-chave.](../figures/Chapter1/Fig01-14.png)

<img alt="LocRotScale animation" src="../figures/Chapter1/Fig01-15.png" width="50%" align="right">
<br><br>
A maneira mais fácil de animar é alterar o local, a rotação e a escala de um objeto ao longo do tempo. Por exemplo, alterando essas variáveis, você pode animar realisticamente o movimento de uma bola quicando. Lembre-se de que as curvas representam o valor dos canais (neste caso, localização xyz) da bola, não o caminho real do movimento da bola.

<br><br>

<img alt="Armature animation" src="../figures/Chapter1/Fig01-16.png" width="33%" align="left">
<br><br>
Para animar algo mais complicado, como um humano, não basta mover, girar e dimensionar o objeto como um todo. É aqui que as armaduras entram. Armaduras são esqueletos que podem ser "inseridos" em um modelo para controlar a deformação do modelo. Usando esse sistema, você pode criar animações complexas, porém com aparência orgânica.

<br><br><br><br>
<img alt="Shape keys animation." src="../figures/Chapter1/Fig01-17.jpg" width="50%" align="right">
<br>
Uma terceira maneira de animar é usar as teclas de forma. As teclas de forma são instantâneos da malha em diferentes formas. Eles são frequentemente usados para animar mudanças diferenciadas que não podem ser facilmente animadas com armaduras.


<img alt="Procedural physics-based motion." src="../figures/Chapter1/Fig01-18.jpg" width="33%" align="left">
<br>
Por fim, lembre-se de que fazer mover objetos nem sempre precisa ser um processo manual. Você também pode mover objetos usando o mecanismo de física (consulte o Capítulo 6).

<br>

### Jogo <a id="Game"></a>

Até agora, falamos sobre o 3D em detalhes. Mas como o mecanismo de jogo se encaixa? Bem, um mecanismo de jogo simplesmente pega os recursos 3D existentes e anexa um "cérebro" a eles para que os objetos saibam como responder aos eventos. O "cérebro" pode estar na forma de blocos lógicos (que podem executar ações diferentes dependendo da entrada do usuário), scripts (que podem estender a funcionalidade dos blocos lógicos) ou outras propriedades físicas de um objeto (como configurações rígidas do corpo fazer um objeto cair e cair de maneira realista).

![Game = Objeto + Logic.](../figures/Chapter1/Fig01-19.jpg)

Um mecanismo de jogo é composto de muitos componentes distintos:

- ** Rendering Engine **: transforma a cena 3D que você construiu (incluindo modelos, luzes e câmera) em uma imagem para ser exibida na tela.
- ** Física **: lida com colisões e simulações físicas de objetos.
- ** Logic / Scripting **: o cérebro por trás de um jogo [md] reage às informações do usuário, toma decisões e acompanha o que está acontecendo no jogo.
- ** Som **: produz os eventos de áudio.

A lista acima não pretende ser exaustiva, mas deve fornecer uma idéia do que um mecanismo de jogo faz. O mecanismo de jogo do Blender oferece muito controle sobre cada um desses componentes, que você aprenderá um a um nos próximos capítulos.

> **Qualidade vs. Desempenho**
>
>Fazer um videogame é um constante equilíbrio entre qualidade e desempenho. Como artistas, você deseja tornar o mundo virtual o mais rico e detalhado possível; por outro lado, você precisa garantir que o jogo funcione sem problemas para pessoas que podem não ter computadores de primeira linha. Durante todo o processo de criação de jogos, você encontrará casos em que precisa decidir se deve priorizar a qualidade visual ou o desempenho do jogo. Você também aprenderá truques para obter visual de alta qualidade sem comprometer o desempenho, bem como otimizar o jogo, identificando o que está diminuindo sua velocidade.

## Configurando <a id="Setting_up"></a>

Finalmente chegou a hora de mergulhar no Blender! A partir de agora, é melhor você ler o livro com o computador ao seu lado. Nesta seção, faremos um breve tour pelo Blender, apenas o suficiente para você se familiarizar com o software.

### Instalação <a id="Installation"></a>

O Blender roda em Windows, Mac OS X e Linux. Você pode encontrar o instalador do Blender para o seu sistema operacional em www.blender.org. O tamanho completo do download do Blender é de aproximadamente 100 MB.

Vá em frente e instale o Blender. Inicie o aplicativo uma vez instalado.

> **Instalação não requerida**
>
> Tecnicamente, o Blender não precisa ser instalado antes de poder ser usado. O instalador está disponível apenas por conveniência. O Blender será executado em qualquer local. Você pode até copiá-lo para um dispositivo de armazenamento USB e carregá-lo com você, para nunca se separar do seu programa favorito. Embora, por padrão, o Blender salve algumas configurações do usuário no diretório do usuário.

Mesmo que você precise do Blender para desenvolver o jogo, os jogos do Blender podem ser empacotados como aplicativos autônomos, para que outros jogadores não precisem instalar nada. Consulte o Capítulo 9, "Publicando e além", para obter mais detalhes.

### Requisitos do sistema <a id="System_Requirements"></a>

O Blender não possui requisitos explícitos de sistema. O desempenho do software depende da complexidade do projeto. Desnecessário dizer que, quanto mais rápido o seu computador, melhor o Blender será executado.

## O Basico de Blender <a id="Blender_Basics"></a>

Ao iniciar o Blender, você será recebido com a tela inicial. Embora você possa personalizar todos os aspectos do Blender, neste livro, assumiremos que você está usando as configurações e atalhos padrão do Blender.

Clicando em qualquer outro lugar para descartar a tela inicial, você verá um espaço de trabalho vazio como este:

![Blender default workspace.](../figures/Chapter1/Fig01-20.jpg)

A janela do Blender é dividida em Editores. Cada região do Editor pode ser redimensionada, movida e alterada para exibir um conjunto específico de conteúdo. Por enquanto, vamos nos concentrar na configuração padrão.

#### Menu Principal <a id="Main_Menu"></a>

Na parte superior da tela, está o menu principal, que oferece funcionalidades básicas, como Abrir, Salvar e Ajuda. Além disso, o menu principal controla a visualização do restante da janela do Blender. A opção Mecanismo de renderização no meio do menu controla como a interface está configurada.

<img alt="Selecting the Game Engine" src="../figures/Chapter1/Fig01-21.png" width="40%" align="left">
Por padrão, Cycles Render está selecionado. Nesse modo, a interface está configurada para modelagem, animação e renderização em 3D com o Cycles. Mas vamos mudar para o modo Blender Game. Clique no menu suspenso e selecione Jogo do Blender na lista. Essa configuração desbloqueia certos recursos que não são visíveis normalmente e também oculta os recursos que não estão disponíveis no mecanismo de jogo do Blender.


#### 3D Viewport <a id="3D_Viewport"></a>

Ocupando a maior parte da tela está uma viewport 3D. Aqui você pode ver o mundo 3D que você criou e testar o jogo. Por enquanto, fique à vontade para explorar a Viewport 3D mantendo pressionado o botão do meio do mouse sobre a Viewport 3D e arrastando o mouse; a vista deve girar com o movimento do mouse. (Os usuários de Mac podem usar o gesto de rotação de dois dedos no trackpad). A cena padrão contém três objetos: um cubo, uma câmera e uma luz. Para selecionar um dos objetos, clique com o botão direito do mouse. O objeto selecionado é destacado em amarelo.

>**Controles básicos de navegação**

>Pressione e segure o botão do meio do mouse para girar a visualização 3D. Role a roda do mouse para ampliar a visualização 3D. Clique com o botão direito do mouse para selecionar um objeto 3D. Os objetos selecionados são destacados em amarelo.


<img alt="Number pad keyboard layout." src="../figures/Chapter1/Fig01-23.png" width="25%" align="left">
<br>
Outra configuração comum para o 3D Viewport é dividir a vista em quatro quadrantes: vista superior, lateral, frontal e frontal. Você pode ativar a visualização Quad pressionando Ctrl + Alt + Q com o mouse sobre a viewport 3D (veja a Figura 1.22). Pressione a mesma combinação de teclas para voltar à exibição única.

Para encaixar rapidamente em uma das vistas predeterminadas (lateral, superior, frontal etc.), o teclado numérico é o caminho a percorrer.

<br><br>


#### Outliner <a id="Outliner"></a>

<img alt="Outliner" src="../figures/Chapter1/Fig01-20b.png" width="33%" align="right">

À direita da tela há dois editores. A parte superior é o Outliner, que contém uma lista de todos os dados no arquivo atual do Blender. Para um projeto grande, o Outliner é uma ferramenta indispensável para organizar sua cena. Por enquanto, você pode ignorá-lo com segurança.

#### Editor de Propriedades <a id="Properties_Editor"></a>


<img alt="Properties Editor icons." src="../figures/Chapter1/Fig01-24.png" width="33%" align="right">
Sob o Outliner à direita, você tem o Editor de propriedades. Aqui você pode acessar configurações globais para o arquivo, bem como configurações para objetos individuais. Este é um dos painéis mais usados no Blender, talvez depois da visualização em 3D. O Editor de propriedades é sensível ao contexto, o que significa que ele exibirá automaticamente conteúdo diferente, dependendo do objeto que estiver ativo. Observe mais de perto a linha de ícones na parte superior do Editor de propriedades, como mostra a Figura 1.24. Essas guias organizam as propriedades em grupos, com as configurações mais gerais na guia mais à esquerda e as configurações mais específicas à direita.


#### Timeline <a id="Timeline"></a>

Na parte inferior da tela, há uma janela da linha do tempo, que será útil quando você começar a fazer animações.
![Timeline](../figures/Chapter1/Fig01-20c.png)


#### Personalização da área de trabalho <a id="Workspace_Customization"></a>

A tela padrão, conforme descrito anteriormente, é configurada para uso geral. Em algum momento, torna-se necessário alterar o layout da tela para realizar outras tarefas. Para selecionar um layout diferente, use o menu suspenso Layout de telas no menu principal.

Além dos layouts de tela predefinidos, você pode personalizar o layout da tela da maneira que desejar. Você pode dividir um editor existente em dois ou mesclar dois editores adjacentes.

>**Editor, região e área**
>
>Uma região dentro das janelas do Blender é chamada de _editor_. Um editor exibe um conjunto específico de conteúdo e ferramentas. As áreas comuns incluem: Visualização 3D, Editor de propriedades, Editor de UV / imagem e Editor de tijolo lógico.



A Figura 1.25 mostra uma área dividida em duas. Você pode fazer isso arrastando o canto superior da área para a direita ou para baixo

![Divisão de área](../figures/Chapter1/Fig01-25.png)

Mesclar duas áreas adjacentes em uma é exatamente o mesmo mostrado na Figura 1.25, mas é feito na ordem inversa. Opcionalmente, você pode clicar com o botão direito do mouse na borda da área que deseja dividir ou unir e selecionar a opção no menu pop-up Opções de Área.


<img alt="Seleção de editor." src="../figures/Chapter1/Fig01-27.png" width="25%" align="left">
<br>
Não apenas você pode alterar o tamanho e o layout do editor, mas também o tipo de editor. Como você pode ver na Figura 1.27, o ícone mais à esquerda no cabeçalho pode ser usado para alterar o tipo de editor.

<img alt="Dopesheet, Image Editor, and Logic Brick Editor." src="../figures/Chapter1/Fig01-28.png" width="45%" align="right">
Quase tudo o que um estúdio precisa para criar o jogo está integrado em uma única interface: você pode criar o jogo, testar o jogo e jogar tudo no mesmo programa. Isso significa que, como artista, você pode criar um jogo no menor tempo possível, sem ter que se preocupar em importar e exportar arquivos entre aplicativos diferentes. Como programador, você não precisará alternar entre softwares diferentes apenas para testar seu código. A Figura 1.28 mostra algumas capturas de tela de diferentes editores que você usará ao longo do livro.


### Mais sobre a vista 3D <a id="More_on_the_3D_View"></a>

A visualização 3D é onde você passará a maior parte do tempo, então vamos dar uma olhada em mais detalhes. Você já aprendeu algumas maneiras de navegar pela cena anteriormente neste capítulo, usando o mouse e o teclado.

#### Modos de sombreamento da viewport <a id="Viewport_Shading_Modes"></a>

<img alt="Drawing Modes" src="../figures/Chapter1/Fig01-29.png" width="25%" align="right">
Vejamos os quatro modos diferentes de Viewport Shading disponíveis na visualização 3D. Eles são usados para alterar a maneira como a cena é exibida na tela. Os quatro modos são:

- ** Caixa delimitadora **: representa todos os objetos como um limite de estrutura de arame. Útil para quando a cena fica realmente complexa.
- ** Wireframe **: desenha todos os objetos como wireframe, o que permite ver através dos objetos.
- ** Sólido **: desenha todos os objetos como faces sólidas, comumente usadas na modelagem.
- ** Texturizado **: desenha todos os objetos como faces sólidas, também com textura e iluminação precisa. Isso é útil para visualizar a cena.

Os dois modos de sombreamento mais usados são Wireframe e Solid. Portanto, eles são atribuídos a uma alternância de teclado para facilitar o acesso. Pressione a tecla Z para alternar entre os modos Wireframe e Solid View. Além disso, você pode pressionar Alt + Z para alternar entre os modos de exibição Sólido e Texturizado.

> **Destacando-se**
>
> Objetos individuais também podem substituir o modo de sombreamento da viewport por meio de uma configuração no Editor de propriedades> Objeto> Tela> Tipo.



### Modos de edição <a id="Editing_Modes"></a>

À esquerda do seletor de modo de sombreamento está o seletor de modo de edição.

- ** Modo de objeto **: o modo padrão, que permite a manipulação de objetos na cena como um todo. Nesse modo, você pode selecionar qualquer um dos objetos na cena e movê-los, girá-los e redimensioná-los. De fato, quase tudo, além da modelagem, pode ser feito no modo Objeto.
- ** Edit Mode **: Este modo pode ser visto como o equivalente ao modo Objeto. Permite editar a geometria subjacente do objeto. Se você estiver modelando, provavelmente desejará estar no modo de edição. Por esse motivo, o modo de edição não está disponível quando um objeto não editável é selecionado (por exemplo, uma câmera ou lâmpada).

Para alternar entre o modo Objeto e o modo Editar, pressione a tecla Tab.

Além dos dois modos de edição que acabamos de discutir, existem alguns outros modos que são menos usados.

- ** Modo Sculpt **: Disponível apenas para objetos Mesh. Permite modificações na malha como se fosse argila.
- ** Vertex **, ** Weight, ** e ** Texture Paint Mode **: Disponível apenas para objetos de malha. Esses modos permitem a atribuição de cor ou peso à malha.
- ** Modo de pose **: É usado para animar ossos em uma armadura.

O modo de edição e o modo de objeto são, de longe, os modos de edição mais usados, por isso, nos absteremos de mergulhar profundamente nos outros modos por enquanto.

### Teclado e Mouse <a id="Keyboard_and_Mouse"></a>

A piada é que, para mover um objeto no Blender, você precisa pressionar a tecla G, que significa "movinG". Essa mordaça decorre do fato de que, para um iniciante, muitos dos atalhos no Blender parecem contra-intuitivos. No entanto, há uma boa razão pela qual "G" é preferido em vez de "M." Nesse caso, a tecla G pode ser facilmente acessada no teclado pela mão esquerda enquanto a mão direita está no mouse. Além disso, oficialmente, G significa Grab.



> **Pense diferente**
>
> Por padrão, o teclado do Mac usa Command em vez de Control como a tecla modificadora padrão. Portanto, sempre que vir Ctrl + Something neste livro, mapeie-o mentalmente para o Cmd se você estiver usando um produto Jobsian.
>
> Além disso, o Blender oferece um bom suporte para gestos multitoque no OS X. Você pode beliscar para ampliar, girar para orbitar e girar.



Vamos começar com alguns atalhos que funcionam da maneira que você esperaria:

* ** Ctrl + S: ** Salvar arquivo
* ** Ctrl + O: ** Abrir arquivo
* ** Ctrl + N: ** Novo arquivo
* ** Ctrl + Z: ** Desfazer
* ** Ctrl + Shift + Z: ** Refazer
* ** Ctrl + Q: ** Fechar (Sair) do aplicativo

Os atalhos acima funcionam em qualquer lugar do Blender: eles são efetivamente globais. Infelizmente, a familiaridade termina aqui.

Para manipular um objeto na vista 3D, geralmente é necessário selecioná-lo primeiro:

- ** Clique com o botão direito do mouse: ** Selecionar objeto
- ** Shift + clique com o botão direito do mouse: ** Estende a seleção para vários objetos
- ** A: ** Selecionar tudo

Todas as ações acima são "reversíveis". Se alguma coisa já estiver selecionada, clicar com o botão direito do mouse nela cancelará a seleção. Se todos os objetos já estiverem selecionados, pressionar A desmarcará tudo.

Depois que um objeto é selecionado, você pode começar a manipulá-lo. Os atalhos de teclado abaixo correspondem às três transformações mais básicas:

- ** G: ** Comece a agarrar
- ** S: ** Iniciar o dimensionamento
- ** R: ** Comece a girar
- ** Mova o mouse: ** Execute a ação de transformação
- ** Clique com o botão esquerdo: ** Confirme a transformação
- ** Enter: ** Confirmar transformação

Pressionar uma das teclas iniciará a transformação e você poderá mover o mouse para controlar o grau do efeito. Para finalizar a transformação, clique com o botão esquerdo do mouse ou pressione Enter.

### Busca <a id="Search"></a>

<img alt="A caixa de busca" src="../figures/Chapter1/Fig01-30.png" width="30%" align="right">

A dica final que você aprenderá é a funcionalidade de pesquisa no Blender. Se você não conseguir se lembrar de como chamar uma determinada operação, seja através de um botão ou de um atalho de teclado, uma maneira rápida de encontrá-la é usando a funcionalidade de pesquisa. Digite algumas letras do que você está procurando e o resultado deverá aparecer como mostrado na Figura 1.30.
Tocar na barra de espaço de qualquer lugar exibirá uma caixa de pesquisa que contém uma lista de ações.



Uma palavra de cautela: a implementação atual da pesquisa não é muito sensível ao contexto; portanto, às vezes, operações que não são permitidas no contexto ativo podem aparecer.

### A Filosofia de Blender <a id="Blender_Philosophy"></a>

O Blender é projetado com certas filosofias em mente. Entender isso permitirá que você use o Blender da maneira que se destina, o que permite navegar pelo Blender mais rapidamente e trabalhar com mais eficiência.

Que comece a lavagem cerebral!

### Interface <a id="Interface"></a>

Como o Blender foi criado originalmente como um software interno, sua interface foi projetada para maximizar a velocidade e a eficiência dos usuários que o dominam. Desde o Blender 2.5, muito trabalho foi feito para tornar a interface mais amigável. Dito isto, o Blender provavelmente é diferente de qualquer outro programa que você já usou antes, incluindo outros tipos de software 3D. Felizmente, a interface do Blender é muito consistente dentro do aplicativo. Isso significa que depois que você aprender a fazer algo, poderá usá-lo em outra parte do programa.

### Teclado <a id="Keyboard"></a>

Devido ao grande número de comandos que o Blender é capaz de executar, invocar uma função através de um toque rápido no teclado geralmente é mais rápido do que usar o mouse para encontrar a entrada do menu. Conforme você segue o restante desta seção, preste atenção especial às teclas de atalho usadas, porque o Blender foi projetado para permitir que você trabalhe rapidamente depois de aprender os atalhos.


Os atalhos de teclado do Blender são otimizados para um teclado QWERTY em tamanho inglês. O teclado numérico (que, infelizmente, não está presente em muitos laptops) é usado para navegar rapidamente pela cena 3D. Os usuários de laptops geralmente precisam pressionar teclas extras no teclado (como a tecla Fn ou uma alternância) para simular uma tecla do teclado numérico. Como solução, vá para Arquivo> Preferências do usuário (Ctrl + Alt + U), alterne para a guia Entrada e ative a opção "Emular Numpad" para usar as teclas principais 1 a 0 em vez das teclas Numpad. Se você deseja que essa configuração permaneça permanentemente, clique no botão "Salvar configurações do usuário".
![Emular Numpad](../figures/Chapter1/Fig01-30-1.png)

<img alt="Navegação 3D." src="../figures/Chapter1/Fig01-31.png" width="20%" align="right">
Como alternativa, o Blender também possui um complemento chamado "Navegação 3D" que fornece uma maneira mais fácil de navegar pelo mundo para pessoas sem teclado numérico. Para ativar o plug-in de navegação 3D para ajudá-lo a navegar rapidamente pela Viewport 3D, vá para Arquivo> Preferências do usuário> Complementos e ative Exibições 3D: Navegação 3D. Em seguida, você pode alternar as visualizações rapidamente da prateleira de ferramentas da visualização 3D.

### Mouse <a id="Mouse"></a>

O Blender foi desenvolvido para um mouse de três botões: um mouse com dois botões e uma roda de rolagem. Embora exista uma opção para emular o botão do meio do mouse (quando você clica na roda de rolagem), este livro pressupõe que você esteja trabalhando com um mouse de três botões por conveniência.

> **Como emular um mouse de três botões**
>
> Se você não possui um mouse de três botões, pode usar a combinação de botões Alt + Esquerdo para emular o botão do meio. Para ativar esse recurso, vá para Arquivo> Preferências do usuário> Entrada e ative o Emulate 3 Button Mouse.

### Contexto <a id="Context"></a>

No Blender, as ações que você pode executar a qualquer momento são limitadas ao estado atual do Blender, também conhecido coletivamente como "contexto". Por exemplo, certas operações só podem ser invocadas quando você tiver um objeto selecionado; os editores de propriedades são alterados, dependendo do objeto selecionado; o efeito dos atalhos do teclado muda até mesmo, dependendo da posição do mouse. Essa natureza sensível ao contexto permite que você se concentre na tarefa em questão, fornecendo apenas as opções que fazem sentido no momento. Esta é a maneira do Blender de impedir que a interface fique muito confusa.

O "contexto" geralmente se refere a um ou a uma combinação dos seguintes itens:

- ** Mecanismo de renderização ativo: ** Blender Render, Blender Games e Cycles Render são os três padrão.
- ** Editor ativo: ** O editor ativo é definido como a subdivisão da janela sobre a qual o cursor do mouse está passando o mouse. As teclas de atalho geralmente têm efeitos diferentes, dependendo de qual editor o mouse acabou.
- ** Objeto ativo: ** O objeto ativo é definido como o objeto que foi selecionado mais recentemente.
- ** Objeto selecionado: ** Todos os objetos que foram selecionados (destacados). Lembre-se de que pode haver mais de um objeto selecionado, mas apenas um objeto ativo.
- ** Modo de edição: ** O Blender possui seis modos diferentes de edição. Dois dos mais usados ​​são o modo de edição e o modo de objeto. No modo Objeto, você pode manipular objetos como um todo. No modo de edição, você pode alterar a forma de uma malha. Em cada modo, há um conjunto exclusivo de ferramentas e opções à sua disposição. Você aprenderá sobre os outros quatro modos (Sculpt, Vertex Paint, Texture Paint, Weight Paint) nos próximos capítulos.

### Bloco de Dados <a id="Datablocks"></a>

Freqüentemente, um único arquivo Blender contém centenas de objetos, cada um com cores, texturas e animações diferentes. Como tudo isso está organizado?

O Blender usa "blocos de dados" para representar o conteúdo armazenado em um arquivo Blender. Cada bloco de dados representa uma coleção de dados ou configurações. Alguns tipos comuns de blocos de dados que você encontrará são: bloco de dados Objeto, bloco de dados Mesh, bloco de dados Material, bloco de dados Texture e bloco de dados Image.


<img alt="Hierarquia de bloco de dados" src="../figures/Chapter1/Fig01-32.png" width="30%" align="right">

Para reduzir a aparente complexidade do programa, o Blender organiza ainda mais os blocos de dados em hierarquias. No nível superior, há cenas que podem ter vários mundos, cada qual com vários objetos (os objetos podem ser uma malha, uma lâmpada, uma câmera e assim por diante). Se o objeto for uma malha, um bloco de dados Mesh será anexado a ele. Se o objeto for uma lâmpada, um bloco de dados da lâmpada será anexado ao objeto.

Um exemplo de uma cadeia de hierarquia de blocos de dados é mostrado na Figura 1.32: Cena> Objeto> Malha> Material> Textura> Imagem


Em toda a interface do Blender, você encontrará muitos gerenciadores de blocos de dados. Todos eles se parecem com a Figura 1.33.


<img alt="Compartilhamento de Datablock" src="../figures/Chapter1/Fig01-33.png" width="30%" align="left">

Como os blocos de dados podem ser compartilhados, copiados e reutilizados, cenas grandes podem ser gerenciadas eficientemente através do uso de blocos de dados compartilhados. A Figura 1.33 mostra um bloco de dados que foi compartilhado por três "usuários", conforme indicado pelo número ao lado de seu nome.

### Parentalidade e Agrupamento <a id="Parenting_and_Grouping"></a>

O agrupamento e a criação dos pais permitem introduzir alguma forma de ordem na cena, estabelecendo relacionamentos arbitrários entre objetos diferentes. Mas agrupar e criar filhos funcionam de maneiras diferentes.

A parentalidade é usada para estabelecer links entre vários objetos, para que transformações básicas como localização, rotação e escala sejam propagadas do pai para seus filhos. Dessa forma, qualquer transformação aplicada ao pai é automaticamente aplicada a todos os filhos. A paternidade é uma maneira útil de "colar" objetos diferentes para que eles se comportem como um.

Para pai de um objeto para outro, basta selecionar o objeto que você deseja que seja o filho primeiro. Se mais de um objeto for filho, selecione todos eles agora. Por fim, selecione o objeto que você deseja que seja o pai. Em seguida, pressione Ctrl + P para definir o pai.

Um objeto pode ter apenas um objeto pai, mas um objeto pai pode ter muitos filhos.

O agrupamento também pode ser usado para vincular logicamente objetos na cena, sem nenhuma restrição de transformação aos objetos. Ao contrário dos pais, o agrupamento não tem um relacionamento pai-filho; objetos são simplesmente membros de um grupo.

Selecione todos os objetos que você deseja agrupar. Em seguida, pressione Ctrl + G para adicioná-los a um novo grupo. Você também pode gerenciar a associação ao grupo no Editor de propriedades do objeto.

Agrupar, por si só, não é muito útil. Mas os grupos podem ser "instanciados" rapidamente como instâncias de grupo. A Instância de grupo é uma maneira muito útil de criar várias cópias de objetos sem fazer cópias reais dos objetos. O agrupamento também será útil para o gerenciamento de ativos, que será discutido no próximo capítulo.

Um único objeto pode estar em vários grupos. Um grupo pode ter vários objetos.

### Compatibilidade com versões anteriores <a id="Backward_Compatibility"></a>

O Blender foi desenvolvido para que arquivos mais antigos possam ser abertos com versões mais recentes do Blender. Porém, devido à taxa que o Blender amadurece, alguns comportamentos inesperados são esperados quando você menos espera.

Devido à alteração da API do Blender Python no Blender 2.5, os scripts antigos escritos para 2.4x serão quebrados nas versões posteriores do Blender. Mas quando você estiver lendo isso, deve haver conteúdo novo suficiente disponível para você encontrar.

## Adiante <a id="Onward"></a>

Isso conclui o curso intensivo do Blender e do mecanismo de jogo. Até agora, você deve ter uma compreensão superficial da função de um mecanismo de jogo e estar familiarizado com a interface do Blender. No próximo capítulo, você vai sujar as mãos e criar um jogo simples, seguindo o tutorial passo a passo.
