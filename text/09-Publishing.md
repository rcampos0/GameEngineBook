**Table of Contents**

- [Chapter 9: Publishing and Beyond](#Chapter_9_Publishing_and_Beyond)
	- [Getting Ready for Publishing](#Getting_Ready_for_Publishing)
	- [Resources](#Resources)
	- [The Theory of Relativity](#The_Theory_of_Relativity)
	- [Packing](#Packing)
	- [Blenderplayer](#Blenderplayer)
		- [Export as Runtime](#Export_as_Runtime)
		- [Resource Files](#Resource_Files)
		- [Interface Options](#Interface_Options)
		- [File Security](#File_Security)
	- [Licensing](#Licensing)
	- [Web Publishing: Burster](#Web_Publishing_Burster)
	- [Mobile Publishing: Android](#Mobile_Publishing_Android)
	- [Other Tools](#Other_Tools)
		- [GameKit](#GameKit)
		- [Unity, SIO2](#Unity,_SIO2)
	- [Blender Development Cycle](#Blender_Development_Cycle)
	- [How to Report Bugs](#How_to_Report_Bugs)
	- [Do It Yourself](#Do_It_Yourself)

# Capítulo 9: Publicação e além <a id="Chapter_9_Publishing_and_Beyond"></a>

Você chegou até aqui! Agora você deve ter um conhecimento sólido de tudo o que é necessário para fazer um jogo. Agora a questão é: como você colocar esse jogo nas mãos do público?

Este capítulo se concentrará na publicação do jogo, incluindo como empacotar seu jogo, usando o Blenderplayer autônomo e entendendo os problemas de licenciamento relacionados ao uso do Blender. Também exploraremos alternativas para o mecanismo de jogo do Blender enquanto ainda usamos o Blender como a principal ferramenta de criação de conteúdo. Mesmo que este seja um livro específico do Blender, nós encorajamos você a se familiarizar com outros motores de jogo e entender seus prós e contras para que possa decidir por si mesmo qual é a melhor plataforma de publicação para usar em um jogo específico.

## Preparando-se para publicar <a id="Getting_Ready_for_Publishing"></a>

Você terminou seu jogo, e agora? Além do teste de resistência, promoção e aperfeiçoamento, existem algumas coisas técnicas que você precisa fazer para implantar seu projeto. Eles se aplicam a quase todas as opções discutidas neste capítulo e, mesmo se você estiver usando mecanismos externos, deve levá-los em consideração.

## Recursos <a id="Resources"></a>

De modo geral, para outros usuários rodarem um jogo criado pelo Blender, eles precisarão de todos os seguintes arquivos:

- **arquivo Blender** : Este é um arquivo .blend que contém sua cena 3D e a lógica do jogo.

- **Recursos** : Isso inclui texturas de imagem, áudios, fontes e scripts.

- **Binário do Blender (ou executável)**: Pode ser o binário do Blender ou do Blenderplayer que é necessário para rodar o jogo para pessoas que ainda não têm o Blender instalado.

Esta lista é simplificada. Por exemplo, em um projeto maior, em vez de um único arquivo do Blender, um jogo pode ser composto de vários arquivos do Blender, mas sempre haverá um arquivo que atua como um ponto de entrada para iniciar o jogo. Recursos são arquivos externos usados no jogo. Os recursos podem ser compactados, o que basicamente copia esses arquivos para o arquivo do Blender. Finalmente, o binário do Blender geralmente não é um único arquivo. Ele contém bibliotecas e scripts que o Blender irá precisar. Normalmente é uma boa ideia incluir o binário com o lançamento, porque a menos que o jogo seja distribuído exclusivamente dentro da comunidade Blender, o usuário provavelmente não terá o Blender (ou a versão correta do Blender) instalado para executar o arquivo do Blender.

## A teoria da relatividade <a id="The_Theory_of_Relativity"></a>

A primeira regra de implantação é lembrar que, como não temos controle sobre o computador do usuário, é impossível prever onde nosso jogo será instalado. Se isso não for ruim o suficiente, diferentes sistemas operacionais (Windows, Mac, Linux) tratam os caminhos de arquivo de maneira diferente. A única maneira de garantir a compatibilidade entre sistemas diferentes é certificar-se de que todos os caminhos de arquivo usados no jogo são relativos e aninhados na pasta raiz do jogo.

Alguns caminhos de arquivo relativos:

_//textures/color.png_

_//audio/music/background.mp3_

Alguns caminhos de arquivo relativos incorretos (evite-os):

_//..\..\..\Fonts\ComicSans.ttf_

_//../../Downloads/textures/floor.png_

Alguns caminhos de arquivo absolutos (evite-os):

_C:\Users\Documents\Peter\MyBlenderProject\textures\color.png_

_/home/desktop/DownloadedFromInternet/audio/music/background.mp3_

Como você pode ver, não só um caminho de arquivo absoluto revela muitas coisas que você provavelmente não quer que outros vejam, mas um caminho de arquivo absoluto simplesmente não funcionaria em outro computador a menos que tenha a mesma configuração de pasta que você e um sistema operacional compatível.

Por padrão, o Blender faz referência a todos os ativos externos (como texturas de imagem, arquivos de áudio e arquivos do Blender vinculados) usando um caminho relativo. O caminho do arquivo é sempre relativo ao arquivo do Blender.

Como todos os caminhos relativos são relativos ao arquivo do Blender aberto atualmente, para que o caminho relativo funcione, o arquivo do Blender deve ser salvo antes que quaisquer ativos externos sejam carregados.

Se estiver usando scripts Python para carregar um arquivo do computador, você deve sempre usar o módulo "os" (os.path.sep, os.path.join,…) para lidar com a localização desses arquivos.

>**Nunca é tarde demais para fazer a coisa certa**
>
> Se você esqueceu de salvar seu arquivo antes de anexar ativos, ou perdeu a opção "Caminho Relativo" no menu de carregamento, não se preocupe. Há uma opção no menu de arquivo que ajuda a reorganizar os caminhos de arquivo dos ativos:
> `File > External Data > Make all Paths Relative`

## Empacotando <a id="Packing"></a>

Se você não quer lidar com arquivos externos, o Blender também oferece outra ferramenta útil para simplificar a distribuição de uma embalagem de jogo [md]. O empacotamento torna o arquivo do Blender auto-suficiente, coletando todos os recursos externos, como imagens, sons e fontes no arquivo atual do Blender.

Para empacotar um arquivo, clique em File > External Data > Pack into .blend file.

Não é preciso dizer que a embalagem fará o arquivo do Blender aumentar de tamanho. A embalagem é uma maneira muito grosseira de ocultar a estrutura de arquivos do seu jogo de observadores casuais, mas de forma alguma a embalagem garante a segurança desses arquivos. É fácil para alguém descompactar os arquivos e ter acesso a todo o ativo do jogo que você criou. A embalagem é uma ferramenta conveniente, não um método de criptografia.

Desempacotar faz o contrário de embalar; ele pega todos os dados compactados de um arquivo do Blender e os grava como arquivos separados.

>**Para os preguiçosos e desorganizados**
>
> Ao iniciar um projeto, use dados externos de qualquer lugar em seu computador, sem se preocupar com sua localização. Quando você quiser se organizar, simplesmente execute uma operação de empacotamento e, em seguida, execute imediatamente uma operação de descompactação (com a opção Descompactar para o diretório atual). Isto irá primeiro empacotar todas as imagens no Blender e então descompactá-las ordenadamente em um diretório chamado _textures_. Dessa forma, não há necessidade de mover as coisas manualmente. Todos os dados externos usados serão movidos automaticamente para uma única pasta para fácil distribuição. As imagens em seus locais originais permanecem intocadas.

## Blenderplayer <a id="Blenderplayer"></a>

Um dos pontos fortes do motor de jogo é sua forte integração com o Blender e o feedback quase instantâneo que você obtém ao iniciar um jogo dentro da janela de visualização do Blender. Esta mistura de editor de níveis, design de personagens e gerenciamento de ativos em geral é de fato uma tendência na indústria de jogos hoje em dia. Freqüentemente, vemos motores de jogo que foram trazidos para dentro das ferramentas de edição 3D. No entanto, deve haver uma distinção entre a ferramenta de edição e a ferramenta de implantação. Seu jogo, uma vez publicado, precisa ser um aplicativo de software próprio. O jogador não deve estar ciente da ferramenta que você está usando [md], não que os mágicos nunca revelem seus truques. (Você pode incluir uma boa descrição de suas ferramentas em seus créditos se isso lhe agradar.) Mas passar pela interface do Blender para abrir seu jogo certamente quebrará o encanto.

### Exportar como Runtime <a id="Export_as_Runtime"></a>

Como mencionamos anteriormente, o Blenderplayer é uma forma de reproduzir seus arquivos independentemente do Blender. A primeira etapa é certificar-se de que o complemento "Salvar como Game Engine Runtime" esteja ativado. O próximo é executá-lo através do menu Arquivo  Exportar  Salvar como Game Engine Runtime. Veja a Figura 9.1.

Isso abrirá uma caixa de diálogo para você escolher onde salvar seu arquivo binário, que funciona de maneira diferente em diferentes sistemas operacionais:

![Exportar como Game Engine Runtime](../figures/Chapter9/Fig09-01.png)

- **Windows:** Alguns arquivos serão copiados para a pasta para a qual você exportou o tempo de execução. O arquivo principal é um executável (.exe) que você usará para iniciar o jogo. O nome do arquivo é aquele que você escolhe na caixa de diálogo Exportar. Ele contém seu arquivo do Blender (.blend) e o Blenderplayer (.exe) agrupados. Algumas bibliotecas (.dll) também são apresentadas. Eles são necessários para jogar seu jogo, portanto, certifique-se de levá-los com seu executável aonde quer que vá (copiar, compactar, compactar).

Por fim, algo que está presente em todos os sistemas operacionais, você encontrará uma pasta que contém os arquivos necessários para executar scripts Python. A pasta é nomeada após a versão atual do Blender (por exemplo, 2.66\python\).

- **Linux:** No Linux (e Mac OSX), o binário do Blenderplayer é vinculado estático às bibliotecas. Isso significa que você tem um único arquivo executável que contém quase tudo que você precisa. O arquivo recém-criado (nomeado na caixa de diálogo Exportar como tempo de execução) já possui a permissão de usuário adequada para ser executado por qualquer usuário.

Assim como o tempo de execução do Windows, no Linux temos uma pasta com os arquivos necessários para os scripts Python. Mesmo se o sistema já tiver o Python instalado, o Blenderplayer (e o Blender para esse assunto) depende de uma versão particular do Python para sua execução. Isso evita que seus jogos apresentem problemas de compatibilidade com diferentes versões de Python que podem existir no sistema do usuário. Isso também permite que você use scripts Python compilados, como veremos em breve.

- **Mac OSX:** Neste caso, o Export as Runtime cria um executável (.app) que você pode rodar clicando duas vezes nele. Este executável é nomeado a partir da caixa de diálogo Exportar, mas não é mais do que uma pasta que você pode explorar através da linha de comando. Esta pasta contém o executável do Blenderplayer, o arquivo do Blender (game.blend), as bibliotecas Python e os ícones usados para o arquivo do jogo.

>**Usando o Blenderplayer sem exportar seu jogo**
>
> Você não precisa exportar seu jogo toda vez que quiser testá-lo no Blenderplayer.
> Na mesma pasta onde você instalou o Blender, você pode encontrar o executável do Blenderplayer. Execute-o a partir da linha de comando / console com seu arquivo como argumento:
>Blenderplayer.exe C:\MyFileWindows.blend
>./blenderplayer.app/Contents/MacOS/blenderplayer ~/myFileOSX.blend
>./blenderplayer ~/myFileLinux.blend
> Se você executá-lo com o argumento "-h", poderá ver todas as opções disponíveis na linha de comando. Outra opção é usar o botão Iniciar na aba Reprodutor Independente no menu Cena para iniciar o arquivo atual no Blenderplayer (veja "Opções de Interface" a seguir neste capítulo).

### Arquivos de Recursos <a id="Resource_Files"></a>

Freqüentemente, seu jogo precisará de mais do que você incluiu no Blender. Por exemplo, se você decidiu não compactar as texturas em seu arquivo, você precisará copiá-las para a mesma estrutura de pastas em que estavam originalmente. O mesmo se aplica a sons, fontes, filmes, scripts Python e assim por diante.

Para Linux e Windows, você simplesmente precisa copiá-los para a mesma pasta do executável exportado. Em outras palavras, você precisa manter a mesma estrutura de arquivo que estava usando dentro do Blender.

Para Mac OSX, você precisa copiá-los para "mygame.app/Contents/Resources/." Esta é a pasta base (por exemplo, texturas vão em mygame.app/Contents/Resources/textures/ ").

### Opções de Interface <a id="Interface_Options"></a>

No painel Render, você pode encontrar algumas opções específicas para o Blenderplayer, conforme mostrado na Figura 9.2.

![Blenderplayer e outras opções](../figures/Chapter9/Fig09-02.png)

- **Start:** Uma maneira rápida de lançar seu jogo no Blenderplayer. Ele o abrirá em uma nova janela. Primeiro, você precisa salvar seu arquivo. Não confunda isso com o botão Iniciar na guia Player incorporado, que reproduz o jogo dentro do Blender.

- **Width** e **Height:** A largura e a altura do Player incorporado determinam a proporção da câmera. Os que estão no painel do Blenderplayer alteram o tamanho real da tela.

- **Full-Screen** e **Desktop:** Se você deseja iniciar o jogo em tela inteira, pode usar esta opção. Se você definir a opção Desktop, o mecanismo de jogo usará a resolução da tela do computador atual para o modo de tela inteira. Caso contrário, a resolução do Blenderplayer mudará a resolução da área de trabalho.

- **AA Samples:** Para bordas renderizadas suaves, você pode ativar o anti-aliasing. Se o computador que está executando o jogo não oferecer suporte a um nível específico de AA ou não oferecer suporte a AA de forma alguma, o mecanismo do jogo retornará ao parâmetro máximo compatível.

- **Bit Depth** e **Refresh Rate:** A profundidade da cor e a taxa de atualização dos gráficos.

- **Framing:** O que você pode fazer quando a tela é dimensionada? Escolha uma dessas três opções: Letterbox, Extend e Scale. A escala estenderá o quadro para o novo tamanho de tela (espere algumas distorções de proporção); Extend revelará mais do quadro, como se você tivesse alterado a resolução do Blenderplayer e do Embedded Player ao mesmo tempo. A caixa de correio preencherá qualquer diferença entre a proporção da câmera (resolução do Embedded Player) e o tamanho da tela com a cor que você escolher na caixa de cores (preto por padrão).

### File Security <a id="File_Security"></a>

Como o Blender está disponível gratuitamente para todos, se você distribuir seu jogo como um arquivo do Blender (.blend), não há realmente nenhuma maneira de evitar que as pessoas abram o Blender e dêem uma olhada em seu arquivo do Blender. Mesmo que o jogo seja compactado e transformado em um runtime na forma de um único executável, ainda é relativamente fácil para alguém com um pouco de habilidade técnica extrair os dados do jogo. O resultado final é que compactar, compactar e criar tempo de execução são apenas conveniências para você; um arquivo Blend nunca é seguro contra uma mente maligna curiosa (e determinada).

>**No-Cheating**
>
> Se o jogo envolver vários jogadores conectados pela Internet, a única maneira de garantir que o jogo seja à prova de falsificação é fazer uma verificação rigorosa no servidor. Qualquer código Python do lado do cliente para garantir a integridade pode ser facilmente modificado pelo usuário e, portanto, é efetivamente inútil. Por exemplo, para um jogo de tiro, o servidor do jogo deve controlar a munição restante de cada jogador; dessa forma, um jogador malicioso não seria capaz de trapacear alterando sua própria contagem de munição.

A parte do seu programa que você pode proteger facilmente são os scripts Python. Embora o arquivo .py de texto simples seja fácil de ser lido por qualquer pessoa, um script compilado é um blob ininteligível de código binário. Para compilar seu script, tudo que você precisa fazer é executá-lo uma vez e o mecanismo de jogo irá gerar um arquivo .pyc para você. Este arquivo pode ser encontrado na mesma pasta que seus scripts originais em uma subpasta chamada \ _ \ _ pycache \ _ \ _. Agora, tudo o que você precisa fazer é substituir os arquivos de script originais (.py) por sua versão compilada (.pyc). Alternativamente, você pode usar o Python autônomo para gerar os arquivos .pyc: python –m compileall –b <folder-with-scripts>.

Mesmo que seus arquivos de produção sejam expostos, este não é o fim do mundo. Seu trabalho ainda está protegido pelos direitos de licenciamento. Qual é o nosso próximo tópico [md] quais eram as chances?

## Licenciamento <a id="Licensing"></a>

É verdade que 11 em cada 10 pessoas nunca leram um único software EULA (Contrato de Licença do Usuário Final) em suas vidas. Você sabe, aquela caixa cheia de texto com a qual você tem que concordar antes de instalar um programa. Para iluminar sua mente e aliviar sua consciência culpada, tente não pular esta seção.

Assim como um documento que você compôs no Word pertence por direito a você, e não à Microsoft, qualquer arquivo do Blender que você criou é inteiramente seu. Você é livre para distribuir, vender e mostrar publicamente o arquivo do Blender o quanto quiser.

O motor do jogo tem um problema, entretanto. O Blender e o Blenderplayer são licenciados sob a GNU General Public License (GPL). Resumindo, isso significa que qualquer arquivo executável derivado de um desses binários precisa seguir a mesma licença original. E dessa perspectiva legal, um jogo exportado como um Runtime é considerado um binário derivado.

Em outras palavras, você precisa garantir que todos os arquivos que não deseja licenciar sob a GPL não estejam incluídos no Blenderplayer. A opção de exportar como Runtime ainda pode ser usada, mas seu arquivo inicial (aquele incorporado no Blenderplayer) terá que ser licenciado sob GPL.

Uma maneira simples de manter seus arquivos separados do Blenderplayer é criar um arquivo de carregamento inicial. Este arquivo terá um atuador de jogo que só então carregará seu arquivo principal real. Dessa forma, todos os seus arquivos de jogo reais podem ser mantidos externos ao binário. Seu arquivo nem precisa terminar em ".blend" para que o atuador do jogo funcione.>**Why the Blender Game Engine Won't Run on iOS**
>
>There is a downside of the GPL license when publishing in some distribution platforms. For legal (and perhaps economic) reasons, most distribution game platforms do not accept GPL code in their components. That means it will be hard to get the game engine ported over to consoles and some more restrictive mobile and portable devices.

## Web Publishing: Burster <a id="Web_Publishing_Burster"></a>

_www.geta3d.com_

Burster is a plug-in that allows you to publish and play your games in a Web browser. The plug-in was developed and is supported by a third-party company, independently of Blender Foundation. The plug-in contains a slightly modified version of Blenderplayer that runs as fast as if it were installed natively.

Not all Python modules are supported (for security reasons), but external assets (for example, textures and videos) work pretty well. Additionally, Burster offers a protection system for your work through online on-the-fly decryption of your Blender files. This does not violate the GPL and can provide the necessary security that some commercial works demand.

If you are considering using the Web as a publishing platform, you can find updated information in the Burster website. Make sure you test your game extensively. Even though most of the features are supported, more advanced resources can get a bit tricky (for example, video texture is supported, but the only way to play videos is with external URLs in a server that supports streaming).

>**Beyond Packing**
>
>For Web deployment and mobile, you need to include all the external dependencies into the main file. While textures can be incorporated with the Packing option, the files and scripts need to be merged in manually.
>If you are using Python scripts follow these advanced instructions:
>- Open all the external scripts (e.g., originally in //scripts/) in the Blender Text Editor
>- Remove all the "from ." from the scripts
>- Fix all the Python Module controllers by copying this into the Blender Text Editor and running it as a script (in Blender, not inside the game engine):
```python
import bpy
for obj in bpy.data.objects:
    for cont in obj.game.controllers:
        if cont.type == 'PYTHON' and cont.mode == 'MODULE':
            cont.module = cont.module.replace('script.', '')
```

## Mobile Publishing: Android <a id="Mobile_Publishing_Android"></a>

_wiki__.blender.org/index.php/Doc:2.6/Manual/Game_Engine/Blender_Player/Android_

Although it is early to know how far this will go, the Android deployment for the game engine is starting to get in shape. An experimental branch of Blender, "soc-2012-swiss\_cheese" makes an Android-compatible Blenderplayer that can open simple .blend game files. Animation, Physics, GLSL materials, and mouse interaction are already supported.

In Figure 9.3, you can see the final sample file from Chapter 4 running in an Android phone. To see this in action go to: [http://youtu.be/bF1m5b4jEKs](http://youtu.be/bF1m5b4jEKs).

![Android deployment](../figures/Chapter9/Fig09-03.png)

To run your game, you can download the Blenderplayer Android app and open the game from it. As of the time of writing, the app is not yet on the Android market. You can download it from this BlenderArtists forum thread: [http://blenderartists.org/forum/showthread.php?255746](http://blenderartists.org/forum/showthread.php?255746)

A mobile platform is a limited deployment target. The phones and tablets are getting more powerful every day, yet they still lack in hardware horsepower compared to gaming PCs. As such, you need to be especially careful with optimizing your games.

Some general guidelines:

- Simplify the geometry.

- Chop down big objects into small parts.

- Use Occlusion Culling when possible.

- Work with power of two textures.

## Other Tools <a id="Other_Tools"></a>

The Blender game engine can be used for prototyping, before the game is fully developed in another game engine. Or, another common situation, you can use Blender only for asset making for an external engine, and the Blender game engine for previewing the animation playbacks and basic interactions. In those cases, you will not be using the logic components of the game, but mostly making sure your assets (objects, materials, animations) can be transferred easily to other engines.

>**Exchange File Formats**
>
>When your engine does not support Blender files directly, you have to find the best format to export from Blender. There is one format in Blender intended for games. It supports not only mesh and texture, but also animation, shading, and physics.
>Collada is an open exchange file format maintained by Khronos consortium (the same group behind the well known OpenGL, OpenCL, and others). >Although the support for it in Blender is not complete yet, it's getting there.
>Another format broadly used is FBX. This is a proprietary format created and maintained by Autodesk with proper support in Blender going on and off in the past releases.

Even when you are using Blender only to build your assets, the game engine can be of great value. It should be simple to create test levels for your character animations, test ideas, and, in some cases, even build a whole game prototype before migrating to another engine.

In the next chapter, you will learn about some projects that used the game engine in one way or another. One of these projects is _Cubic World,_ originally created in the game engine for a game contest. The project was so well received that the main developer decided to port it to the iPhone, writing a specific engine from scratch. Whether you are building your own engine, porting it to an open or commercial alternative, or deploying with the game engine, be aware of the alternatives to better support your decisions. This is an ever-changing topic. New technologies come and go, and it's up to you to keep yourself updated on the subject. Sign up for newsletters, visit forums, and go to conferences (and although it may eventually help, we don't mean wandering around on Twitter or Facebook).

### GameKit <a id="GameKit"></a>

_www.gamekit.org_

GameKit is a "basic game engine that allows fast prototyping built around open source software free for commercial use." GameKit uses Bullet for physics, Ogre for rendering, OpenAL for sound, Lua for scripting, and AnimKit for animation (a stand-alone library created specifically for this engine but open for use elsewhere). It reads Blender files and supports all of its Logic Bricks.

This modular approach makes it quite interesting for indie developers who often need to design their own engine from scratch. You can borrow their support for Blender files and Render engine and implement a unique logic system, for example.

One of its key benefits over the Blender game engine is that GameKit fully supports non-PC platforms such as Android and iOS. GameKit also uses a non-viral license, meaning the games you create can have any license you want.

As of the time this book went to press, GameKit is still in its early stages. Nevertheless, it's generating some hype in the Blender game community. We are following this project closely and recommend you do the same.

### Unity, SIO2 <a id="Unity,_SIO2"></a>

While GameKit stands out for its tight integration with Blender, there are other engines with strong supports for the Blender native file.

SIO2 is an engine targeted exclusively to the mobile market. It currently supports both Android and iPhone devices. It also supports native Blender files, so there is no need to fiddle with export file types.

If your market does not use only portable devices, then Unity3D is another commercial engine that works with Blender files; it's as simple as drag-dropping them inside the editor.

Unity3D has been broadly used by the indie industry. They support mobiles to desktops, and by the time you read this, they can probably deploy for all the main consoles on the market. You still need to rework your materials once you import them inside the engine, but changes in the original file can be merged into the Unity3D editor.

## Blender Development Cycle <a id="Blender_Development_Cycle"></a>

The development of the game engine is tied to the development cycle of Blender itself. Although improvements in different parts of the software are done separately, the release of new versions of the game engine happens as part of the Blender releases.

Once a week there is an online developers' meeting[md]Blender Sunday Meeting. At the meeting, they deliberate on pending issues, present current development from coders, and trace plans for the upcoming weeks and months. The meetings happen in the #blendercoders channel in the Freenode IRC network every Sunday at 4 p.m. Amsterdam time.

For topics that require longer discussions and a larger audience, the developers use a mailing list hosted at the Blender Institute servers: bf-committers@blender.org.

To subscribe to this list or visit its archives, go to: _http://lists.blender.org/mailman/listinfo/bf-committers_

Proposals and roadmaps are presented and discussed in both channels. Some long-term projects end up resting in the Blender wiki, which in turn can be incorporated at the official development documentation page: _http://www.blender.org/development/._

Approximately every two months, a new release cycle starts. In the first week, the proposals for what features should be in the trunk (official Blender code) are presented, discussed, and, if necessary, voted in or out of the upcoming Blender release.

This is especially applicable for big features developed on branches (code not incorporated into the trunk yet). Developers may go for long periods of time coding, testing, and calling for feedback, before the code ever gets incorporated into Blender's main source.

To follow new developments, to help beta-test new features, and to make sure we keep the game engine backward compatible, you can keep track of the branches, which are always announced in the Blender Sunday Meetings and in the mailing lists.

Additionally, if you want to talk with Blender game engine coders directly, or follow our discussions, the #bgecoders IRC channel (also on Freenode) is a place where development is discussed.

## How to Report Bugs <a id="How_to_Report_Bugs"></a>

All software has bugs. Make no mistake about that. For those unfamiliar with this technical terminology, a bug is a problem in the software. Think about the last time you swore at a computer. Behind your lost hours of work lies a bug (and the imprudence of not saving your work; haven't you learned anything from playing videogames?).

Blender has a webpage dedicated solely to report and track bugs from users: _http://projects.blender.org._

The guidelines for bug reporting are simple:

- Make sure you can reproduce the bug several times.

- Re-create or isolate the bug in the simplest file you can think of.

- Report the environment you are working in if it's relevant (OS, hardware, version).

- Be patient. Reporting a bug can be a very-time consuming task. And a fix may take a long, long time with some further tests and interactions with you and the coders.

And remember, the more time you spend on making a good report[md]with good sample files, concise descriptions, and so on[md]the more you free a developer to work on fixing the bug itself.

## Do It Yourself <a id="Do_It_Yourself"></a>

As a provocative final thought, have you considered literally expanding the game engine yourself? We haven't been giving enough attention to the fact that the Blender source code is open and available to everyone. That may not be the reason you got into the software, but it's interesting to explore its potential.

Blender and the game engine are partly maintained by the Blender Foundation and partially by online volunteer coders. Most of the coders started as users, implementing specific features required for their projects. In the short term, that leads to solutions that make life easier and a project more complete. In the long term, it helps build the community that dedicates energy to the game engine project.

If nothing else, you can try building Blender and replacing the splash screen (see Figure 9.4). It's definitively the first step to looking cool and impressing your boss:

_http://wiki.blender.org/index.php/Dev:Doc/Building_Blender_

DF: To be replaced with a splash screen with Blender 2.6 say on it and the cover of the book. Waiting for the cover of the book.

![Custom splash screen](../figures/Chapter9/Fig09-04.png)
