**Table of Contents**

- [Capítulo 5: Gráficos](#Chapter_5_Graphics)
	- [Estilo Visual](#Visual_Style)
	- [Projetando para Tempo Real](#Designing_for_Real_Time)
	- [Geometria](#Geometry)
	- [Materiais e Texturas](#Materials_and_Textures)
	- [Iluminação](#Lights)
	- [Modos de Sombreamento](#Shading_Modes)
		- [Modo GLSL](#GLSL_Mode)
			- [Materiais e Texturas](#Material_and_Textures)
				- [O Painel de Material](#The_Material_Panel)
					- [Gerencimento de Material](#Material_Management)
					- [Objetos de Multi-Material](#Multi-Material_Objects)
					- [Objeto vs. Dado](#Object_vs._Data)
					- [Preview](#Preview)
					- [Diffuse](#Diffuse)
					- [Specular](#Specular)
					- [Ramp](#Ramp)
					- [Shading](#Shading)
					- [Game Settings](#Game_Settings)
					- [Physics](#Physics)
					- [Additional Options](#Additional_Options)
				- [The Texture Panel](#The_Texture_Panel)
					- [Texture Data Blocks](#Texture_Data_Blocks)
					- [Image](#Image)
					- [Image Sampling Panel](#Image_Sampling_Panel)
					- [Mapping Panel](#Mapping_Panel)
					- [Influence Panel](#Influence_Panel)
			- [Combined Exercise](#Combined_Exercise)
			- [Nodes](#Nodes)
		- [Multitexture](#Multitexture)
	- [Lights](#Lights)
	- [World Settings](#World_Settings)
	- [Texture Painting](#Texture_Painting)
	- [Custom GLSL Shaders](#Custom_GLSL_Shaders)
	- [GLSL Primer](#GLSL_Primer)
	- [Custom GLSL Shaders](#Custom_GLSL_Shaders)
		- [A Useful Fragment Shader](#A_Useful_Fragment_Shader)
		- [A Useful Vertex Shader](#A_Useful_Vertex_Shader)
		- [Going Further](#Going_Further)
	- [2D Filters](#2D_Filters)
		- [Why Use 2D Filters?](#Why_Use_2D_Filters?)
		- [How to Use 2D Filters](#How_to_Use_2D_Filters)
		- [Custom Filter](#Custom_Filter)
		- [Limitations](#Limitations)
	- [Text](#Text)
	- [Bitmap Text](#Bitmap_Text)
	- [Text Object](#Text_Object)
	- [Video Texture](#Video_Texture)
	- [Stereo](#Stereo)
	- [Dome](#Dome)

# Capítulo 5: Gráficos <a id="Chapter_5_Graphics"></a>

Bem-vindo ao Capítulo 5, onde se trata de recursos visuais! Quando você joga, os gráficos geralmente são o primeiro elemento a causar uma boa impressão, muito antes de você poder formar uma opinião mais abrangente sobre o jogo com base em outros aspectos como jogabilidade, história, física ou som. Quer se trate de uma captura de tela, um trailer de vídeo ou um pôster impresso, os gráficos são o único elemento em que os editores contam constantemente para chamar a atenção do público. Portanto, é justo que examinemos esse tópico em detalhes.

![Blender game arts de Martins Upitis.](..\figures\Chapter5\Fig05-01.jpg)


Em um jogo moderno, não é incomum que o computador gaste a maior parte de seu tempo de processamento renderizando os gráficos, enquanto a lógica, a física e o som do jogo normalmente ocupam apenas uma pequena fração do tempo total de computação. Esse fato por si só deve convencê-lo da complexidade da computação gráfica em tempo real.

Neste capítulo, aprenderemos primeiro como trabalhar com os sistemas de material, textura e sombreamento no motor de jogo; seguido por uma rápida introdução ao GLSL - OpenGL Shading Language, a linguagem de sombreamento que permite estender ainda mais a capacidade gráfica do motor de jogo; e conclua o capítulo mostrando algumas das ferramentas e recursos mais especializados que podem ser usados em um jogo.

## Visual Style <a id="Visual_Style"></a>
Para a maioria dos artistas gráficos, o objetivo final de seu trabalho sempre foi o fotorrealismo. Fotorrealismo significa que a cena parece o mais verossímil possível, replicando todas as geometrias intrincadas, interações de luz e propriedades de superfície do mundo físico. Embora o fotorrealismo seja uma meta perfeitamente válida para jogos que se esforçam para obter os gráficos mais realistas possíveis, muitos jogos empregam intencionalmente estilos não fotorrealistas. Conseguir looks como um estilo de desenho animado, estilo anime ou mesmo um estilo retro de 8 bits certamente é possível dentro do motor de jogo. Com algumas pequenas mudanças no processo de criação de conteúdo, combinadas com um bom entendimento de sombreamento, texturização e iluminação, você poderá criar uma arte impressionante de qualquer estilo visual.

![Different visual styles of games.](..\figures\Chapter5\Fig05-02.jpg)

## Designing for Real Time <a id="Designing_for_Real_Time"></a>

For a typical computer animation, the rendering time is effectively unlimited. A movie studio like Pixar has hundreds, if not thousands of computers working together as a rendering farm to make the images. Games don't have this luxury of rendering time. Because games are interactive, there is no way to pre-render frames ahead of time. Games need to pump out many frames every second (and from a single computer!) in order to achieve interactivity with the player. That means that preparing art assets for games is a bit trickier than for non-real-time animation, where performance usually isn't a concern.

> **Art Assets**
>
> Ativo de arte refere-se a qualquer peça de trabalho usada em um jogo. Inclui modelos, texturas, animações, som e até códigos de shader.

Como os jogos são geralmente distribuídos para um grande público com uma ampla variedade de hardware de computador, você precisa se certificar de que os jogos serão executados em velocidades aceitáveis em diferentes configurações de hardware. Dessa forma, você evita alienar pessoas sem computadores de última geração. O Blender tem suporte para alternar entre diferentes modos de sombreamento para ajudar os artistas a criar jogos que funcionam com diferentes gerações de hardware de computador. Isso será discutido em detalhes posteriormente neste capítulo.

Placas de vídeo modernas são surpreendentemente rápidas em enviar imagens de alta qualidade em uma velocidade surpreendente, mas você ainda precisa manter algumas coisas em mente ao fazer ativos de arte, a fim de evitar lentidão.

## Geometry <a id="Geometry"></a>

<img alt="Low polygon model vs. high polygon model" src="../figures/Chapter5/Fig05-03.jpg" width="50%" align="right">

A geometria é a base para qualquer cena 3D. Você pode medir quantitativamente a quantidade de dados geométricos em uma cena usando uma "contagem de polígonos", que se refere ao número de faces (triângulos ou quadrantes, no caso do Blender) em uma cena. Quanto mais dados de geometria houver, mais lento será o jogo. Então, quantos polígonos são demais? Em vez de impor uma limitação absoluta, lembre-se de usar polígonos de maneira sensata, gaste-os onde são necessários e não desperdice polígonos excessivos em partes desnecessárias que não serão visíveis para o jogador. Dito isso, o computador médio de hoje deve ser capaz de renderizar um milhão de polígonos em uma taxa de quadros interativa, então a contagem de polígonos não é tão preocupante quanto costumava ser. Um modelo de alta resolução é mais suave, mais detalhado, mas é mais lento para processar pelo computador.

Os tipos de objetos do Blender suportados no motor de jogo são: câmera, luz, vazio, malha e texto.

Os tipos de objetos do Blender não suportados são: curva, superfície e metaball. Esses objetos ficarão escondidos durante o jogo.

## Materials and Textures <a id="Materials_and_Textures"></a>

<img alt="Oil barrel models without and with textures applied" src="../figures/Chapter5/Fig05-04.jpg" width="50%" align="right">

Uma vez que a modelagem é feita, materiais e texturas, que adicionam fidelidade visual, podem ser aplicados à malha. Usando uma combinação de materiais e texturas, você pode definir as características da superfície, como cor, brilho, saliência e transparência. As texturas também permitem "assar" certos efeitos, como mapas de luz e sombras complexos, no objeto, porque de outra forma esses efeitos demorariam muito para serem computados em tempo real. Devido à importância dos materiais e texturas, uma grande parte deste capítulo se concentrará em materiais e texturas. (Para uma discussão mais aprofundada sobre cozimento de textura, consulte o Capítulo 8.)

O motor de jogo do Blender implementa um subconjunto com alguma sobreposição de todos os recursos encontrados no Blender regular. Nem todas as opções disponíveis para o renderizador interno do Blender estão disponíveis no motor de jogo; muitos recursos gráficos avançados são simplesmente muito lentos para serem implementados em tempo real. Mas como você logo descobrirá, até mesmo alguns dos efeitos complexos como reflexão, sombras suaves e oclusão de ambiente podem ser aproximados no motor de jogo usando truques inteligentes em placas gráficas modernas.

## Lights <a id="Lights"></a>

A iluminação não apenas define o tom geral da cena, mas também ajuda a destacar certos detalhes enquanto oculta outros. Hardware mais antigo ou dispositivos móveis não podem se dar ao luxo de usar iluminação dinâmica por motivos de desempenho, então eles geralmente empregam iluminação estática pré-computada, que é mais rápida de renderizar, mas não tem a flexibilidade que a iluminação dinâmica oferece (como luzes de banheiro oscilantes que projetam sombras em movimento) .

Na verdade, sem iluminação, o mundo virtual que você cria ficaria totalmente escuro.

![The effect of lighting on an object.](..\figures\Chapter5\Fig05-05.png)

O motor de jogo suporta oito luzes em tempo real no modo multitextura e pelo menos oito no modo GLSL (mais sobre os diferentes modos de sombreamento posteriormente). Mas as luzes são caras e mais luzes tornarão o jogo significativamente mais lento. Recursos avançados, como sombra em tempo real, tornarão o jogo ainda mais lento. A luz é um fenômeno muito complexo; efeitos como oclusão de ambiente, luz refletida e feixes de luz volumétricos são todos muito intensivos em computação e simplesmente inviáveis para a maioria dos projetos em tempo real. Cabe ao artista criar maneiras de falsificar esses efeitos, quando necessário.

> Técnicas Avançadas de Sombreamento
>
> Graças aos rápidos avanços na linguagem de sombreamento e unidades de processamento gráfico (GPU), efeitos como oclusão de ambiente, luz refletida e muitos outros que eram considerados "impossíveis" agora são possíveis usando alguns sombreamentos muito complexos. Explicar essas técnicas avançadas está fora do escopo deste livro, mas uma seleção de arquivos de amostra está incluída no disco que acompanha. Para exemplos de shaders avançados, você pode olhar o livro _GPU Gems_ da Nvidia.


## Shading Modes <a id="Shading_Modes"></a>

O motor de jogo oferece dois modos diferentes de sombreamento em tempo real. Pense neles como diferentes canais de renderização - um é mais limitante, o outro é mais avançado. Neste capítulo, você será apresentado ao modo de sombreamento mais rico em recursos: **GLSL**. Então vamos falar um pouco sobre os mais antigos modo de **Multitexture**.

Para alternar entre os modos de sombreamento, vá para o Editor de propriedades de renderização.

![Shading mode options.](..\figures\Chapter5\Fig05-06.png)



> **Game Engine Interface**
>
> Se você está seguindo este capítulo por conta própria sem usar o arquivo de modelo fornecido no livro, lembre-se de definir o mecanismo de renderização para o Game Blender assim que iniciar o Blender. Isso revelará todos os recursos relevantes do mecanismo de jogo na interface do usuário e ocultará elementos não relevantes da interface. ! [Fig05-07] (../Figures/Chapter5/Fig05-07.png)

Aqui está uma tabela que mostra as vantagens e desvantagens dos dois modos de sombreamento. O modo GLSL, apesar de ser o modo de sombreamento mais avançado do Blender, também é o mais fácil de usar, pois podemos realizar o efeito usando o material regular e o painel de textura. A menos que a compatibilidade com versões anteriores de hardware mais antigo seja uma grande preocupação, eu recomendo fortemente o uso do modo de sombreamento GLSL para todos os seus projetos. Mesmo se você não estiver planejando usar todos os recursos avançados, é bom saber que eles estão disponíveis se você precisar deles mais tarde.

Tabela 5.1 Comparação dos modos de sombreamento no mecanismo de jogo
|                        			| Multitexture | GLSL        |
| ---------------------------------------------	| ------------ | ----------- |
| Data de Introdução	 			| 2006         | 2008        |
| Compatibilidade de Hardware 			| OpenGL 1.3+  | OpenGL 2.0+ |
| Precisão de iluminação     			| Por vértice  | Per pixel   |
| Número de Luzes    				| 8            | 8+          |
| Sombra em tempo real	        		| Não          | Sim         |
| Camada de textura máxima     	 		| 4            | 16          |
| Mistura de textura	        		| Sim          | Sim         |
| Shader personalizado   			| Não          | Sim         |
| Nós de material     				| Não          | Sim         |
| Visualização da janela de visualização        | Parcial      | Total       |
| Devo usar?				        | Não...       | Sim!        |

Como a maneira de aplicar materiais e texturas varia um pouco dependendo do modo de sombreamento, é uma boa ideia decidir sobre um modo de sombreamento antes de iniciar o projeto para evitar conversões desnecessárias posteriormente. Um exemplo do que cada modo oferece é mostrado aqui usando este modelo de carro.

![Different shading modes: Multitexture, GLSL.](..\figures\Chapter5\Fig05-08.png)



### GLSL Mode <a id="GLSL_Mode"></a>

O modo de sombreamento GLSL é o mais novo modo de sombreamento em tempo real no Blender, adicionado para aumentar os antigos modos de multitextura. Resumindo, o modo GLSL tenta emular a funcionalidade do mecanismo de renderização interno tanto quanto possível. Ao fazer isso, ele confunde a distinção entre o renderizador interno do Blender e o motor de jogo. No modo GLSL, o artista usa o painel Material familiar e o painel Textura para aplicar sombreamento e textura a um objeto, como alguém normalmente faria ao trabalhar com o renderizador interno. Isso significa que os materiais criados para o mecanismo de jogo no modo GLSL podem ser usados para renderizar quase sem fazer nenhuma modificação.

> **Technical Background**
>
> GLSL, ou OpenGL Shading Language, é uma linguagem de programação semelhante a C que roda na placa de vídeo (ao contrário da maioria das outras linguagens de programação, que funcionam na CPU). GLSL permite que o artista defina sombreadores personalizados para obter efeitos de animação, material, sombreamento e textura mais complexos do que são possíveis com o processamento tradicional de pipeline fixo. O Blender é capaz de gerar códigos GLSL automaticamente, então não se assuste só porque mencionamos "linguagem de programação". O Blender converte suas configurações do painel Material e Textura em GLSL internamente. Na verdade, todo o processo é totalmente transparente para o artista. A única razão pela qual mencionamos isso agora é para que você tenha uma melhor compreensão do que está acontecendo nos bastidores.

Este é o modo de sombreamento mais fácil de usar, já que os mesmos materiais e configurações de texturas que são usados no Blender normal também são usados no motor de jogo.

> **GLSL Requirements**
>
> Sendo o modo de sombreamento mais avançado, GLSL requer uma placa gráfica relativamente moderna que suporte OpenGL 2.0 ou superior. Se você tiver um computador com gráficos Intel integrados, o GLSL pode não funcionar como esperado. Também ajuda a atualizar os drivers de vídeo visitando amd.com, nvidia.com ou intel.com, dependendo do fabricante da placa gráfica.



#### Material and Textures <a id="Material_and_Textures"></a>

Para ajudá-lo a conhecer melhor o sistema de materiais, vamos brincar com um arquivo de amostra.

Abra /files/Chapter5/GLSL1.blend. Você verá uma cena muito simples, com as luzes e uma cabeça de macaco já configuradas para você, conforme mostrado aqui. Pressione P para iniciar o jogo e ver como fica no jogo.

![Basic material demo setup.](../figures/Chapter5/Fig05-09.png)

Observe que o visual na janela de exibição 3D é exatamente igual ao do jogo. Este verdadeiro "o que você vê é o que você obtém" só é possível no modo GLSL. Isso significa que, conforme você configura as configurações de material e textura no Editor de propriedades, as alterações serão refletidas em tempo real na janela de exibição 3D. Na verdade, desde que o sombreamento da janela de exibição esteja definido como Texture, não há necessidade de executar o jogo para visualizar como o objeto realmente será.

As próximas duas seções abordarão cada opção nos painéis Material e Texture, explicarão o que eles fazem e quando usá-los. Acompanhe enquanto trabalhamos na enorme lista de controles deslizantes e opções mostradas neste painel.



#####  The Material Panel <a id="The_Material_Panel"></a>

Em GLSL1.blend, você verá o painel Material no lado direito do Viewport 3D. Na configuração de demonstração, o material preso ao chão é mostrado por padrão. Lembre-se de que esse painel já foi discutido brevemente no Capítulo 2, então vá em frente e brinque com as configurações e veja como elas afetam o modelo na visualização 3D em tempo real.

<img alt="The Material Panel" src="../figures/Chapter5/Fig05-10.png" width="25%" align="right">



Se você já está familiarizado com o sistema de materiais do Blender, estará em casa com esta seção. Como artista, lembre-se de que o mecanismo de jogo oferece suporte a um subconjunto menor de recursos encontrados no painel Material normal. Recursos avançados de sombreamento, como reflexos traçados por raio e refrações e espalhamento de subsuperfície, não estão disponíveis no motor de jogo. Portanto, eles ficam ocultos do painel Material quando o Blender Game é selecionado como o mecanismo de renderização ativo.



###### Material Management <a id="Material_Management"></a>

A seção superior do painel Material permite gerenciar os blocos de dados de materiais. Como cada objeto pode ter vários materiais, a caixa mostra uma lista de todos os materiais anexados ao objeto ativo. Os materiais selecionados são destacados em azul.

Para criar um primeiro material para um objeto:

1. Na visualização 3D, selecione um objeto sem um material (por exemplo, o macaco em GLSL1.blend).
2. No painel Material abaixo da Lista de Slot de Material, clique no ícone [+ Novo] para criar um novo material para o objeto.
3. Como o objeto não tem material, por padrão, o novo material será aplicado a todo o objeto.

###### Multi-Material Objects <a id="Multi-Material_Objects"></a>

Se o objeto tiver um material existente, você pode criar outro material e atribuir os novos materiais a parte da malha da seguinte maneira:

1. Na visualização 3D, selecione o objeto.

2. No Painel de Material abaixo da Lista de Slot de Material, clique no ícone [+ Novo] para criar um novo material de base para o objeto.

3. No Painel de Material, clique no ícone [+] à direita dos slots de material para criar outro slot de material, seguido de clicar no botão [+ Novo] para criar um novo material. Você atribuirá este material à parte selecionada do objeto.

   ![Fig05-11](../figures/Chapter5/Fig05-11.png)

4. Mude a cor do material recém-criado para verde apenas para que você possa diferenciar os materiais.

5. Na vista 3D, entre no modo Editar para o objeto usando Tab. Selecione todos os vértices aos quais deseja atribuir o novo material.

6. Com o novo material destacado, pressione o botão Assign para aplicar o novo material à parte selecionada do objeto.

   ![Fig05-12](../figures/Chapter5/Fig05-12.png)

Abaixo da Lista de Slot de Material está o controle para o material selecionado. Você pode (e deve) renomear um material para ser mais descritivo. Isso o ajudará imensamente em um grande projeto, já que geralmente não é muito óbvio o que "Material.001" é, "Orange" é melhor, "OrangePlastic" é ainda melhor e "MatteYellowishOrangeSoftPlasticWithSmallBumps" é exagero.

Um bloco de dados de material pode ser compartilhado por vários objetos. Clicar no ícone do material em miniatura (rotulado como Browse ID Data) trará uma lista de todos os materiais existentes no arquivo atual do Blender. Para atribuir um objeto a um material existente, basta selecionar um bloco de dados de material dessa lista.

![The Material panel: datablock management.](../figures/Chapter5/Fig05-13.png) 

O conceito de bloco de dados é muito importante no Blender: ele permite que você organize efetivamente todos os ativos em uma hierarquia lógica. Os blocos de dados são discutidos em detalhes no Capítulo 2.



###### Object vs. Data <a id="Object_vs._Data"></a>

Você deve ter notado outro menu suspenso ao lado do botão Novo material. Este seletor de link controla se o material está vinculado ao objeto ou aos dados do objeto (também conhecido como _mesh_). Essa distinção é praticamente desprezível para objetos únicos, mas se você tiver um objeto com malha compartilhada na cena, a diferença se torna importante.

Quando um material está vinculado a uma malha (e não ao objeto), duplicar o objeto usando Alt + D para criar uma cópia do objeto que compartilha a mesma malha do objeto original resultará no material sendo compartilhado entre os dois objetos.

Por outro lado, se o material estiver vinculado a um objeto, duplicar o objeto com Alt + D resultará no material sendo vinculado diretamente ao objeto. Dessa forma, você pode atribuir um material diferente a cada objeto, mesmo que eles compartilhem a mesma malha.

**Material datablock linked to the mesh:**

![Material datablock linked to the mesh.](../figures/Chapter5/Fig05-14.png)



**Material datablock linked to the object:**

![Material datablock linked to the object.](../figures/Chapter5/Fig05-15.png)



###### Preview <a id="Preview"></a>

O painel Visualização mostra como o material selecionado ficaria se renderizado. Por causa dos modelos genéricos e de uma única fonte de luz, a precisão da visualização é limitada se o material depende de uma configuração de iluminação complexa. Normalmente, você pode obter uma visualização mais precisa diretamente da janela de exibição 3D. Apenas lembre-se de ter certeza de que o sombreamento da janela de visualização está definido como Texturizado alternando Alt + Z.



###### Diffuse <a id="Diffuse"></a>

Difuso é o componente macio (fosco) refletido de uma superfície. Em comparação com os destaques especulares abaixo, a luz difusa não depende do ângulo de visão.

Usando o seletor de cores, você pode alterar a cor difusa do material.

O controle deslizante de intensidade controla a quantidade de luz difusa refletida na superfície - em outras palavras, o brilho de uma superfície quando exposta à luz. Use-o em conjunto com o seletor de cores para obter a cor de superfície desejada. Por exemplo, para criar um material branco, você não apenas precisa selecionar uma cor branca na paleta de cores, mas também precisa aumentar a intensidade de difusão para 1,0; caso contrário, você acabará com um cinza médio. Definir a intensidade para 0 cria instantaneamente uma superfície preta, independentemente da cor definida no seletor de cores. A figura abaixo mostra a diferença entre um material de baixo valor difuso e um material de alto valor difuso.

![Left: Low diffuse value. Right: High diffuse value.](../figures/Chapter5/Fig05-16.png)

- Lambert é o algoritmo de sombreamento difuso padrão; é adequado para a maioria das superfícies.
- Oren-Nayer se aproxima melhor das superfícies ásperas, pois fornece uma transição mais gradual da luz para a escuridão do que Lambert. Assim, Oren-Nayer geralmente tem uma aparência "mais suave" do que Lambert.
- O Minnaert é como um sombreador Lambert regular, mas com processamento adicional na borda do objeto onde a superfície normal é paralela à câmera. Ele pode atingir um material de aparência um tanto aveludada sem o uso de um sombreador de rampa.
- Toon shader cria um efeito de faixa muito distinto, resultando em uma aparência de desenho animado que é adequado para um jogo com sombra de células.
- O shader de Fresnel usa o ângulo de luz incidente para obter uma aparência interessante que pode ser melhor descrita como "anisotrópica", perfeita para aqueles objetos de metal escovado que refletem luzes em faixas ou padrões radiais.

De todos os algoritmos de sombreamento difuso, Lambert é o mais simples em termos de complexidade de sombreamento. Portanto, por motivos de desempenho, é melhor ficar com Lambert, a menos que você possa realmente utilizar os benefícios adicionais de outros algoritmos especializados.

Conforme um algoritmo de sombreamento diferente é selecionado, opções adicionais para esse modo específico podem aparecer. Em vez de tentar explicar essas configurações extras para cada algoritmo de sombreamento (o que é fútil sem falar sobre a matemática por trás disso), convidamos você a experimentá-las e ver como elas afetam o resultado. No final, tudo o que importa é a aparência.



###### Specular <a id="Specular"></a>

Especular é o componente duro (brilhante) refletido de uma superfície. Depende do ângulo de visão: conforme a câmera, objeto ou luz se move em relação um ao outro, o realce especular parece se mover ao longo da superfície. Com o seletor de cores, você pode alterar a cor do realce especular. A maioria dos materiais (plástico, madeira, vidro) tem um realce especular branco. O único material comum que pode fisicamente ter um realce especular colorido é o metal colorido, como ouro e cobre. A Figura 5.17 mostra três configurações especulares diferentes.

![From left to right: medium specular intensity and low hardness; high specular intensity and high hardness, specular shader set to Toon.](../figures/Chapter5/Fig05-17.png)

A intensidade controla o quão brilhante é o realce especular, enquanto a dureza controla o tamanho do ponto ativo especular. Um alto valor de dureza é útil para materiais brilhantes, como plástico rígido ou vidro. Um valor de dureza baixo é útil para objetos foscos, como plástico áspero ou plantas. Para superfícies com quase nenhum componente especular visível, como paredes de tijolos secos, sujeira ou carpete, você pode até desativar o Specular inteiramente configurando a intensidade para 0. Isso pode melhorar ligeiramente o desempenho do jogo.

Assim como o difuso, existem diferentes algoritmos para obter realces especulares de aparência diferente: Wardlso pode ser usado para criar realces especulares muito pequenos e Toon é usado para criar aquela queda acentuada frequentemente desejada em um desenho animado. CookTorr é o algoritmo padrão, mas Phong é outra escolha popular. Visualmente, cookTorr e Phong são muito semelhantes.



###### Ramp <a id="Ramp"></a>

Ramp permite adicionar um gradiente de cor arbitrário ao objeto. Seu poder reside no fato de que você pode mapear uma paleta de cores no objeto de muitas maneiras diferentes. Alguns usos comuns para o sombreador de rampa incluem adicionar uma "penugem de pêssego" ao material de pele e adicionar luz de borda a objetos para um efeito dramático.

<img alt="The Ramp shader interface" src="../figures/Chapter5/Fig05-18.png" width="33%" align="left">



A parte superior da rampa é usada para configurar a faixa de cor. Para definir um gradiente, você pode adicionar ou excluir interrupções de cor; cada interrupção de cor tem sua própria posição, cor e valor alfa. Por padrão, quando você ativa a rampa, duas paradas de cor são criadas para você. Para selecionar uma determinada cor de parada, clique com o botão esquerdo nela. As paradas de cores ativas são desenhadas com uma linha pontilhada. Depois que uma interrupção de cor é selecionada, você pode arrastar para alterar sua posição e alterar sua cor e valores alfa usando o seletor de cores abaixo dela.

A parte inferior do painel Ramp Shader controla como a banda de cores é mapeada no objeto. As opções de entrada disponíveis incluem:

- **Normal:** A banda colorida é mapeada para a normal da superfície do objeto no espaço da câmera. Assim, quaisquer superfícies perpendiculares à câmera (de frente para a câmera) obterão sua cor do lado direito da faixa de cor, enquanto as superfícies paralelas à câmera (voltadas para os lados) serão atribuídas ao lado esquerdo da faixa de cor.

- **Energy:** A faixa de cores é mapeada para a energia incidente de todas as lâmpadas. As áreas de alta energia são mapeadas para a faixa de cor à direita e vice-versa.

- **Shader:** A banda de cores é mapeada para o resultado da intensidade do sombreador calculada. Esta opção é semelhante à energia, exceto que também leva em consideração o modelo de sombreamento.

- **Result:** A banda de cores é mapeada para a cor final do material resultante, incluindo todas as informações de sombreamento e textura. Pixels brilhantes são mapeados para a direita da faixa colorida e pixels escuros são mapeados para a faixa colorida mais à esquerda.

  ​

A opção Mistura controla como as cores da banda de cores são misturadas com a cor existente, não muito diferente da opção de mistura de camadas em um software de manipulação de imagens 2D como o Photoshop. Esses métodos de mistura freqüentemente aparecem no Blender, então você deve estar familiarizado com eles.

- **Mix:** Usa uma combinação de ambas as entradas. Um fator de 0,5 significa que cada entrada contribui exatamente com a metade para a cor final. Um fator de 1 significa que uma das entradas domina completamente a outra.
- **Add:** As duas cores de entrada são somadas numericamente, geralmente resultando em uma imagem mais brilhante.
- **Multiply:** As duas cores de entrada são multiplicadas numericamente juntas, geralmente resultando em uma imagem mais escura.
- **Subtract:** Uma entrada é subtraída da outra, às vezes resultando em uma imagem mais escura e às vezes resultando em uma imagem "negativa" em que as cores são invertidas.

Tanto os canais difusos quanto os especulares podem ter sua própria rampa. Enquanto o sombreador de rampa difuso pode ser visível em todo o objeto, a rampa para especular só é visível na região onde os realces especulares são visíveis. Fora isso, o painel Ramp Shader para especular é exatamente o mesmo que o painel Ramp Shader para Diffuse Shader.



###### Shading <a id="Shading"></a>

**Emit**: Controla a quantidade de luz que uma superfície parece emitir. Um valor diferente de zero significa que uma superfície é visível mesmo quando está completamente apagada. Como emit é uma propriedade do material e não uma fonte de luz real, você não pode contar com o uso de materiais emit para iluminar outros objetos na cena. Emit é frequentemente usado para simular superfícies que emitem luz por conta própria.

**Ambient**: Controla quanta influência a cor ambiente tem sobre o material. A cor ambiente é uma cor global adicionada sobre todos os materiais, incluindo objetos sem um material explícito. Por padrão, a cor ambiente é preta, desativando-se efetivamente. A cor do ambiente pode ser alterada no painel Mundial. Se você deseja aumentar uniformemente o brilho da cena sem adicionar lâmpada adicional, a cor ambiente é uma maneira rápida de conseguir isso. Você também pode criar uma tonalidade de cor no mundo usando uma cor ambiente não branca, que é uma ótima maneira de definir o clima de sua cena.



> **Ambient Drawbacks**
>
> O ambiente tem suas desvantagens. Por adicionar luz a todas as superfícies de maneira uniforme, o ambiente excessivo reduzirá o contraste da cena, fazendo com que tudo pareça plano e desbotado.



**Shadeless:** Quando ativado, desativa todos os cálculos de luz para este material. Esta opção ignora todos os cálculos complexos de sombreamento; assim, pode melhorar o desempenho sem nenhum cálculo de iluminação. Esta opção é útil para situações em que você não deseja que o objeto reaja à luz.

**Cubic Interpolation:** Quando ativado, oferece uma transição mais suave da luz para a sombra, ao custo de uma ligeira diminuição do desempenho. Para certas formas suaves, como esferas, esta opção ajuda a aparência da forma mais natural.

###### Game Settings <a id="Game_Settings"></a>

**Backface Culling:** Quando desativado, torna os dois lados de um rosto visíveis ao executar o jogo. Por padrão, apenas a parte frontal da face é renderizada por motivos de desempenho, enquanto a parte traseira de uma face é invisível. Isso não é crítico para a maioria dos novos computadores, se você quiser lidar com alguns rostos. No entanto, é melhor adotar uma abordagem segura e desativar a seleção da face posterior apenas quando você precisar de faces de dois lados.

 **Invisible:** Quando ativado, torna a superfície completamente invisível. Esta opção é freqüentemente usada para criar objetos ocultos de colisão física. Os objetos também podem ficar invisíveis no painel Física (consulte o Capítulo 6).

**Text:** Quando habilitado, diz ao Blender que este objeto é usado para exibir texto de bitmap. O uso de texto de bitmap no mecanismo de jogo é abordado posteriormente neste capítulo. Como o texto de bitmap é bastante difícil de configurar, usar o objeto de texto do Blender é uma alternativa fácil.

 **Alpha Blend:** Seleciona a maneira como as faces são desenhadas. As opções são mostradas na Figura 5.19 e em detalhes na Figura 5.19b.

- **Opaque** : Trata o material como um sólido regular. Este é o modo de desenho mais rápido.

- **Add:** Adiciona numericamente sua própria cor de superfície com o que está por trás, tornando a superfície combinada mais brilhante. Esta opção pode ser usada para simular luzes de halo, partículas e outros efeitos especiais "brilhantes".

- **Alpha Clip:** Ativa a transparência binária. Usado com frequência para texturas em que há uma borda muito distinta, como folhas de árvores e uma cerca de arame. Esta é a maneira mais rápida de renderizar texturas com alfa, já que não há mistura alfa: um pixel é totalmente opaco ou totalmente transparente.

- **Alpha Blend:** Ativa o alfa blend entre sua própria cor e o plano de fundo. É usado para materiais verdadeiramente transparentes como o vidro. Uma desvantagem do Alpha Blend é que várias camadas de superfícies do Alpha Blend geralmente não são exibidas na ordem Z correta. Este é um problema comum com a renderização alfa acelerada por hardware. A solução é usar o Alpha Sort, conforme explicado a seguir.

- **Alpha Sort:** Semelhante ao Alpha Blend, mas resolve o problema de classificação Z inerente ao Alpha Blend. Se você vir um objeto com mapeamento alfa que está aparecendo por meio de outros objetos transparentes, ou se várias camadas de alfa forem exibidas na ordem errada, você deve usar Alpha Sort em vez de Alpha Blend. Lembre-se de que o Alpha Sort é muito mais lento do que o Alpha Blend normal.

  ![Blending Modes: (from left to right) Add, Alpha Clip, Alpha Blend, and Alpha Sort.](../figures/Chapter5/Fig05-19.jpg)




![Blending Modes magnified: (from left to right) Add, Alpha Clip, Alpha Blend, and Alpha Sort.](../figures/Chapter5/Fig05-19b.jpg)



- **Face Orientations:** Gira as faces para longe de sua orientação original. Observe que as orientações das faces não são visíveis na viewport; portanto, para visualizar o efeito dessas configurações, você precisa entrar no modo de jogo.

- ![Face orientation illustrated. The top-row images show the actual geometry. The bottom row shows the face set to normal(A), billboard(B), halo(C), and shadow(D).](../figures/Chapter5/Fig05-20.jpg)

 - Normal: a opção padrão. Nenhuma orientação extra é aplicada e as faces são renderizadas normalmente. (Ver um)
 
 - Billboard: Força o eixo X do objeto a ficar de frente para a câmera, enquanto mantém o eixo Z do objeto na posição vertical. Para visualizar isso, imagine alguém segurando um outdoor e tentando chamar sua atenção sempre girando o outdoor para ficar de frente para você. Billboard é freqüentemente usado para renderizar vegetação e árvores simplistas na visualização arquitetônica, de forma que uma árvore possa ser representada por um único plano que sempre gira em torno de seu centro. (Veja B)
 
 - Halo: Força o eixo X do objeto a sempre ficar de frente para a câmera. Isso é semelhante à opção do quadro de avisos, mas nenhum eixo está bloqueado. Halo, como o nome indica, pode ser usado para renderizar partículas e outros sprites não 3D (consulte C).
 
 - Sombra: os objetos irão se reposicionar e se reorientar para que o centro do objeto corresponda ao objeto mais próximo diretamente abaixo dele no eixo Z. Isso é usado para fazer um objeto "cair" e grudar no chão, como ao fingir uma sombra projetada (ver D).
 
Lembre-se de que a orientação facial é aplicada após cálculos lógicos e físicos. Isso significa que a malha de colisão ainda estará em sua posição original, então o que você vê na tela pode ser diferente da malha de colisão física interna.


###### Physics <a id="Physics"></a>

A configuração física controla algumas das propriedades físicas da superfície. Eles não afetam a propriedade visual do objeto, mas alteram a maneira como o objeto interage sob o mecanismo de física. Vá para o Capítulo 6 se quiser aprender sobre essas configurações.

###### Additional Options <a id="Additional_Options"></a>

- **Exclude Mist:** Exclui o objeto do cálculo de névoa quando ativado. Mist é um cenário mundial que pode ser acessado no painel Mundial.
   - Texturas Faciais: Força o Blender a substituir a cor difusa do material pela textura UV. Esta é uma maneira fácil de aplicar uma textura simples em um material sem criar um bloco de dados de textura para o material.
   - Texturas Faciais Alpha: Esta opção só é visível quando as Texturas Faciais estão ativadas. Também substituirá a transparência do material usando os canais alfa da textura, além de substituir a cor difusa do material.
   - Vertex Color Paint: Multiplica a cor do vértice da malha sobre o material regular.
   - Receber sombras: torna as sombras em tempo real lançadas por lâmpadas visíveis na superfície. Apenas lâmpadas de spot e sol projetam sombras.
- **Object Color:** Modula a cor do material com a cor do objeto. Útil para fazer com que objetos diferentes compartilhando o mesmo material tenham cores diferentes. A cor do objeto pode ser definida no Editor de propriedades do objeto.

Até agora, cobrimos todas as funcionalidades do painel Material. A maioria das configurações é muito intuitiva e seus efeitos podem ser vistos diretamente na janela de visualização, com exceção das configurações de orientação de rosto, que exigem que o mecanismo de jogo esteja funcionando para ver seus efeitos.



##### The Texture Panel <a id="The_Texture_Panel"></a>

A textura é a principal forma de adicionar detalhes a uma superfície sem adicionar polígonos extras. Isso é feito mapeando uma imagem 2D na superfície do objeto 3D. A Figura 5.21 ilustra o conceito de mapeamento de textura.

<img alt="How texture mapping works." src="../figures/Chapter5/Fig05-21.jpg" width="50%" align="left">



###### Texture Data Blocks <a id="Texture_Data_Blocks"></a>

Os blocos de dados de textura quase sempre estão vinculados a um material (veja a nota abaixo para exceção). Cada material pode ter várias texturas e, por meio de camadas e combinação de texturas, podem ser obtidos efeitos complexos. A área superior do Painel de textura mostra todas as texturas anexadas ao material ativo.

> Texturas não materiais
>
> A única exceção é uma textura "mundo", que está ligada diretamente às configurações do mundo sem um material, e a textura Pincel, que é usada para pintar ou esculpir. No entanto, ambos são suportados apenas no renderizador interno do Blender e não são implementados no motor de jogo. Portanto, para os nossos objetivos de jogo, todos os blocos de dados de textura devem de fato estar vinculados a um material.
>

Note que no Blender, os slots de textura são ordenados de forma que as texturas mais abaixo nos slots de textura substituem as texturas no topo da lista. Isso é o oposto de como a maioria dos editores de imagem trata as camadas.

<img alt="The Texture panel with two textures slots in use." src="../figures/Chapter5/Fig05-22.png" width="40%" align="left">



1. Para criar uma nova textura, o objeto já deve ter um material. Selecione o objeto e adicione um novo material, se necessário.
2. Em seguida, no painel de textura, clique no ícone [+ Novo] para criar uma nova textura no primeiro slot de textura (consulte a Figura 5.23).
3. Para trabalhar com o motor de jogo, defina o tipo da textura para a imagem. (A textura da imagem é o que usaremos na maioria das vezes.) A única outra opção de tipo de textura disponível é o mapa de ambiente. Texturas procedurais, como nuvens e ruído, não são suportadas no motor de jogo.

![Using an image texture](../figures/Chapter5/Fig05-23.png)



###### Image <a id="Image"></a>

Para carregar uma imagem como textura, você pode:

- Carregue um bloco de dados de imagem existente (um que já esteja sendo usado neste arquivo do Blender).
- Gere uma nova imagem diretamente de dentro do Blender.
- Navegue e carregue um arquivo de imagem de seu computador.

![Create a new image by selecting New or browse for an existing image by selecting Open.](../figures/Chapter5/Fig05-24.png)

Depois que uma imagem é carregada, você tem algumas opções para alterar a maneira como o espaço de cores e o canal alfa são interpretados.

- **Input Color Space:** Controla a transformação do espaço de cores que ocorre quando a imagem é usada. Normalmente, as texturas são criadas no espaço de cores sRGB, portanto, a configuração padrão é suficiente. Para trabalhos sensíveis às cores, você pode alterar o Espaço de cores de entrada para corresponder ao arquivo de imagem.
- **View as Render:** Aplique uma transformação de cor adicional para levar em consideração a transformação de cor ao renderizar.
-  **Use Alpha:** Usa o canal alfa de uma imagem, quando disponível. Se ativado, você também pode escolher entre Alfa direto e Alfa pré-multiplicado. A diferença está além do escopo deste capítulo, mas se a textura alfa tiver uma franja escura ou brilhante ao redor da borda, às vezes alternar entre alfa direto e alfa pré-multiplicado pode resolvê-lo.


###### Image Sampling Panel <a id="Image_Sampling_Panel"></a>

O painel de Amostragem de Imagem contém algumas das opções que mudam como a imagem é interpretada dentro do Blender:

- **Calculate (Alpha):** Ignora o canal alfa real do arquivo de imagem e, em vez disso, calcula o canal alfa a partir da intensidade da imagem. Isso trata os pixels pretos como transparentes e os pixels brancos como opacos.

- **Normal Map:** Diz ao Blender para tratar a imagem como um mapa normal, de forma que o valor RGB seja interpretado como normal da superfície, que pode ser mapeado para o canal normal do material para criar saliências na superfície.

###### Mapping Panel <a id="Mapping_Panel"></a>

O mapeamento controla como a textura 2D é mapeada no objeto 3D. As opções disponíveis incluem global, objeto, gerado, UV, reflexão e normal. A opção padrão, gerada, pode funcionar em alguns casos muito simples. Mas na maioria das vezes, você precisará usar o Editor de UV / Imagem para controlar exatamente como a imagem é projetada no objeto. O uso do UV / Image Editor é abordado no Capítulo 2. Quando o mapeamento UV é selecionado, você pode especificar qual canal UV usar, se houver mais de um layout UV para a malha.

- Offset: Traduzir as coordenadas da textura.

- Tamanho: altera a escala das coordenadas da textura.

  ​

###### Influence Panel <a id="Influence_Panel"></a>

Este painel controla como o valor da textura é realmente aplicado à superfície. Por padrão, a cor é selecionada com a influência definida como 1. Isso significa que a textura substitui completamente a cor difusa do material. Uma configuração de 0 significa que não há influência, desativando efetivamente o canal de textura. Qualquer número intermediário mesclará a textura atual com a camada anterior.

_Normal_ é outra configuração de influência comumente usada. Usando um mapa normal, você pode criar irregularidades de superfície falsas, mas convincentes, sem usar grandes quantidades de geometria. Para aplicar um mapa normal a um material existente:

1. No painel Texture, crie um novo slot de textura pressionando o ícone [+].

2. Defina o tipo de textura para imagem e carregue uma imagem de mapa normal do disco.

3. Ative a opção de mapa normal no painel Amostra de imagem.

4. Desative a influência da textura na cor do material, desmarcando a cor no painel Influência.

5. Habilite a influência da textura no normal do material marcando normal no painel Influência. Mova o controle deslizante para ajustar a intensidade do efeito.

   ![A low resolution model and a normal mapped model.](../figures/Chapter5/Fig05-25.jpg)



> Normals maps e height maps
>
> Um normal map é armazenado como um arquivo de imagem regular, mas em vez de alterar a cor da superfície como uma textura de cor regular, os mapas normais são usados para alterar a superfície normal por pixel. Ao alterar a normal da superfície, você pode alterar a irregularidade aparente de uma superfície.
>
> Internamente, um mapa normal usa os três canais de cores (RGB) para armazenar as direções normais (XYZ) de uma superfície. Como a maioria dos normais de superfície está apontando para cima, eles têm um valor normal de (X = 0,5, Y = 0,5, Z = 1,0), que é o que dá aos mapas normais aquela cor roxa distinta (quando no espaço tangente).
>
> Por falar em espaço tangente, os mapas normais podem ser armazenados em vários espaços diferentes, como tangente, objeto, mundo e espaço da câmera. Eles afetam como os mapas normais são interpretados e usados em cálculos de iluminação. Basta dizer que o espaço tangente é a opção mais comumente usada.
>



As outras opções na seção de influência funcionam da maneira exata como cor e normal. Cada um deles influencia um aspecto diferente do material. Por exemplo, se você deseja que uma textura influencie o valor alfa de um material, ative alfa e defina a influência como 1. Em seguida, no painel Material, certifique-se de que alfa esteja definido como 0.

- Mistura: O seletor de mistura é outra configuração chave que controla como as texturas são misturadas umas com as outras. A opção de mistura controla como a textura é misturada com a cor do material existente.
- Negativo: Inverte a cor da textura.
- RGB em intensidade: Como a dica de ferramenta sugere, converte uma imagem RGB em uma imagem em tons de cinza.


#### Combined Exercise <a id="Combined_Exercise"></a>

Se todas as caixas de seleção e controles deslizantes parecerem assustadores, não se preocupe! Agora vamos colocar em prática o que acabamos de ler sobre materiais e texturas. Logo ficará claro como tudo se encaixa.

1. Abra\Book\Chapter5\GLSL2.2blend

2. Você será saudado com um modelo parcial de carro que preparamos, conforme mostrado na Figura 5.26. Com sorte, você concordará que o modelo é de qualidade decente e que tudo o que falta é um bom material para fazê-lo, er, brilhar.

![A car model with the default materials](../figures/Chapter5/Fig05-26.jpg)

Ao trabalhar com materiais, é importante garantir que haja iluminação suficiente para ver o modelo, pois as luzes podem afetar significativamente a forma como os materiais são percebidos. Na verdade, sem iluminação, tudo ficará escuro como breu!

Neste exemplo de carro, como estamos tentando duplicar uma configuração de estúdio fotográfico, configuramos uma única lâmpada hemi na cena, apontando diretamente para baixo sobre o corpo do carro. Esta configuração básica de iluminação oferece uma iluminação muito uniforme em toda a superfície do carro, sem sombras fortes.

Queremos dar a esta máquina esportiva um acabamento metálico brilhante para que pareça que acabou de sair de um comercial de carro. Para conseguir esse efeito, precisaremos de duas camadas de textura: uma camada responsável por criar aquele brilho encontrado na pintura metálica de automóveis, e outra camada que contém uma textura reflexiva para transmitir a ideia de um acabamento brilhante. As duas texturas mostradas na Figura 5.27 são fornecidas online.

![The two textures (magnified) that will be used for the car body material](../figures/Chapter5/Fig05-27.jpg)

3. Selecione o corpo do carro (objeto "Shell") na janela de exibição 3D. Observe que há um material padrão anexado a ele. Mas antes de perdermos muito tempo ajustando o material, vamos adicionar as texturas primeiro.

4. Vá para o Editor de propriedades da textura. Clique em Novo para adicionar uma nova textura. Observe que o primeiro slot de textura agora está ocupado. Renomeie o bloco de dados de "Textura" para algo mais descritivo como "MetallicSpeck".

5. Como as texturas procedurais não são suportadas no motor de jogo, criamos nossa própria imagem de ruído em um software de manipulação de imagem externo. Você pode encontrar um já feito para você online, chamado Noise.png

6. Mude o tipo de textura para imagem. Em seguida, clique em Abrir para revelar o navegador de arquivos. Navegue até \ Book \ Chapter5 \ Textures e selecione Noise.png. Abra. Agora o carro deve estar coberto com a textura que você acabou de carregar.

O primeiro problema que você notará é que a textura é esticada em uma certa parte vertical da casca. Isso ocorre porque um layout de textura UV adequado não foi configurado, então o Blender está tentando o seu melhor usando um mapeamento de textura padrão. Portanto, vamos primeiro ter certeza de que a textura está mapeada uniformemente no objeto.

7. Com o objeto de carroceria ainda selecionado, entre no modo de edição com a tecla tab; selecione todos os vértices com alguns toques na tecla A até que todas as faces sejam destacadas.

8. Com o mouse ainda sobre a janela de exibição 3D, pressione a tecla U para abrir o menu de mapeamento UV. Selecione Smart UV Project e deixe as opções como padrão. Isso projetará de forma inteligente todo o modelo em um mapa UV com distorção mínima. Esta operação leva alguns segundos para ser concluída.

9. Opcionalmente, defina um dos tipos de janela para Editor de Imagens UV para ver o resultado do projeto inteligente.

10. Não se preocupe se você ainda não puder ver o novo mapa UV no modelo 3D. No painel Texture, altere as coordenadas de mapeamento de geradas para UV e selecione UVMap no menu suspenso, conforme mostrado na Figura 5.28. Isto dirá ao Blender para usar o novo mapa UV que você acabou de criar.

![Setting the texture mapping to UV](../figures/Chapter5/Fig05-28.png)

Agora, a janela de visualização 3D deve ser semelhante à Figura 5.29

![Noise texture with adjusted UV layout](../figures/Chapter5/Fig05-29.jpg)

11. É evidente que o ruído é muito grande para ser realista. Para reduzir, altere o atributo Tamanho em Mapeamento de 1,0 para 10,0 para todos os eixos X, Y e Z.

  Para obter o brilho metálico, você não quer que a textura afete o canal de cor do material.

11. Role para baixo até a parte inferior do painel Textura e localize o painel Influência. Desative a cor. Agora, ligue Intensidade e Cor em Especular. Isso fará com que a textura afete apenas o canal especular do material. Dessa forma, o speckle só será visível quando houver luz brilhando sobre ele, que é exatamente o que você deseja. A Figura 5.30 mostra todas as configurações relevantes no painel Textura. As configurações não mostradas não são alteradas.

![Texture options for the noise image texture](../figures/Chapter5/Fig05-30.png)

12. Para adicionar uma segunda camada de textura, volte ao topo do painel Textura e selecione o slot de textura vazio na parte superior da lista. Deve ser um com um ícone de padrão quadriculado vermelho e branco.

13. Clique em Novo para criar outro bloco de dados de textura. Esta será sua camada de reflexão. Então, chame-o de "ReflectionMap".

14. Novamente, defina o tipo de textura para imagem. Clique em Abrir, navegue até \ Book \ Chapter5 \ Textures e carregue uffizi \ _rectangular.jpg. Esta imagem será usada como seu mapa de ambiente.

15. Em Mapeamento, defina as Coordenadas como Reflexão. Isso envolverá automaticamente a textura no objeto de forma que se pareça com um reflexo real.

16. No entanto, observe que o brilho que você criou no slot de textura anterior desapareceu. Isso ocorre porque a nova textura ReflectionMap está cobrindo a textura anterior. Para tornar a reflexão menos intensa, defina o valor de Influência da cor de 1,0 a 0,75.

17. Mude o modo de mesclagem de Mix para Multiply. Isso permitirá que o mapa de reflexão tenha uma aparência melhor na cor de base.

 Neste ponto, você deve ter algo semelhante à Figura 5.31.

![The completed car material](../figures/Chapter5/Fig05-31.jpg)

18. Agora você pode voltar ao painel Material e alterar a cor base do carro alterando a cor difusa como desejar.

>**Material Caching**
>
> Há uma nova configuração no Blender 2.66 no Editor de Propriedades de Renderização chamada _Material Caching._ Com isso ativado, o carregamento do jogo será mais rápido porque os materiais GLSL são armazenados em cache. Esta configuração não funciona bem nos modos Multitextura e Singletexture.

#### Nodes <a id="Nodes"></a>

Node é uma nova forma de trabalhar com materiais e texturas no Blender. Em vez de usar uma interface de usuário em estilo de painel para definir um material, os nós permitem que você crie materiais usando componentes básicos. Isso pode parecer um retrocesso porque provavelmente levará muito mais tempo para criar um material simples no Editor de Nó do que usar os painéis Material e Textura para obter o mesmo efeito. Mas o node oferece ao artista a liberdade de realizar muito mais do que é possível usando os painéis fixos de Material e Textura.

Trabalhar com materiais e texturas do Node é mais um processo, portanto, esta seção será apresentada como um tutorial contínuo. Depois de dominar este exemplo simples, você será capaz de adaptar o fluxo de trabalho para criar efeitos muito mais complexos.

1. Abra /Book/Chapter5/GLSL3.blend e familiarize-se com a configuração da cena; observe que há um objeto de esfera sem qualquer material anexado. A metade inferior da tela foi alterada para o Node Editor.

2. Crie um novo material clicando no botão Novo no painel Material. Renomeie o material para NodeMat para que possamos consultá-lo mais tarde.

3. Clique no botão Use Shader Nodes para habilitar os nós. O Node Editor agora deve ser semelhante à Figura 5.32. Observe que o objeto na viewport 3D ficou preto; isso ocorre porque o material do nó acabou de ser ativado, mas como você não configurou realmente um material do nó válido, a cor padrão é preto.

![The Node Editor](../figures/Chapter5/Fig05-32.png)

4. Como não queremos criar o material do zero, podemos usar um material existente como base para o material do nó. Para fazer isso, no nó Material, clique no ícone Browse Material e selecione NodeMat. Agora, o material de entrada para o nó é o material definido no painel Material no lado direito da tela. Altere qualquer uma das propriedades no painel Material e você poderá ver que a alteração se reflete no sistema de material do nó. Tente definir a cor do material para vermelho.

5. Insira um novo nó Hue-Saturation-Value entre o nó de entrada e o nó de saída e conecte-os desenhando uma linha de um ponto amarelo ao outro. A configuração resultante deve ser a mesma da Figura 5.33.

![The Node Editor-reusing a material](../figures/Chapter5/Fig05-33.jpg)

Parabéns! Você está usando materiais de nó! Embora o exemplo que trabalhamos seja muito básico, o poder do Editor de Nó é a capacidade de criar combinações quase infinitas de aparências usando apenas alguns nós de blocos de construção básicos.

Alguns usos típicos para materiais baseados em nós incluem:

- **Mixing multiple materials:** Com o Node Editor, você pode carregar vários materiais como entrada e combiná-los para criar um meta-material.

- **More control:** Quer que a posição do objeto afete o brilho da textura? Deseja que a intensidade da iluminação afete a transparência do objeto? Com nós, você pode configurar quase qualquer efeito que imaginar.

- **Experimentation:** Usar o sistema de nó como uma caixa de areia para experimentar diferentes efeitos é muito mais rápido do que escrever código de sombreador para obter o mesmo efeito. Em muitos casos, você pode usar o sistema de nós como uma plataforma de prototipagem para construir shaders.

### Multitexture <a id="Multitexture"></a>

A multitextura é mais antiga que o modo de sombreamento GLSL, mas ainda muito mais capaz do que o sistema de material de textura simples.

Conforme descrito na Tabela 5.1, a multitextura usa luz por vértice em vez da luz por pixel do GLSL. Isso significa que a multitextura é geralmente mais rápida ao custo de um sombreamento menos preciso.

No modo Multitextura, os artistas ainda usam os painéis Material e Textura para aplicar sombras e texturas. Comparado ao modo GLSL, as seguintes opções de material não têm efeito no modo Multitextura:

- **Diffuse Shader Model:** O padrão sempre será usado.

- **Specular Shader Model:** O padrão sempre será usado.

- **Cubic Interpolation:** Sempre desativado porque o cálculo da iluminação é por vértice.

- **Ramp Shaders:** Sempre desativado.

- **Shadow Settings:** Sempre desativado. Nenhum objeto projeta sombras no modo Multitextura.


Comparado ao modo GLSL, as seguintes opções de textura não têm efeito no modo Multitextura:

- **Blending Mode:** Diferente de Mix, Add, Subtract, Multiply e Screen.

- **Influence Setting:** Diferente de cor e alfa.

- **Mapping Coordinates:** Diferente de Global, Gerado, Reflexo e UV.

Para adicionar uma textura para o modo de sombreamento Multitexture, você precisa usar o Editor de UV/Imagem. O painel Material pode ser usado para alterar algumas das propriedades da superfície do modelo, como intensidade difusa, intensidade especular e dureza especular.

## Lights <a id="Lights"></a>

As luzes foram abordadas brevemente no Capítulo 2. Iremos revisá-las aqui com mais detalhes.

No modo GLSL, os tipos de lâmpadas suportados são Point, Sun, Spot e Hemi. A lâmpada de área não é compatível e será ignorada pelo mecanismo de jogo. As lâmpadas Spot e Sun são capazes de projetar sombras dinâmicas se o botão Shadow estiver habilitado. A Tabela 5.2 resume as características das lâmpadas.

_Tabela 5.2 Tipos de luzes_

| Tipo  | Suportada      | Direcional	| Sombra      |
|:-----:|:--------------:|:------------:|:-----------:|
| Point | Singletexture+ | Não          | Não         |
| Sun   | Singletexture+ | Sim          | Paralela    |
| Spot  | Singletexture+ | Sim          | Perspectiva |
| Hemi  | GLSL           | Sim          | Não         |
| Area  | Não            | Sim          | Não         |

Nos modos Multitexture e Singletexture, Point, Sun e Spot são suportados, todos os outros tipos de lâmpadas não suportados serão tratados como lâmpadas pontuais. Não há suporte para sombra nesses dois modos.

## World Settings <a id="World_Settings"></a>

No World Property Editor, você pode alterar coisas que afetam o mundo inteiro, como a cor de fundo e as configurações de névoa:

- **Horizon Color:** Define a cor do céu. Na visualização texturizada, essa cor preenche o plano de fundo.

- **Ambient Color:** Define a cor da luz ambiente. A luz ambiente é uma luz de preenchimento que ilumina um objeto uniformemente de todos os ângulos. Isso torna as sombras menos escuras, ao custo de fazer tudo parecer "desbotado". Por padrão, a cor ambiente é definida como preto, o que é equivalente à cor ambiente sendo desativada.

- **Mist:** Ative a névoa para adicionar uma névoa atmosférica a toda a cena. Objetos mais distantes irão desbotar na cor do céu (conforme definido pela cor do horizonte).

- **Mist Start:** Conforme ilustrado na Figura 5.34, a distância inicial na qual a névoa é aplicada.

- **Mist Depth:** Conforme ilustrado na Figura 5.34, a distância na qual um objeto é totalmente obscurecido pela cor da névoa.

![Mist distance illustrated](../figures/Chapter5/Fig05-34.jpg)

>**Smog Can Be Good**
>
> O Névoa pode ajudá-lo a ocultar os limites do seu mundo de faz-de-conta, mesclando suavemente o objeto distante no horizonte. Além disso, a névoa pode aumentar a atmosfera da cena, dando uma melhor sensação de profundidade à cena.
> Um bom exemplo de névoa em jogos são os jogos extremamente nebulosos de _Silent Hill_. Sua equipe de desenvolvimento foi capaz de colocar mais detalhes nos modelos, combinando um corte de câmera mais agressivo com altos valores de névoa.

## Texture Painting <a id="Texture_Painting"></a>

Normalmente, a edição de uma textura de imagem deve ser feita com um software externo, como GIMP ou Photoshop. Usando a pintura de textura, você pode editar a textura diretamente no modelo de dentro do Blender (veja a Figura 5.35). Isso não apenas dá a você a capacidade de ver as alterações interativamente no modelo, mas as pinceladas feitas no modelo também serão automaticamente projetadas de volta na textura da imagem. Isso torna a pintura de textura ideal como uma ferramenta de esboço grosseiro para marcar alguns pontos-chave no modelo para referência ou dar os toques finais na textura. (É muito mais fácil pintar no modelo diretamente do que pintar uma textura 2D.)

![Entering Texture Painting mode](../figures/Chapter5/Fig05-35.png)

Para ver como a pintura de textura funciona:

1. Inicie um novo arquivo e defina a visualização 3D para o modo Textura (Alt + Z).

2. Para pintar diretamente em um objeto, você precisará configurar uma imagem de textura UV primeiro. Portanto, na visualização 3D, certifique-se de que o objeto que deseja pintar (o cubo inicial, neste caso) esteja selecionado e entre no modo de edição pressionando Tab.

3. Certifique-se de que todos os vértices estão selecionados (alterne A até que todos estejam destacados).

4. Na janela de exibição 3D, pressione U para chamar o menu UV. Selecione Smart UV Project com os parâmetros padrão.

5. No Editor de UV / Imagem, crie uma nova imagem clicando no botão Novo. No menu pop-up, selecione UV Grid ou Color Grid como o tipo gerado e clique em OK.

6. Observe que o modelo agora tem a textura de imagem recém-criada mapeada nele.

7. Mude do modo de edição para o modo de pintura de textura.

8. Comece a desenhar no modelo!

9. Você pode alterar as opções das ferramentas usando a estante de ferramentas à esquerda da janela de exibição 3D.

10. No momento da escrita, as imagens atualizadas pela pintura de textura não foram salvas automaticamente. Assim que terminar, certifique-se de voltar ao Editor de UV / Imagem e salve a textura clicando em Imagem> Salvar.

11. Opcionalmente, se você estiver trabalhando com o modo GLSL, você precisará criar uma nova textura no material do objeto e atribuir a imagem recém-criada a ele. Neste caso, você também precisa definir UV como Coordenadas no painel Mapeamento.

## Custom GLSL Shaders <a id="Custom_GLSL_Shaders"></a>

Outra maneira de aplicar material a um objeto é substituir o sistema de material do mecanismo de jogo completamente aplicando shaders GLSL personalizados. Isso lhe dará o controle final sobre a aparência exata do objeto, e você pode obter certos efeitos que não são possíveis com os painéis de Material e Textura integrados.

>**More GLSL?**
>
>Os shaders GLSL personalizados não devem ser confundidos com filtros 2D, que também usam códigos GLSL. Um filtro 2D é o código GLSL que é aplicado a toda a tela como um efeito de pós-processamento, enquanto shaders GLSL personalizados são aplicados aos objetos.

Os sombreadores GLSL personalizados funcionam no modo de sombreamento GLSL e Multitexture; eles não funcionam no modo Singletexture. Shaders GLSL personalizados não são visíveis na janela de exibição 3D: você deve executar o jogo para vê-los. Para usar sombreadores GLSL personalizados, você precisará usar um pouco de script Python para vincular sombreadores ao objeto. Mas, primeiro, aqui está um curso intensivo sobre GLSL.

## GLSL Primer <a id="GLSL_Primer"></a>

GLSL é a linguagem de sombreamento para a API gráfica OpenGL. Ele tem uma sintaxe semelhante ao C e é compilado em código assembly pelo driver gráfico em tempo de execução. É também multiplataforma e neutro em relação ao fornecedor (palavrões para dizer que eles rodam em tudo: Windows, Linux, Mac, AMD, Nvidia e Intel). O objetivo principal do GLSL é dar aos artistas mais controle sobre como eles querem que uma superfície pareça, permitindo-lhes escrever um código personalizado que muda a maneira como um objeto é renderizado.

Os shaders GLSL podem ser divididos em três tipos. Eles diferem em onde no pipeline gráfico os códigos são executados e a quais tipos de dados eles têm acesso.

- **Vertex shader:** Opera em vértices, permitindo a transformação da geometria.

- **Geometry shader:** Capaz de gerar ou deletar vértices.

- **Fragment shader:** Opera em cada pixel da tela, permitindo efeitos de textura e sombreamento.

Todas as três categorias de sombreadores compartilham a mesma construção de linguagem e seguem a mesma sintaxe geral. Os programas GLSL são executados nesta ordem:

 vertex shader> geometry shader> fragment shader

Como o shader de geometria ainda é relativamente novo e requer OpenGL 3.2 ou superior, o Blender não o suporta. No momento, apenas o sombreador de vértice e o sombreador de fragmento podem ser usados ​​no mecanismo de jogo.

Em vez de percorrer todos os fundamentos de GLSL, presumiremos que você tenha experiência em pelo menos uma linguagem de programação e simplesmente descreveremos o que torna a GLSL única como linguagem baseada em GPU. GLSL não é muito diferente de linguagens como C. Tem tipos de dados familiares, como float (0,5, -3,5), int (0,1, -3) e bool (verdadeiro, falso). Além disso, como GLSL é projetado para trabalhar com dados gráficos, que normalmente incluem informações de cor (RGB ou RGBA), dados de localização (XYZ ou XYZW) e matrizes (matriz 3x3, matriz 4x4), existem muitos tipos de dados vetorizados projetados apenas para este propósito.

Considere este snippet de código GLSL:

```c++
vec4 color1 = vec4(1.0,0.0,0.0,1.0);

vec4 color2 = vec4(0.0,0.5,0.0,1.0);

vec4 final = color1 + color2;
```

vec4 inicializa a variável para ser um vetor de ponto flutuante de quatro componentes. color1 e color2 são os nomes das variáveis. E, finalmente, vec4 () pode ser visto como um construtor que pega quatro constantes literais e gera um tipo de dados vec4 a partir delas.

Mas o que o código realmente faz? Aqui, primeiro declaramos dois vetores de quatro componentes, color1 e color2. Os valores à direita do operador de atribuição (=) são mapeados para os canais vermelho, verde, azul e alfa do vetor, respectivamente. Assim, color1 é inicializado com uma cor vermelha com um alfa de 1; enquanto color2 é inicializado com uma cor verde escura, também com um alfa de 1. Na última linha do código, adicionamos color1 a color2 e copiamos o resultado para uma nova variável chamada _final, _ que deve ter o valor (1.0 , 0,5,0,0,1.0).

Os operadores swizzling de aparência engraçada da linguagem GLSL são uma de suas características distintas. Eles se parecem com isto:

```c++
vec4 myColor = vec4 (0.0,1.0,0.5,0.6);

float intensity  = myColor.r + myColor.g + myColor.b;
```

A notação de ponto (.) No final da variável de cor é usada para selecionar um único componente do vetor de quatro componentes. No caso acima, pegamos os componentes vermelho, verde e azul de myColor e os adicionamos para obter a soma dos três canais. O resultado é armazenado em uma variável chamada _intensidade_ como um único número de ponto flutuante. Os seletores válidos incluem RGBA, XYZW e STQR. Você também pode repetir os operadores de swizzling ou reorganizá-los.

```c++
vec4 myColor = vec4 (0.0,1.0,0.5,0.6);

vec4 newColor  = myColor.ggrr;
```

newColor agora tem o valor (1.0,1.0,0.0,0.0) porque o conteúdo do canal verde de myColor é copiado para os canais vermelho e verde de newColor, e o canal vermelho de myColor é copiado para os canais azul e alfa de newColor. O valor de myColor não é alterado.

GLSL suporta controle de fluxo básico semelhante ao C, como loops while, loops for, instruções if e declarações de função. Embora com suporte, a ramificação com instruções if é geralmente evitada porque são relativamente lentas.

>**Using "If"**
>
> Se você deve usar "if", tenha cuidado ao escrever suas condições. Valores de ponto flutuante em GLSL geralmente não são precisos o suficiente para que uma operação de comparação de igualdade funcione. Então, ao invés de escrever
> `if (myVar == 1.0)`
> que pode nunca ser avaliado como verdadeiro, use o muito mais seguro
> `if (abs (myVar - 1,0) <0,001)`
> Este código examinará a diferença absoluta entre os dois valores que está comparando e retornará verdadeiro, desde que a diferença entre eles seja pequena o suficiente (0,001, neste caso).

Embora saibamos que você gostaria de aprender sobre trigonometria, matemática 3D, matriz, ortogonalidade, espaço vetorial euclidiano e lerp, ensinar GLSL não é o objetivo deste livro. O livro _OpenGL Shading Language_ de Randi J. Rost faz um trabalho fantástico ao explicar do que se trata o GLSL.

>**GLSL Implementations "Gotchas"**
>
> Como o GLSL é compilado pelo driver gráfico, cada fornecedor (AMD, Nvidia, Intel, etc.) faz isso de maneira um pouco diferente. Isso significa que os códigos que funcionam em um podem não funcionar em outro. Por exemplo, na Nvidia, a função noise () sempre retorna 0. (No entanto, isso ainda está tecnicamente dentro da especificação GLSL, que afirma que o valor de retorno para a função noise () deve estar entre -1,0 e 1,0.)
> Apenas tenha em mente que alguns drivers são mais rígidos do que outros, portanto, um programa GLSL que funciona em um computador pode não funcionar em outro.

## Custom GLSL Shaders <a id="Custom_GLSL_Shaders"></a>

Então, agora que você aprendeu o básico de GLSL, está pronto para lidar com seu primeiro shader GLSL completo?
```c++
void main(){
gl_FragColor.rgba = vec4(0.9,0.4,0.2,1.0);
}
```

É isso aí. Este shader de fragmento de uma linha atribuirá a cada pixel de saída (uma variável predefinida com o nome de gl \ _FragColor) a cor (0.9,0.4,0.2), que é um laranja agradável. O último valor define o alfa em 1,0, para garantir que o rosto esteja completamente visível.

Um dos requisitos para qualquer sombreador GLSL válido é que ele contenha um sombreador de vértice e um sombreador de fragmento. Portanto, fornecer apenas o sombreador de fragmento acima não é suficiente; você também precisa de um sombreador de vértice. Mas na maioria dos casos, você não quer fazer nada extravagante com os vértices, então um simples

```c++
void main(){
gl_Position = ftransform();
}
```

basta. Ele diz ao GLSL que você deseja que o vértice permaneça na mesma posição que ficaria se você usasse um pipeline de transformação fixa.

No Blender, para usar shaders GLSL customizados como um substituto para qualquer material regular, você precisa rodar um script Python que ajuda a vincular o shader GLSL a um material em tempo de execução. Um script completo é mostrado abaixo:

```python
01 from bge import logic
02 ShaderObject = logic.getCurrentScene().objects.get("Cube")
03
04 VertexShader = """
05 void main()
06 {
07     gl_Position = ftransform();
08 }
09 """
10
11 FragmentShader = """
12 void main()
13 {
14     gl_FragColor.rgba = vec4(0.9,0.4,0.2,1.0);
15 }
16 """
17

18 for mesh in ShaderObject.meshes:
19     for material in mesh.materials:
20         shader = material.getShader()
21         if shader != None and not shader.isValid():
22             shader.setSource(VertexShader, FragmentShader, True)
```

Se você estiver se sentindo tonto, não entre em pânico! (Apenas espere até chegar ao Capítulo 7.) Este script tem uma boa combinação de Python e GLSL, mas não é complicado depois de decompô-lo.

Python será formalmente apresentado no Capítulo 7. Você pode pular e ler a parte relevante antes de continuar a partir daqui.

A linha 1 carrega o módulo bge Python, que nos permite usar a API BGE dentro do script Python.

Linha 2 é equivalente a

```python
scene = logic.getCurrentScene()

objects = scene.objects

ShaderObject = objects.get("Cube")
```

Um conceito importante a ser lembrado é que o sombreador GLSL está vinculado ao material. Mesmo que você tenha obtido o material referenciando um objeto, o sombreador GLSL está sempre substituindo um material. Isso significa que se vários objetos compartilham o mesmo material, o sombreador será executado em todos os objetos.

Portanto, você está procurando um objeto chamado "Cube" em uma lista de todos os objetos na cena atual e atribui o objeto Cube a uma variável chamada ShaderObject. Portanto, se um objeto com o nome Cube existir, ShaderObject agora conterá uma referência a esse objeto. Se nenhum objeto com esse nome for encontrado, ShaderObject terá o valor Nenhum.

Na linha 4, VertexShader é simplesmente uma string Python de várias linhas. Strings multilinha são declaradas por aspas triplas. O conteúdo da string é o código GLSL real. (Para esclarecer, a variável VertexShader ainda é um objeto string Python, mas o conteúdo passa a ser outra linguagem: GLSL. Mas é tudo a mesma coisa para Python: a string poderia estar em chinês e Python não se importaria.). Observe que o sombreador de vértice está envolvido em uma função main (), assim como em C. É aqui que a execução do código começará.

Começando na linha 11, análogo ao VertexShader, FragmentShader é outra string Python multilinha contendo o código GLSL do sombreador de fragmento.

Da linha 18 em diante até o final, o código Python é usado para invocar o sombreador GLSL declarado acima. Primeiro, você percorre as malhas internas anexadas ao objeto. Em seguida, iterando em cada malha, você encontra todos os materiais anexados a ela. Como as malhas podem ter vários materiais (até 16), a iteração por todos eles garante a substituição de todos os materiais naquele objeto pelo sombreador. (Por outro lado, você pode modificar o código para aplicar um sombreador exclusivo a cada material na mesma malha.)

>**Don't Write This Code!**
>
> Como estávamos tentando manter este exemplo o mais curto e simples possível, o código tem uma capacidade muito ruim de tratamento de erros. Por exemplo, não seria bom se um objeto com o nome de Cube não fosse encontrado na cena, ou se o objeto chamado Cube não fosse uma malha. Não escreva código como este na vida real!

A linha 21 pode parecer um pouco complicada. Mas em inglês, significa simplesmente que, se houver um shader, o script continua para verificar se o shader é válido. Se não for, um novo shader é criado usando a string de texto VertexShader e FragmentShader como entrada. Se já houver um sombreador válido, nada mais será feito. (Shaders só precisam ser compilados e vinculados uma vez no início do jogo, não em todos os quadros. Caso contrário, a compilação GLSL tornará o jogo significativamente mais lento)

Salve o script como um novo arquivo de texto no Blender. Para usar o script de sombreador GLSL acima, ele precisa ser invocado uma vez no mecanismo de jogo. Você pode fazer isso facilmente configurando uma cadeia simples de blocos lógicos, conforme mostrado na Figura 5.36.

![Logic brick setup to load a custom GLSL shader](../figures/Chapter5/Fig05-36.png)

Você pode tentar copiar esta configuração com o arquivo Blender fornecido em \ Book \ Chapter5 \ GLSL1.blend.

Nesse caso, como não há nenhum objeto denominado _Cube_, você precisa modificar um pouco o script, substituindo a linha:

```python
ShaderObject = logic.getCurrentScene().objects.get("Cube")
```
por

```python
ShaderObject = logic.getCurrentScene().objects.get("Monkey")
```

Execute o jogo e curta o novo macaco laranja.

Como o GLSL substitui todo o pipeline de material pelo seu próprio código, nenhum sombreamento é aplicado ao modelo, a menos que você explicitamente o indique. É por isso que a cabeça do macaco tem um tom liso de laranja.

Lembre-se de que sombreadores GLSL personalizados são sempre aplicados a cada material, não ao objeto, nem à malha. Isso significa que todos os objetos com o mesmo material compartilharão o mesmo sombreador.

### A Useful Fragment Shader <a id="A_Useful_Fragment_Shader"></a>

O primeiro shader GLSL que você conheceu é bastante trivial e quase inútil. Aqui está um shader difuso de Lambert muito mais útil:

```python
from bge import logic
ShaderObject = logic.getCurrentScene().objects["Monkey"]
lamp = logic.getCurrentScene().objects["MainLight"]

VertexShader = """
uniform vec3 light_position;
varying vec3 light_vec;
varying vec3 normal_vec;

void main(){
 vec3 vert =(gl_ModelViewMatrix * gl_Vertex).xyz;
 light_vec = (gl_ModelViewMatrix * vec4(light_position,1.0)).xyz – vert;
 normal_vec = gl\_NormalMatrix * gl_Normal;
 gl_Position = ftransform();
}
"""

FragmentShader = """
varying vec3 light_vec;
varying vec3 normal_vec;

void main(){
 vec3 l = normalize(light_vec);
 vec3 n = normalize(normal_vec);
 float ndotl = clamp(dot(n,l), 0.0, 1.0);

 vec4 color = ndotl * vec4(1.0,1.0,1.0,1.0);

 gl_FragColor = color;
}

"""

mesh = ShaderObject.meshes[0]
for material in mesh.materials:
 shader = material.getShader()
 if shader != None:
  if not shader.isValid():
   shader.setSource(VertexShader, FragmentShader,1)
  shader.setUniformfv('light_position', lamp.position)
```

Este sombreador usa o algoritmo de sombreamento difuso de Lambert para aplicar algum sombreamento básico ao objeto, levando em consideração a posição da lâmpada e a normal da superfície em cada pixel. Este ainda não é um shader muito útil, já que o mesmo efeito pode ser obtido sem uma única linha de codificação por meio do painel Material.

Deixaremos que você descubra sombreadores mais complexos por conta própria.

### A Useful Vertex Shader <a id="A_Useful_Vertex_Shader"></a>

Este sombreador GLSL aplica uma transformação a cada vértice ao longo do eixo X, produzindo um efeito "ondulado", semelhante ao das folhas balançando ao vento. Usar sombreadores de vértice para deformar a geometria é uma alternativa rápida ao uso de bones.

```python
from bge import logic
ShaderObject = logic.getCurrentController().owner

VertexShader = """
uniform float timer;

void main()
{
 //get the first UV layout
 gl_TexCoord[0] = gl_MultiTexCoord0;


 // Fetch the Vertex Position
 vec4 v = gl_Vertex;

 //Displaces each vertex using a sine wave
 v.x = v.x + sin(timer);

 gl_Position = gl_ModelViewProjectionMatrix * v;
}
"""

FragmentShader = """
uniform sampler2D colorMap;

void main(void)
{
 vec4 color = texture2D(colorMap,gl_TexCoord[0].st);
 gl_FragColor = color;
}
"""

mesh = ShaderObject.meshes[0]
for material in mesh.materials:
 shader = material.getShader()
 if shader != None:
  if not shader.isValid():
   shader.setSource(VertexShader, FragmentShader,1)

  shader.setSampler('colorMap',0)
  shader.setUniform1f('timer',ShaderObject["timer"])
```

Este sombreador introduz outro novo conceito, chamado _uniformes_. Usar uniformes é uma maneira de passar dados do mundo do Blender para o sombreador.

### Going Further <a id="Going_Further"></a>

Embora a GLSL possa parecer assustadora no início, muito material de aprendizado está disponível. O disco que acompanha tem mais alguns exemplos de como o GLSL pode ser usado; eles podem ser encontrados em \Book\Chapter5\.

## 2D Filters <a id="2D_Filters"></a>

Filtros 2D são sombreadores GLSL pós-processamento que são aplicados a cada quadro antes de ele ser exibido. Filtros 2D podem ser usados para aprimorar a aparência da imagem e adicionar efeitos especiais de espaço na tela. Existem alguns shaders integrados que vêm com o Blender para você começar, mas os filtros 2D também permitem shaders GLSL personalizados para lhe dar a liberdade de fazer potencialmente muito mais.

### Why Use 2D Filters? <a id="Why_Use_2D_Filters?"></a>

O uso de filtros 2D facilita ajustar o clima do seu visual, sem ter que refazer a iluminação, o material ou as texturas. Como um filtro 2D opera em uma imagem (o buffer de quadro) e não nos objetos 3D individuais, o desempenho do filtro 2D não depende da complexidade da cena, apenas do número de pixels na tela e da complexidade do próprio efeito.

O sombreador de fragmento GLSL é a linguagem que capacita todos os filtros 2D. A Figura 5.37 mostra alguns exemplos do que os filtros 2D podem fazer:

![Sample Filters: Normal color, grayscale, blur, sepia](../figures/Chapter5/Fig05-37.jpg)

Os recursos dos filtros 2D:

- Aplique efeitos como nitidez, detecção de bordas, anti-aliasing e desfoque de movimento.

- Altere os atributos básicos da cor, como brilho, contraste e saturação da cor.

- Adicione efeitos de espaço na tela, como desfoque gaussiano, desfoque radial, flor de luz e distorção.

- Adicione efeitos cinematográficos, como profundidade de campo, granulação do filme, tom sépia e vinheta de lente.

- Simule efeitos de iluminação complexos, como oclusão de ambiente e dispersão de luz.

### How to Use 2D Filters <a id="How_to_Use_2D_Filters"></a>

Os filtros 2D podem ser acessados como um atuador padrão na janela do Logic Editor. Se você não souber o que o Logic Editor faz, consulte o Capítulo 3.

Para habilitar um filtro 2D básico, adicione um sensor Always, um controlador And e um atuador de filtro 2D e vincule-os. Lembre-se de que, embora você queira que o efeito seja aplicado a todos os quadros, não há necessidade de ligar o pulso "verdadeiro" no sensor Always. Porque uma vez que o sombreador é vinculado (inicializado), ele permanecerá ativo até que você o desative explicitamente. Vincular o filtro 2D a cada quadro só tornará o jogo mais lento.

Também não importa a qual objeto o tijolo lógico está anexado; O filtro 2D é um efeito de tela e, portanto, não depende do objeto ao qual está anexado. Você pode anexá-lo a qualquer objeto conveniente. Anexar a lógica do filtro 2D à câmera principal é uma boa ideia, porque é um lembrete intuitivo de que o filtro 2D é um efeito de tela. A Figura 5.38 mostra uma configuração básica de filtro 2D.

![Logic brick setup to load a custom GLSL shader](../figures/Chapter5/Fig05-38.png)

Depois de configurar os blocos lógicos, vamos dar uma olhada mais de perto no atuador Filtro 2D. A função exata de cada opção no painel do atuador é explicada no Capítulo 3.

O número de passe na parte inferior atua como uma configuração de "camada" onde reside o efeito de filtro 2D. Cada "camada" pode ter apenas um filtro, mas você pode empilhar camadas de filtro para obter um efeito mais complexo. Apenas certifique-se de que cada efeito tenha um número de passe exclusivo para que eles não se sobreponham. Obviamente, para configurar vários efeitos de filtro 2D, mais de um atuador é necessário.

No menu suspenso, você verá uma pequena seleção de efeitos predefinidos (Inverter, Sépia, Escala de cinza, Desfoque de movimento). Selecione um e execute o jogo para ver como fica.

Habilitar e Desabilitar ligam ou desligam um certo efeito. Você precisa fornecer um número de passe válido. Portanto, se você vinculou um filtro 2D à passagem número 5 em um ponto, pode desligar o efeito com Desativar e definir o número da passagem como 5. Por outro lado, você pode ativar rapidamente o mesmo efeito usando Ativar.

Remover Filtro é semelhante a Desativar: ele desativa um certo efeito em um determinado número de passe. Além disso, Remover filtro também desassocia completamente o sombreador, tornando impossível habilitar o mesmo filtro (ou seja, número de passagem) novamente.

Filtro personalizado é usado para especificar sombreadores arbitrários. É útil quando os filtros integrados não conseguem obter o efeito que você está procurando. Para usar um filtro personalizado, o Blender precisa do nome de um arquivo de texto. O arquivo de texto deve ser um dos blocos de dados de texto armazenados no arquivo do Blender.

Com o sistema de passagem, você pode fazer uma pilha de pós-processamento muito robusta. Você pode configurar alguns filtros para serem executados em um sensor Always para fazer alguma correção básica de cores e adicionar os efeitos que sempre estarão ativados. Em seguida, você pode configurar mais alguns filtros que são ativados momentaneamente quando você precisar deles.

### Custom Filter <a id="Custom_Filter"></a>

Um filtro 2D personalizado muito simples é mostrado abaixo:

```c++
uniform sampler2D bgl_RenderedTexture;
const float contrast 1.5
void main(void)
{
  vec4 texcolor = texture2D(bgl_RenderedTexture, gl_TexCoord[0].st);
  gl_FragColor.rgb = texcolor.rgb * contrast;
  gl_FragColor.a = texcolor.a;
}
```

Se o código acima parece um tanto familiar, provavelmente é porque um filtro 2D é na verdade apenas um sombreador de fragmento GLSL. Este sombreador busca a cor do pixel atual, multiplica-o por 1,5 e exibe o resultado. Isso produz uma imagem com maior contraste do que o original.

### Limitations <a id="Limitations"></a>

O filtro 2D pode ser lido a partir das seguintes entradas:

- Frame Buffer Color Image (sampler2D bgl\_RenderedTexture)

- Profundidade do buffer de quadro (sampler2D bgl\_DepthTexture)

- Frame Buffer Luminance (sampler2D bgl\_LuminanceTexture)

- Tamanho da imagem (float bgl\_RenderedTextureWidth, float RenderedTextureHeight)

- Texturas personalizadas como entrada (sampler2D)

Filtros 2D são aplicados por cena, com o efeito sendo construído um sobre o outro. Por exemplo, se você tiver uma cena principal e uma cena de sobreposição, o mecanismo de jogo irá proceder da seguinte forma:

1. Renderize a cena principal.

2. Aplique na tela os filtros disponíveis naquela cena.

3. Renderize a cena de sobreposição em cima da cena principal já pós-processada.

4. Aplique os filtros na parte superior desta lasanha de pixel de várias camadas.

## Text <a id="Text"></a>

Para exibir texto, você pode pré-criar um objeto de malha que tenha a geometria real do texto ou um mapa de textura de um plano. Este método é simples, mas é muito limitante porque o texto não pode ser alterado durante o jogo. Para mostrar um texto diferente, o artista precisaria criar um novo recurso para cada string de texto de que o jogo precisava.

Para exibir texto que pode mudar potencialmente durante o jogo, existem quatro maneiras de exibir textos dinâmicos dentro do mecanismo de jogo. Dois deles são úteis apenas para texto estático: texto que não muda durante o jogo. Os outros dois são dinâmicos: o texto que eles exibem pode ser alterado instantaneamente.

- Texto estático usando geometria real.

- Texto estático usando texturas pré-fabricadas.

- Texto de bitmap dinâmico.

- Objeto de texto dinâmico.

Texto estático não é tratado de forma diferente dos objetos normais do Blender. No restante desta seção, examinaremos maneiras de criar textos dinâmicos.

## Bitmap Text <a id="Bitmap_Text"></a>

Se o mecanismo de jogo pode renderizar gráficos 3D hiper-realistas em tempo real, quão difícil pode ser renderizar algum texto na tela? Acontece que é realmente difícil devido ao fluxo de trabalho estranho necessário para criar o texto.

O processo envolve a criação de uma textura contendo todas as letras do alfabeto inglês (mais números e símbolos) - sim, os idiomas que usam um alfabeto não latino não são suportados usando este método; UV mapeia a textura em um plano; ative a opção Texto na configuração de material; e crie uma propriedade GameLogic no objeto de texto chamado "Texto". Preencha esta variável com alguma string. Depois de executar o jogo, o Blender exibirá automaticamente o conteúdo da string "Texto" na tela. Tada! Olá? Volte!

Ok, vamos tentar novamente.

1. Comece com um arquivo do Blender vazio.

2. Selecione Blender Game na caixa suspensa Render Engine.

3. Na vista superior, adicione um Plano clicando em Adicionar> Malha> Plano.

4. Configure um dos Viewports para ser o Editor de UV/Imagem.

5. Selecione o Plano; entre no modo de edição pressionando Tab.

6. No UV/Image Editor, carregue a textura da imagem de texto da pasta /Book/Chapter5/Textures/text.png.

7. A textura da imagem merece um pouco mais de atenção. Esta textura é gerada por uma ferramenta gratuita que pode ser encontrada em [http://www.ashsid.sk/wp/?p=21](http://www.ashsid.sk/wp/?p=21). Ele contém os caracteres e símbolos mais comumente usados, dispostos de forma que o Blender saiba exatamente onde cada personagem está.

8. Crie um material para o objeto; nas configurações do jogo, habilite Texto. Isto dirá ao Blender para tratar a textura da imagem que você carregou no passo acima como uma imagem de texto especial. O avião agora mostrará um símbolo @, o primeiro caractere disponível da imagem de texto. Isto é normal.

9. Configure um dos Viewports para ser o Logic Editor.

10. Mantenha o plano selecionado. No Logic Editor, adicione uma nova Game Property e nomeie-a como Text. (Isso é importante! Caso contrário, não funcionará). E defina o tipo de dados como String.

11. No campo de valor, digite o que quiser; tudo o que estiver armazenado nesta propriedade Text será exibido como texto no jogo.

12. Execute o jogo. O conteúdo da propriedade Text substituirá o símbolo @.

Este método de exibição de texto tem várias desvantagens. Por exemplo, como os textos são desenhados com texturas, eles podem parecer borrados quando mostrados em ângulos extremos em relação à câmera. Além disso, como o conjunto de caracteres é extremamente limitado, o suporte internacional para alfabetos não latinos e idiomas da direita para a esquerda é impossível de alcançar.

## Text Object <a id="Text_Object"></a>

Usar texto de bitmap é um processo muito confuso. Objeto de texto é uma maneira mais fácil de exibir texto (consulte a Figura 5.39). O mesmo tipo de objeto de texto do Blender pode ser usado no jogo. Simplesmente crie um objeto "Texto" no Blender, e ele será renderizado como um texto dentro do motor de jogo. Para alterar o valor do texto, você pode usar os tijolos lógicos para alterar a propriedade "Texto" dos objetos de texto.

Ou pode-se usar Python:

```python
from bge import logic

logic.getCurrentController().owner.text = "Hello World"
```

![Text Object: 3D view and in-game](../figures/Chapter5/Fig05-39.png)

## Video Texture <a id="Video_Texture"></a>
A função de textura de vídeo permite que você atualize ou substitua uma textura durante o jogo. Isso não só dá a você a capacidade de usar um arquivo de vídeo como textura, como o nome da função indica, mas a textura de vídeo também pode ser usada para substituir uma textura estática pelo seguinte:

- Um arquivo de vídeo (útil como textura animada)

- Uma textura de imagem diferente (útil se você quiser apenas substituir a textura)

- Uma renderização de outra câmera (útil para renderizar reflexos de espelhos)

Como a textura do vídeo é um recurso bastante avançado que requer algum conhecimento de script Python, ela será deixada para sua própria exploração. Os arquivos do livro contêm alguns exemplos de como a textura do vídeo pode ser usada. Você pode encontrá-los em /Book/Chapter7/6\_texture/.

## Stereo <a id="Stereo"></a>

Os olhos humanos são capazes de perceber a profundidade principalmente de três maneiras:

- Usar pistas ambientais, como neblina, iluminação, perspectiva e conhecimento existente das dimensões de objetos comuns. Usando esse método, você ainda pode ter uma sensação de profundidade ao olhar para uma imagem plana.

- Usando a distância de foco do olho, porque as coisas que não estão em foco tendem a ficar mais desfocadas.

- Usando a distância paralaxe entre dois olhos para ver duas imagens ligeiramente diferentes.

A ideia básica por trás de todas as técnicas estereoscópicas 3D utiliza o terceiro ponto da lista acima: paralaxe. Ou seja, para exibir uma imagem diferente renderizada de uma perspectiva ligeiramente diferente para cada olho. Existem muitos métodos usados ​​hoje para garantir que o olho esquerdo veja apenas a imagem destinada ao olho esquerdo e o olho direito apenas veja a imagem destinada ao olho direito. A maioria dos cinemas 3D consegue isso usando óculos polarizados combinados com uma configuração de projetor duplo. As TVs 3D baseadas em vidro para consumidores usam um obturador que alterna rapidamente entre bloquear o olho esquerdo e o direito, sincronizado com uma tela de atualização rápida que também alterna entre as imagens do olho direito e esquerdo.

O Blender pode gerar renderizações estereoscópicas de várias maneiras. A Figura 5.40 mostra como configurá-lo. Mas, independentemente do formato de saída final, ele começa renderizando a cena duas vezes, com um leve deslocamento horizontal da câmera (controlado pela configuração de Separação dos olhos) para imitar a separação entre os olhos humanos. Para um ambiente de visualização típico, a separação ocular ideal é aproximadamente a Distância Focal / 30.

>**The Nitty Gritty Details**
>
>O Blender usa a técnica de paralaxe zero para configurar as câmeras estéreo.

![Stereo setting panel](../figures/Chapter5/Fig05-40.png)

Quando o modo Stereo é selecionado no painel Render, conforme mostrado na Figura 5.40, seis modos Stereo tornam-se disponíveis.

- **V-interlace and Interlaced:** As imagens esquerda e direita estão entrelaçadas. Este modo requer hardware 3D adicional para ver corretamente.

- **Above-Below:** As imagens esquerda e direita são empilhadas verticalmente. Este modo também requer hardware 3D adicional para ver corretamente.

- **Side by Side:** As imagens esquerda e direita são colocadas lado a lado sem sobreposição. Neste modo estéreo, você deve ser capaz de ver o efeito 3D cruzando os olhos (sério!). Mas esse método de visualização em 3D é muito cansativo para os olhos. Eu não recomendo que você tente isso por um longo período de tempo.

- **Anaglyph:** Neste modo, o Blender filtra as imagens esquerda e direita com uma cor diferente e então as sobrepõe uma na outra. Este modo requer que o visualizador use um par de óculos 3D com lentes coloridas. O olho esquerdo deve ser tingido de vermelho e o olho direito deve ser tingido de ciano. Com os óculos colocados, a lente colorida deve permitir a passagem de apenas uma imagem, bloqueando a imagem do outro olho. Esta forma de ver 3D é menos estressante do que Lado a Lado, mas requer que o monitor seja suficientemente brilhante em relação ao ambiente para uma imagem ideal. A única desvantagem dessa abordagem é a falta de representação precisa das cores.

- **Quad-Buffer:** Quad-Buffer é a extensão natural de um sistema de renderização de buffer duplo típico, que é usado para renderização de um único olho. Este modo também requer hardware adicional para exibir a imagem. Quad-Buffering é um método estereoscópico nativo compatível com OpenGL. Infelizmente, ele não funciona em placas de vídeo Nvidia e ATI / AMD de nível de consumidor; apenas as mais caras Nvidia Quadro e ATI / AMD FireGL suportam esta funcionalidade.

## Dome <a id="Dome"></a>

O modo Dome no motor de jogo é um grande exemplo de como a natureza de código aberto do Blender o torna o playground perfeito para os desenvolvedores experimentarem recursos especializados que praticamente nenhum outro motor de jogo no mercado tem. O modo Dome foi implementado por Dalai Felinto como um trabalho parcialmente escolar e parcialmente encomendado.

Semelhante a como os mapas de ambiente são renderizados no Blender, o modo Dome funciona renderizando a cena de várias direções, até seis vezes. Esses dados são então agrupados e mapeados em uma nova tela de qualquer forma arbitrária e, finalmente, exibidos na tela. A imagem gerada pelo modo Dome é projetada para telas esféricas como as encontradas nos cinemas OMNIMAX e planetários.

Mesmo que você não tenha acesso à tela de seu teatro OMNIMAX local (não tem ?!), telas de domo imersivo menores também estão se tornando mais populares, como a mostrada na Figura 5.41.

![The Dome mode in action](../figures/Chapter5/Fig05-41.jpg)

Mesmo com uma tela plana, o modo Dome pode fornecer a você uma experiência de visualização muito melhor do que o modo de perspectiva OpenGL padrão em ângulos extremamente amplos, conforme mostrado na Figura 5.42. Ambas as câmeras têm 170 graus. Observe a forte distorção na imagem à esquerda e a aparência de olho de peixe que a perspectiva da cúpula obtém.

![Comparison between regular perspective and dome perspective](../figures/Chapter5/Fig05-42.jpg)

Dome settings can be enabled from the Render panel, as shown in Figure 5.43.

![Dome settings](../figures/Chapter5/Fig05-43.png)

- **Dome type:** Controla como as imagens são mapeadas na tela. Cube Map mostra a renderização bruta feita pelo motor de cúpula, disposta de forma a combinar como o Blender armazena os mapas de ambiente. Isso é útil principalmente para depuração ou se você deseja salvar o mapa do cubo para uma finalidade diferente. Outras opções incluem Spherical Panoramic, Front-Truncated, Rear-Truncated e Fisheye. Essas opções distorcem as imagens de maneiras diferentes para caber na tela. Experimente você mesmo! Porém, tenha cuidado - algumas dessas configurações podem ser muito desorientadoras!

- **Resolution** : Define a dimensão das imagens renderizadas para textura; um valor menor proporcionará melhor desempenho ao custo de uma imagem final de resolução mais baixa.

- **Tessellation** : Define o número de subdivisões da malha usada para exibir a imagem final. Um valor maior significa menos distorção, mas também será mais lento. Você pode verificar o efeito desta configuração executando o jogo na visualização de estrutura de arame.

- **Angle:** Define o campo de visão da câmera.

- **Tilt** : Aumenta e diminui a visualização sem realmente girar a câmera do jogo.

>**Beware of Artifacts!**
>
> Como a imagem estéreo e o modo Dome exigem que o jogo reposicione ou reoriente a câmera para criar várias visualizações por quadro, certas funções de sombreamento e textura dependentes da câmera (como normal e reflexão e realces especulares) podem conter artefatos quando renderizados em estéreo ou modo Dome.

//TODO
//BY 'Mike Pan'
//ON '2013-04-10T07:30:00'MP
//NOTE: 'Before that, still in domes, maybe talk about warping mesh? The wiki page covers it nicely/simply. You can even be shorter than there.']
//

Antes que você se empolgue com a criação do melhor colírio para os olhos, lembre-se de que um jogo realista não envolve apenas fidelidade visual. Como John Carmack (o diretor técnico da id Software, conhecido pelas séries _Doom_ e _Quake_) observou na QuakeCon 2009: Não importa o quão boa uma cena pareça graficamente, é necessário apenas um quadro de animação estranha para quebrar completamente a ilusão de realismo. Muitos jogos hoje alcançaram gráficos quase fotorrealistas, mas uma vez que o personagem começa a se mover, torna-se dolorosamente óbvio o quão artificial tudo é. Portanto, tenha em mente que mesmo o modelo 3D mais detalhado não pode mergulhar o jogador em um mundo de fantasia se a jogabilidade, o som ou a animação não corresponderem.
