**Table of Contents**

- [Chapter 7: Python Scripting](#Chapter_7_Python_Scripting)
	- [Why Script When You Can Logic Brick It?](#Why_Script_When_You_Can_Logic_Brick_It?)
		- [Sane Replacement for Large-Scale Logic-Bricked Objects](#Sane_Replacement_for_Large-Scale_Logic-Bricked_Objects)
		- [Better Handling of Multiple Objects](#Better_Handling_of_Multiple_Objects)
		- [Access to Blender's Advanced Features](#Access_to_Blender's_Advanced_Features)
		- [Use Features That Are Not Part of Blender](#Use_Features_That_Are_Not_Part_of_Blender)
		- [Keep Track of Your Changes with a Version Control System](#Keep_Track_of_Your_Changes_with_a_Version_Control_System)
		- [Debug Your Game While It Runs](#Debug_Your_Game_While_It_Runs)
	- [So What Exactly Is Python?](#So_What_Exactly_Is_Python?)
		- [Flexible Data Types](#Flexible_Data_Types)
		- [Indentation](#Indentation)
		- [OOP - Object-Oriented Programming](#OOP_-_Object-Oriented_Programming)
	- [Where to Learn Python](#Where_to_Learn_Python)
		- [Online Material](#Online_Material)
		- [Offline Material](#Offline_Material)
		- [Python Built-in Help](#Python_Built-in_Help)
	- [Python and the Game Engine](#Python_and_the_Game_Engine)
		- [Integrating Python in the Game Engine](#Integrating_Python_in_the_Game_Engine)
		- [Writing Your Python Scripts](#Writing_Your_Python_Scripts)
			- [Text Editors](#Text_Editors)
				- [Blender Text Editor](#Blender_Text_Editor)
			- [Reference Material and Documentation](#Reference_Material_and_Documentation)
			- [Testing Your Scripts](#Testing_Your_Scripts)
		- [Designing Your Python Script - Study Example](#Designing_Your_Python_Script_-_Study_Example)
			- [3D World Elements](#3D_World_Elements)
			- [Understanding the Code](#Understanding_the_Code)
				- [Global Initialization](#Global_Initialization)
				- [Event Management](#Event_Management)
					- [scripts.mouse_move](#scripts.mouse_move)
					- [scripts.keyboard](#scripts.keyboard)
				- [Internal Functions](#Internal_Functions)
					- [scripts.move_camera](#scripts.move_camera)
					- [scripts.orbit_camera](#scripts.orbit_camera)
					- [scripts.look_camera](#scripts.look_camera)
				- [Game Interaction](#Game_Interaction)
					- [Outcome of the functions: scripts.move_camera, scripts.look_camera, and scripts.orbit_camera](#Outcome_of_the_functions_scripts.move_camera,_scripts.look_camera,_and_scripts.orbit_camera)
					- [scripts.change_view](#scripts.change_view)
				- [More Python](#More_Python)
			- [Reusing Your Script](#Reusing_Your_Script)
				- [File Organization - Groups and Layers](#File_Organization_-_Groups_and_Layers)
				- [Tweaks and Adjustments - Getting Your Hands Dirty](#Tweaks_and_Adjustments_-_Getting_Your_Hands_Dirty)
					- [Organize and Append Your File](#Organize_and_Append_Your_File)
					- [Adjustments in Loco](#Adjustments_in_Loco)
					- [Script Tweaks](#Script_Tweaks)
		- [Using the Game Engine API - Application Programming Interface](#Using_the_Game_Engine_API_-_Application_Programming_Interface)
			- [bge.logic](#bge.logic)
				- [getCurrentController()](#getCurrentController())
				- [getCurrentScene()](#getCurrentScene())
				- [expandPath()](#expandPath())
				- [sendMessage(), addScene(), start/restart/endGame(),](#sendMessage(),_addScene(),_start/restart/endGame())
				- [LibLoad(), LibNew(), LibFree(), LibList()](#LibLoad(),_LibNew(),_LibFree(),_LibList())
				- [globalDict, loadGlobalDict(), saveGlobalDict()](#globalDict,_loadGlobalDict(),_saveGlobalDict())
				- [keyboard](#keyboard)
				- [mouse](#mouse)
				- [joysticks](#joysticks)
				- [Others](#Others)
			- [bge.types](#bge.types)
				- [Class KX_GameObject](#Class_KX_GameObject)
					- [Python Internal Methods](#Python_Internal_Methods)
					- [Instance Methods](#Instance_Methods)
					- [Instance Variables](#Instance_Variables)
					- [Sub-Class KX_Camera](#Sub-Class_KX_Camera)
					- [Sub-Class KX_Lamp](#Sub-Class_KX_Lamp)
			- [bge.render](#bge.render)
				- [Window and Mouse](#Window_and_Mouse)
				- [World Settings](#World_Settings)
				- [Stereo Settings](#Stereo_Settings)
				- [Material Settings](#Material_Settings)
				- [Others](#Others)
			- [bge.events](#bge.events)
			- [bge.texture](#bge.texture)
			- [bge.constraints](#bge.constraints)
			- [Mathutils - Math Types and Utilities](#Mathutils_-_Math_Types_and_Utilities)
				- [Vector](#Vector)
				- [Matrix](#Matrix)
				- [Euler and Quaternion](#Euler_and_Quaternion)
			- [aud - Audio System](#aud_-_Audio_System)
				- [Example: Basic Audio Playback](#Example_Basic_Audio_Playback)
			- [bgl - OpenGL Wrapper](#bgl_-_OpenGL_Wrapper)
				- [Example 01: Line Width Changing](#Example_01_Line_Width_Changing)
				- [Example 02: Color Picker](#Example_02_Color_Picker)
			- [blf - Font Drawing](#blf_-_Font_Drawing)
				- [Example: Writing Hello World](#Example_Writing_Hello_World)

# Capítulo 7: Scripting Python <a id="Chapter_7_Python_Scripting"></a>

Parabéns, você finalmente chegou a uma das partes mais técnicas do livro. Tenha isso em mente no caso de você se perder.

O mecanismo de jogo do Blender já foi famoso por permitir que você crie um jogo completo sem tocar em uma única parte do código. Embora isso possa parecer atraente, também leva a uma experiência muito limitada de criação de jogos. Os blocos lógicos, conforme apresentados no Capítulo 3, são muito úteis para uma prototipagem rápida. No entanto, uma vez que você precisa acessar recursos avançados, bibliotecas e dispositivos externos, ou simplesmente otimizar seu aplicativo, uma linguagem de programação se torna seu novo melhor amigo.

Através do uso de uma linguagem de script chamada _Python_, o motor de jogo (como o próprio Blender) é totalmente extensível. Esta linguagem de programação é fácil de aprender, embora extremamente poderosa. Esteja ciente, porém, de que você não encontrará um guia completo para aprender Python aqui. Existem muitos recursos online e offline que irão atendê-lo melhor. No entanto, mesmo que você não esteja inclinado a estudar profundamente Python agora, mais cedo ou mais tarde você se encontrará lutando com arquivos de script. Portanto, é importante saber com o que você está lidando.

>**Sim você pode**
>
> Para os programadores Python experientes (ou para aqueles que estão se atualizando com o material de aprendizagem de referência), lembre-se sempre: se você pode fazer algo com Python, é provável que você possa fazê-lo no motor de jogo.

Após uma breve visão geral dos fundamentos do Python, explicaremos como aplicar seu conhecimento de Python dentro do mecanismo de jogo. Você também aprenderá como acessar os métodos, propriedades e objetos do Python que usará.

## Por que criar scripts quando você pode usar o Logic Bricks? <a id="Why_Script_When_You_Can_Logic_Brick_It?"></a>

Podemos comparar tijolos lógicos com tijolos reais. Por um lado, temos elementos fortes sobre os quais construir nosso sistema, mas, por outro lado, temos um sistema tão flexível quanto uma parede cega.

Existem muitas ocasiões em que o mesmo efeito pode ser obtido de maneiras diferentes. As diferentes fases da produção também podem exigir fluxos de trabalho variados. A razão para escolher um método específico costuma ser pessoal. No entanto, apresentamos aqui alguns argumentos que podem convencê-lo a ler um bom livro de Python e começar a aprender mais sobre ele:

- Substituição sensata para objetos de tijolos lógicos em grande escala.

- Melhor manuseio de vários objetos.

- Acesso aos recursos avançados do Blender.

- Use recursos que não fazem parte do Blender.

- Acompanhe suas mudanças com um sistema de controle de versão.

- Depure seu jogo enquanto ele é executado.

>**Tijolo lógico, o bem necessário**
>
> Você nunca pode fugir dos tijolos lógicos. Mesmo ao usar Python exclusivamente para o seu jogo, você precisará invocar os scripts de um controlador Python. O ideal é encontrar o equilíbrio que se adapta ao seu projeto.

### Substituição Sensata para Objetos Logic Bricked em grande escala <a id="Sane_Replacement_for_Large-Scale_Logic-Bricked_Objects"></a>

É sempre bom ter uma desculpa para mostrar uma imagem em um capítulo de programação, e aqui está. Na Figura 7.1 você vê os blocos lógicos de Frankie, o personagem principal do jogo aberto _Yo Frankie! _

![Chapagetti](../figures/Chapter7/Fig07-01.png)

Este sistema é bem organizado: diferentes ações pertencem a diferentes estados e sensores; controladores e atuadores são devidamente nomeados. No entanto, não é difícil se perder tentando entender qual sensor se conecta a qual controlador. Uma das razões para um projeto tão complexo depender de blocos lógicos é porque _Yo Frankie! _ Serve como um projeto didático para artistas que desejam começar com o motor de jogo. Qualquer pessoa com um pouco de experiência em programação pode pegar os arquivos e expandir o jogo livremente. (Você já experimentou?)

No entanto, você geralmente busca desempenho e fluxo de trabalho. Ter tudo centralizado em um único arquivo de script pode economizar muito tempo.

Outro aspecto importante durante o trabalho é documentar seu projeto. É fácil abrir um arquivo de apenas alguns meses e ficar completamente perdido. Os arquivos de script, por outro lado, são naturalmente estruturados para serem autodocumentados. Para documentar tijolos lógicos, você precisa confiar em arquivos de texto dentro ou fora de seus arquivos do Blender (e diagramas de imagem legais). Definitivamente, não é tão útil quanto os comentários embutidos no seu código. (Os diagramas de código ainda podem ser úteis, mas esse é um tópico diferente.)

>**Para o artista por trás da fachada do programador**
>
> Resista à tentação de criar arte ASCII enquanto documenta seus scripts.

```
   \_\_\_\_\_.-.\_\_\_\_\_

  '-------------'

  |             |    /

  |             | \_\_/

  \             /

   |           |

    \         /

     |  >|<  |

     \\_\_\_\_\_\_\_/

  .'==========='.

 / o o o o o o o \

'-----------------'
```

### Melhor manuseio de vários objetos <a id="Better_Handling_of_Multiple_Objects"></a>

Grandes projetos levam a vários arquivos [md] esta é uma verdade inevitável. Mesmo quando você usa links externos e bibliotecas, é crucial otimizar o tempo gasto na alteração de vários conjuntos de uma vez. Este é um dos pontos fracos dos blocos lógicos [md], eles tornam difícil alterar automaticamente uma grande variedade de elementos ao mesmo tempo.

Se você precisar alterar um nome de propriedade ou valor inicial de um objeto, precisará repetir essa alteração em outras instâncias do mesmo. Temos maneiras de tornar isso mais fácil usando copiar e colar blocos / propriedades lógicas entre objetos ou até mesmo através do compartilhamento de lógica. No entanto, você ainda terá que atualizar todos os sensores de propriedade, controladores e atuadores que podem contar com o valor antigo. Isso é especialmente verdadeiro para objetos com blocos lógicos entre eles [md], como vimos, o mecanismo de jogo permite que você vincule blocos lógicos de diferentes objetos. No entanto, objetos autocontidos / blocos lógicos são mais fáceis de trabalhar (e com menos espaguete).

Se você achou que a Figura 7.1 era uma bagunça, tente entender a Figura 7.2. Aqui temos os blocos lógicos de _Frankie, _ mais os objetos que possuem blocos lógicos conectados a ele. Como você deve se lembrar, você pode restringir as lógicas visíveis por meio da opção Mostrar Painel, mas isso ilustra como é difícil obter uma visão global do seu sistema.

![Spaghetti](../figures/Chapter7/Fig07-02.png)

Depois de começar a trabalhar com scripts, você verá como é fácil assumir o controle de todos os elementos da cena de forma global. Isso lhe trará muitos benefícios a longo prazo.

### Acesso aos recursos avançados do Blender <a id="Access_to_Blender's_Advanced_Features"></a>

Você ficará feliz em saber que o motor de jogo possui um conjunto poderoso de recursos além daqueles encontrados na interface do tijolo lógico. Além disso, quase todas as funcionalidades encontradas nas peças lógicas podem ser realizadas por meio de um método equivalente da API do mecanismo de jogo (que será abordada na seção "Usando a API do Game Engine - Interface de Programação do Aplicativo"). A API abrange desde tarefas que podem ser realizadas com tijolos lógicos, como alterar uma propriedade em um sensor ou remover completamente um objeto do jogo, até funcionalidades não disponíveis de outra forma, como reprodução de vídeos e conexão de rede.

>**Nunca esquecemos o primeiro patch**
>
> A habilidade de finalizar diretamente um objeto do Python foi introduzida no Blender 2.47. Este é um bom exemplo de como os métodos de script podem ser convenientes. E aí vem um pouco de história. . . em agosto de 2008, o projeto em que estávamos trabalhando, OceanViz (leia mais sobre ele nos Estudos de caso no Capítulo 10), exigia uma grande quantidade de objetos para aparecer e morrer dinamicamente. A simulação do motor de jogo tinha problemas críticos de desempenho e a otimização não era um luxo ali. Nesse ponto, reduzimos os objetos finais com um sensor de propriedade simples que acionaria um atuador Edit Object **  ** EndObject. Por enquanto, tudo bem. No entanto, um sensor extra rodando cada quadro para cada objeto na cena estava nos custando algum desempenho que poderíamos usar em outro lugar. (Estamos falando de centenas de objetos aqui.)
> Quando culpar nosso software não ajudou (pode eventualmente), era hora de sujar as mãos. Depois de muito trabalho e ajuda online, tivemos nossa primeira versão com patch do mecanismo de jogo do Blender funcionando bem na nossa frente. Não precisávamos mais desses sensores múltiplos porque um simples

>`myobjects.endObject()`

> estava fazendo o trabalho agora. (Onde está o champanhe?)
> Ter permissão para estender nossa própria versão do Blender dessa forma foi legal. Enviar o patch e implementá-lo no núcleo do Blender foi memorável.

Existem algumas razões para não ter todos os métodos acessíveis por meio de blocos lógicos. Primeiro, uma interface gráfica é muito limitada para codificação complexa. Você pode acabar com um sistema lento que está longe de ser otimizado. Em segundo lugar, ter métodos independentes da interface permite que ela seja expandida de forma mais fácil e constante (do ponto de vista do desenvolvimento). Alguns recursos avançados, como sistema de espelhamento, carregamento dinâmico de malhas, chamadas OpenGL e restrições personalizadas dificilmente caberiam na interface do mecanismo de jogo atual do Blender. Eles provavelmente acabariam não sendo implementados devido à quantidade de trabalho extra necessária. Outras coisas que você encontrará nos métodos integrados do mecanismo de jogo são: fazer capturas de tela; alterar as configurações do mundo (gravidade, taxas de tique lógico); acessar os dados retornados dos sensores (teclas pressionadas, posição do mouse); alterar as propriedades do objeto (lente da câmera, cores claras, massa do objeto); e muitos outros que iremos cobrir no decorrer deste capítulo.

### Use recursos que não fazem parte do Blender <a id="Use_Features_That_Are_Not_Part_of_Blender"></a>

Nenhum homem é uma ilha. Nenhum jogo é uma ilha (exceto _Monkey Island_). E a maneira mais fácil de integrar o seu jogo Blender com o mundo exterior é com Python. Se você deseja usar dispositivos externos para controlar a entrada do jogo ou vincular aplicativos externos ao seu jogo, você pode achar o Python adequado para essa tarefa.

Aqui estão alguns exemplos que mostram o que pode ser feito com bibliotecas externas Python:

- Pegue dados da Internet para a pontuação do jogo.

- Controle seu jogo com um controlador Nintendo Wiimote.

- Combine Head-tracking e displays imersivos para realidade aumentada.

Essas possibilidades vêm com a declaração anterior de que quase tudo o que você pode fazer com Python, você pode fazer no motor de jogo. E, como o Python pode ser usado com módulos escritos em outras linguagens (devidamente agrupados), você pode usar virtualmente qualquer aplicativo como base para seu sistema.

>**Plataforma cruzada, sim; Versão cruzada, não**
>
> Para usar bibliotecas externas, você deve saber a versão do Python com a qual foram construídas. A biblioteca Python que você está usando deve ser compatível com a versão Python que vem com seu Blender. Também é importante verificar com que frequência a biblioteca é atualizada e se será mantida no futuro.

### Acompanhe suas alterações com um sistema de controle de versão <a id="Keep_Track_of_Your_Changes_with_a_Version_Control_System"></a>

Se você pegar um arquivo do Blender em dois momentos diferentes de sua produção, terá dificuldade em encontrar o que mudou entre eles. Isso ocorre porque o formato de arquivo nativo do Blender é um tipo binário. Os arquivos binários são escritos de uma maneira que você não pode acessá-los diretamente [md] eles são projetados para serem acessados por programas e não por seres humanos.

Os scripts, por outro lado, são arquivos de texto simples. Você pode abrir um script em qualquer editor de texto e ver imediatamente as diferenças entre dois arquivos semelhantes. Encontrar essas diferenças é vital para avançar e retroceder em suas experimentações durante o trabalho. Na verdade, se você não deseja verificar as diferenças manualmente, pode considerar o uso de arquivos de script externos com um sistema de controle de versão como Git, SVN, Mercury ou CVN.

>**E a captura é ...**
>
> Isso funciona apenas para scripts mantidos fora do Blender. Este é um dos fortes motivos para preferir os controladores de módulo Python em vez dos controladores de script Python.

Um sistema de controle de versão permite que você alterne entre as versões de trabalho de seus arquivos de projeto. Torna-se relativamente seguro experimentar diferentes métodos de forma destrutiva. Em outras palavras, é um sistema para protegê-lo de você mesmo. Na Figura 7.3, você pode ver uma aplicação disso. Alguém alterou o arquivo de script online enquanto trabalhávamos localmente nele. Em vez de rastrear manualmente as diferenças, poderíamos usar uma ferramenta para mesclar as alterações em um novo arquivo e confirmá-lo. Estávamos usando TortoiseSVN para Windows aqui, uma interface gráfica para usar com um sistema SVN. Para sistemas Linux, a linha de comando svn mais o software "meld" funcionam da mesma forma.

![TortoiseSVN merging](../figures/Chapter7/Fig07-03.png)

### Depure o seu jogo durante a execução <a id="Debug_Your_Game_While_It_Runs"></a>

Linguagens interpretadas (também conhecidas como linguagens de script) são mais lentas que o código compilado. Portanto, para acelerar seu desempenho, eles são pré-compilados e armazenados em cache na primeira vez em que são executados (quando você inicia o jogo). Isso não é obrigatório, entretanto, e se você estiver usando scripts Python externos (em vez daqueles criados dentro do Blender), você pode usar o botão de depuração para recarregá-los toda vez que forem chamados.

Na Figura 7.4, temos o módulo scripts.reload\_me que será recarregado a cada quadro. Dessa forma, você pode alterar dinamicamente o conteúdo de seus scripts, variáveis e funções sem ter que reiniciar o jogo. Experimente você mesmo: copie o conteúdo da pasta\Book\Chapter7\1\_reloadme para o seu computador e execute debug\_python.blend. Jogue o seu jogo e você verá um cubo giratório. A velocidade do cubo é controlada pela 14ª linha do arquivo script.py, localizado na mesma pasta.

```python
 # edit the speed value and you will see the rotation changing

 # (try with values from 0.01 to 0.05)

 speed = 0.025
```

![Controladores de módulo Python](../figures/Chapter7/Fig07-04.png)

Sem fechar o Blender ou mesmo parar o jogo, abra o arquivo script.py em um editor de texto, altere esta linha para 0,05, por exemplo, e salve. Você verá a velocidade mudando imediatamente. Seu jogo está literalmente sendo atualizado em tempo de execução e você pode alterar qualquer módulo que tenha sido chamado com a opção de depuração ativada.

>**Desligue quando você sair**
>
> Lembre-se de desligar a depuração quando terminar com este script. Recarregar o script a cada quadro pode reduzir drasticamente o seu desempenho.

## Então, o que exatamente é Python? <a id="So_What_Exactly_Is_Python?"></a>

Agora que você está ciente de todos os benefícios de usar Python, é hora de entender o que é Python. Mais uma vez, não podemos examinar todos os aspectos da linguagem aqui. No entanto, uma visão geral ainda é desejável para ajudá-lo a entender os exemplos apresentados neste livro.

Para estudar seus scripts, você deve estar ciente dos seguintes aspectos:

- Tipos de dados flexíveis

- Recuo

- Programação Orientada a Objetos OOP [md]

### Tipos de dados flexíveis <a id="Flexible_Data_Types"></a>

Sempre que você escreve um programa, você deve usar variáveis para armazenar os valores alterados em tempo de execução. Ao contrário de linguagens como C e Java, as variáveis do Python são muito flexíveis: elas podem ser declaradas instantaneamente quando você as usa pela primeira vez; você pode atribuir diferentes tipos de dados para a mesma variável; e você pode até mesmo nomeá-los dinamicamente:

```python
for i in range(10): exec("var\_%d = %d" % (i,i))
```

Este fragmento de código é equivalente ao seguinte:

```python
var_1 = 1

var_2 = 3

var_3 = 3

(...)
```

Como você pode ver, os nomes das variáveis são criados no tempo de execução. Portanto, se você nomear seus objetos corretamente no arquivo do Blender, você pode armazená-los em variáveis nomeadas após eles. O fragmento de código a seguir atribui os objetos de cena (recuperados do mecanismo de jogo) a variáveis nomeadas após seus nomes.

```python
(...)

for object in scene.objects:

    exec("%s = \"object\" " % (object.name))
```

Embora tenhamos tipos de dados flexíveis, devemos respeitar os tipos de variáveis ao manipulá-los e transmiti-los/retorná-los às funções. Aqui você pode ver uma lista dos tipos de dados que encontrará na API do mecanismo de jogo do Blender:

- **Integer:** Este é o mais comum dos tipos numéricos. Ele pode armazenar qualquer número que caiba na memória do computador. Você pode realizar qualquer operação matemática regular nele, como soma, subtração, divisão, módulo e potência.

```python
 my_integer  = 112358132134
```

- **Float:** Este tipo é muito semelhante aos inteiros, mas possui uma gama de números que inclui frações. Se você dividir um número par pela metade, o Python converterá automaticamente seu número inteiro em um número flutuante.

```python
 simple_float = 0.5

 phi = (1 + math.sqrt(5)) / 2 # ~1.618
```

- **Boolean:** Tão simples quanto parece, este tipo de dados armazena um valor verdadeiro ou falso. Também pode ser entendido como um número inteiro com o valor de 1 ou 0.

```python
 i_am_enjoying_the_book = True

 i_am_understanding_the_book = i_am_enjoying_the_book - 1
```

- **List:** Uma lista contém um conjunto de elementos ordenados por índices crescentes. Embora o tamanho de uma lista possa mudar rapidamente, você não pode acessar um índice de lista que ainda não foi criado (isso irá travar o Python). A lista pode ter elementos mistos, como inteiros, strings e objetos.

```python
 my_list = [3.14159265359, "PI", True]
```

- **Tuple:** Este é outro tipo de lista onde os elementos não podem ser substituídos. Tal como acontece com as listas, você pode lê-las usando índices. Mas é mais comum acessar todos os valores de uma vez, atribuindo-os a diferentes variáveis.

```python
 t,u,p,l,e = (1,2,3,4,5) # works as: t = 1, u = 2, p = 3, ...
```

- **String:** Sempre que precisar armazenar um texto, você usará strings. Como as palavras são uma combinação de letras individuais, uma string consiste em caracteres individuais. Na verdade, strings podem ser entendidas como uma lista de caracteres porque você pode acessá-los usando seu índice de localização, embora não possa sobrescrevê-los (como em uma tupla).

```python
 python = "rulez"
```

- **Dictionary:** Como uma lista, um dicionário pode armazenar vários valores. Ao contrário de uma lista, um dicionário não se baseia no acesso ao índice numérico. Portanto, temos strings trabalhando como "chaves" para armazenar e recuperar as variáveis individuais. Na verdade, qualquer coisa pode ser uma chave para um dicionário, um número, um objeto, uma classe ...

```python
 _3d_software = {"name ": "Blender", "version": 2.6}
```

- **Custom Types:** São coisas como vetores e matrizes. O mecanismo de jogo combina alguns dos tipos de dados básicos para criar outros mais complexos. Eles são usados principalmente para vetores e matrizes. Dessa forma, você pode interagir matematicamente com eles de uma forma que os tipos básicos não farão.

```python
 mathutils.Vector(1,0,0) * object.orientation # the result is a Matrix
```

### Indentation <a id="Indentation"></a>

_Indentation[md]the amount of white spaces or tabs you leave before a new line._

Ao codificar em uma linguagem de programação específica, é obrigatório seguir sua sintaxe geral. Nesse sentido, Python é uma das linguagens mais restritas que existe. Pense nisso como um exame de gramática difícil. Você não conseguirá uma pontuação alta a menos que siga todas as regras gramaticais pré-estabelecidas. Agora imagine que poderia ser ainda pior [md] tão ruim quanto um documento legal escrito. Estamos falando de parágrafos rígidos, recuo, hierarquia de informações e regras semelhantes.

Como em um documento legal, essas regras têm uma razão de ser. Com forma / sintaxe estrita, você pode se concentrar mais no conteúdo do texto. E a ambiguidade no contexto da criação de código é fatal.

O recuo é o aspecto mais importante da sintaxe Python. O código Python usa o nível de indentação para definir onde os loops, as funções e o aninhamento geral começam/terminam. Dê uma olhada neste exemplo:

```python
1 def here_i_am(): # definition of the first function

2     print("I'm inside the first function.")

3 print("I'm outside the function.")

4 def but_I'm_not_here(): # definition of the second function

5     print("For you can't see me!")

6 print("I'm still outside the function.")

7 here_i_am() # calling the first function
```

Aqui estamos definindo uma função (1–2), chamando uma função de impressão embutida (3), definindo outra função (4–5), chamando outra função de impressão embutida (6) e, finalmente, chamando a primeira função que declarado (7).

A saída desse script será:

`I'm outside the function.`
`I'm still outside the function.`
`I'm inside the first function.`

A primeira coisa que você pode notar é que o Python é executado de cima para baixo. Portanto, você deve definir sua função antes de chamá-la. Em segundo lugar, você pode ver que a segunda função nunca é chamada. Então, como o interpretador de código pode determinar quais instruções de impressão chamar? A resposta é: recuo! Sempre que você altera o nível de recuo (linhas 1–2, 2–3, 4–5 e 5–6), você determina a relação hierárquica entre os elementos. Portanto, a linha 2 pertence à função definida na linha 1, da linha 5 à linha 4 e as outras linhas estão todas no mesmo nível.

Usar espaços ou tabulações em seus scripts é uma questão de preferência pessoal. Mas seja consistente [md] torna mais fácil copiar e colar seu código para reutilizá-lo.

>**Sinal de libra, eu (finalmente) te amo**
>
> Se, como eu, você nunca entendeu o motivo da tecla do número / jogo da velha (#) em seu telefone, você acabará considerando-a muito útil. Em Python, qualquer texto à direita de um sinal de libra é ignorado pelo interpretador. Portanto, o sinal de libra é usado para adicionar comentários ao seu código ou para desativar temporariamente parte dele.

### OOP - Programação Orientada a Objetos <a id="OOP_-_Object-Oriented_Programming"></a>

Como os jogos lidam com objetos do mundo 3D, faz sentido usar uma linguagem orientada para eles. O motor do jogo em si é escrito em C ++, uma linguagem muito forte e orientada a objetos, e os recursos Python OOP permitem que você manipule os dados do jogo de uma forma nativa do Python. Isso se reflete nos objetos do motor de jogo tendo seu próprio conjunto de funções e variáveis ​​acessadas diretamente de uma API Python (a ser explicado posteriormente neste capítulo na seção "Usando a API Game Engine - Interface de programação de aplicativo").

No código Python, você pode (e irá) criar suas próprias classes, módulos e elementos. Por exemplo, você pode querer controlar alguns elementos 3D como um grupo definido por seu código. Isso tornará mais fácil chegar a todos eles de uma vez. Portanto, você pode ter uma classe personalizada que armazenará todos os objetos relacionados que deseja acessar e preservará algumas propriedades como um grupo.

Abra o arquivo do livro: \Book\Chapter7\2\_oop\oop.blend

O primeiro script executado neste arquivo é o init \_world.py. Aqui estamos criando dois grupos para armazenar diferentes tipos de elementos (cubo e esfera). Para ordenar os objetos entre os grupos, percorremos toda a lista de objetos da cena e verificamos se há objetos com uma propriedade "cubo" ou "esfera" e os acrescentamos às suas respectivas listas.

```python
# ############### #

#  init\_world.py  #

# ############### #

import bge
from bge import logic as G
from bge import render as R

# showing the mouse cursor
R.showMouse(True)

# storing the current scene in a variable
scene = G.getCurrentScene()

# define a class to store all group elements and the click object
class Group():
    def __init__(self, name):
        self.name = name
        self.click = None
        self.objects = []

# create new element groups
cube_group   = Group("cubes")
sphere_group = Group("sphere")

# add all objects with an "ui" property to the created element
for obj in scene.objects:
    if "cube" in obj:
        cube_group.objects.append(obj)
    elif "sphere" in obj:
        sphere_group.objects.append(obj)
    elif "click" in obj:
        exec("%s\_group.click = obj" % (obj["click"]))

G.groups = {"cube":cube_group, "sphere":sphere_group}
```

Após armazená-los no módulo global `bge.logic`, esperamos que o usuário clique no cubo ou esfera no meio da cena. Quando isso acontecer, ele alternará o valor da propriedade on/off do cubo ou esfera. O seguinte script (que executa todos os quadros) irá então ocultar/mostrar os objetos do grupo de acordo.

```python
## ################## #

# visibility\_check.py #

# ################### #

from bge import logic

# defines a function to hide/turn visible all the objects passed as argument
def change_visibility(objects, on_off):
    for obj in objects:
        obj.visible = on_off

# retrieve the stored groups to local variables
cube_group   = logic.groups["cube"]
sphere_group = logic.groups["sphere"]

# read the current value of the "on\_off" property in the cube/sphere
cube_visible   = cube_group.click["on\_off"]
sphere_visible = sphere_group.click["on\_off"]

# calls the function into the group object with the visibility flag
change_visibility(cube_group.objects, cube_visible)
change_visibility(sphere_group.objects, sphere_visible)
```

E terminamos com essa interação. Brinque com o arquivo adicionando novos elementos (tubos, aviões, macacos) e faça com que eles interajam como temos aqui. Algumas cópias e pastas devem ser suficientes para adaptar este código à sua nova situação. Lembre-se de observar o recuo atual usado.

## Onde aprender Pythonn <a id="Where_to_Learn_Python"></a>

Se você tiver experiência anterior com outra linguagem de programação, aprenderá Python rapidamente. Se você ler alguns tutoriais básicos do Python, olhar alguns exemplos de script e verificar a API do mecanismo de jogo do Blender, isso pode ser o suficiente. Mas se aprender Python é seu primeiro passo na experiência de codificação, não se preocupe. Reserve um tempo para ler o básico da linguagem, comece com as tarefas mais simples e nunca desista.

Normalmente, uma boa maneira de começar é ajustando scripts prontos para uso, o que não exige que você entenda todos os aspectos da linguagem antes de seus primeiros experimentos. Além disso, dá a você um bom impulso motivacional, produzindo resultados rápidos para seus esforços. Recomendamos que você primeiro aprenda Python e depois se concentre em sua aplicação no mecanismo de jogo. Mas você pode se sentir mais confortável mexendo com os arquivos do mecanismo de jogo primeiro e depois aprendendo Python mais profundamente.

### Online Material <a id="Online_Material"></a>

Abaixo estão alguns sites onde você pode aprender mais sobre Python.

_www.python.org_

Aprenda sobre as novas versões do Python, mudanças na API e documentação do módulo.

_www.blender.org/documentation/blender_python_api_2_66_release/#game-engine-modules_

Documentação oficial da API BGE [md] todos os módulos integrados que podem ser usados com o motor de jogo.

_www.blenderartists.org/forum_

No fórum Blender Artists [md], você pode encontrar bons exemplos de scripts na seção Python (geral, Blender Python) e na seção do mecanismo de jogo do Blender.

[_www.diveintopython3.net_](http://www.diveintopython3.net)

Dive Into Python 3 cobre o Python 3 e suas diferenças com o Python 2. Um livro completo disponível online.

### Offline Material <a id="Offline_Material"></a>

Aqui estão alguns outros recursos para ajudá-lo a aprender Python.

_Learning Python,_ by Mark Lutz and David Ascher, published by O'Reilly Media

Você pode aprender Python em uma semana com este livro. Você também pode encontrá-lo como um e-book, o que é útil para pesquisas rápidas. Tente obter a edição mais recente do livro que encontrar. Diferentes séries Python (2.x, 3.x) têm certas particularidades com as quais você não deseja lidar.

>**Antes de comprar um livro**
>
> Se você for comprar um livro de Python, esteja ciente de seu público-alvo. Alguns livros são escritos para pessoas com absolutamente nenhum conhecimento prévio em linguagens de programação, enquanto outros assumem o contrário. E certifique-se de que o livro cobre a versão do Python que está incluída no Blender (no momento da escrita, Python 3.2).

_Yo Frankie! DVD www.yofrankie.org_

Um jogo aberto feito com o motor de jogo da Fundação Blender. Você pode baixar todos os arquivos deste projeto gratuitamente e revisar seus scripts. Embora isso possa ser confuso para alguém nas primeiras fases de aprendizagem do Python, é um bom material de referência para mais tarde.

### Ajuda integrada do Python <a id="Python_Built-in_Help"></a>

Você também pode acessar a ajuda diretamente no Python.

```python
dir(python_object)
```

A função Python "dir" cria uma lista com todas as funções/módulos/atributos disponíveis para serem acessados a partir deste objeto.

```python
help(python_function)
```

Esta função embutida revela a documentação oficial para este módulo ou tipo de dados.

## Python e o mecanismo de jogo <a id="Python_and_the_Game_Engine"></a>

Todo este capítulo está organizado em três partes principais: por que, o quê e como. Portanto, se você leu desde o início, já tem motivos sólidos para começar a usar scripts em seu projeto e entende o que é Python. A parte final deste capítulo cobrirá como usar seu conhecimento Python dentro do motor de jogo. Esta parte é dividida em quatro submódulos:

- Integrando Python no motor de jogo.

- Escrevendo seus scripts Python.

- Desenhando seu roteiro.

- Usando a API Game Engine.

### Integrando Python no Game Engine <a id="Integrating_Python_in_the_Game_Engine"></a>

No mecanismo de jogo, a interface do script é centrada no controlador por design. Portanto, você pode considerar o script Python simplesmente como um controlador mais complexo para substituir os controladores Expression ou Boolean. Nesses casos, o script ficará responsável por controlar como os sensores se relacionam com os atuadores de um determinado objeto. Na verdade, os sensores, atuadores e até mesmo o objeto de onde você está chamando o script são todos atributos do controlador.

Como mencionamos anteriormente, com um script Python você pode controlar dispositivos externos, controlar vários objetos de uma vez e muito mais. No entanto, você nunca estará livre de usar uma estrutura de tijolo lógico. E da combinação de blocos lógicos, sensores individuais, sensores globais e atuadores, a elegância de seu sistema surgirá.

No primeiro exemplo, você encontrará um estudo de caso muito simples de como fazer seu controlador Python funcionar. Ele cobrirá o comportamento básico de receber entrada de sensores no script e disparar atuadores a partir dele.

Abra o arquivo \Book\Chapter7\3\_template\abracadabra.blend.

![Abracadabra](../figures/Chapter7/Fig07-05.png)

Inicie o jogo e mantenha a barra de espaço pressionada. Na Figura 7.5, você pode ver o resultado antes e depois de pressionar a tecla. Você pode ler o texto girando? Pode não ser impressionante, mas certamente é didático. Aqui está o script por trás desse efeito:

```python
import bge
from bge import logic

cont = logic.getCurrentController()
owner = cont.owner
scene = logic.getCurrentScene()
objects = scene.objects
text_obj = objects["Text"]

sens = cont.sensors['my\_sensor']
act = cont.actuators['my\_actuator']

if sens.positive:
    cont.activate(act)
    text_obj.text = "CADABRA"
else:
    cont.deactivate(act)
    text_obj.text = "ABRA"
```

Este script é disparado a partir de um sensor de teclado, executado a partir de um controlador no objeto de câmera, ativa um atuador na própria câmera e altera uma propriedade no objeto de texto. A Figura 7.6 mostra blocos lógicos para este.

![Tijolos lógicos simples com um controlador Python](../figures/Chapter7/Fig07-06.png)

Vejamos desde o início:

```python
import bge
from bge import logic
```

As primeiras linhas importam o módulo bge e depois a lógica do submódulo. Não é grande coisa aqui. Na verdade, não precisamos importar explicitamente o módulo bge, pois estamos importando um submódulo diretamente. No entanto, não custa nada fazer. As linhas 4 e 5 armazenarão o controlador atual em uma variável e criarão um ponteiro para o objeto de onde foi chamado (conhecido como _owner_). Não estamos usando a variável owner aqui, mas é bom estar familiarizado com ela. Você o usará muito.

```python
cont = logic.getCurrentController()
owner = cont.owner
```

As linhas a seguir obtêm mais elementos do jogo para serem usados no script: cena lhe dará acesso direto à cena atual; objetos é a lista atual a ser usada posteriormente; text\_obj é um elemento da lista de objetos (acessado por seu nome no Blender).

```python
scene = logic.getCurrentScene()
objects = scene.objects
text_obj = objects["Text"]
```

Lembra quando dissemos que o motor de jogo é centrado no controlador? Todos os sensores e atuadores são acessados a partir do controlador, não do objeto ao qual pertencem (seu proprietário), como você pode esperar. As linhas 11 e 12, respectivamente, leem a lista de sensores e atuadores integrados para obter os que estamos procurando.

```python
sens = cont.sensors['my\_sensor']
act = cont.actuators['my\_actuator']
```

De forma semelhante a como funcionam os tijolos lógicos, vamos ativar o atuador se o sensor disparar positivo e desativá-lo caso contrário. A desativação ocorre no quadro após o sensor deixar de validar, por exemplo, a tecla não é pressionada ou o botão do mouse é liberado.

```python
if sens.positive:
    cont.activate(act)
else:
    cont.deactivate(act)
```

Não estamos restritos a controlar apenas atuadores, no entanto. As linhas 15 e 18 alteram o texto do objeto quando você pressiona/solta a barra de espaço:

```python
15  text_obj.text = "CADABRA"

18  text_obj.text = "ABRA"
```

Este arquivo pode ser simples, mas contém a essência do design da arquitetura do motor de jogo. Agora é um bom momento para revisar os três arquivos de modelo do mecanismo de jogo que vêm com o Blender. Vá para Editor de Texto  Modelos  GameLogic \ * e passe algum tempo estudando esses exemplos. Você também pode obtê-los nos arquivos do livro em \Book\Chapter7\3\_template\.

### Escrevendo seus scripts Python <a id="Writing_Your_Python_Scripts"></a>

Se você ainda não iniciou seus próprios scripts, agora é um bom momento para fazê-lo. Você precisará de um editor de texto, dos módulos da API documentados e de uma boa maneira de testar seus arquivos.

#### Editores de texto. <a id="Text_Editors"></a>

É importante encontrar um editor de scripts com o qual você ache agradável trabalhar. Os recursos mais importantes que você procura são: coloração e realce de sintaxe, recuo automático e preenchimento automático. Você pode encontrar editores com ainda mais recursos do que esses, então experimente diferentes alternativas e decida o que é melhor para você.

>**Notepad? Notepad++**
>
>A maioria dos scripts apresentados neste capítulo foi codificada usando o Notepad ++. Este editor de texto de código aberto baseado no Windows não é específico para Python, mas lida bem com o realce da sintaxe Python. Você pode baixar o Notepad ++ do site:
> http://notepad-plus.sourceforge.net
> Se você estiver usando Linux ou OSX, existem muitas alternativas nativas que podem atendê-lo ainda melhor.

##### Editor de Texto do Blender <a id="Blender_Text_Editor"></a>

Como você provavelmente sabe, o Blender tem seu próprio editor de texto interno (veja a Figura 7.7). Embora possa não ser tão poderoso quanto um software desenvolvido exclusivamente para essa tarefa específica, pode ser muito conveniente. É útil para testes rápidos, pequenos scripts ou quando você deseja manter tudo empacotado dentro do arquivo do Blender. Aqui estão seus principais recursos:

- Realce de sintaxe

- Tamanhos de fonte dinâmicos

- Conversão de recuo (espaços para tabulações e vice-versa)

- Contagem de linha e navegação

- Pesquise vários arquivos internos

- Sincronizar com arquivos externos

![Editor de texto interno do Blender](../figures/Chapter7/Fig07-07.png)

#### Material de referência e documentação <a id="Reference_Material_and_Documentation"></a>

Como a API Python do mecanismo de jogo está disponível online, você tem uma desculpa oficial para manter um navegador da Web aberto enquanto trabalha. Não é uma má ideia manter uma versão offline dele também. (Você pode encontrá-lo nos arquivos do livro.) Use-o quando precisar ser mais produtivo e a Internet estiver atrapalhando (como sempre).

É bom começar a reunir materiais de exemplo da Internet e mantê-los organizados. Se você usar o recurso append no Blender para navegar e importar arquivos de texto de sua "coleção", você nem precisará abrir outro aplicativo Blender. Além disso, se você for consistente com seu estilo de nomenclatura, regras de recuo e estruturas de arquivo, será fácil reutilizar seus próprios scripts.

#### Testando seus scripts <a id="Testing_Your_Scripts"></a>

Não importa o quão fácil é o Python, você passará noites testando e testando novamente seus scripts antes de fazê-los funcionar corretamente. A maneira mais completa de testar seu script é reproduzi-lo dentro do mecanismo de jogo. No entanto, você pode não querer carregar seu jogo toda vez que precisar ter certeza de alguma sintaxe Python, funções embutidas dos tipos de dados ou simplesmente verificar se a matemática de um resultado está correta.

Nesses casos, você pode usar um intérprete interativo para ajudá-lo. Se você tem o Python instalado em seu sistema, você já o tem. Se você estiver usando o Windows, este será o aplicativo python.exe em seu diretório de instalação do Python (C:\Python31\ por padrão, considerando a instalação do Python 3.1), conforme visto na Figura 7.8. No Linux ou OSX, você precisa digitar "python" em qualquer console e pronto.

![Python IDE](../figures/Chapter7/Fig07-08.png)

Você também pode usar o console do Blender Python. Mude uma de suas janelas atuais para o console e você verá a tela mostrada na Figura 7.9.

![Blender Python console](../figures/Chapter7/Fig07-09.png)

Agora você pode usá-lo para digitar códigos simples ou para executar uma ajuda ou um diretório em qualquer um dos módulos Python. Infelizmente, apenas os módulos do Blender têm o autocompletar funcionando a partir daí.

Outra estratégia importante é manter o desenvolvimento de novas funcionalidades fora do arquivo principal. Por exemplo, se você precisa desenvolver um sistema de navegação (como faremos em breve), você não precisa usar seu cenário real grande e de alta textura. Definitivamente, não para os primeiros testes. Se você mantiver sistemas independentes que funcionam juntos, você será capaz de identificar erros de forma mais rápida e fácil e até mesmo transferir correções para outros projetos sem problemas.

### Projetando Seu Script Python - Exemplo de Estudo <a id="Designing_Your_Python_Script_-_Study_Example"></a>

Agora vamos mergulhar em um exemplo de como escrever e planejar um script Python para o mecanismo de jogo do zero. Assumiremos que você já cobriu todos os fundamentos do script Python e o entendimento geral da parte interna do mecanismo de jogo para que possamos prosseguir para seu uso real. Mais especificamente, vamos revisar o processo de escrita de um sistema de navegação por câmera para um passo a passo de visualização arquitetônica. Este estudo de caso é na verdade o sistema desenvolvido para um projeto comercial de um projeto de livro italiano. Em geral, precisávamos implementar um sistema para navegar e interagir em um modelo virtual de um templo dórico italiano. Aqui, no entanto, vamos desenvolvê-lo em uma sandbox e reaplicá-lo em outro arquivo, emulando o que você poderia fazer com seus próprios projetos.

Ao contrário das câmeras de jogos, um passeio virtual pode usar um sistema de navegação muito simples composto de (1) um modo de órbita para ver o exterior do edifício; (2) um modo de caminhada para navegar dentro do edifício com simulação de gravidade e colisão; (3) e um modo de voo para explorar livremente o ambiente virtual apenas com colisão. O outro requisito era tornar o sistema o mais portátil possível e com o mínimo de peças lógicas.

Todos esses aspectos devem ser considerados desde as primeiras fases do processo de codificação. Com um design bem definido, você pode planejar o sistema mais eficiente a curto e longo prazo.

>**Lápis e papel, ativos valiosos de codificação**
>
> Um dos momentos mais marcantes durante meus estudos de codificação foi na Blender Conference 2008. Eu ainda estava em meus primeiros passos de aprendizagem de codificação C ++ e OpenGL e tive a chance de explicar um bug do motor de jogo para Brecht van Lommel [md] a um programador de Blender realmente experiente e reconhecido e uma pessoa muito inspiradora. O bug em si era difícil de explicar pela Internet; é o que está por trás da implementação das coordenadas do canvas para filtros 2D apresentadas no Capítulo 5. Fiquei bastante satisfeito com sua opinião sobre isso, mas ainda mais impressionante foi vê-lo codificar uma solução parcial bem na minha frente.

> Nesse ponto, aprendi uma lição importante. Não importa o quão avançada e técnica seja a codificação em que você está trabalhando; você sempre pode se divertir esboçando suas idéias e planos com lápis e papel antiquados. Foi assim que ele resolveu o problema, estabelecendo claramente as ideias e organizando-as de forma lógica. Nunca me esqueci disso [md] obrigado, Brecht!

O sistema consistirá em uma câmera para o modo de órbita e uma para ser usada para o modo voar e andar. Cada modo funciona conforme descrito na Tabela 7.1.

_Tabela 7.1 Comparação de diferentes câmeras de navegação_

|                                  | Órbita        | caminhar         | voar   |
|:--------------------------------:|:-------------:|:----------------:|:------:|
| Ângulo de Rotação Vertical (Z)   | -200º à  200º | Livre            | Livre  |
| Ângulo de Rotação Horizontal (X) | 10º à 70º     | -15º to 45º      | Livre  |
| Movendo o Pivot                  | Nenhuma       | Empty            | Empty  |
| Pivô de rotação horizontal       | Empty         | Empty e Camera   | Camera |
| Pivô de rotação vertical         | Empty         | Empty            | Empty  |

- **Empty:** é um objeto vazio ao qual a câmera é parente.


>**Experimente**
>
> Para ilustrar melhor, você pode ver o sistema de trabalho demonstrado no arquivo do livro: \Book\Chapter7\4\_navigation\_system\camera\_navigation.blend.
> Para alternar entre os modos, pressione 1, 2 ou 3. Isso mudará o modo para orbitar, andar e voar, respectivamente. Para navegar, você pode usar o mouse e as teclas WASD.

#### Elementos do mundo 3D <a id="3D_World_Elements"></a>

Abra o arquivo \Book\Chapter7\4\_navigation\_system\camera\_navigation.blend.

Você encontrará duas câmeras e diferentes objetos vazios na primeira camada:

- scripts - um vazio para chamar todos os scripts.

- CAM_Move - a câmera para o modo andar e voar.

- CAM_Orbit - a câmera para o modo de órbita.

- CAM_back, CAM_front, CAM_side, CAM_top - esvazia para armazenar a posição e orientação das câmeras do jogo.

- MOVE_PIVOT - o pivô para a câmera walk and fly.

- ORB_PIVOT - o pivô para a câmera orbital.

Na segunda camada, você encontrará as malhas de colisão [md] do solo e os elementos verticais. Tudo é muito simples aqui, já que só precisamos testar o sistema, e para isso alguns obstáculos de baixo polímero funcionam bem.

#### Entendendo o Código <a id="Understanding_the_Code"></a>

/Book/Chapter7/4_navigation_system/camera_navigation.py

Este programa está dividido em cinco partes diferentes:
1. Inicialização global,
2. Gerenciamento de eventos,
3. Funções internas,
4. Interação do jogo,
5. Mais Python.

O diagrama da Figura 7.10 ilustra como eles se relacionam. Agora, vamos dar uma olhada em cada um deles.

![Arquitetura de Script](../figures/Chapter7/Fig07-10.png)

##### Inicialização Global <a id="Global_Initialization"></a>

`camera_navigation.init_world()`

Existe uma função que é carregada uma vez no início do jogo; nós o chamamos de "init world" [md] init \_world dentro de scripts.py. Vamos verificar a opção de prioridade no controlador Python para garantir que este script seja executado em cima de todos os outros. Nesta função, você encontrará primeiro a inicialização global. Vamos armazenar na lógica do módulo global todos os elementos que vamos reutilizar nos scripts. Dessa forma, não precisamos obter a lista de objetos toda vez que precisarmos de um determinado objeto. Uma técnica comum é armazenar o objeto da cena também. Portanto, para cada cena, você pode executar um script no início do jogo que armazena uma referência à cena atual globalmente:

```python
33 G.scenes = {"main":G.getCurrentScene()}

34 objects = G.scenes["main"].objects
```

>**Salve e Carregue um Jogo com GlobalDict**
>
> Uma vez que a lógica do módulo é acessível a partir de todas as funções e todas as cenas, ela pode ser usada para armazenar objetos "globais". Se precisar preservar esses objetos e variáveis entre as sessões do jogo (ou seja, depois de fechar o jogo), você pode armazená-los dentro do dicionário logic.globalDict e usar logic.saveGlobalDict () e logic.loadGlobalDict () para salvá-lo e carregá-lo .

Para armazenar as informações da câmera, vamos primeiro criar um dicionário global denominado câmeras. Vamos usá-lo para armazenar os objetos da câmera, seu pivô e a orientação original do pivô da órbita:

```python
43     G.cameras = {}

44     # orbit camera

45     camera = objects["CAM\_Orbit"]

46     pivot = objects["ORB\_PIVOT"]

47     G.cameras["ORB"] = [camera, {"orientation":pivot.worldOrientation}, pivot]

48     # fly/walk camera

49     camera = objects["CAM\_Move"]

50     pivot = objects["MOVE\_PIVOT"]

52     G.cameras["MOVE"] = [camera, {"orientation":pivot.worldOrientation, "position":pivot.worldPosition}, pivot]
```

Agora que instanciamos nossos objetos, podemos definir os valores iniciais para nossas funções, como as restrições de rotação da câmera. Não queremos que as câmeras olhem para o subsolo; portanto, precisamos definir manualmente nossos limites. Embora pudéssemos definir esses limites diretamente nas funções de órbita e aparência, ter todos os parâmetros na mesma parte do código é mais fácil de ajustar (e um pouco mais rápido, pois não precisam ser reatribuídos a cada quadro).

>**Arquivo de configurações externas**
>
> Outro fluxo de trabalho comum é ter um arquivo python separado (por exemplo, settings.py) com todas as variáveis definidas. Então, em seu script de trabalho, você simplesmente precisa fazer: import settings.py e use e.g. settings.left.

```python
       # Camera Orbit settings:

58     # angle restriction in degrees

59     left = -220.0

60     right = 220.0

61     top = 70.0

62     bottom = 10.0

63

64     # convert all of them to radians

65     left = m.radians(left)

       (. . .)

70     # store them globally

71     G.orb_limits = {"left":left, "right":right, "top":top, "bottom":bottom}

72

       # Camera Walk/Fly settings:

       (. . .)
```
       
Por último, mas não menos importante, precisamos criar as variáveis que vamos ler e escrever entre as funções. Inicializá-los aqui nos permite lê-los desde o primeiro frame do jogo. Isso é especialmente importante para variáveis que serão usadas nas funções de gerenciamento de eventos - para diferentes valores de nav_mode e walk_fly, iremos executar diferentes funções para o movimento da câmera.

```python
103 G.walk_fly = "walk"

104 G.nav_mode = "orbit"
```

##### Gestão de Eventos <a id="Event_Management"></a>

```python
camera_navigation.mouse_move

camera_navigation.keyboard
```

Além do sensor Always necessário para a função `camera_navigation.init_world ()`, existem dois outros sensores de que precisamos - um teclado e um sensor de mouse. Toda a interação que você terá com este sistema de navegação será executada por meio dessas funções.

###### scripts.mouse\_move <a id="scripts.mouse_move"></a>

Vamos primeiro dar uma olhada no sistema de controle do sensor do mouse:

```python
210 def mouse_move(cont):

211     owner = cont.owner

212     sensor = cont.sensors["s\_movement"]

213

214     if sensor.positive:

215         if G.cameras["CAM"] == "ORB":

216             orbit_camera(sensor)

217         else:

218             look_camera(sensor)
```

Vamos primeiro dar uma olhada no sistema de controle do sensor do mouse:

```python
def mouse_move():
    cont = G.getCurrentController()
```

###### scripts.keyboard <a id="scripts.keyboard"></a>

A segunda função de gerenciamento de eventos trata das entradas do teclado. Esta função recebe a entrada do sensor e chama funções internas de acordo com a tecla pressionada. Se a tecla pressionada for W, A, S ou D, movemos a câmera. Se a chave for 1, 2 ou 3, nós a trocamos.

```python
110 def keyboard(cont):

111     owner = cont.owner

112     sensor = cont.sensors["s\_keyboard"]

113

114     if sensor.positive:

115         keylist = sensor.events

117         for key in keylist:

118             value = key[0]

119

120             if G.cameras["CAM"] == "MOVE":

121                 if value == GK.WKEY:

122                     # Move Forward

123                     move_camera(0)

124                elif value == GK.SKEY:

125                    # Move Backward

126                     move_camera(1)

127                 elif value == GK.AKEY:

128                     # Move Left

129                     move_camera(2)

130                 elif value == GK.DKEY:

131                     # Move Right

132                     move_camera(3)

133

134            # CAMERA SWITCHING

135            if value == GK.ONEKEY:

136                change_view("orbit", "orbit")

137            elif value == GK.TWOKEY:

138                change_view("front")

139            elif value == GK.THREEKEY:

140                change_view("top", "fly")

    (...)
```

>**Por um mundo com menos peças lógicas**
>
> Se você não quiser usar um sensor de teclado, pode usar uma instância interna do módulo de teclado. Você pode ler sobre isso na seção "API bge.logic" posteriormente neste capítulo ou na página da API online: _http://www.blender.org/documentation/blender\_python\_api\_2\_66\_release/bge.logic.html # bge.logic.keyboard._

##### Funções Internas <a id="Internal_Functions"></a>

```python
scripts.move_camera

scripts.orbit_camera

scripts.look_camera
```

Essas três funções são chamadas a partir das funções de gerenciamento de eventos. Em suas falas, você encontra a matemática responsável pelo movimento da câmera. Estamos chamando-as de "funções internas" porque são a ponte entre as entradas dos sensores e as saídas no mundo do motor de jogo.

###### scripts.move\_camera <a id="scripts.move_camera"></a>

A função responsável pelo movimento da câmera é muito simples. No modo andar e voar, vamos mover o pivô na direção desejada (que é passada como argumento). Portanto, primeiro precisamos criar um vetor para este curso. Se você não está familiarizado com matemática vetorial, pense em vetor como a direção entre a origem [0, 0, 0] e as coordenadas do vetor [X, Y, Z].

```python
336 def move_camera(direction):

338     if not G.cameras["CAM"] == "MOVE": return

339     MOVE = 0.25 # speed

340

341     if direction == 0: # Forward

342         vector = M.Vector([0, 0, -MOVE])

344     elif direction == 1: # Backward

345         vector = M.Vector([0, 0, MOVE])

347     elif direction == 2: # Left

348         vector = M.Vector([-MOVE,0,0])

350     elif direction == 3: # Right

351         vector = M.Vector([MOVE, 0, 0])

   (...)

356     # now that we calculated the vector we can move the pivot

357     # to be continued in the Game Interaction section
```

Aqui, o vetor é o movimento que precisamos aplicar ao pivô para fazê-lo se mover. O tamanho do vetor (MOVE) atuará como intensidade ou velocidade do movimento.

###### scripts.orbit\_camera <a id="scripts.orbit_camera"></a>

Decidimos usar métodos diferentes para a câmera walk/fly e a de órbita. Na câmera de órbita, cada posição na tela corresponde a uma orientação da câmera.

Se você deseja estudar esta parte do script em particular, pode ativar o cursor do mouse no painel de renderização. Dessa forma, você pode ver que a mesma posição do cursor irá (ou deverá) sempre gerar a mesma visualização.

```python
224 def orbit_camera(sensor):

228     # Get screen size, attributes from the sensor and global variables

229     screen_width = R.getWindowWidth()

230     screen_height= R.getWindowHeight()

231

232     win_x, win_y = sensor.position

233

234     # G.orb_clamp is in radians

235     orb_limits   = G.orb_limits

236     left_limit   = orb_limits["left"]

237     right_limit  = orb_limits["right"]

238     bottom_limit = orb_limits["bottom"]

239     top_limit    = orb_limits["top"]

240

241     # Normalizing x to run from left to right limits

242     x = win_x / screen_width

243     x = left_limit + (x * (right_limit - left_limit))

244

245     # Normalize y to run from top to bottom limits

246     y = win_y / screen_height

247     y = top_limit + (y * (bottom_limit - top_limit))

248

249     # Flip the vertical movement

250     y = m.pi/2 - y

251

254     # Calculate the new orientation matrix

255     mat_ori = G.cameras["ORB"][1]["orientation"]

256

257     mat_x = M.Matrix.Rotation(x, 3, 'Z')

258     mat_y = M.Matrix.Rotation(y, 3, 'X')

259

260     ori = mat_x * mat_y

261

262     # now we can use ori as our new orientation matrix

264     # to be continued in the Game Interaction section

        (...)
```
        
As primeiras linhas que merecem nossa atenção aqui são a operação de normalização. Normalizar um valor significa convertê-lo em um intervalo de 0,0 a 1,0. No nosso caso, pode ser entendido como as coordenadas do ponteiro do mouse em relação às dimensões da tela (largura e altura):

```python
242     x = win_x / screen_width
```

>**Mesmo menos blocos lógicos e coordenadas normalizadas do mouse**
>
> É importante sempre usar coordenadas normalizadas para suas operações de tela. Caso contrário, diferentes resoluções da área de trabalho produzirão resultados diferentes em um jogo. Como um caso de contra-ataque, você pode precisar das coordenadas absolutas para eventos de mouse se quiser garantir áreas clicáveis ​​mínimas para seus eventos.

> Você nem sempre precisa normalizar as coordenadas do mouse manualmente. Como o sensor do teclado, você pode substituir o sensor do mouse por uma instância interna do módulo do mouse.

> As coordenadas de bge.logic.mouse vão de 0,0 a 1,0 e podem ser lidas a qualquer momento. (Você pode até vincular seu script a um sensor Always, deixando o sensor de Mouse para os momentos em que estiver usando mais peças lógicas.)

> Você pode ler sobre isso na seção "API bge.logic" neste capítulo ou na página da API online: _http://www.blender.org/documentation/blender_python_api_2_66_release/bge.logic.html#bge.logic.keyboard_

Agora, uma operação simples para converter o valor normalizado em um valor dentro de nossa faixa de ângulo horizontal (-220º a 220º):

```python
243     x = left_limit + (x * (right_limit - left_limit))
```

Executamos a mesma operação para a coordenada vertical do mouse. Embora você deva estar ciente de que a altura da tela vai do topo (0) para o fundo (altura), isso é diferente do que poderíamos esperar (ou das coordenadas OpenGL, por exemplo). Para entender melhor a operação de inversão (linha 257), você pode primeiro comentar / descomentar o código para ver a diferença.

A seguir encontre no arquivo .blend o pivô vazio (ORB \ _PIVOT) e brinque com sua rotação no eixo X. A rotação é demonstrada na Figura 7.11. Portanto, se subtrairmos nosso ângulo de 90º (__PI__/2 em radianos), obtemos o ângulo adequado para girar o pivô verticalmente.

```python
250     y = m.pi/2 – y
```

![Rotação do pivô de órbita](../figures/Chapter7/Fig07-11.png)

###### scripts.look\_camera <a id="scripts.look_camera"></a>

A função de girar a câmera caminhar/voar é bastante diferente da órbita. Não temos mais uma relação direta entre as coordenadas do mouse e a rotação da câmera. Aqui obtemos a posição relativa do cursor (do centro) e depois forçamos o mouse a ser centralizado novamente [md] para evitar o movimento contínuo, a menos que o mouse seja movido novamente.

Para obter a posição relativa do cursor, a função de normalização precisa ser diferente. Desta vez, queremos que o centro da tela seja 0,0 e as bordas extremas da tela (borda da janela do jogo) sejam -0,5 e 0,5.

```python
291     x = (win_x / screen_width)  - 0.5

292     y = (win_y / screen_height) - 0.5
```

Os valores de x e y podem ser usados diretamente como ângulos radianos para girar a câmera. No entanto, quando estamos caminhando, queremos restringir a visão verticalmente. Esta decisão de design significa que precisamos limitar o ângulo de visão a um intervalo máximo e mínimo. Claro, isso transforma amarrar seus sapatos em um desafio de circo. Embora possa parecer um exagero, essa limitação ajuda a adicionar um melhor senso de realidade ao nosso sistema de navegação.

A solução é obter o ângulo vertical da câmera atual e ver se, adicionando o novo ângulo (ou seja, movimento vertical do mouse), acabaríamos ultrapassando o limite de 45º. Nesse caso, fixamos o novo ângulo para respeitar esse valor. Para obter o ângulo vertical, lembre-se de que o pivô da câmera (um objeto vazio) está sempre paralelo ao solo. Portanto, o ângulo vertical pode ser extraído da matriz de orientação local da câmera. Se isso ainda não fizer sentido para você, tente encontrar alguns tutoriais de matemática 3D online).

```python
302     # limit top - bottom angles

303     if G.walk_fly == "walk":

304         angle = camera.localOrientation[2][1]

305         angle = m.asin(angle)

306

307     # if it's too high go down. if it's too low go high

308         if (angle + y) > top_limit: y = top_limit - angle

309         elif (angle + y) < bottom_limit: y = bottom_limit - angle
```

Para o projeto real para o qual este foi originalmente projetado, acabamos movendo o código da câmera de órbita para ser um subconjunto do andar/voar. Ter o mouse sempre centralizado é útil quando você tem uma interface de usuário em cima disso e precisa alternar entre o clique do mouse e a rotação da câmera. Embora os métodos sejam diferentes, os resultados são os mesmos.

##### Game Interaction <a id="Game_Interaction"></a>

```python
camera_navigation.change_view
```

E o resultado das funções:

```python
camera_navigation.move_camera

camera_navigation.look_camera

camera_navigation.orbit_camera
```
Na seção anterior, vimos como os ângulos e direções foram calculados com Python. No entanto, deliberadamente pulamos a parte mais importante: aplicá-lo aos elementos do motor de jogo. Inclui a ativação de atuadores (como fazemos na função change\_view ()) ou a interferência direta em nossos elementos de jogo (câmeras e pivôs).

###### Outcome of the functions: scripts.move\_camera, scripts.look\_camera, and scripts.orbit\_camera <a id = "Outcome_of_the_functions_scripts.move_camera, _scripts.look_camera, _and_scripts.orbit_camera"></a>

Vamos juntar as peças agora. Já sabemos a orientação e a posição futura da câmera. Portanto, não há quase nada a ser calculado aqui. No entanto, existem maneiras distintas de alterar a posição e orientação do objeto.

Em move_camera (), vamos usar um método de instância do objeto pivô chamado applyMovement (vector, local). Isso faz parte dos métodos do mecanismo de jogo (outro é applyRotation que você verá a seguir) que explicamos mais tarde neste capítulo na seção "Usando a API do mecanismo de jogo". Esta função embutida traduz o objeto usando o vetor passado como parâmetro. Pode ser relativo às coordenadas locais ou mundiais:

```python
336 def move_camera(direction):

    (. . .)

356     # now that we calculated the vector we can move the pivot

357     pivot = G.cameras["MOVE"][2]

358     pivot.applyMovement(vector, True)
```

De forma semelhante na função look_camera (), vamos aplicar a rotação no objeto de câmera. Isso tem a vantagem de evitar os aborrecimentos da matemática, matrizes e orientações 3D. Além disso, em vez de calcular manualmente a nova matriz de orientação em Python, podemos contar com a implementação nativa do motor de jogo C ++ (ou seja, rápida) para essa tarefa.

```python
269 def look_camera(sensor):

    (. . .)

314     if G.walk_fly == "walk":

315         # Look Up rotation

316         camera.applyRotation([y,0,0], 1)

317

318         # Look Side rotation

319         pivot.applyRotation([0, -x, 0], 1)
```

Embora estejamos deixando o cálculo matemático para o motor de jogo, ainda devemos estar cientes de como ele funciona. A rotina applyRotation () funciona com ângulos de Euler (como uma máquina de cardan). Os efeitos para os modos andar e voar são muito semelhantes. A única diferença é se a rotação é local ou global e o eixo para girar:

```python
322     else: # G.walk_fly == "fly"

323         # Look Side rotation

324         pivot.applyRotation([0, 0, -x], 0)

325

326         # Look Up rotation

327         pivot.applyRotation([y, 0, 0], 1)
```

Na função orbit_camera (), calculamos a matriz de orientação do pivô. Essa matriz nada mais é do que uma maneira matemática sofisticada de descrever uma rotação. Como já temos a matriz, tudo o que precisamos fazer é configurá-la para nossa orientação de pivô.

A orientação é uma variável embutida do Python que pode ser lida e escrita diretamente por nosso script. Falaremos mais sobre isso na parte "Usando a API Game Engine - Interface de programação de aplicativo" deste capítulo.

```python
223 def orbit_camera(sensor):

    (...)

261     # now we can use ori as our new orientation matrix

262     pivot = G.cameras["ORB"][2]

263     pivot.orientation = ori
```

###### scripts.change\_view <a id="scripts.change_view"></a>

Depois que o usuário pressiona uma tecla (1, 2 ou 3) para alterar a visualização, chamamos a função change \ _view () para alternar para a nova câmera (com um parâmetro especificando qual câmera usar). Esta função consiste em duas partes: primeiro, definimos a posição e a orientação corretas para a câmera e o pivô; em segundo lugar, mudamos a câmera atual para a nova.

>**Decompondo a orientação da vista**
>
> Lembre-se que a orientação desejada (armazenada no vazio e acessada através do dicionário G.views) representa a nova orientação da vista. Em nosso sistema, esta orientação de vista é a combinação da orientação do objeto pai (pivô) com a orientação filho (câmera).

Vamos começar de forma simples e aumentar à medida que avançamos. Primeiro a câmera de órbita: no modo de órbita a câmera fica parada [md] sua posição nunca muda. Tudo o que precisamos fazer é redefinir a orientação do pivô para seus valores iniciais. Sua orientação foi globalmente armazenada de volta na função init \_world (). Portanto, agora podemos recuperá-lo e aplicá-lo ao pivô:

```python
155         dict = G.cameras["ORB"]

157         pivot = dict[2]

158         pivot.orientation = dict[1]["orientation"]
```

A câmera da mosca é ligeiramente diferente. Neste caso, a orientação da câmera não contém rotação (ou seja, uma matriz de identidade). Portanto, cabe à orientação do pivô corresponder à orientação da vista. Em outras palavras, a matriz de orientação do pivô é exatamente a mesma que a matriz de orientação da vista:

```python
169         pivot.position = G.views[view].position

170         pivot.orientation = G.views[view].orientation

171         camera.orientation = [[1,0,0],[0,1,0],[0,0,1]]

177         if G.walk_fly == "walk":

178             fly_to_walk()
```

Para a câmera de caminhada, temos mais uma situação. O modo de onde estamos vindo (voar) tem a orientação do pivô da câmera (igual a camera.worldOrientation) como a orientação de vista atual. No entanto, para o modo de caminhada, o pivô precisa estar paralelo ao solo.

Para isso, precisamos girá-lo alguns graus para alinhá-lo com o horizonte. A câmera agora estará olhando para um ponto diferente (acima / abaixo da direção original). Para realinhar a câmera com a orientação da vista, precisamos girar a câmera na direção oposta. Dessa forma, o pivô e as rotações da câmera se anulam (com a vantagem de ter o pivô agora devidamente alinhado com o solo).

```python
190 def fly_to_walk():

    (...)

194     view_orientation = camera.worldOrientation

195     euler = view_orientation.to_euler()

196     angle = euler[0] - (m.pi/2)

197

198     pivot.applyRotation([-angle,0,0],1)

199     camera.applyRotation([angle,0,0],1)
```

>**Raciocínio por trás do design**
>
> Há outra razão para manter isso como uma função separada. Originalmente, planejava alternar os modos (andar/voar), mantendo a mesma posição e visão da câmera. Apesar de ter abandonado a ideia, decidi manter o sistema flexível em caso de qualquer mudança nos acontecimentos (clientes [md] quem entende o que pensam?).

Agora que a nova câmera e o pivô estão na posição e orientação corretas, podemos trocar as câmeras com eficácia. Para isso, primeiro configuramos a nova câmera no atuador Scene Set Camera. Em seguida, ativamos o atuador e a câmera mudará:

```python
181     act_camera.camera = dict[0]

182     cont.activate(act_camera)
```

##### Mais Python <a id="More_Python"></a>

```python
scripts.collision_check

scripts.stick_to_ground
```

O sistema de script mostrado até agora lida com toda a interação dos sensores do motor do jogo aos elementos do mundo 3D. Mesmo que isso cubra a maioria das partes de uma arquitetura de script típica, eu estaria mentindo se dissesse que isso é tudo o que você fará em seus projetos. Freqüentemente, você precisará de um script chamado de vez em quando que lida diretamente com os dados do mecanismo de jogo. No nosso caso, teremos dois "PySensors" para controlar a colisão e fixar nossa câmera no chão enquanto caminhamos.

Poderíamos ter os dois trabalhando ligados a um sensor Always. No entanto, isso não seria muito eficiente. Como só precisamos deles enquanto caminhamos e voamos, eles podem ser integrados ao pipeline do sensor do teclado. A função stick \ _to \ _ground () será chamada depois que qualquer tecla for pressionada se o modo atual for "andar":

```python
142         if G.nav_mode == "walk" and G.walk_fly == "walk":

143             stick_to_ground()
```

O sistema de colisão pode ser usado ainda mais especificamente. Dentro da função move \ _camera (), usaremos o teste de colisão para validar ou descartar nosso vetor móvel:

```python
353         # if there is any obstacle reset the vector

354         vector = collision_check(vector, direction)
```

Se o teste de colisão\_check () encontra algum obstáculo na frente da câmera, ele retorna um vetor nulo ([0, 0, 0]). Caso contrário, ele deixa o vetor como foi definido, o que moverá a câmera.

O código dessas funções é muito específico para este projeto; portanto, não entraremos em mais detalhes aqui. (No entanto, recomendamos que você dê uma olhada no código completo no arquivo do livro). No entanto, o ponto principal é entender o papel dessas funções na arquitetura do script. Esses scripts podem complementar a funcionalidade de outras funções, para governar seu jogo de forma global e direta, ou simplesmente para amarrar as coisas.

#### Re-usando Seu Script <a id="Reusing_Your_Script"></a>

Uma das razões pelas quais este sistema foi projetado com tanto cuidado é a necessidade de portabilidade. Você não quer reescrever um sistema de navegação sempre que tiver um novo projeto. Isso não é específico para este exemplo de script. Freqüentemente, você reciclará seus próprios scripts para adaptá-los a novos arquivos. Vamos repassar alguns princípios que você deve conhecer.

##### Organização de arquivos - grupos e camadas <a id="File_Organization_-_Groups_and_Layers"></a>

A primeira coisa a ter em mente é a aparência do arquivo final. Você deseja que o sistema de script seja mesclado com o resto do arquivo existente do Blender? Você deseja mantê-los em cenas separadas (muito comum para interfaces de usuário)? Você precisará acessar/editar os elementos do sistema de script posteriormente?

No nosso caso, não há necessidade de uma cena extra. No entanto, precisamos ter certeza de que os elementos do sistema de navegação são de fácil acesso (especialmente os vazios com as posições das câmeras). Se você pode dedicar uma camada exclusivamente aos elementos do sistema de navegação, faça-o. Certifique-se de que a camada desejada esteja vazia no arquivo de modelo e que todos os objetos que deseja importar estejam contidos nesta camada.

Se não for possível ter todos os seus elementos em uma única camada, você pode criar um grupo para eles. Dessa forma, você sempre pode isolá-los rapidamente para serem listados no outliner e selecionados individualmente. A outra vantagem de usar grupos é durante a importação. É mais fácil selecionar um grupo a ser importado do que percorrer todos os objetos individuais, determinando qual deles deve ser importado e qual faz parte do ambiente de teste (que geralmente não precisa ser importado).

##### Ajustes e ajustes - Sujar as mãos <a id="Tweaks_and_Adjustments_-_Getting_Your_Hands_Dirty"></a>

Abra o arquivo /Book/Chapter7/4_navigation_system/walkthrough_1_base/walkthrough.blend

Este pequeno arquivo é parte da apresentação de um passo a passo arquitetônico de um projeto urbano (ver Figura 7.12) que eu (Dalai) fiz. É um projeto acadêmico e apenas meu segundo projeto usando o motor de jogo. Como você pode ver, não há absolutamente nenhum script nele [md] toda a interação é feita com blocos lógicos. Não usei Python para este projeto principalmente porque não tinha absolutamente nenhum conhecimento de Python naquela época (e o projeto foi concluído em seis dias).

![Arquivo de exemplo de explicação arquitetônica](../figures/Chapter7/Fig07-12.png)

É hora de redenção. Vamos substituir seu sistema de navegação pelo sistema Python que acabamos de estudar. Por conveniência, este arquivo já estava organizado para receber os elementos de navegação (câmeras, vasilhames, etc.).

###### Organize e anexe seu arquivo <a id="Organize_and_Append_Your_File"></a>

Neste caso, decidimos agrupar todos os elementos de navegação em um grupo chamado NAVIGATIONSYSTEM e ter certeza de que estão todos na camada 1. Você pode usar o Outliner para ter certeza de que não perdeu nenhum objeto fora do grupo. Deixe as lâmpadas e os objetos de colisão fora do grupo.

Para ver um instantâneo do arquivo neste momento, você pode encontrá-lo nos arquivos do livro em: /Book/Chapter7/4_navigation_system/walkthrough_2_partial/camera_navigation.blend

Agora abra o arquivo de explicação passo a passo novamente e anexe o NAVIGATIONSYSTEM que criamos. É importante não vincular o grupo, mas anexá-lo. Os elementos vinculados só podem ser movidos em seus arquivos originais; portanto, você deve evitá-los neste caso.

1. Abra a caixa de diálogo Anexar objetos (Shift + F1).

2. Encontre o grupo NAVIGATIONSYSTEM dentro do arquivo camera_navigation.

3. Certifique-se de que a opção "Grupos de instâncias" não esteja marcada. (Isso inseriria o grupo, não os elementos individuais.)

4. Clique em "Link / Anexar da Biblioteca". (Isso adicionará o grupo.)

5. Defina CAM_Orbit como a câmera padrão. (Dica: use o Outliner para encontrar o objeto; ele está dentro do ORB\_PIVOT.)

Um instantâneo com essas mudanças pode ser encontrado em: /Book/Chapter7/4_navigation_system/walkthrough_2_partial/walkthrough.blend

Agora, se você executar o aplicativo, o sistema de navegação deve funcionar - mais ou menos (consulte a Figura 7.13).

![Ainda não ai](../figures/Chapter7/Fig07-13.png)

###### Ajustes in Loco <a id="Adjustments_in_Loco"></a>

Como você pode ver na Figura 7.13, o novo sistema de câmeras parece absurdamente errado. Existem duas razões principais para isso: os elementos do arquivo de passo a passo estão distantes da origem do arquivo [0, 0, 0] e as câmeras não estão preparadas para um projeto com essa magnitude (seus parâmetros de recorte são muito baixos). Precisaremos mover os objetos para seus novos lugares corretos, ajustar os parâmetros da câmera e fazer uma pequena intervenção no arquivo de script:

Todos os elementos do grupo NAVIGATIONSYSTEM (camada 1):

Mova-os 2.000 em X e 350 em Y.

**Empties** :

- CAM_front e CAM_back - Esses empties manterão a posição das câmeras de caminhada. Certifique-se de que a posição deles a partir do solo esteja nos olhos humanos (~ 1,68).

- CAM_top e CAM_side - Esses empties serão usados no modo Fly. Aqui, também devemos ter certeza de que sua orientação inicial parece boa. A maneira mais fácil de fazer isso é usando o modo Fly (selecione o objeto, defina-o como câmera atual e use Shift + F).

A única coisa que falta para a câmera é aumentar a distância de recorte. Dessa forma, podemos ver todo o skydome ao redor da câmera (veja antes e depois na Figura 7.14).

**Cameras** :

- CAM_Orbit - Ajuste o Z inicial, mude o final do clipe para 1000.

- CAM_Move - mude o clipe que termina em 1000.

Um snapshot com essas mudanças pode ser encontrado em:

/Book/Chapter7/4_navigation_system/walkthrough_3_partial/walkthrough.blend

| Camera clipping of 400    | Camera clipping of 1000   |
|:-------------------------:|:-------------------------:|
![Camera clipping of 400](../figures/Chapter7/Fig07-14a.png)  |  ![Camera clipping of 1000](../figures/Chapter7/Fig07-14b.png)

>**Certifique-se de que a colisão está configurada corretamente**
>
> Todas as casas, o solo e os outros objetos 3D já têm a colisão habilitada neste arquivo. Em outras situações, no entanto, você pode precisar alterar os objetos de colisão, habilitando ou desabilitando suas colisões de acordo. O raycast Python usa o mecanismo interno Bullet Physics sob o capô. Para evitar que a câmera atravesse as paredes e o solo, defina superfícies de colisão suficientes (mas não muito, para não comprometer o desempenho do jogo).

###### Ajustes de script <a id="Script_Tweaks"></a>

Finalmente, é bom mexer um pouco no script. Devido às particularidades deste projeto (principalmente sua escala), você pode sentir que tudo acontece um pouco rápido demais. Depende de você alterar as configurações na função `init_world`. Além disso, seria interessante explorar vários pontos de vista para esta apresentação. Já posicionamos os vasilhames laterais e traseiros. Embora não os estivéssemos usando anteriormente, seus nomes estão presentes no script como parte da lista de câmeras disponíveis:

```python
93     available_cameras = ["front", "back", "side", "top"]
```

A diferença agora é que faremos a câmera realmente mudar para as visualizações lateral e traseira quando você pressionar as teclas quatro e cinco, respectivamente. Como você pode ver aqui, é muito fácil expandir um sistema como este. Tente criar uma quinta câmera (adicione um novo vazio) e veja como funciona. Para habilitar as câmeras "lateral" e "posterior", o único código que precisamos adicionar é:

```python
110 def keyboard(cont):

    (. . .)

new             elif value == GK.FOURKEY:

new                 change_view("side")

new             elif value == GK.FIVEKEY:

new                 change_view("back", "fly")
```

Não há muito mais a ser feito aqui. Este é um script simples, mas sua estrutura e o fluxo de trabalho que apresentamos não são muito diferentes do que você encontrará em sistemas mais complexos que você pode ter que implementar ou trabalhar. Existem diferentes maneiras de implementar um sistema de navegação. Este foi projetado com foco em uma estrutura didática (código limpo em oposição a um sistema altamente otimizado que é difícil de ler) e robustez (fácil de expandir). Tente encontrar outros exemplos ou, melhor ainda, crie um você mesmo.

O arquivo final está nos arquivos do livro como:

/Book/Chapter7/4_navigation_system/walkthrough_4_final/walkthrough.blend.

### Usando a API Game Engine - Interface de Programação de Aplicativo <a id="Using_the_Game_Engine_API_-_Application_Programming_Interface"></a>

A API do mecanismo de jogo é uma ponte que conecta seus scripts Python aos dados do jogo. Por meio desses módulos, métodos e variáveis, você pode interagir com seus blocos lógicos, objetos de jogo e funções gerais de jogo existentes.

A documentação oficial pode ser encontrada online no site da Blender Foundation:

_http://www.blender.org/documentation/blender_python_api_2_66_release_

Vamos agora percorrer os destaques dos módulos. Depois de se familiarizar com suas principais funcionalidades, você deve se sentir confortável para navegar pela documentação e encontrar outros recursos.

**Módulos internos do motor de jogo**

- Game Logic (bge.logic)

- Tipos de jogos (bge.types)

- Rasterizer (bge.render)

- Chaves de jogo (bge.events)

- Textura de vídeo (bge.texture)

- Restrições físicas (bge.constraints)

- Dados do aplicativo (bge.app) // TODO

**Módulos autônomos**

- Sistema de áudio (aud)

- Tipos e utilitários matemáticos (mathutils)

- Wrapper OpenGL (bgl)

- Desenho de fonte (blf)

#### bge.logic <a id="bge.logic"></a>

O módulo principal é uma mistura de funções utilitárias, configurações globais do jogo e substituições de blocos lógicos. Algumas dessas funções já foram abordadas no tutorial, mas estão aqui novamente por uma questão de conveniência. Veremos alguns dos destaques.

##### getCurrentController() <a id="getCurrentController()"></a>

Retorna o controlador atual. Isso é usado para obter uma lista de sensores e atuadores (para verificar o status e desativar, respectivamente) e o objeto ao qual o controlador pertence:

```python
controller  = bge.logic.getCurrentController()

object = controller.owner

sensor = controller.sensors['mysensor']
```

Se você estiver usando módulos Python em vez de scripts Python diretamente (consulte Controlador Python), o controlador é passado como um argumento para a função:

```python
def moduleFunction(cont):
    object = cont.owner
    sensor = cont.sensors['mysensor']
```
    
##### getCurrentScene() <a id="getCurrentScene()"></a>

Esta função retorna a cena atual a partir da qual o script foi chamado. O uso mais comum é fornecer uma lista de todos os objetos do jogo:

```python
for object in bge.logic.getCurrentScene().objects: print(object)
```

##### expandPath() <a id="expandPath()"></a>

Se você precisa acessar um arquivo externo (imagem, vídeo, Blender, etc.), você precisa primeiro obter seu caminho absoluto no computador. Use uma barra invertida (/) para separar as pastas e uma barra invertida dupla (//) se precisar se referir à pasta atual:
```python
video_absolute_path  = bge.logic.expandPath('//videos/video01.ogg')
```

##### sendMessage(), addScene(), start/restart/endGame(), <a id="sendMessage(),_addScene(),_start/restart/endGame()"></a>

Essas funções copiam a funcionalidade de atuadores existentes. Eles são a substituição do Python para aqueles eventos globais quando você precisa de uma maneira direta de chamá-los, contornando os blocos lógicos.

##### LibLoad(), LibNew(), LibFree(), LibList() <a id="LibLoad(),_LibNew(),_LibFree(),_LibList()"></a>

Existem casos em que você precisa carregar o conteúdo de um arquivo externo do Blender durante a execução. Isso é conhecido como _carregamento dinâmico._ O mecanismo de jogo oferece suporte ao carregamento dinâmico de ações, malhas ou cenas completas. Os novos blocos de dados são mesclados com a cena atual e se comportam como objetos internos:

```python
bge.logic.LibLoad("//entities.blend", "Scene")
```

>**Cuidado com as lâmpadas**
>
> Novos objetos Lamp podem ser carregados dinamicamente de arquivos externos. No entanto, no modo GLSL, eles não funcionarão como fonte de luz para os shaders de material, uma vez que os shaders precisariam ser recompilados para isso.

##### globalDict, loadGlobalDict(), saveGlobalDict() <a id="globalDict,_loadGlobalDict(),_saveGlobalDict()"></a>

O bge.logic.globalDict é um dicionário Python que está vivo durante todo o jogo. É um local de jogo para armazenar dados se você precisar reiniciar o jogo ou carregar um novo arquivo (nível) e precisar salvar algumas propriedades. Na verdade, você pode até salvar o globalDict com o arquivo do Blender durante o jogo e recarregar mais tarde.

```python
bge.logic.globalDict["password"] = "kidding, kids never save your passwords in files!"

bge.logic.saveGlobalDict() # save globalDict externally

bge.logic.loadGlobalDict() # replace the current globalDict with the saved one
```

##### keyboard <a id="keyboard"></a>

Você pode controlar todas as entradas do teclado diretamente de um script. O uso e a sintaxe são muito semelhantes aos do sensor do teclado. Você precisa de um script que execute todos os tiques lógicos (Sensor sempre pulsando com frequência 0 ou toda vez que uma tecla é pressionada; sensor de teclado com "Todas as teclas" definido) onde você pode ler o status de todas as teclas no bge.logic. teclado. dicionário de eventos. Se, em vez de consultar o status de uma tecla específica (por exemplo, se a barra de espaço for pressionada), você quiser listar todas as teclas pressionadas, pode usar o dicionário bge.logic.keyboard.active \ _events.

As teclas para ambos os dicionários de eventos são as mesmas que você usa com o sensor do teclado (consulte o módulo bge.events). O status de cada tecla (se foi pressionada, liberada, mantida pressionada ou nada) é o valor armazenado no dicionário. Os valores das chaves são definidos no próprio módulo bge.logic:

```python
keyboard = bge.logic.keyboard

space_status = keyboard.events [bge.events.SPACEKEY]

if space_status == bge.logic.KX_INPUT_JUST_ACTIVATED:

    print("space key was just pressed.")

elif space_status == bge.logic.KX_INPUT_ACTIVE:

    print("space key is still pressed.")

elif space_status == bge.logic.KX_INPUT_JUST_RELEASED:

    print("space key was just released.")

else: # bge.logic.KX_INPUT_NONE

    pass
```
    
Um arquivo de amostra pode ser visto em \Book\Chapter7\5\_game\_keys\key\_detector\_python.blend. Isso mostra a maneira mais centrada em Python de lidar com o teclado. Para obter o método clássico de usar um sensor de teclado, procure mais neste capítulo na seção "bge.events".

##### mouse <a id="mouse"></a>

Semelhante ao teclado, este objeto Python pode funcionar como um substituto para o sensor do Mouse. Existem algumas diferenças que o tornam ainda mais atraente para scripts [md] em particular, o fato de que as coordenadas do mouse já estão normalizadas. Conforme explicamos no tutorial, isso ajuda a obter resultados consistentes, independentemente da resolução da área de trabalho. Os atributos disponíveis são:

- **events:** Um dicionário com todos os eventos do mouse (clique com o botão esquerdo, roda para cima e assim por diante) e seus status (por exemplo, bge.logic.KX_INPUT_JUST_ACTIVED).

- **position** : Posição normalizada do cursor do mouse na tela (de [0,0] a [1,1]).

- **visible** : Mostrar/ocultar o cursor do mouse (também pode ser definido no painel Render para o estado inicial).

##### joysticks <a id="joysticks"></a>

Esta é uma lista de todos os joysticks compatíveis com o seu computador. Isso significa que a lista é preenchida principalmente por objetos None e alguns, se houver, objetos Python de joystick. Para imprimir o índice, nome, número de eixo e botões ativos dos joysticks conectados, você pode fazer:

```python
for i in bge.logic.joysticks:

    joystick = bge.logic.joysticks[i]

    if joystick and joystick.connected:

        print(i, joystick.name, joystick.numAxis, joystick.activeButtons)
```
        
Para obter a lista completa de todos os parâmetros suportados pelo objeto Joystick python, visite a API oficial: _http://www.blender.org/documentation/blender\_python\_api\_2\_66\_release/bge.types.SCA\_JoystickSensor.html_

Um arquivo de amostra pode ser encontrado em \Book\Chapter7\joystick.blend.

##### Outros <a id="Others"></a>

Existem ainda mais funções disponíveis neste módulo (setMist, getLogicTicRate e setGravity, por exemplo). Certifique-se de visitar a documentação online (ou a documentação incluída nos arquivos do livro) para ver todos eles.

#### bge.types <a id="bge.types"></a>

Objetos, malhas, blocos lógicos e até sombreadores são todos tipos de jogos diferentes. Cada vez que você chama uma função interna de um deles, você está acessando uma dessas funções. Isso acontece quando você obtém a posição de um objeto, altera o valor de um atuador e assim por diante.

Cada uma das aulas tem a mesma anatomia. Você pode acessar métodos e variáveis de instância. Para explicar seu uso de maneira adequada, examinaremos um dos módulos mais usados, o objeto de jogo.

Algumas das variáveis só funcionarão dentro do contexto correto. Portanto, você não pode obter a posição do mouse de um sensor de mouse se o sensor ainda não foi acionado. Esteja ciente do contexto certo e do tipo de jogo.

##### Class KX\_GameObject <a id="Class_KX_GameObject"></a>

Se você executar um print (dir (objeto)) dentro do seu script, obterá uma lista muito confusa. Inclui métodos internos Python, métodos de instância e variáveis de instância. A maioria deles é comum a todos os objetos, então vamos falar sobre eles primeiro. No entanto, lâmpadas e câmeras não apenas herdam todos os métodos de objetos do jogo, mas também os estendem com métodos específicos.

>**A verdade está lá fora**
>
>Para ver todos os métodos disponíveis, consulte a documentação. Estamos cobrindo apenas alguns deles aqui.

###### Métodos internos Python <a id="Python_Internal_Methods"></a>

`__class__, __doc__, __delattr__ . . .`

A maioria desses métodos são herdados do objeto Python com o qual estamos lidando. Entretanto, dada a natureza das classes Python apresentadas no Blender, alguns desses métodos podem não ser totalmente acessíveis. É improvável que você os use. Por enquanto, é seguro ignorar qualquer método que comece e termine com sublinhados duplos (__ignoreme__).

###### Instance Methods <a id="Instance_Methods"></a>

`endObject(), rayCast(), getAxisVect(), suspendDynamics(), getPropertyNames() . . .`

Se parecer uma função, deveria ser. Cada objeto do motor de jogo fornece um conjunto de funções para interagir com eles ou deles para os outros. Aqui estão alguns métodos que você deve conhecer:

- **rayCast (objto, objfrom, dist, prop, face, xray, poly)**

_ "Olhe de um ponto/objeto para outro ponto/objeto e encontre o primeiro objeto atingido em dist que corresponda a prop."_

Este método é uma versão mais completa de rayCastTo (). Possui tantas aplicações que fica difícil delimitar seu uso. Por exemplo, esse foi o método usado para calcular a colisão no script do sistema de navegação que estudamos anteriormente.

- **getPropertyNames()**

_"Get a list of all property names."_

Depois de recuperar a lista de nomes de propriedades, você pode usá-la para ver se o objeto tem uma propriedade específica antes de usá-lo. Para obter propriedades individuais, você pode usar _if "prop" in object_: ou _object.get("prop", default=None)_.

>**Um uso para propriedades**
>
>As propriedades têm vários usos no motor de jogo. Um desses usos é marcar um objeto a ser identificado pelo script Python. Por que não usar seus nomes? Enquanto os nomes funcionam bem para recuperar objetos individuais, as propriedades permitem que você marque e acesse vários objetos de uma vez. Francamente, é mais fácil criar uma coleção de MP3 organizada, nomeada e marcada do que encontrar tempo para nomear corretamente todos os seus blocos de dados do Blender [ms], objetos, malhas, materiais, texturas, imagens e assim por diante.

- **endObject()**

_"Excluir este objeto pode ser usado no lugar do EndObject Actuator."_

Este método é uma das funções que imitam atuadores existentes. Você também encontrará esse design em métodos como sendMessage (), setParent () e replaceMesh ().

- **applyRotation()**

_"Defina o movimento/rotação do objeto do jogo."_

Existem alguns métodos que o deixarão livre de fazer matemática 3D manualmente. Este em particular é um substituto para a multiplicação da matriz de orientação de objeto por uma matriz de rotação. (Se você for da "velha escola", ainda pode definir a matriz de orientação diretamente.)

Outros métodos são applyMovement (), applyForce (), applyTorque (), getDistanceTo (), getVectTo (), getAxisVect () e alignAxisToVect ().

###### Variáveis de instância <a id="Instance_Variables"></a>

`_name, position, mass, sensors, actuators . . ._`

Por último, mas definitivamente não menos importante, temos as variáveis embutidas. Eles funcionam como parâmetros internos do objeto (por exemplo, nome, posição, orientação) ou objetos de classe vinculados a ele (por exemplo, pai, sensores, atuadores). Nas versões do Blender anteriores a 2.49, essas variáveis eram acessíveis apenas por meio de um conjunto de instruções get e set (setPosition (), getOrientation () e assim por diante). No Blender 2.5, 2.6 e em diante, eles não só podem ser acessados diretamente, mas também manipulados como qualquer outra variável, lista, dicionário, vetor ou matriz que você possa ter:

```python
obj.mass = 5.0

obj.worldScale *= 2

obj.localPosition [2] += 3.0

obj.worldOrientation.transpose()

print(obj.worldTransform)
```

- **position, localPosition, worldPosition**

Posição é um vetor [x, y, z] com a localização do objeto na cena. Podemos obter a posição absoluta (worldPosition) ou a posição relativa ao pai do objeto (localPosition). E que tal acessar a variável de posição diretamente? Ele está obsoleto, mas você pode encontrá-lo em arquivos antigos que encontrar online. Se você acessar a variável de posição diretamente, obtém a posição mundial na leitura e define a posição local na escrita. Está confuso? É por isso que está obsoleto;)

- **orientation, localOrientation, worldOrientation**

Esta variável dá acesso a uma matriz 3x3 com a orientação do objeto. A matriz de orientação é o resultado da transformação de rotação de um objeto e da influência de seu objeto pai. Assim como a posição, a variável de orientação fornecerá a orientação mundial na leitura e definirá a orientação local na escrita. Assim como com a posição, você sempre deve especificar se deseja a orientação local ou mundial.

- **visible**

Temos diferentes maneiras de definir a visibilidade de um objeto. Se o seu material não estiver definido como invisível no painel do jogo, você pode usar este método. Para alterar a visibilidade recursivamente (para os filhos do objeto), você deve usar o método setVisibility.

- **sensors, controllers, actuators**

Todos os blocos lógicos de um objeto podem ser acessados por meio desses dicionários. O nome do sensor / controlador / atuador será usado como a chave do dicionário, pois é importante nomeá-los corretamente.

###### Sub-Class KX\_Camera <a id="Sub-Class_KX_Camera"></a>

Nem todos os objetos têm acesso aos mesmos métodos e variáveis. Por exemplo, um objeto vazio não tem massa e um objeto estático não tem torque.

Quando o objeto é uma câmera, a diferença é ainda mais nítida. O objeto de câmera tem sua própria classe derivada de KX_GameObject. Ele herda todas as variáveis e métodos de instância e os expande com seus próprios. Você encontrará algumas funções de espaço de tela (getScreenPosition (), getScreenVect (), getScreenRay ()), alguns métodos de frustum (sphereInsideFrustum (), boxInsideFrustum (), pointInsideFrustum ()) e algumas variáveis de instância (lente, perto, longe, frustum_culling , world_to_camera, camera_to_world).

###### Sub-Class KX\_Lamp <a id="Sub-Class_KX_Lamp"></a>

Assim como as câmeras, as lâmpadas também têm sua própria subclasse. Ele herda todas as variáveis e métodos de instância e apenas expande as variáveis disponíveis.

Os parâmetros que podem ser alterados com Python incluem tudo o que pode ser animado com o atuador Action: energia, cor, distância, atenuação, tamanho do ponto e mistura do ponto. Além disso, você pode alterar a camada da lâmpada em tempo de execução.

#### bge.render <a id="bge.render"></a>

Se compararmos os jogos com a arte 3D tradicional, o rasterizador seria a fase de renderização do processo. Internamente, é quando toda a geometria é finalmente desenhada para a tela com o cálculo de luz, os filtros aplicados e o conjunto de telas. Por esse motivo, o módulo Rasterizer apresenta funções relacionadas à estereoscopia, gerenciamento de janelas e mouse, configurações mundiais e configurações globais de material GLSL.

##### Janela e Mouse <a id="Window_and_Mouse"></a>

`getWindowWidth() / getWindowHeight()`

Obtenha a largura/altura da janela (em pixels).

`showMouse(visible)`

Habilite ou desabilite o cursor do mouse do sistema operacional.

`setMousePosition(x, y)`

Defina a posição do cursor do mouse (em pixels).

##### Configurações mundiais <a id="World_Settings"></a>

`setBackgroundColor(rgba), setAmbientColor(rgb)`

Defina a cor do ambiente e do plano de fundo.

`setMistColor(rgb), disableMist(), setMistStart(start), setMistEnd(end)`

Defina as configurações de névoa (névoa).

##### Configurações estéreo <a id="Stereo_Settings"></a>

`getEyeSeparation() / setEyeSeparation(eyesep)`

Obtenha a separação atual dos olhos para o modo estéreo. Normalmente, a distância focal/30 fornece um valor confortável.

`getFocalLength() / setFocalLength(focallength)`

Obtenha a distância focal atual para o modo estéreo. Ele usa a distância focal atual da câmera como valor inicial

##### Configurações de material <a id="Material_Settings"></a>

`getMaterialMode(mode) / setMaterialMode(mode)`

Get/set the material mode to use for OpenGL rendering. The available modes are:

`KX_TEXFACE_MATERIAL, KX_BLENDER_MULTITEX_MATERIAL, KX_BLENDER_GLSL_MATERIAL`

`getGLSLMaterialSetting(setting) / setGLSLMaterialSetting(setting, enable)`

Get/set the state of a GLSL material setting. The available settings are:

`"lights", "shaders", "shadows", "ramps", "nodes", "extra\_textures"`

##### Others <a id="Others"></a>

`drawLine(fromVec, toVec, color)`

Draw a line in the 3D scene.

`enableMotionBlur(factor) / disableMotionBlur()`

Enable/disable the motion blue effect.

`makeScreenshot(filename)`

Write a screenshot to the given filename.

#### bge.events <a id="bge.events"></a>

The Keyboard sensor allows you to set individual keys. As you can see in Figure 7.15, it can also be triggered by any key once you enable the option "All Keys." This is very useful to configure text input in your game or to centralize all keyboard events with a single sensor and script.

![Key codes visualizer](../figures/Chapter7/Fig07-15.png)

In this case, every key pressed into a Keyboard sensor, will be registered as a unique integer. Each number corresponds to a specific key, and finding them allows you to control your actions accordingly to the desired key map. In order to clarify this a bit more, try the file in /Book/Chapter7/5_game_keys\key_detector_logicbrick.blend.

This file is similar to the key\_detector\_python.blend we used to demonstrate bge.logic.keyboard. However, this file is using the Keyboard sensor directly, instead of its wrapper.

```python
from bge import logic
from bge import events
cont = logic.getCurrentController()
owner = cont.owner
sensor = cont.sensors["s\_keyboard"]

if sensor.positive:
    # get the first pressed key
    pressed_key = sensor.events[0][0]
    text = "the key number is: %d\n" % pressed_key
    text += "the key value is: %s\n" % events.EventToString(pressed_key)
    text += "the character is: %s" % events.EventToCharacter(pressed_key, 0)
    
    # press space to reset the initial text
    if pressed_key == events.SPACEKEY:
        text = "Please, press any key."
    owner["Text"] = text
```

This script is called every time someone presses a key. The key (or keys) are registers as a list of events, each one being a list with the pressed key and its status. In this case, we are reading only the first pressed key:

`pressed_key = sensor.events[0][0]`

This line stores the integer that identifies the pressed key. However, we usually would need to know the actual pressed key, not its internal integer value. Therefore, we are using the only two functions available in this module to convert our key to an understandable value:

```python
    text += "the key value is: %s\n" % events.EventToString(pressed_key)

    text += "the character is: %s" % events.EventToCharacter(pressed_key, 0)
```
    
After that, we are checking for a specific key (spacebar). bge.events.SPACEKEY is actually an integer (to find the other keys' names, visit the API page):

```python
    if pressed_key == events.SPACEKEY: text = "Please, press any key."
```

And, voilà, now we only need to visualize the pressed key:

```python
    owner["Text"] = text
```

>**Key Status**
>
>The status of a key is what informs you whether the key has just been pressed or if it was pressed already. The Keyboard sensor is always positive as long as any key is held, and you may need to trigger different functions when some keys are pressed and released. The status values are actually stored in bge.logic:

```python
0 = bge.logic.KX_INPUT_NONE

1 = bge.logic.KX_INPUT_JUST_ACTIVATED

2 = bge.logic.KX_INPUT_ACTIVE

3 = bge.logic.KX_INPUT_JUST_RELEASED
```

#### bge.texture <a id="bge.texture"></a>

The texture module was first discussed in the Chapter 5, "Graphics." With the texture module, you can change any texture from your game while the game is running. The texture can be replaced by a single image, a video, a game camera, and even a webcam stream.

Let's look at a basic example. Please open the file: Book\Chapter7\6\_ texture\basic\_texture\_replacement.blend.

This file has a single plane with a texture we will replace with an external image. Press the spacebar to change the image and Enter to return to the original one. The script responsible for the texture switching is:

```python
from bge import logic
from bge import texture
def createTexture(cont):
    """Create a new dynamic texture"""
    object = cont.owner

    # get the reference pointer (ID) of the texture
    ID = texture.materialID(obj, 'IMoriginal.png')

    # create a texture object
    dynamic_texture = texture.Texture(object, ID)

    # create a new source
    url = logic.expandPath("//media/newtexture.jpg")
    new_source = texture.ImageFFmpeg(url)

    # the texture has to be stored in a permanent Python object
    logic.dynamic_texture = dynamic_texture

    # update/replace the texture
    dynamic_texture.source = new_source
    dynamic_texture.refresh(False)

def removeTexture(cont):
    """Delete the dynamic texture, reversing it back to the original one."""
    try: del logic.dynamic_texture
    except: pass
```

It's a simple script, but let's look at the individual steps. We start by getting the material ID (that can be retrieved for an image used by an object, hence the prefix IM) or a material that uses a texture (with the prefix MA).

```python
    ID = texture.materialID(object, 'IMoriginal.png')
```

With this ID, we can create a Texture object that controls the texture to be used by this object (and the other objects sharing the same image/material).

```python
    dynamic_texture = texture.Texture(object, ID)
```

The next step is to create the source to replace the texture with. The bge.texture module supports the following sources: ImageFFmpeg (images), VideoFFmpeg (videos), ImageBuff (data buffer), ImageMirror (mirror), ImageRender (game camera), ImageViewport (current viewport), and ImageMix (a mix of sources).

```python
    new_source = texture.ImageFFmpeg(url)
```

Now we only need to assign the new source to be used by the object texture and to refresh the latter. The refresh function has a Boolean argument for advanced settings. A rule of thumb is: for videos, use refresh (True); for everything else, try refresh (False) first.

```python
    dynamic_texture.source = new_source
    dynamic_texture.refresh(False)
```

For the image to be permanent, we have to make sure the new dynamic_texture is not destructed after we leave our Python function. Therefore, we store it in the global module bge.logic. If you need to reset the texture to its original source, simply delete the stored object (for example, _del logic.dynamic_texture_).

Since this is a simple image, you don't need to do anything after that. If you are using a video as source, you need to keep refreshing the texture every frame. Videos also support an audio-video syncing system. To make them play harmoniously together, you first play the audio and then query its current position to pass as a parameter when updating the video frame (for example,  _logic.video.refresh(True, logic.sound.time)_). The audio can come from an Audaspace object or even a Sound actuator.

In the book files, you can find other examples using different sorts of source objects:

Basic replacement of texture:

_/Book/Chapter7/6_texture/basic_texture_replacement.blend_

Basic video playback with Sound actuator:

_/Book/Chapter7/6_texture\basic_video_sound.blend_

Video player with interface controllers:

_/Book/Chapter7/6_texture/player_video_audio.blend_

Basic video playback with Audaspace:

_/Book/Chapter7/6_texture/video_audaspace.blend_

Mirror effect:

_/Book/Chapter7/6_texture/mirror.blend_

Render to texture:

_/Book/Chapter7/6_texture/render_to_texture.blend_

Webcam sample:

_/Book/Chapter7/6_texture/webcam.blend_

#### bge.constraints <a id="bge.constraints"></a>

The Bullet Physics engine allows for advanced control over the physics simulation in your game. Using Bullet as a backend, this module (formerly known as _Physics Constraints_) allows you to create and set up rigid joints, dynamic constraints, and even a vehicle wrapper. The constraints' functionalities make sense only when you understand the context in which they are to be used (with physic dynamic objects). Therefore, this module is covered in the previous chapter on game physics.

#### Mathutils - Math Types and Utilities <a id="Mathutils_-_Math_Types_and_Utilities"></a>

Mathutils is a generic module common to both Blender and the game engine. There are a lot of methods to facilitate your script in handling 3D math operations. You won't have to reinvent the wheel every time you need to multiply vectors or transpose matrixes. Simply using the mathutils classes and built-in methods frees you to invest your time in something far more important: relearning all of the long-forgotten math lessons you skipped.

Unless your background is in math, physics, or engineering, you won't use this module any time soon. For those already familiar with the passionate secrets of math, you'll be glad to know that those module's functions are mainly self-explanatory. Names such as cross, dot, slerp (what?), and a quick look at their specifications will be all you need to know to start working with them. Nevertheless, newcomers often use this module without even knowing it. Every time you change an object position, get the vector from an object, or apply a rotation, you are using mathutils classes and methods. Therefore, it's good to have this module as a reference for further studies and more advanced coding. (We all get there eventually.)

We are going to present the four available classes in this module: vector, matrix, Euler, and quaternion. For a list of the available methods, refer to the API documentation.

##### Vector <a id="Vector"></a>

This class was already present in the KX\_GameObject class and in the script example. It behaves like a list object, with some advanced features (for example, swizzle and slicing) expanded with its instance methods. Some of those methods are: reflect, dot, cross, and normalize.

A recurring problem that new Python programmers have is with list copying. If you forget to manually copy the list when assigning it to a new variable, you end up with two variables sharing the same list values forever (each of the variables becomes a pointer to the same data).

The same behavior happens with Vectors. Look at the differences:

`new_vector = old_vector`

if you change new\_vector you will automatically change old_vector (and vice-versa).

`new_vector = old_vector[:]`

new_vector is a new independent list object initialized with the old_vector values.

`new_vector = vector.copy()`

new_vector is a new Vector, an independent copy of the old_vector object.

##### Matrix <a id="Matrix"></a>

While vectors behave similarly to lists, matrices behave similarly to multidimensional lists. A multidimensional list is a list of a list, organized either in columns or rows.

While in Python, a list of a list is always the same:

`matrix_row = [[1,2,3], [4,5,6], [7,8,9]]`

In a mathutils.Matrix, the data can be stored differently, accordingly to the matrix orientation (row/column). Following you can see how the order of the elements in a matrix changes, according to its orientation (note, this is not actual Python code):

```python
matrix_row_major    =  [[1 2 3]

                       [4 5 6]

                       [7 8 9] ]

                       [1][4][7]

matrix_column_major = [|2||5||8|]

                      [3][6][9]
```

It's important to be aware of the ordering of your matrices; otherwise, you end up using a transposed matrix for your calculations. Since all the game engine internal matrices (orientation, camera to world, and so on) are column-major oriented, you will be safer sticking to this standard.

If your matrix represents a transformation matrix (rotation, translation, and scale) you can get its values separately. Matrix.to_quaternion() and Matrix.to_euler() will give you the rotation part of the matrix in the form you prefer (see next section), and Matrix.to_translation() and Matrix.to_scale () will give you the translation and the scale vector, respectively.

##### Euler and Quaternion <a id="Euler_and_Quaternion"></a>

Euler and quaternion are different rotation systems. The same rotation can be represented using Euler, quaternion, or an orientation matrix.

>**Guerrilla CG**
>
>You can find two great video tutorials on the Guerrilla CG vimeo channel that explain and compare the two rotation system:
>Euler Rotations Explained: http://vimeo.com/2824431
>The Rotation Problem: http://vimeo.com/2649637

>When you convert an orientation matrix to Euler (`Matrix.to_euler()`), you get a list with three angles. They represent the rotation in the x, y, z axis of the object. In the navigation system script example, we are using this exact method to determine the horizontal camera angle. You can find this usage in the function `fly_to_walk()` (lines 190 to 199 of navigation\_system.py or in the early pages of this chapter).
>
>Conversion Between Different Rotation Forms
>You can convert an orientation matrix to Euler, an Euler to a quaternion, a quaternion to an orientation matrix, and on and on and on:

```python
original_matrix=mathutils.Matrix.Rotation(math.pi, 3, "X")

converted_matrix=original_matrix.to_euler().to_quaternion().to_matrix().to_euler().to_matrix().to_quaternion().to_euler().to_matrix().to_quaternion().to_euler().to_quaternion().to_matrix()
```
>In this example, converted_matrix ends up as the same matrix as original_matrix.

#### aud - Audio System <a id="aud_-_Audio_System"></a>

This module allows you to play sounds directly from your scripts. There are three classes you will be working with: Device, Factory, and Handle.

The audaspace module in a nutshell: you need to create one audio Device per game. You need one Factory per audio file (which can also be any video file containing a sound track). And every time you need to play a sound, a new Handle object will be generated from the Factory (this is where its name comes from).

##### Example: Basic Audio Playback <a id="Example_Basic_Audio_Playback"></a>

```python
import aud
device = aud.device()
```

## load sound file (it can be a video file with audio)

```python
factory = aud.Factory('music.ogg')
```

## play the audio, this return a handle to control play/pause

```python
handle = device.play(factory)
```

## if the audio is not too big and will be used often you can buffer it

```python
factory_buffered = aud.Factory.buffer(factory)
handle_buffered = device.play(buffered)
```

## stop the sounds (otherwise they play until their ends)

```python
handle.stop()
handle_buffered.stop()
```

We start by creating an audio device. This is simply a Python object you will use to play your sounds. Next, we create a Factory object. A factory is a container for a sound file. When we pass the Factory object into the device play function, it will start playing the sound and return a handle. Handles are used to control pause/resume and to stop an audio.

>**When Will This Music Stop?**
>
>After you initialize a sound, you can get its current position in seconds with the handle.position Python property. This is especially useful to keep videos and audio in sync. If you need to check whether or not the audio is ended, you shouldn't rely on the position, though. Instead, you can get the status of the sound by the property handle.status. If you are using the sound position to control a video playback, the sound status will also tell you if the video is over (handle.status = aud.AUD\_STATUS\_INVALID).
>The possible statuses are:

```python
0 = aud.AUD_STATUS_INVALID

1 = aud.AUD_STATUS_PLAYING

2 = aud.AUD_STATUS_PAUSED
```

#### bgl - OpenGL Wrapper <a id="bgl_-_OpenGL_Wrapper"></a>

This module is a wrapping of OpenGL constants and functions. It allows you to access low-level graphic resources within the game engine. You can use this module to draw directly to the screen or to read OpenGL matrices and buffers directly.

Sometimes, you will need to run your OpenGL code specifically before or after the game engine drawing routine, so you can store your Python function as a list element either in the scene attributes pre_draw and/or in the post_draw. This will be demonstrated in our first example.

>**To Learn OpenGL**
>
>You can find good OpenGL learning material on the Internet or in a bookstore. _The Official Guide to Learning OpenGL_ (also known as _The Red Book_) is highly recommended, and some older versions of it can be found online for download.

##### Example 01: Line Width Changing <a id="Example_01_Line_Width_Changing"></a>

Open the file /Book/Chapter7/7_bgl/line_width.blend.

(run it in wireframe mode)

```python
from bge import logic
import bgl
def line_width():
    bgl.glLineWidth(100.0)

scene = logic.getCurrentScene()
if line_width not in scene.pre_draw:

    scene.pre_draw.append(line_width)
```

This code needs to run only once per frame and will change the line width of the objects. Be aware that the line is only drawn in the wireframe mode.

You will find on the book files another example where the line width changes dynamically - /Book/Chapter7/7_bgl/line_width_animate.blend.

##### Example 02: Color Picker <a id="Example_02_Color_Picker"></a>

Open the file /Book/Chapter7/7_bgl/color_pickup.blend.

In this file, you can change the light color according to where you click.

```python
from bge import logic
from bge import render
import bgl

cont = logic.getCurrentController()
lamp   = cont.owner
sensor = cont.sensors["s\_mouse\_click"]

if sensor.positive:
    width = render.getWindowWidth()
    height = render.getWindowHeight()
    viewport = bgl.Buffer(bgl.GL_INT, 4)
    bgl.glGetIntegerv(bgl.GL_VIEWPORT, viewport);
    x = viewport[0] + sensor.position[0]
    y = viewport[1] + (height - sensor.position[1])
    pixels = bgl.Buffer(bgl.GL_FLOAT, [4])

    # Reads one pixel from the screen, using the mouse position
    bgl.glReadPixels(x, y, 1, 1, bgl.GL_RGBA, bgl.GL_FLOAT, pixels)

    # Change the Light colour
    lamp.color = [pixels[0], pixels[1], pixels[2]]
```

There are three important bgl methods been used here. The first one is bgl.Buffer. It creates space in the memory to be filled in with information taken from the graphics driver:

```python
viewport = bgl.Buffer(bgl.GL_INT, 4)

pixels = bgl.Buffer(bgl.GL_FLOAT, [4])
```

The second one is the `bgl.glGetIntegerv`. We use it to get the current Viewport position and dimension to the buffer object previously created:

```python
glGetIntegerv(bgl.GL_VIEWPORT, viewport);
```

The buffer coordinates run from the left bottom [0.0, 0.0] to the right top [1.0, 1.0]. The mouse coordinates, on the other hand, run from left top [0, 0] to the right bottom [width, height]. We need to convert the mouse coordinate position to the correspondent one in the Buffer.

```python
x = viewport[0] + sensor.position[0]

y = viewport[1] + (height - sensor.position[1])
```

The third one is bgl.glReadPixels. This is the method that's actually reading the pixel color and storing it in the other buffer object:

```python
bgl.glReadPixels(x, y, 1, 1, bgl.GL_RGBA, bgl.GL_FLOAT, pixels)
```

And, finally, let's apply the pixel color to the lamp:

```python
lamp.color = [pixels[0], pixels[1], pixels[2]]
```

#### blf - Font Drawing <a id="blf_-_Font_Drawing"></a>

If you need to control text drawing directly from your scripts, you may need to use this module. Be aware, though, that this module is a low-level API that has to be combined with the OpenGL wrapper to handle texts properly.

The blf module works in three stages:

1. Create a new font object.

2. Set the parameters for the text (size, position, and so on).

3. Draw the text on the screen.

##### Example: Writing Hello World <a id="Example_Writing_Hello_World"></a>

Open the file /Book/Chapter7/8_blf/hello_world.blend.

In the init function, we load a new font in memory and store the generated font ID to use later.

```python
def init():

    """init function - runs once"""

    # create a new font object
    font_path = bge.logic.expandPath('//fonts/Zeyada.ttf')
    bge.logic.font_id = blf.load(font_path)

    # set the font drawing routine to run
    scene = bge.logic.getCurrentScene()
    scene.post_draw=[write]
```

The actual function responsible for writing the text is stored in the scene post\_draw routine. Apart from the OpenGL calls, the setup for using the text is quite simple.

```python
def write():
    """write on screen – runs every frame"""
    width = bge.render.getWindowWidth()
    height = bge.render.getWindowHeight()

    # OpenGL calls to re-set drawing position
    bgl.glMatrixMode(bgl.GL_PROJECTION)
    bgl.glLoadIdentity()
    bgl.gluOrtho2D(0, width, 0, height)
    bgl.glMatrixMode(bgl.GL_MODELVIEW)
    bgl.glLoadIdentity()

    # blf settings + draw

    font_id = bge.logic.font_id
    blf.position(font_id, (width*0.2), (height*0.3), 0)
    blf.size(font_id, 50, 72)
    blf.draw(font_id, "Hello World")
```

On the book files, in the same folder, you can find two other examples following the same framework_: hello_world_2.blend_ and _object_names.blend_.
