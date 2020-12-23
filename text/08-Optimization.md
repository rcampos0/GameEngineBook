**Table of Contents**

- [Chapter 8: Workflow and Optimization](#Chapter_8_Workflow_and_Optimization)
	- [Optimization Basics](#Optimization_Basics)
	- [Understanding Hardware](#Understanding_Hardware)
	- [Performance Target](#Performance_Target)
	- [Performance Scaling](#Performance_Scaling)
	- [When to Optimize](#When_to_Optimize)
	- [How to Optimize](#How_to_Optimize)
	- [The Performance Profiler](#The_Performance_Profiler)
		- [The Profiler](#The_Profiler)
	- [Quick 'n Dirty Optimization Techniques](#Quick_'n_Dirty_Optimization_Techniques)
	- [Advanced Optimization Techniques](#Advanced_Optimization_Techniques)
		- [Think Small](#Think_Small)
		- [Collision Proxy](#Collision_Proxy)
		- [Partial Collision](#Partial_Collision)
		- [Texture Baking](#Texture_Baking)
			- [Limitations of Texture Baking](#Limitations_of_Texture_Baking)
		- [Normal Map](#Normal_Map)
		- [Level of Detail](#Level_of_Detail)
		- [Object Culling](#Object_Culling)
		- [Scene Management](#Scene_Management)
		- [Linked Libraries](#Linked_Libraries)
			- [Linking vs. Appending](#Linking_vs._Appending)
			- [Relative Path vs. Absolute Path](#Relative_Path_vs._Absolute_Path)
            - [StreetLamp vs. Cube.001](#StreetLamp_vs._Cube.001)
		- [Layers](#Layers)
	- [Beauty Trumps Complexity](#Beauty_Trumps_Complexity)

# Capítulo 8: Fluxo de Trabalho e Otimização <a id="Chapter_8_Workflow_and_Optimization"></a>

Certa vez, disseram-nos que fazer um videogame é uma luta constante entre quatro forças elementares:
- Qualidade

- Atuação

- Tempo de desenvolvimento

- reuniões de segunda-feira de manhã

Ok, talvez o último item não deva estar na lista, o que a Figura 8.1 reflete. Mas a questão é que é fácil fazer um jogo visualmente impressionante quando o desempenho não é um problema. Por outro lado, também é fácil fazer um jogo ter um bom desempenho se o jogo tiver gráficos muito básicos. A parte difícil é conseguir os dois ao mesmo tempo. Felizmente, isso geralmente pode ser feito investindo mais tempo de desenvolvimento no projeto. Por fim, se você trabalhou em um ambiente de equipe, sem dúvida sabe que as reuniões de segunda-feira de manhã não garantem um jogo melhor, mas terminam em frustração e café derramado.

![A sagrada trindade do desenvolvimento de jogos](../figures/Chapter8/Fig08-01.png)

Neste capítulo, falaremos sobre algumas das técnicas usadas para melhorar o desempenho do jogo, acelerar o desenvolvimento e como sobreviver às reuniões de segunda-feira pela manhã para manter a alta administração feliz.

## Noções básicas de otimização <a id="Optimization_Basics"></a>

Fazer um videogame é uma ciência e uma arte. O aspecto criativo de um jogo não pode ser realizado sem tecnologia, e a tecnologia sozinha é inútil sem o trabalho criativo.

Quando jogamos, raramente pensamos nas centenas de funções do programa que são invocadas a cada segundo, nem nos milhões de linhas de códigos que são executados a cada quadro, nem nos bilhões de transistores que mudam de estado a cada nanossegundo para fazer tudo isso acontecer. Não pensamos em todas essas coisas porque nosso jogo roda em um motor de jogo, que roda em cima do sistema operacional, que por sua vez gerencia todo o hardware de baixo nível. Portanto, como desenvolvedor, você pode se concentrar em tornar o jogo divertido.

## Entendendo Hardware <a id="Understanding_Hardware"></a>

Dito isso, ter um bom conhecimento do hardware do computador é essencial no processo de criação do jogo, porque permite gerenciar os recursos de hardware limitados de forma eficiente. Tirar o máximo proveito do hardware disponível permite que o jogo seja executado o mais rápido possível.

Os principais componentes de um computador moderno estão listados abaixo:

- **CPU** (unidade de processamento central), ou processador, é freqüentemente chamado de cérebro do computador. Tudo é controlado pela CPU, com exceção dos gráficos, que são controlados pela placa de vídeo. Uma CPU mais rápida permite lógica e física mais complexas, pois essas coisas são calculadas na CPU. Hoje, muitas CPUs são multicore, portanto, podem fazer várias tarefas simultaneamente sem desacelerar. No entanto, uma CPU multicore não torna o jogo automaticamente mais rápido; o software precisa ser multithread de uma maneira que utiliza vários núcleos. Atualmente, o motor de jogo do Blender não está otimizado para tirar vantagem de múltiplos núcleos. Portanto, ter até mesmo um processador quad-core não aumenta significativamente o desempenho do jogo.

- **RAM** (memória de acesso aleatório), ou memória, é um local para armazenar dados temporários para programas em execução. Quanto mais complexa a cena, mais RAM será usada. Como a maioria dos computadores tem 4 GB de RAM ou mais, geralmente não precisamos nos preocupar em ficar sem memória, a menos que o jogo seja excepcionalmente grande. Para um jogo de pequena a média escala, o tamanho da memória efetivamente não é um problema.

- **GPU** (Unidade de processamento gráfico), ou placa gráfica, é um processador especialmente projetado para exibir gráficos 3D. O Blender usa a GPU para renderizar o mundo 3D, então uma placa de vídeo mais rápida definitivamente ajuda a tornar o jogo mais rápido. De modo geral, uma GPU mais rápida permitiria ao jogo ter uma geometria mais complexa, mais luzes e efeitos gráficos mais complexos.

## Alvo de desempenho <a id="Performance_Target"></a>

Se você é um jogador de PC, sem dúvida está familiarizado com a noção (talvez frustrante) de requisitos mínimos do sistema. Ao contrário dos consoles de videogame, que têm um conjunto fixo de hardware, os computadores variam muito em capacidade e desempenho. O requisito mínimo do sistema é uma forma de garantir que o jogo será executado em um nível de desempenho suficientemente aceitável para uma determinada configuração de hardware.

Uma das perguntas que você deve se fazer antes de iniciar qualquer projeto é: Quem é o seu público-alvo?

Por exemplo, se você está fazendo um jogo online casual baseado na Web, provavelmente deseja manter os requisitos de sistema relativamente baixos, para que um número maior de jogadores casuais possa apreciá-lo. Por outro lado, se o seu jogo for um jogo de ação totalmente desenvolvido, há uma chance maior de que ele seja apreciado por jogadores "sérios" com computadores relativamente rápidos. A Figura 8.2 ilustra a diferença gráfica entre um dos primeiros videogames e um jogo 3D moderno feito no Blender.

![_Pong_ (1972) vs. _Dead Cyborg_ (2010)](../figures/Chapter8/Fig08-02.png)
_Pong_ Source: Atari, Inc. Dead Cyborg [c] 2014 Endre Barath.

>**Blender na Web**
>
> A publicação de um jogo Blender como um jogo de navegador é mencionada no Capítulo 9, "Publicação e além".

Uma vez que uma meta mínima do sistema é definida, você pode começar a criar seu jogo sabendo exatamente quantos detalhes e complexidade você pode colocar nele. Você pode comprometer os detalhes para obter o desempenho que procura. Felizmente para nós, reduzir o nível geral de detalhes geralmente significa que os artistas têm menos trabalho a fazer.

## Escala de Desempenho <a id="Performance_Scaling"></a>

Depois que uma meta de desempenho foi decidida, a maioria dos estúdios de jogos ainda precisa pensar em como o jogo será executado em um hardware significativamente mais rápido ou mais lento do que a plataforma de destino.

Grandes jogos comerciais para PC são excelentes em termos de dimensionamento. Eles conseguem isso dando ao usuário as opções de alterar as configurações do jogo para caber em uma ampla gama de computadores. No entanto, fazer um jogo rodar bem em uma ampla variedade de computadores consome tempo, porque tempo adicional de desenvolvimento é necessário para garantir que o jogo funcione bem em todas as combinações de configurações. Por exemplo, você não quer que o jogo deixe de fora um efeito gráfico que é crucial para a jogabilidade apenas porque o usuário tem um computador mais lento.

O Blender possui algum suporte embutido para desabilitar certos recursos gráficos avançados, que podem ajudá-lo a adaptar o jogo a computadores mais antigos. A Figura 8.3 mostra _Yo Frankie! _ Sendo executado em diferentes níveis de detalhes.

![_Yo Frankie! _ Gráficos com efeitos de sombreamento desativados à direita](../figures/Chapter8/Fig08-03.png)

Ao executar no modo GLSL, os efeitos avançados de sombreador podem ser desativados para reduzir a carga de trabalho na placa gráfica. Essas configurações podem ser encontradas no Editor de Propriedades de Renderização, conforme mostrado na Figura 8.4.

![Editor de propriedades de renderização](../figures/Chapter8/Fig08-04.png)

- **Lights:** Desativa todos os cálculos de iluminação GLSL. Tem o maior impacto no desempenho, bem como no visual.

- **Shaders:** Desativa shaders de superfície GLSL avançados, apenas shaders básicos difusos e especulares serão usados.

- **Shadows:** Desativa sombras projetadas por lâmpadas.

- **Ramps:** Shaders de material de rampa desativados.

- **Nodes:** Desativa os sombreadores de Materiais do Nó.

- **Texturas Extras:** Desabilita texturas que não são mapeadas para o canal difuso de um material. Portanto, na verdade, isso desativará qualquer mapa especular, mapa normal ou emitirá textura, e apenas manterá a textura difusa na superfície.

Todas as opções acima só podem ser alteradas no modo GLSL. Nos modos Singletexture e Multitexture, o mecanismo de jogo sempre renderizará tudo exatamente da mesma maneira.

Além de mexer em recursos gráficos para influenciar o desempenho do jogo, muitos jogos comerciais também variam o nível de detalhe do objeto, reduzem a densidade dos efeitos das partículas e até mudam a qualidade do áudio para tornar o jogo mais suave em hardware mais antigo. Algumas dessas técnicas são explicadas neste capítulo.

## Quando otimizar <a id="When_to_Optimize"></a>

Ao longo do processo de desenvolvimento, você terá que tomar decisões de alto nível que afetarão o desempenho do jogo, por isso é importante manter o desempenho em mente o tempo todo. Por outro lado, fazer a micro-otimização muito cedo só vai desacelerar seu fluxo de trabalho, levando a bugs e às vezes tornando o jogo difícil de manter, o que é ruim.

Um exemplo de otimização prematura é compactar todas as texturas em JPEG para que ocupem menos espaço. Por que isso é ruim? JPEG é uma compactação com perdas [md] sempre que você abre e salva novamente um arquivo JPEG, alguns dados são perdidos. Portanto, ao editar constantemente um arquivo JPEG, sua qualidade de imagem diminuirá consideravelmente. Durante o desenvolvimento, é sempre melhor salvar os arquivos em formatos sem perdas, como TGA ou PNG. Isso se aplica a arquivos de áudio também; a edição deve sempre ser feita em formatos sem perdas, como WAV.

A Figura 8.5 mostra o artefato de compactação JPEG vs. TGA, que é compactado sem perdas.

![TGA sem perdas (esquerda) vs. JPEG altamente compactado (direita)](../figures/Chapter8/Fig08-05.png)

>**The Tale of Two Tabs**
>
> Para o projeto de visualização marinha subaquática em que Dalai Felinto e eu estávamos envolvidos na University of British Columbia, recebi a tarefa de "ver se você consegue colocar mais peixes na cena e fazê-la funcionar mais rápido" [md] um pedido típico de uma reunião de segunda-feira de manhã. Como esta visualização BGE já contém centenas de objetos na cena, eu simplesmente assumi que o Blender não era bom em lidar com um grande número de objetos separados. Mas, apesar do palpite (que se mostrou muito errado), continuei tentando diferentes cenários, ligando e desligando objetos, desligando scripts Python, brincando com a física e selecionando configurações. Então eu encontrei um script que, quando desabilitado, aceleraria o desempenho do jogo em cinco vezes! Quando 12fps de repente se tornou 60fps, eu sabia que havia encontrado a proverbial bala de prata. Mas, sendo o autor do script, não estava convencido de que um script de 70 linhas pudesse retardar o jogo tanto, então cavei mais, até que finalmente percebi que havia um erro no código que fazia um loop interno rodar muito mais do que deveria.
> Portanto, após duas horas de criação de perfil, a única descoberta foi um loop Python mal aninhado. A correção demorou dois segundos e envolveu a remoção da indentação do código ofensivo. Mas o resultado final foi espetacular, para dizer o mínimo.
> Erros bobos como esse podem não estar presentes em seu projeto. Sem encontrar um bug como esse, você nunca aumentará seu desempenho cinco vezes corrigindo alguns recuos no código. Mas nunca presuma que você sabe onde está o problema [md] sempre o perfil.

## Como Otimizar <a id="How_to_Optimize"></a>

Por mais óbvio que pareça, a primeira etapa da otimização é localizar o gargalo. Um gargalo é o ponto do jogo em que está demorando mais para ser computado. Focar no gargalo garantirá que o trabalho que você faz na otimização do jogo tenha o maior impacto no desempenho.

O senso comum no mundo da programação diz nunca presuma que você sabe onde está o gargalo. A experiência pode dizer onde deve estar a desaceleração, mas se houver um bug inesperado em algum lugar, o gargalo pode não estar onde você pensa que está. Sempre certifique-se de localizar o gargalo antes de tentar removê-lo. O perfil de desempenho no Blender pode lhe dar algumas informações muito perspicazes sobre o desempenho do jogo e onde pode estar o gargalo.

## O Perfil de Desempenho <a id="The_Performance_Profiler"></a>
O Blender tem um perfil de desempenho básico disponível para você. Ele fornece informações de tempo sobre quanto tempo um quadro leva para ser atualizado, bem como o detalhamento de quanto tempo o mecanismo de jogo gastou em tarefas específicas.

Para ligá-lo, vá para o Editor de Propriedades de Renderização e marque Framerate e Profile em Performance, como mostrado na Figura 8.6.

![Opções de desempenho no Editor de propriedades de renderização](../figures/Chapter8/Fig08-06.png)

O criador de perfil também pode ser acessado no menu superior em Jogo.

Depois de habilitado, você verá uma sobreposição de texto conforme ilustrado na Figura 8.7 no canto superior esquerdo ao executar o jogo.

![Sobreposição de informações de taxa de quadros e perfil](../figures/Chapter8/Fig08-07.png)

### The Profiler <a id="The_Profiler"></a>

A medida mais comum de desempenho para um aplicativo em tempo real é o quadro por segundo; é quantas imagens o computador pode renderizar por segundo. Esse número é mostrado na parte superior do criador de perfil de duas maneiras. Primeiro, como "troca", que se refere ao tempo que leva para trocar o quadro anterior pelo novo, expresso em milissegundos. Em segundo lugar, como um valor de "quadros por segundo" mais legível, expresso em hertz.

Descendo, você pode ver que o número na primeira coluna é o tempo que levou para concluir a operação em milissegundos; a segunda coluna é o mesmo valor expresso como uma porcentagem do tempo total.

Para entender o criador de perfil, basta olhar para a porcentagem relativa de tempo que leva para concluir todas as operações. A tabela abaixo mostra o significado de cada um.

_Tabela 8.1 Análise do Profiler_

| Rótulo      | Signficado                  | Hadware Usado | Taxa típica   |
|:----------:|:----------------------------:|:-------------:|:-------------:|
| Frametime  | Tempo Combinado              | Entire system | 100%          |
| Physics    | Tempo do Bullet physics      | CPU           | 10%           |
| Logic      | Tempo do Game Logic          | CPU           | 5%            |
| Animation  | Tempo de Animação            | CPU           | 5%            |
| Network    | Tempo de Rede                | Network       | 0%            |
| Scenegraph | Tempo de configuração de cena| CPU           | 10%           |
| Rasterizer | Tempo de Renderização        | Placa Gráfica | 65%           |
| Services   | Tempo Misc.                  | CPU           | 2%            |
| Overhead   | Tempo Misc.                  | CPU           | 2%            |
| Outside    | Tempo Ocioso                 | CPU           | 0%            |

É impossível dizer qual seria a proporção ideal do profiler-tempo. O rácio típico destina-se apenas a dar-lhe uma ideia geral do desempenho de um jogo "médio". Cada aplicativo é diferente. Um jogo de ação rápida com muita física poderia facilmente gastar 25 por cento do tempo em física, uma cena de corte com gráficos intensos pode gastar 95 por cento do tempo em rasterizador, enquanto uma visualização científica pode usar 40 por cento do tempo em lógica.

O tempo "fora" merece menção especial. Este tempo representa o tempo ocioso que não é gasto ativamente fazendo nada. Portanto, não se assuste se o valor externo for muito alto, especialmente quando a taxa de quadros estiver limitada a 60.

Além disso, as proporções mudam dependendo do hardware do computador. Por exemplo, um computador com uma placa de vídeo rápida passaria rapidamente pela renderização em quase nenhum momento, tornando a proporção de tempo de rasterização muito menor. Por isso, o criador de perfil funciona melhor quando é executado em um computador com hardware compatível com o público-alvo pretendido. Caso contrário, pode dar uma falsa sensação de onde está o gargalo.

Para uma análise detalhada do que cada um dos componentes faz, Mitchell Stokes escreveu um artigo muito abrangente sobre o assunto. Pode ser encontrado em http://wiki.blender.org/index.php/Doc:2.6/manual/Game_Engine/Performance/Display/Framerate_and_Profile.

## Quick 'n Dirty Optimization Techniques <a id="Quick_'n_Dirty_Optimization_Techniques"></a>

Depois de localizar a parte mais lenta do jogo olhando para o criador de perfil, aqui estão algumas coisas que você pode tentar para acelerar o jogo:

- **Desative a física para objetos não essenciais:** Se a física está consumindo uma grande parte do tempo da CPU, então talvez considere desativar a colisão para objetos não essenciais. Por padrão, todos os objetos na cena têm a detecção de colisão ativada, então isso pode ser lento. Mudar o tipo de física de estático para sem colisão fará com que o mecanismo de física funcione menos. A configuração é encontrada no Editor de propriedades físicas do objeto.

- **Mude para formas de colisão simples:** Quanto mais complexos os limites de colisão, mais difícil será o mecanismo de física. Considere o uso de formas simples que se aproximam dos modelos, alternando para uma caixa delimitadora diferente. A configuração é encontrada no Editor de propriedades físicas do objeto.

- **Use a lista de exibição:** Quando ativada, a lista de exibição armazena em cache os dados de geometria na placa gráfica para que eles não tenham que ser enviados para a placa gráfica a cada quadro; isso aumenta significativamente o desempenho de jogos que contêm geometria complexa. A configuração é encontrada no Editor de propriedades de renderização. Quase não há nenhuma desvantagem nesse recurso. Algumas placas gráficas muito antigas podem não suportá-lo, mas no momento em que este artigo foi escrito, a lista de exibição funcionava para quase todos os computadores em uso.

[lb] **Use texturas potentes:** As placas gráficas mais antigas esperam que as texturas tenham dimensões que são potências de dois. Por exemplo, 512 x 512 pixels, 2048 x 2048 pixels e 512 x 64 pixels são todos bons tamanhos. Tradicionalmente, texturas sem potência de dois são automaticamente estendidas para a próxima potência de dois mais alta, então uma textura de 513 x 513 pixels ocupará tanta memória quanto uma textura de imagem de 1024 x 1024 quando o jogo estiver rodando. Mesmo que a maioria das placas gráficas mais recentes não imponha esse requisito para tamanhos de imagem, é sempre uma boa ideia salvar manualmente todas as suas imagens em um tamanho mais compatível.

- **Use texturas compactadas DDS:** Se o seu jogo contiver muitos mapas de textura de alta resolução, eles ocuparão muita memória de vídeo. Formatos de arquivo como PNG, JPEG ou TGA são compactados no nível do arquivo, mas quando essas imagens são carregadas no Blender, elas são descompactadas em um formato bruto para que a placa gráfica possa decodificá-las rapidamente. Isso torna muito difícil estimar o uso da memória de textura com base no tamanho do arquivo, já que 40 MB de JPEG podem ocupar 200 MB de memória de textura real na placa gráfica. Se um jogo tiver muitas texturas, pode valer a pena olhar para as texturas compactadas Direct Draw Surface (DDS).

DDS é um nome comum que se refere a um conjunto de formatos de imagem compactados (especificamente DXT1 a DXT5) projetados para uso em tempo real. No Blender, as texturas DDS permanecem compactadas mesmo após serem carregadas na memória. Portanto, eles ocupam muito menos memória do que uma textura de imagem convencional.

Editores de imagens populares, como Photoshop e GIMP, possuem plug-ins que suportam o carregamento e o salvamento de arquivos DDS.

- **Reduza o número de luzes dinâmicas:** Se o rasterizador estiver ocupando muito tempo no criador de perfil, considere reduzir o número de luzes dinâmicas. Luzes dinâmicas são maravilhosas. Quando habilmente colocados e animados, eles contribuem com muito realismo para a cena. Infelizmente, eles têm um custo alto para a placa de vídeo: mais luzes significam desempenho mais lento. Portanto, use-os com moderação. De modo geral, é melhor manter o número de luzes abaixo de quatro. Lembre-se de que você pode realizar muitas coisas pré-fabricando os efeitos de luz, discutidos posteriormente neste capítulo.

Luzes com sombras em tempo real são ainda mais lentas.

- **Reduza o número de objetos:** Nem é preciso dizer que menos objetos são mais rápidos. Às vezes, mesmo reunindo todos os objetos estáticos em um, você pode obter um aumento de desempenho impressionante. Um grande número de objetos geralmente faz com que o tempo do gráfico de cenário no criador de perfil seja incomumente alto.

- **Use instanciamento:** Se o seu mundo de jogo é povoado por centenas de objetos idênticos, certifique-se de que eles compartilham uma malha. Isso é feito pressionando Alt + D para duplicar o objeto, em vez do Shift + D usual. O compartilhamento de blocos de dados torna o jogo carregado e executado mais rápido. Ao usar a instanciação, a cor do objeto pode ser uma maneira prática de adicionar alguma variação ao material sem ter que criar vários materiais.

- **Brinque com o tamanho da janela:** Se ao redimensionar a janela de exibição 3D para um tamanho menor, você obtém um aumento maior no desempenho, significa que o jogo é limitado pelo desempenho da taxa de preenchimento da placa gráfica. Objetos transparentes, sombreadores complexos e filtros 2D são todos pesados na taxa de preenchimento. Reduzir esses efeitos tornará o jogo mais rápido em placas gráficas mais lentas.

- **Use o Blenderplayer:** O Blenderplayer, o motor de jogo autônomo do Blender, pode ser um pouco mais rápido que o Blender. Então, se você está procurando um último pedaço de desempenho fora do jogo, tente mudar para o Blenderplayer. Na verdade, é sempre uma boa ideia usar o Blenderplay ao publicar seu jogo.

- **Observe o console:** Por padrão, a janela do console do Blender está oculta em todos os sistemas operacionais. Ligue o console e veja se há alguma mensagem de erro sendo impressa. As mensagens de erro geralmente indicam um problema muito maior com o jogo. Sem mencionar que uma quantidade excessiva de impressão do console pode tornar o jogo significativamente lento.

Para ativar a janela do console no Windows: Vá para Menu Principal> Janela> Alternar Console do Sistema

Para executar o Blender com uma janela de console no OS X ou Linux, execute o aplicativo a partir da linha de comando.

- **Experimente outra versão do Blender:** Quando tudo mais falhar, considere a possibilidade de que haja um bug no Blender que esteja causando a lentidão. (Isso já aconteceu antes.) Tente seu arquivo com outra versão (mais antiga ou mais recente) do Blender e veja se o problema de desempenho ainda está lá. Se você acredita que algo está anormalmente lento quando não deveria, envie um relatório de bug para que os desenvolvedores tenham a chance de consertá-lo. Isso pode não apenas resolver o seu problema, mas também torna o programa melhor para todos.

## Técnicas de Otimização Avançada <a id="Advanced_Optimization_Techniques"></a>

Aqui estão algumas outras técnicas de otimização mais avançadas para tentar.

### Pense pequeno <a id="Think_Small"></a>

Se você estiver fazendo um jogo grande, em vez de fazer uma paisagem extensa de um milhão de acres, considere separar o mapa em muitos pedaços menores e usar túneis, elevadores ou entradas habilmente projetados para acionar o carregamento de uma nova seção do mapa. Half-Life 2 é um exemplo maravilhoso disso; seu enorme terreno é, na verdade, composto de muitas zonas. Dessa forma, o computador não precisa carregar e renderizar tantos ativos de uma vez.

Além disso, se os blocos de nível forem mantidos em arquivos diferentes, ao contrário de diferentes cenas no mesmo arquivo, você também pode ter várias pessoas trabalhando nos níveis e não causar problemas de controle de versão.

Depois que o nível é dividido em seções diferentes, cada uma pode ocupar uma cena. Você pode usar o atuador Scene para alternar entre as cenas, conforme mostrado na Figura 8.8.

![Usando os atuadores de cena para carregar um nível diferente](../figures/Chapter8/Fig08-08.png)

### Proxy de colisão <a id="Collision_Proxy"></a>

Embora seja justificável gastar centenas, senão milhares, de polígonos em um modelo para torná-lo bonito na tela, a malha de colisão usada para física raramente precisa ser tão detalhada quanto a representação visual. Por causa disso, uma técnica comum usada em jogos é aproximar malhas físicas com primitivos embutidos, como cubos ou esferas. Esses são os mais rápidos de calcular.

Se mais definição for necessária, você pode criar um proxy de colisão para um objeto complexo. Um proxy de colisão é um shell simplificado e invisível que ocupa o mesmo espaço que o modelo visual, mas só é usado para detecção de colisão. A Figura 8.9 explica.

![Proxy de colisão: malha visual (L) vs. malha de colisão (R)](../figures/Chapter8/Fig08-09.png)

_**Tutorial**_
Para usar o proxy de colisão:

1. Abra /Chapter8/collisionProxy.blend.

2. A cena contém um modelo de árvore com alto polígono. Inicie o jogo e observe que todos os seus rostos reagem à colisão. Você pode confirmar pressionando a barra de espaço para lançar bolas na árvore. Observe que não importa onde a bola atinja a árvore, ela detectará a colisão.

3. Se você tem uma CPU mais lenta, observe também que a física está demorando muito, principalmente por causa da complexidade da malha da árvore.

4. Para visualizar melhor o que está acontecendo, ative Mostrar visualização física no menu superior. Todas as faces com colisão ativada serão destacadas em verde quando o jogo estiver em execução.

5. Se tivermos que construir um proxy de colisão para o objeto árvore manualmente, isso envolverá a modelagem de uma malha que tem o formato bruto da árvore, mas usando muito menos detalhes. Para este exercício, uma versão simplificada da árvore foi criada para você. Na camada 2 do arquivo, você encontrará um proxy de colisão que se ajusta à árvore. O modelo consiste nos troncos principais das árvores, combinados com uma esfera para aproximar a copa.

6. Ative as camadas 1 e 2: Pressione a tecla 1 e, enquanto mantém pressionada a tecla Shift, pressione a tecla 2.

7. Para vincular o modelo de árvore de alto detalhe ao modelo de árvore de baixo detalhe, iremos gerenciá-los juntos. Primeiro, clique com o botão direito do mouse no objeto treeHigh para selecioná-lo; em seguida, enquanto mantém pressionada a tecla Shift, clique com o botão direito no objeto TreeProxy para selecioná-lo também. Agora, simplesmente pareie o objeto treeHigh ao objeto treeProxy pressionando Ctrl + P. Observe que a ordem em que selecionamos os dois objetos é importante!

8. No momento, ambos os objetos ainda estão com a colisão e a tela ativadas. Se você fosse jogar agora, o mecanismo do jogo teria dificuldade para tentar resolver a colisão entre dois objetos que estão ocupando o mesmo espaço e exibir uma confusão de polígonos em colisão.

9. Para remover a propriedade de colisão em treeHigh: Selecione treeHigh. No Editor de propriedades de física, defina o tipo de física como Sem colisão.

10. Para desativar a visibilidade do treeProxy, selecione treeProxy. No Editor de propriedades físicas, ative o botão Invisível.

11. Execute o jogo agora para ver como a colisão é tratada por treeProxy, enquanto treeHigh é exibido.

12. Lembre-se de que, como treeProxy é o pai de treeHigh, qualquer tijolo lógico deve ser anexado ao objeto proxy. treeHigh é simplesmente um modelo sem colisões, sem lógica e de boa aparência.

![Proxy de colisão: malha visual (L) vs. malha de colisão (R)](../figures/Chapter8/Fig08-10.png)

Então, isso é proxy de colisão em poucas palavras. Como você pode ver, muitas etapas estão envolvidas nessa abordagem, o que torna o uso de proxy de colisão adequado apenas para modelos muito complexos que têm uma forma única. Caso contrário, é muito mais fácil (e eficiente) usar uma das primitivas de limite de colisão predefinidas.

### Colisão Parcial <a id="Partial_Collision"></a>

Outra alternativa ao proxy de colisão é simplesmente desligar a colisão em parte do modelo. Isso pode ser feito no Editor de propriedades do material. Ao adicionar vários materiais, você pode controlar qual parte do modelo é detectada por colisão e qual parte é ignorada pela detecção de colisão.

_**Tutorial**_

1. Abra /Chapter8/collisionMultiMaterial.blend.

2. Inicie o jogo e observe que todo o objeto da árvore reage à colisão. Você pode confirmar isso olhando para a visualização da física do wireframe.

3. Para fazer o jogo funcionar melhor, desabilitemos as colisões para os galhos menores das árvores.

4. Selecione o objeto árvore e vá para o Editor de Propriedades de Material.

5. Selecione o slot de material denominado _Trunk_ e certifique-se de que a caixa de seleção Physics esteja ativada.

6. Selecione o slot de material denominado _Branches_ e desative a colisão desmarcando a caixa de seleção Física. O arquivo resultante deve ser semelhante à Figura 8.11

7. Execute o jogo novamente e observe que os ramos menores serão ignorados pelo mecanismo de física. Isso não apenas irá liberar alguns cálculos físicos, mas também tornará o jogo mais realista, permitindo que os objetos passem pelas folhas.

![Editor de propriedades de materiais](../figures/Chapter8/Fig08-11.png)

### Texture Baking <a id="Texture_Baking"></a>

O mecanismo de renderização do Blender é capaz de criar alguns efeitos impressionantes. Você não gostaria de ter esse nível de qualidade gráfica em seu jogo? Com cozimento de textura, você pode! O cozimento de textura é o processo de renderização de efeitos, como mapa de sombras, oclusão de ambiente e mapas de luz em uma textura, para que eles não precisem ser calculados em tempo real.

O cozimento de textura requer que o material seja configurado de forma que possa ser renderizado pelo mecanismo de renderização interno. Então, com mais alguns cliques, o material renderizável será cozido em uma textura de imagem que pode ser usada no jogo.

Todo o fluxo de trabalho pode ser resumido como:

1. Torne o material do objeto compatível para renderização.

2. Objeto de desembrulhar UV.

3. Asse.

4. Reatribua a textura cozida ao objeto.

_**Tutorial**_
Vamos experimentar:

1. Abra /Chapter8/TextureBaking.blend.

2. Execute o jogo e observe que a cena interna é muito plana e a iluminação não é muito realista.

3. Saia do jogo e pressione F12 para fazer uma renderização da cena. É assim que queremos que nossa cena se pareça no jogo. Feche a imagem renderizada pressionando F11.

4. Para assar a textura, você precisa primeiro desdobrar a cena por UV para que a textura assada tenha um lugar para ir. Para fazer isso, clique com o botão direito para selecionar o objeto do quarto. Entre no modo de edição com um toque rápido na tecla tab. Pressione a tecla U para invocar o menu UV Unwrap. Selecione Pacote de mapas de luz.

5. No menu pop-up mostrado na Figura 8.12, certifique-se de que a caixa de seleção New Image esteja ativada; isso irá garantir que uma textura de imagem vazia seja criada para você. Clique em OK para desembrulhar o modelo.

![Caixa de diálogo Lightmap Pack UV](../figures/Chapter8/Fig08-12.png)

6. Para um modelo mais complexo, pode ser necessário desdobrar manualmente um modelo por UV, mas para este exercício, o desdobramento automatizado é suficiente. Lembre-se de que para que o cozimento da textura funcione corretamente, o layout UV não deve ter nenhuma região sobreposta. Caso contrário, o cozimento será renderizado na mesma coordenada de textura várias vezes, causando um artefato.

7. Para preparar textura para o objeto de quarto, vá para a parte inferior do Editor de propriedades de renderização, onde a função Bake é encontrada, conforme mostrado na Figura 8.13.

![Painel Bake ](../figures/Chapter8/Fig08-13.png)

8. O seletor Modo de cozimento controla o que será cozido em uma textura. Full Render irá assar toda a cor, luz, sombra e textura na textura. Oclusão de ambiente é outra comumente usada.

9. Selecione Full Render para este projeto e clique em Bake. Isso pode levar alguns minutos, dependendo da complexidade do modelo. Conforme a textura é renderizada, você pode ver a textura cozida preenchendo o Editor de Imagens na parte inferior da tela.

10. Quando o cozimento da textura estiver concluído, deve ser semelhante à Figura 8.14

![A textura cozida](../figures/Chapter8/Fig08-14.png)

11. Agora que o cozimento está concluído, saia do modo de edição alternando a tecla Tab.

12. Finalmente, você precisa dizer ao motor de jogo para usar a textura que você acabou de assar, ao invés dos materiais antigos. A maneira mais fácil é deletar todos os três materiais do objeto clicando no botão [-] no Editor de Propriedades do Material. Esta é uma maneira barata e rápida de forçar o Blender a usar a textura que você acabou de criar.

13. Execute o jogo agora. Observe que toda a luz e cor que você viu na renderização são visíveis em tempo real. No entanto, os efeitos especulares, como realces especulares e reflexos, não podem ser cozidos. Portanto, eles ainda não estão visíveis.

14. A imagem lightmap não é salva automaticamente. Para salvar a imagem, clique em Imagem> Salvar como no Editor de imagens. Você também pode salvar a imagem pressionando F3 com o mouse sobre o editor de imagens.

15. A Figura 8.15 mostra a versão finalizada, que pode ser encontrada em /Chapter8/TextureBaking-finished.blend

![A cena cozida (esquerda) vs. a cena original (direita)](../figures/Chapter8/Fig08-15.png)

#### Limitações do cozimento de textura <a id="Limitations_of_Texture_Baking"></a>

Como com tudo que "parece bom demais para ser verdade", geralmente há um problema.

- Com cozimento de textura, apenas efeitos de iluminação independentes de visão podem ser cozidos. Portanto, embora a cor difusa possa ser transformada em textura porque a cor difusa não está vinculada ao ângulo de visão da câmera, os realces e reflexos especulares são ignorados durante o cozimento da textura porque os realces especulares são luzes dependentes da visualização; não há como assá-los em uma textura estática.

- O cozimento de texturas é um ato de sacrificar a flexibilidade pelo desempenho. Depois que uma cena é preparada, ela se torna bastante estática. Por exemplo, mover um objeto depois de preparar o mapa de luz pode resultar em um ponto preto e alguma sombra fantasma de aparência estranha. Portanto, geralmente o cozimento leve é ​​limitado apenas ao ambiente estático.

- Cada objeto deve ser mapeado em UV de uma maneira não sobreposta. Se duas áreas de um objeto compartilham a mesma coordenada de textura, elas não serão exibidas corretamente.

- Tenha em mente que o Blender não salva arquivos de imagem automaticamente, então certifique-se de salvar manualmente o arquivo de textura cozido clicando em Imagem> Salvar.

Apesar das limitações, o cozimento de texturas é um método popular amplamente usado para incluir efeitos de luz sofisticados em tempo real. Além de assar renderizações completas, também é possível assar apenas um mapa de oclusão do ambiente. A textura de oclusão do ambiente cozido pode então ser usada como uma textura secundária para influenciar o sombreamento da superfície de um objeto.

### Normal Map <a id="Normal_Map"></a>

Cozinhar um mapa normal é na verdade apenas um caso especial de cozimento de textura. O cozimento de mapa normal é comumente usado para gerar um mapa normal tangente de um modelo de alta resolução para mapear em um modelo de baixa resolução.

Então, o que é um mapa normal?

Um mapa normal é um arquivo de imagem regular, mas em vez de influenciar a cor da superfície como uma textura de cor regular, os mapas normais são usados para alterar a normal da superfície por pixel. Ao alterar a normal da superfície, você pode alterar a irregularidade aparente de uma superfície. O efeito de um objeto mapeado normal é aquele que tem muito mais fidelidade aparente do que a malha subjacente real. A Figura 8.16 mostra o efeito de um mapa normal.

![Da esquerda para a direita: modelo original de alta resolução, modelo de baixa resolução, modelo de baixa resolução com mapas normais](../figures/Chapter8/Fig08-16.png)

Existem duas maneiras de criar um mapa normal:

1. Um mapa normal pode ser criado em uma ferramenta de edição de imagem, como Photoshop ou GIMP. Estão disponíveis plug-ins que podem converter um mapa de altura em preto e branco em um mapa normal.

2. Use a ferramenta embutida do Blender para preparar um mapa normal de um modelo de polígono alto para um modelo de polígono baixo.

_**Tutorial**_
Para preparar um mapa normal de um modelo de polígono alto para um modelo de baixo polígono:

1. Abra /Chapter8/NormalMap.blend.

2. Observe que temos dois objetos do mesmo modelo: um modelo de alta resolução que usaremos como entrada e um modelo de baixa resolução para o qual prepararemos o mapa normal. Eles ocupam o mesmo espaço porque isso é necessário para que o processo normal de confecção de mapas funcione corretamente.

3. Assim como na confecção de mapas de luz, primeiro você precisa desdobrar o modelo em UV para que a confecção de texturas saiba onde colocá-la. Selecione o modelo de baixa resolução (já que é para ele que você está cozinhando). Vá para o modo Edit, pressione U e selecione Unwrap.

4. Como nenhuma textura de imagem é criada automaticamente para você, crie manualmente um novo bloco de dados de textura de imagem clicando no botão Novo no Editor de imagens. Uma resolução de 1024 é suficiente para este exemplo.

5. Agora vem a parte complicada. Primeiro, selecione o modelo de alta resolução; em seguida, mantenha pressionada a tecla Shift para adicionar o modelo de baixa resolução à seleção. Desta forma, ambos os objetos devem ser selecionados, sendo o modelo de baixa resolução o objeto ativo. Você pode selecionar o objeto do Outliner para tornar o processo mais simples.

6. No Render Properties Editor, selecione Normal from Bake mode e então clique em Bake.

7. Assim que o cozimento estiver pronto, a textura cozida deve ter uma tonalidade roxa. Se a cor estiver apagada, certifique-se de que você está preparando um mapa normal no espaço normal correto (tangente), conforme mostrado na Figura 8.17.

![Mapa normal cozido](../figures/Chapter8/Fig08-17.png)

8. Neste ponto, você não precisa mais do modelo de alta resolução. Mova o objeto para uma camada diferente ou exclua-o.

9. Para usar o mapa normal, crie uma textura de material e imagem para o modelo de baixa resolução, conforme mostrado na Figura 8.18.

![Material normal do mapa](../figures/Chapter8/Fig08-18.png)

10. O resultado final deve ser semelhante ao arquivo Chapter8 / NormalMap-Finished.blend.

Se você estiver curioso, um mapa normal usa os três canais de cores (RGB) para armazenar as direções normais (XYZ) de uma superfície. Como a maioria dos normais de superfície está apontando para fora, eles têm um valor normal de (X = 0,5, Y = 0,5, Z = 1,0), que é o que dá aos mapas normais essa cor roxa distinta.

>**Normal Map Utilities**
>
>The two most popular normal map utilities seem to be Gimp-NormalMap for (you guessed it!) the GIMP (http://code.google.com/p/gimp-normalmap) and NVIDIA Texture Tools for Photoshop (http://developer.nvidia.com/nvidia-texture-tools-adobe-photoshop).

### Level of Detail <a id="Level_of_Detail"></a>

Level of detail (LOD) is a general term referring to ways to adjust the complexity of the object, depending on its perceived size. The idea is that objects farther away are smaller and generally less significant to the gameplay. Therefore, they can often be removed or simplified.

Ideally, LOD requires computing the size of the object on the screen. Because this is usually very difficult to achieve, LOD is commonly done by looking at the distance between the camera and the object.

For a complex mesh, you can create multiple copies of the same model, with decreasing complexity. So when an object is a certain distance away from the camera, you can ask Blender to swap the mesh to a less detailed version. Additionally, as the object gets further away, you can even set the object to invisible, which avoids rendering that object completely.

Unfortunately, Blender does not have built-in support for LOD, so you have to create your own with Python.

A reference implementation of a LOD system can be found at /Chapter8/LoD.blend. This implementation uses a small script that keeps track of the distance of the object to the camera, and replaces the mesh with a less detailed one as the distance increases. Figure 8.19 shows the script-based LOD system.

![LOD system](../figures/Chapter8/Fig08-19.png)

The script should be a good place for you to start tinkering with your own LOD implementation.

### Object Culling <a id="Object_Culling"></a>

To make the game run as efficiently as possible, objects that are not visible should not be rendered. While it might be obvious that everything behind a solid wall should not be processed, the computer will need a bit more help to accomplish that.

To help the game engine cull objects, set up occluders to hide part of the scene from view. For example, occluders can be used to mark the separation between an indoor scene and an outdoor scene. A sample file is provided at /Chapter8/culling.blend. The effect of culling is shown in Figure 8.20.

![Object Culling: game view (Left), no occluder (Centre), house as occluder (Right)](../figures/Chapter8/Fig08-20.png)

To see the effects of occlusion culling, make sure that you are in wireframe view.

First, run the sample file. Notice that everything inside the house is visible, even when the camera is outside. This is because there is no occluder object.

Now, set the WallOccluder object to be an occluder and rerun the game. Notice that the wall effectively hides objects inside the house until the camera is inside.

Keep in mind that culling is done on a per-object basis. Blender will not hide part of the model. Therefore, occlusion culling is effective only when there are many small objects in the scene hiding behind a large object.

### Scene Management <a id="Scene_Management"></a>

Optimization isn't just about making your game fast; it is also about keeping the project organized and easy to manage. As the game project becomes larger, it gets progressively harder to keep everything organized. Here are some things you can do to maintain your own sanity:

### Linked Libraries <a id="Linked_Libraries"></a>

The size of a single Blender file is virtually unlimited, so in theory, you can make a massive game with everything stored in a one Blender file. However, this approach is not practical for many reasons. Only one person at a time can edit a Blender file. So how do you spread a large project out so that multiple people can work on different aspects of it at the same time, without overwriting each other's work?

The answer is Blender's library system. You have already been exposed to linking and appending in Chapter 2. It's a system that allows you to bring in data blocks (such as a character model) from other Blender files into the current file. This way, each asset can be worked on at the same time separately. This also makes reusing of assets easier.

The game _Yo Frankie!_ (available for free online) is a great example of how a large game project is organized. In it, each entity (for example, tree, character model, and rocks) has its own Blender file, which can be linked into a master file, which makes up the game level.

#### Linking vs. Appending <a id="Linking_vs._Appending"></a>

Both functions import data blocks in Blender from an external file. The difference is that append makes a copy of the data block, and in doing so, severs the ties with the original library file. Once an append operation is done, you can edit, move, or even delete the library file without any consequences on the appended object.

Link does not make a new copy of the data block, but instead references the library file every time the master Blender file is loaded. This way, changes made to the linked object will be propagated to master file.

Linking is generally preferred over appending since it doesn't replicate the data blocks.

#### Relative Path vs. Absolute Path <a id="Relative_Path_vs._Absolute_Path"></a>

Once you start referencing external files (such as image textures and audios files) into a project, you need to decide if you want Blender to point to that file using a relative file path (the default option) or an absolute file path. Generally, keeping paths relative means it's easier to move a whole project around, as long as the overall folder structure is maintained. If multiple people are working on a project jointly using a file-share or source-management system, using relative path is absolutely crucial.

Blender has some helpful tools under the File > External Files menu that can let you mange file paths.

#### StreetLamp vs. Cube.001 <a id="StreetLamp_vs._Cube.001"></a>

A scene teeming with objects with unhelpful names like Cube.001, Cylinder.87, and Material.002 would be a nightmare to manage. First, scripts that refer to objects by their name will be harder to understand if object names aren't clear. By keeping everything named, you reduce the time it takes searching for something.

Assigning proper names is not only limited to objects. All data blocks in Blender can be renamed. This includes objects, object data, lamps, materials, textures, and image data blocks. Renaming everything might seem like a lot of work, even borderline OCD, but once you are used to it, it really does make the project easier to manage. Think of the poor intern who has to pick up your project six month later!

### Layers <a id="Layers"></a>

Not unlike the layer functionality in a 2D image-editing program, the layer functionality in a 3D program is mostly there to keep the scene organized. Blender provides 20 layers for you to work with. How these layers are utilized is up to the artist. Since you cannot assign names to layers, it will be up to you to keep track of, and perhaps document, how the layers are being used.

## Beauty Trumps Complexity <a id="Beauty_Trumps_Complexity"></a>

Armed with these newly acquired optimization methods, you might be tempted to beef up the game with more details. More polygons! Higher-resolution textures! Larger explosions! (Cough[md]Michael Bay[md]Cough.) It's easy to lose sight of the big picture. A visually beautiful game does not have to be photorealistic, nor does it have to be crammed to the brim with details. Sometimes, simple visuals can be just as powerful.

Below are a few games that are faithful to the adage that "less is more":

- **Journey**: http://thatgamecompany.com/games/journey/

- **Limbo**: http://limbogame.org/

- **Love**: http://www.quelsolaar.com/love/
