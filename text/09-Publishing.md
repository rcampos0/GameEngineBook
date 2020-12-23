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

Uma maneira simples de manter seus arquivos separados do Blenderplayer é criar um arquivo de carregamento inicial. Este arquivo terá um atuador de jogo que só então carregará seu arquivo principal real. Dessa forma, todos os seus arquivos de jogo reais podem ser mantidos externos ao binário. Seu arquivo nem precisa terminar em ".blend" para que o atuador do jogo funcione.

>**Por que o Blender Game Engine não funciona no iOS**
>
> Há uma desvantagem da licença GPL ao publicar em algumas plataformas de distribuição. Por razões legais (e talvez econômicas), a maioria das plataformas de distribuição de jogos não aceita código GPL em seus componentes. Isso significa que será difícil transportar o motor de jogo para consoles e alguns dispositivos móveis e portáteis mais restritivos.

## Publicação na Web: Burster <a id="Web_Publishing_Burster"></a>

_www.geta3d.com_

Burster é um plug-in que permite publicar e jogar seus jogos em um navegador da web. O plug-in foi desenvolvido e é suportado por uma empresa terceirizada, independente da Blender Foundation. O plug-in contém uma versão ligeiramente modificada do Blenderplayer que roda tão rápido como se tivesse sido instalado nativamente.

Nem todos os módulos Python são suportados (por razões de segurança), mas ativos externos (por exemplo, texturas e vídeos) funcionam muito bem. Além disso, o Burster oferece um sistema de proteção para o seu trabalho por meio da descriptografia on-the-fly de seus arquivos do Blender. Isso não viola a GPL e pode fornecer a segurança necessária que algumas obras comerciais exigem.

Se você está pensando em usar a Web como plataforma de publicação, pode encontrar informações atualizadas no site da Burster. Certifique-se de testar seu jogo extensivamente. Mesmo que a maioria dos recursos sejam suportados, recursos mais avançados podem ser um pouco complicados (por exemplo, a textura do vídeo é suportada, mas a única maneira de reproduzir vídeos é com URLs externos em um servidor que suporte streaming).

>**Além da embalagem**
>
> Para implantação na Web e móvel, você precisa incluir todas as dependências externas no arquivo principal. Embora as texturas possam ser incorporadas com a opção Packing, os arquivos e scripts precisam ser mesclados manualmente.
> Se você estiver usando scripts Python, siga estas instruções avançadas:
> - Abra todos os scripts externos (por exemplo, originalmente em // scripts /) no Editor de Texto do Blender
> - Remova todos os "de". dos scripts
> - Corrija todos os controladores do Módulo Python copiando isso para o Editor de Texto do Blender e executando-o como um script (no Blender, não dentro do motor de jogo):

```python
import bpy
for obj in bpy.data.objects:
    for cont in obj.game.controllers:
        if cont.type == 'PYTHON' and cont.mode == 'MODULE':
            cont.module = cont.module.replace('script.', '')
```

## Publicação móvel: Android <a id="Mobile_Publishing_Android"></a>

_wiki__.blender.org/index.php/Doc:2.6/Manual/Game_Engine/Blender_Player/Android_

Embora seja cedo para saber até onde isso irá, a implantação do Android para o mecanismo de jogo está começando a entrar em forma. Um ramo experimental do Blender, "soc-2012-swiss\_cheese" faz um Blenderplayer compatível com Android que pode abrir arquivos de jogo .blend simples. Animação, física, materiais GLSL e interação com o mouse já são suportados.

Na Figura 9.3, você pode ver o arquivo de amostra final do Capítulo 4 em execução em um telefone Android. Para ver isso em ação, vá para: [http://youtu.be/bF1m5b4jEKs](http://youtu.be/bF1m5b4jEKs).

![Implantação Android](../figures/Chapter9/Fig09-03.png)

Para executar o jogo, você pode baixar o aplicativo Blenderplayer para Android e abrir o jogo a partir dele. No momento em que este artigo foi escrito, o aplicativo ainda não estava no Android Market. Você pode baixá-lo neste tópico do fórum BlenderArtists: [http://blenderartists.org/forum/showthread.php?255746](http://blenderartists.org/forum/showthread.php?255746)

Uma plataforma móvel é um alvo de implantação limitado. Os telefones e tablets estão ficando mais potentes a cada dia, mas ainda faltam potência de hardware em comparação com PCs para jogos. Como tal, você precisa ter um cuidado especial ao otimizar seus jogos.

Algumas diretrizes gerais:

- Simplifique a geometria.

- Corte objetos grandes em partes pequenas.

- Use a seleção de oclusão quando possível.

- Trabalho com potência de duas texturas.

## Outras Ferramentas <a id="Other_Tools"></a>

O motor de jogo do Blender pode ser usado para prototipagem, antes que o jogo seja totalmente desenvolvido em outro motor de jogo. Ou, outra situação comum, você pode usar o Blender apenas para criação de ativos para um mecanismo externo, e o mecanismo de jogo do Blender para visualizar as reproduções de animação e interações básicas. Nesses casos, você não usará os componentes lógicos do jogo, mas principalmente se certificará de que seus ativos (objetos, materiais, animações) podem ser transferidos facilmente para outros motores.

>**Formatos de arquivo do Exchange**
>
> Quando o seu motor não suporta arquivos do Blender diretamente, você deve encontrar o melhor formato para exportar do Blender. Existe um formato no Blender voltado para jogos. Ele suporta não apenas malha e textura, mas também animação, sombreamento e física.
> Collada é um formato de arquivo de intercâmbio aberto mantido pelo consórcio Khronos (o mesmo grupo por trás do conhecido OpenGL, OpenCL e outros). > Embora o suporte para ele no Blender ainda não esteja completo, ele está chegando lá.
> Outro formato amplamente utilizado é o FBX. Este é um formato proprietário criado e mantido pela Autodesk com o suporte adequado no Blender sendo ativado e desativado nas versões anteriores.

Mesmo quando você está usando o Blender apenas para construir seus ativos, o motor de jogo pode ser de grande valor. Deve ser simples criar níveis de teste para as animações de seu personagem, ideias de teste e, em alguns casos, até mesmo construir um protótipo de jogo inteiro antes de migrar para outro motor.

No próximo capítulo, você aprenderá sobre alguns projetos que usaram a engine do jogo de uma forma ou de outra. Um desses projetos é o _Cubic World, _ originalmente criado no motor de jogo para um concurso de jogo. O projeto foi tão bem recebido que o principal desenvolvedor decidiu portá-lo para o iPhone, escrevendo um motor específico do zero. Esteja você construindo seu próprio motor, portando-o para uma alternativa aberta ou comercial, ou implantando com o motor de jogo, esteja ciente das alternativas para melhor apoiar suas decisões. Este é um tópico em constante mudança. As novas tecnologias vêm e vão, e cabe a você manter-se atualizado sobre o assunto. Inscreva-se para receber boletins informativos, visite fóruns e vá a conferências (embora possa eventualmente ajudar, não queremos dizer vagando pelo Twitter ou Facebook).

### GameKit <a id="GameKit"></a>

_www.gamekit.org_

GameKit é um "mecanismo de jogo básico que permite a prototipagem rápida construída em torno de software de código aberto gratuito para uso comercial". O GameKit usa Bullet para física, Ogre para renderização, OpenAL para som, Lua para scripts e AnimKit para animação (uma biblioteca autônoma criada especificamente para este mecanismo, mas aberta para uso em outros lugares). Ele lê arquivos do Blender e suporta todos os seus blocos lógicos.

Essa abordagem modular o torna bastante interessante para desenvolvedores independentes que frequentemente precisam projetar seu próprio mecanismo do zero. Você pode pegar emprestado o suporte para arquivos do Blender e motor de Renderização e implementar um sistema lógico único, por exemplo.

Um de seus principais benefícios sobre o mecanismo de jogo do Blender é que o GameKit oferece suporte total a plataformas que não sejam de PC, como Android e iOS. O GameKit também usa uma licença não viral, o que significa que os jogos que você cria podem ter qualquer licença que você desejar.

Quando este livro foi impresso, o GameKit ainda estava em seus estágios iniciais. No entanto, está gerando um certo entusiasmo na comunidade de jogos do Blender. Estamos acompanhando este projeto de perto e recomendamos que você faça o mesmo.

### Unity, SIO2 <a id="Unity,_SIO2"></a>

Enquanto o GameKit se destaca por sua forte integração com o Blender, existem outros engines com forte suporte para o arquivo nativo do Blender.

SIO2 é um motor voltado exclusivamente para o mercado móvel. Atualmente, ele suporta dispositivos Android e iPhone. Ele também suporta arquivos nativos do Blender, então não há necessidade de mexer com os tipos de arquivo de exportação.

Se o seu mercado não usa apenas dispositivos portáteis, o Unity3D é outro motor comercial que trabalha com arquivos do Blender; é tão simples quanto arrastá-los e soltá-los dentro do editor.

O Unity3D tem sido amplamente utilizado pela indústria indie. Eles suportam celulares a desktops e, quando você ler isto, provavelmente poderão ser implantados em todos os principais consoles do mercado. Você ainda precisa retrabalhar seus materiais depois de importá-los dentro do mecanismo, mas as alterações no arquivo original podem ser mescladas no editor Unity3D.

## Ciclo de Desenvolvimento do Blender <a id="Blender_Development_Cycle"></a>

O desenvolvimento do motor de jogo está ligado ao ciclo de desenvolvimento do próprio Blender. Embora as melhorias em diferentes partes do software sejam feitas separadamente, o lançamento de novas versões da engine do jogo acontece como parte dos lançamentos do Blender.

Uma vez por semana há uma reunião de desenvolvedores online [md] Reunião de Domingo do Blender. Na reunião, eles deliberam sobre questões pendentes, apresentam o desenvolvimento atual dos programadores e traçam planos para as próximas semanas e meses. As reuniões acontecem no canal #blendercoders da rede Freenode IRC todos os domingos às 16h. Hora de Amsterdã.

Para tópicos que requerem discussões mais longas e um público maior, os desenvolvedores usam uma lista de discussão hospedada nos servidores do Blender Institute: bf-committers@blender.org.

Para se inscrever nesta lista ou visitar seus arquivos, vá para: _http: //lists.blender.org/mailman/listinfo/bf-committers_

Propostas e roteiros são apresentados e discutidos em ambos os canais. Alguns projetos de longo prazo acabam descansando no wiki do Blender, que por sua vez pode ser incorporado na página de documentação oficial de desenvolvimento: _http: //www.blender.org/development/._

Aproximadamente a cada dois meses, um novo ciclo de lançamento é iniciado. Na primeira semana, as propostas de quais recursos devem estar no porta-malas (código oficial do Blender) são apresentadas, discutidas e, se necessário, votadas dentro ou fora do próximo lançamento do Blender.

Isso é especialmente aplicável para grandes recursos desenvolvidos em ramos (código ainda não incorporado ao tronco). Desenvolvedores podem passar longos períodos codificando, testando e pedindo feedback, antes que o código seja incorporado à fonte principal do Blender.

Para acompanhar os novos desenvolvimentos, para ajudar no teste beta de novos recursos e para garantir que mantemos o mecanismo de jogo compatível com as versões anteriores, você pode acompanhar os ramos, que são sempre anunciados nas reuniões de domingo do Blender e nas listas de discussão.

Além disso, se você quiser falar com os programadores do mecanismo de jogo do Blender diretamente, ou seguir nossas discussões, o canal IRC #bgecoders (também na Freenode) é um lugar onde o desenvolvimento é discutido.

## Como relatar bugs <a id="How_to_Report_Bugs"></a>

Todo software tem bugs. Não se engane sobre isso. Para quem não está familiarizado com essa terminologia técnica, um bug é um problema no software. Pense na última vez que você xingou um computador. Por trás das horas perdidas de trabalho está um bug (e a imprudência de não guardar o seu trabalho; não aprendeu nada jogando videogame?).

O Blender tem uma página dedicada exclusivamente a relatar e rastrear bugs dos usuários: _http: //projects.blender.org._

As diretrizes para relatórios de bugs são simples:

- Certifique-se de que você pode reproduzir o bug várias vezes.

- Recrie ou isole o bug no arquivo mais simples que você puder imaginar.

- Relate o ambiente em que você está trabalhando, se for relevante (SO, hardware, versão).

- Seja paciente. Relatar um bug pode ser uma tarefa demorada. E uma correção pode demorar muito, muito tempo com alguns testes adicionais e interações com você e os codificadores.

E lembre-se, quanto mais tempo você gasta fazendo um bom relatório [md] com bons arquivos de amostra, descrições concisas e assim por diante [md], mais você libera um desenvolvedor para trabalhar na correção do próprio bug.

## Faça Você Mesmo <a id="Do_It_Yourself"></a>

Como um pensamento final provocativo, você considerou literalmente expandir o motor de jogo sozinho? Não temos dado atenção suficiente ao fato de que o código-fonte do Blender está aberto e disponível para todos. Esse pode não ser o motivo pelo qual você entrou no software, mas é interessante explorar seu potencial.

O Blender e o motor de jogo são parcialmente mantidos pela Blender Foundation e parcialmente por programadores voluntários online. A maioria dos programadores começou como usuários, implementando recursos específicos necessários para seus projetos. No curto prazo, isso leva a soluções que tornam a vida mais fácil e um projeto mais completo. A longo prazo, ajuda a construir a comunidade que dedica energia ao projeto do motor de jogo.

Se nada mais, você pode tentar construir o Blender e substituir a tela inicial (veja a Figura 9.4). É definitivamente o primeiro passo para parecer legal e impressionar seu chefe:

_http: //wiki.blender.org/index.php/Dev: Doc / Building_Blender_

DF: Para ser substituído por uma tela inicial com o Blender 2.6, digamos, e a capa do livro. Esperando pela capa do livro.

![Tela inicial personalizada](../figures/Chapter9/Fig09-04.png)
