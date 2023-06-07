---
title: Introdução à Linha de Comando Bash
layout: lesson
date: 2023-05-29
authors:
- Ian Milligan
- James Baker
reviewers:
- M. H. Beals
- Allison Hegel
- Charlotte Tupman
editors:
- Adam Crymble
translator:
- Eric Brasil
difficulty: 1
review-ticket:
activity: transforming
topics: [data-manipulation, get-ready]
abstract: "Essa lição lhe ensinará como enviar comandos utilizando uma interface de linha de comando, ao invés de uma interface gráfica. Interfaces de linha de comando possuem vantagens para usuários de computador que precisam de maior precisão em seu trabalho, como historiadores/as digitais. Permitem mais detalhamento ao rodar alguns programas, visto que você pode adicionar modificações para especificar exatamente como deseja que o programa execute. Além do mais, podem ser facilmente automatizados através de scripts, que são basicamente receitas de comandos baseados em texto."
next: research-data-with-unix
redirect_from: /lessons/intro-to-bash
avatar_alt: Soldiers in antique armor with spears
doi: 
---

{% include toc.html %}





# Introdução à Linha de Comando Bash

## Introdução

Muitas das lições do *Programming Historian* exigem que você insira comandos através de uma **interface de linha de comando**. A maneira usual de os usuários de computador hoje interagirem com seu sistema é através de uma **interface gráfica do usuário** ou GUI. Isso significa que, quando você entra em uma pasta, clica em uma imagem de uma pasta de ficheiro; quando você executa um programa, você clica nele; e quando você navega na web, você usa o mouse para interagir com vários elementos em uma página da web. Antes da ascensão das GUIs no final dos anos 1980, no entanto, a principal maneira de interagir com um computador era através de uma interface da linha de comando.

{% include figure.html filename="GUI.png" caption="GUI do computador de Ian Milligan" %}

Interfaces de linha de comando possuem vantagens para usuários de computador que precisam de maior precisão em seu trabalho -- tal como historiadores digitais.Elas permitem maior detalhamento quando executando alguns programas, ao passo que você pode adicionar modificações para especificar exatamente como deseja que o programa execute. Além do mais, elas podem ser facilmente automatizadas através de [scripts](http://www.tldp.org/LDP/Bash-Beginners-Guide/html/chap_01.html), que são basicamente receitas de comandos baseados em texto.

Existem duas interfaces de linha de comando principais, ou 'shells,' que muitos historiadores digitais utilizam. No SO X ou muitas distribuições Linux, o shell é conhecido como `bash`, ou o 'Bourne-again shell' (*shell renascido*). Para usuários de sistemas baseados no Windows, a interface de linha de comando é por padrão baseada em `MS-DOS`, que utiliza comandos e [sintaxe](http://en.wikipedia.org/wiki/Syntax) distinta, mas que comumente pode atingir tarefas similares. Essa lição oferece uma introdução básica ao terminal `bash`, e usuários Windows podem acompanhar instalando shells populares como [Cygwin](https://www.cygwin.com/) ou Git Bash (veja abaixo).

Essa lição utiliza um **[shell Unix](http://en.wikipedia.org/wiki/Unix_shell)**, que é um interpretador de linha de comando que provê uma interface de usuário para o sistema operacional [Unix](http://en.wikipedia.org/wiki/Unix) (em inglês) e similares. Essa lição cobre uma número pequeno de comandos básicos. Ao final desse tutorial, você será capaz de navegar pelo seus sistema de ficheiros e encontrar ficheiros, abri-los, executar tarefas de manipulação de dados básicos tal como combinar e copiar ficheiros, assim como lê-los e fazer edições relativamente simples. Esses comandos constituem o alicerce sobre o qual comandos mais complexos podem ser construídos para se adequar aos seu projeto ou dados de pesquisa. Leitores que busquem um guia de referências que vá além dessa lição são recomendados a ler *Unix and Linux: Visual Quickstart Guide*, 4ª edição (2009) de Deborah S. Ray e Eric J. Ray.

## Apenas para Windows: Instalando o Git Bash

Para aqueles com SO X, e a maioria das distribuições Linux, vocês estão com sorte — vocês já possuem um shell bash instalado. Para aqueles com Windows, vocês precisarão de um passo extra e  instalar o Git Bash. Ele pode ser instalado após o download do mais recente 'Full installer' (_instalador completo_) nessa [página](https://git-for-windows.github.io/) (em inglês). Instruções para instalação estão disponíveis no [Open Hatch](https://web.archive.org/web/20190114082523/https://openhatch.org/missions/windows-setup/install-git-bash) (em inglês).

## Abrindo o seu Shell

Vamos iniciar o shell. No Windows, execute o Git Bash a partir do diretório em que você o instalou. Você terá que executar como administrador - para tal, clique com o botão direito do mouse e selecione 'Executar como administrados.' No SO X, por padrão o shel est´a localizado em:

`Applications -> Utilities -> Terminal`

{% include figure.html filename="Terminal.png" caption="O programa Terminal.app no OS X" %}

Quando você o executa, verá esta janela.

{% include figure.html filename="Blank-Terminal.png" caption="Uma tela vazia do terminal em nosso SO X" %}

Você pode querer alterar a aparência padrão de seu terminal, pois os olhos podem se cansar ao olhar repetidamente para texto preto em um fundo branco. Na alpicação padrão do SO X, você pode abrir o menu 'Settings' nas 'Preferences' no Terminal. Clique na guia 'Settings' e altere-a para um novo esquema de cores. Pessoalmente, preferimos algo com um pouco menos de contraste entre o fundo e o texto, já que você estará olhando para isso por muito tempo. 'Novel' é um agradável, assim como o popular conjunto de paletas de cores [Solarized](http://ethanschoonover.com/solarized).Para usuários Windows, um efeito similar pode ser alcançado utilizando a aba `Properties` do Git Bash. Para alcançá-la, clique com o botão direito do mouse em qualquer lugar na barra superior e selecione `Propriedades`.

{% include figure.html filename="Settings.png" caption="A tela de configurações da Aplicação Shell Terminal do SO X" %}

Assim que você estiver satisfeito(a) com a interface, vamos começar.

## Moving Around Your Computer's File System

Se, ao abrir uma janela de comando, vocês está incerto de onde está localizado no sistema de ficheiros do computador, o primeiro paço é encontrar qual diretório você está. Diferentemente de um sistema gráfico, quando num shell você não pode estar em múltiplos diretórios ao mesmo tempo. Quando você abre seu explorador de diretórios em sua área de trabalho, ele está mostrando ficheiros que estão dentro de um diretório. Você pode descobrir em qual diretório você está através do comando `pwd`, que significa "print working directory" (_imprima o diretório de trabalho_) tente digitar:

`pwd`

e apertar enter. Se você está em um SO x ou Linux, seu computador provavelmente mostrará `/users/USERNAME` com seu nome no lugar de USERNAME. Por exemplo, O caminho de Ian no SO X é `/users/ianmilligan1/`.

Aqui é onde você percebe que aqueles utilizando Windows e aqueles utilizando SO X/Linux terão expperiências um pouco distintas. No Windows, James está em :

`c/users/jbaker`

Existem pequenas diferenças, mas não tenha medo; uma vez que você esteja movendo e manipulando ficheiros, essas divergências de plataformas podem ficar em segundo plano.

Para nos orientar, vamos ver uma lista de quais ficheiros estão nesse diretório. Digite

`ls`

e você verá uma lista de cada ficheiro e diretório no interior de sua atual localização. Seu diretório pode estar confuso ou impecável, mas você verá pelo menos algumas localizações familiares. No SO X, por exemplo, você verá `Applications`, `Desktop`, `Documents`, `Downloads`, `Library`, `Pictures`, etc.

Você pode querer mais informações do que apenas uma lista de ficheiros. Você pode fazer isso ao especificar variadas *flags* para acompanhar nossos comandos básicos. Elas são adições a um comando que provê o computador com um pouco mais de direcionamento sober qual tipo de retorno ou manipulação você pretende. Para acessar uma lista de *flags*, usuários de SO x/Linux podem recorrer ao programa de ajuda integrado. Usuários SO X/Linux podem digitar:

`man ls`

{% include figure.html filename="man-ls.png" caption="A página Manual para o comando LS" %}

Aqui, você vê uma lista dos nomes do comando, as possibilidades de formatação do comando e o que ele faz.   **Muitos deles não farão sentido agora, mas não se preocupe; com o tempo você se ficará mais familiarizado com eles.** Você pode explorar essa página de várias formas: a barra de espaço move uma página abaixo, ou você pode usar as setas para cima e para baixo por todo documento.

Para sair da página do manual, aperte

`q`

e você será trazido de volta para a linha de comando onde você estava antes de entrar na página do manual.

Tente explorar a página `man` para o outro comando que aprendeu até agora, `pwd`.

Usuários de Windows podem utilizar o comando `help`, embora esse comando tenha menos recursos do que o `man` no SO X/Linux. Digite `help` para ver a ajuda disponível, e `help pwd` para obter um exemplo da saída do comando.

Vamos tentar utilizar algumas da opções que você viu na página `man` para ls. Talvez você queira ver apenas os ficheiros TXT que estão no seu diretório inicial. Digite

`ls *.txt`

o que retorna uma lista de ficheiros de texto, se você tiver algum no seu diretório inicial (talvez você não tenha, e tudo bem também). O comando \* é um **wildcard** — significa 'qualquer coisa.' Portanto, nesse caso, você está indicando que qualquer coisa que atenda o padrão:

[qualquer_coisa.txt]

será mostrada. Tente diferentes combinações. Se, por exemplo, você possui vários ficheiros no formato `1-Canadian.txt`, `2-Canadian.txt`, e assim por diante, o comando `ls *-Canadian.txt` irá mostrar todos eles mas escluirá todos os outros ficheiros (aqueles que não correspondem ao padrão).

Digamos que você quer mais informações. Naquela longa página `man`, você viu uma opção que pode ser útil:

>     -l      (a letra "ele" minúscula.)  List in long format.  (See below.)  If the output is to a terminal, a total sum for all the file sizes is output on a line before the long listing.

Logo, se você digitar

`ls -l`

O computador retornará uma lista onga de ficheiros que contém informações similares ao que você encontraria no seu explorador de ficheiros: o tamanho do ficheiro em bites, a data de sua criação ou última modificação, e o nome do ficheiro. Entretanto, isso pode ser um pouco confuso: você vê que um ficheiro test.html possui '620' bites. Em linguagem comum, você está mais acostumado a unidades de medidade como bytes, kilobytes, magabytes e gigabytes.

Felizmente, existe outra *flag*:

>     -h      When used with the -l option, use unit suffixes: Byte, Kilobyte,
>             Megabyte, Gigabyte, Terabyte and Petabyte in order to reduce the number
>             of digits to three or less using base 2 for sizes.

Quando você quer usar duas *flags*, você pode executá-las junto. Então, ao digitar

`ls -lh`

você receberá um resultado em um formato legível para humanos; você descobre que aqueles 6020 bits também é 5.9KB, que outro ficheiro tem 1 megabyte, e assim por diante.

Essas opções são *muito* importantes. Em outras lições do *Programming Historian*, você as encontrará. [Wget](/lessons/applied-archival-downloading-with-wget), [MALLET](/lessons/topic-modeling-and-mallet), e [Pandoc](pt/licoes/autoria-sustentavel-texto-simples-pandoc-markdown) usam a mesma sintaxe. Felizmente, você não precisa memorizar a sintaxe; em vez disso, mantenha essas lições à mão para que você possa dar uma olhada rápida se precisar ajustar alguma coisa. Essas lições podem ser feitas em qualquer ordem.

Agora você passou um bom tempo em seu diretório inicial. Vamos para outro lugar. Você pode fazer isso através do comando `cd` ou *Change Directory* (Mudar diretório).

Se você digitar

`cd Área\ de\ Trabalho/`[^1]

[^1]: Nota: Em SO X e Linux, para informar que o espaço entre palavras é um espaço, você precisa colocar uma barra invertida antes dele. Isso é chamado de 'escapar' o espaço. Você também pode colocar o nome do diretório entre aspas, como em `cd "Área de Trabalho"`.

Você está agora em sua Área de Trabalho. Isso é similar a clicar duas vezes no ícone da Área de Trabalho no seu explorado de ficheiros. Para verificar novamente, digite `pwd` e você verá algo como:

`/Users/ianmilligan1/Área\ de\ Trabalho/`

Tente experimentar um pouco com esses: explore seu diretório atual com o comando `ls`.

Se você quiser voltar, você pode digitar

`cd ..`

Isso nos movimenta um diretório 'acima', colocando-nos de volta em `/Users/ianmilligan1/`. Se você estiver completamente perdido, o comando

`cd --`

lhe trará de volta ao diretório inicial, exatamente onde você começou.

Tente explorar: visite seu diretório documentos, imagens,pastas que você tenha na sua área de trabalho. Se acostume a se movimentar entre os diretórios. Imagine que você está navegando por uma [estrutura de árvore](http://en.wikipedia.org/wiki/Tree_structure) (em inglês). Se você está na área de trabalho, você não será capaz de `cd documents` pois este é um 'filho' de seu diretório inicial, ao passo que sua Área de Trabalho é 'irmã' de sua pasta Documentos. para se mover para uma irmã, você deve retornar ao pai comum. Para fazer isso, você deverá retornar para o seu diretório inicial (`cd ..`) e então se mover para `cd documents`.

Ser capaz de navegar no seus sistema de ficheiros utilizando o shell bash é muito importante para muitas das lições no *Programming Historian*. À medida que você se sentir mais confortável, logo se verá pulando diretamente para o diretório que deseja. No nosso caso, de qualquer lugar em nosso sistema, você pode digitar

`cd /users/ianmilligan1/mallet-2.0.7`

ou, no Windows, algo como

`cd c:\mallet-2.0.7\`

e ser levado ao nosso diretório MALLET para [modelagem de tópicos](/lessons/topic-modeling-and-mallet).

Por fim, tente

`open .`

no SO X ou

`explorer .`

No Windows. Esse comando abrirá seu GUI no diretório atual. Certifique-se de deixar o espaço entre `open` ou `explorer` e o ponto.

## Interagindo com ficheiros

Assim como navegar pelos diretórios, você pode interagir com ficheiros na linha de comando: você pode lê-los, abri-los, executá-los, e mesmo editá-los, geralmente sem nunca precisar sair da interface. Há algum debate sobre por que alguém faria isso. O principal motivo é a experiência fluida de trabalhar na linha de comando: você nunca precisa pegar o mouse ou tocar no *touchpad* e, embora tenha uma curva de aprendizado acentuada, pode eventualmente se tornar um ambiente de escrita único. Além disso, muitos programas exigem que você use a linha de comando para opera-los. Como você usará programas na linha de comando, muitas vezes pode ser mais rápido fazer pequenas edições sem alternar para um programa separado. Para alguns desses argumentos, veja ["Why, oh WHY, do those #?@! nutheads use vi?"](http://www.viemu.com/a-why-vi-vim.html) de Jon Beltran de Heredia.

Aqui estão algumas maneiras básicas de interagir com arquivos.

Primeiro, você pode criar um novo diretório para lidar com ficheiros de texto. Vamos criá-lo em sua área de trabalho, por conveniência. Você sempre movê-lo posteriormente. Navegue até sua Área de Tabalho, e digite:

`mkdir ProgHist-Text`

Isto cria um diretório com o nome, como você pode imaginar, 'ProgHist-Text'. Em geral, é bom evitar colocar espaços nos nomes de arquivos e diretórios ao usar a linha de comando (existem soluções alternativas, é claro, mas essa abordagem é mais simples). Você pode verificar na sua área de trabalho se funcionou. Agora, acesse esse diretório (lembre-se, seria `cd ProgHist-Text`).

Mas espere! Há um truque para tornar as coisas um pouco mais rápidas. Vá para o diretório anterior (`cd ..` - que o levará de volta para a área de trabalho). Para navegar até o diretório `ProgHist-Text`, você poderia digitar `cd ProgHist-Text`. Alternativamente, você poderia digitar cd Prog e depois pressionar a tecla Tab. Você notará que a interface completa a linha para `cd ProgHist-Text`. **Pressionar a tecla tab a qualquer momento no shell irá tentar autocompletar a linha com base nos ficheiros ou subdiretórios no diretório atual. No entanto, isso é sensível a maiúsculas e minúsculas. No exemplo anterior, `cd prog` não seria autocompletado para `ProgHist-Text`. Quando dois ou mais ficheiros têm os mesmos caracteres, o autocompletar preencherá apenas até o primeiro ponto de diferença. Encorajamos o uso desse método ao longo da lição para ver como ele funciona.**

Agora você precisa encontrar um ficheiro de texto simples para nos ajudar com o exemplo. Porque não usar um livro inteiro, tal como revolucionário *Memórias Póstumas de Brás Cuvas*, de Machado de Assis? O ficheiro de texto está disponível no [Internet Archive](https://ia801703.us.archive.org/11/items/memoriasPostumasBrasCubas/memoriasBras_djvu.txt). Se você já instalou o [wget](/lessons/applied-archival-downloading-with-wget) (em inglês), você pode simplesmente digitar

`wget https://ia801703.us.archive.org/11/items/memoriasPostumasBrasCubas/memoriasBras_djvu.txt`

Se você ainda não tem o wget instalado, faça o download do do texto você mesmo utilizando seu navegador. Vá até o link acima, e, em seu navegador, use a opção 'Salvar página como..' no 'menu arquivo'. Salve no seu novo diretório 'ProgHist-Text'. Agora, quando digitar

`ls -lh`

você verá algo como

>> -rw-r--r--+ 1 ianmilligan1  staff   3.1M  1 May 10:03 memoriasBras_djvu.txt

Você pode ler o texto no interior desse ficheiro de algumas maneiras diferentes. Primeiro, você pode informar nosso computador que você quer lê-lo utilizando o programa padrão que você usa para abrir ficheiros de texto. Por padrão, deve ser o TextEdit no SO X ou Notepad no Windows. Para abrir um ficheiro, digite

`open memoriasBras_djvu.txt`

no SO X, ou

`explorer memoriasBras_djvu.txt`

no Windows.

Isso seleciona o programa padrão para abrir aquele tipo de ficheiro, e o abre.

No entanto, muitas vezes você deseja apenas trabalhar na linha de comando sem sair dela. Você também pode ler arquivos dentro desse ambiente. Para experimentar isso, digite:

`cat memoriasBras_djvu.txt`

A janela do terminal irrompe onde *Guerra e Paz* se desenrola em cascada. Isso é ótimo, em teoria, mas você realmente consegue entender essa quantidade de texto? Em vez disso, você pode querer apenas examinar o primeiro ou o último *bit* do arquivo.

`head memoriasBras_djvu.txt`

Fornece uma visão das primeiras dez linhas, enquanto

`tail memoriasBras_djvu.txt `

fornece uma perspectiva das últimas dez linhas. Esta é uma boa maneira de determinar rapidamente o conteúdo do ficheiro. Você poderia incluir um comando para alterar a quantidade de linhas mostradas: `head -20 memoriasBras_djvu.txt`, por exemplo, mostraria as vinte primeiras linhas.

Você também deseja mudar o nome do ficheiro para algo mais descritivo. Você pode 'mover' para um novo nome digitante

`mv memoriasBras_djvu.txt machado.txt`

Posteriormente, ao executar um comando `ls`, você verá que agora é `machado.txt`. Se você quisesse duplicá-lo, também poderia executar o comando copy digitando

`cp memoriasBras_djvu.txt machado.txt`

Você revisitará esses comandos em breve.

Agora que você utilizou diversos comandos novos, é hora de mais um truque. Pressione a seta para cima no seu teclado. Observe que `cp memoriasBras_djvu.txt machado.txt` aparece antes do seu cursor. Você pode continuar pressionando a seta para cima para percorrer seus comandos anteriores. A seta para baixo retorna ao seu comando mais recente.

Após ter lido e renomeado vários ficheiros, você pode desejar reunir todos os seus textos em um único ficheiro. Para combinar. ou concatenar, dois ou mais ficheiros, você pode usar o comando `cat`. Primeiro, vamos duplicar o ficheiro Machado ( `cp machado.txt machado2.txt`). Agora que você tem duas cópias do *Memórias Póstumas*, vamos colocá-los juntos para fazer um livro **ainda mais longo**.

Para combinar, ou concatenar, dois ou mais ficheiros use o comando `cat`. Digite

`cat machado.txt machado2.txt`

e aperte Enter. Isso irá imprimir na tela, ou mostrar, os ficheiros combinados no interior do shell. Contudo, ele é longo demais para ser lido nessa janela! Felizmente, utilizando o comando `>`, você pode enviar o rsultado para um novo ficheiro, ao invés da visualização no terminal. Digita

`cat machado.txt machado2.txt > machado-em-dobro.txt`.

Agora, quando você digitar `ls` você verá `machado-em-dobro.txt` listado em seu diretório.

Quando combinando mais do que dois ficheiros, usar um _wildcard_ pode ajudar a evitar escrever cada nome de ficheiro individualmente. Como você viu anteriormente, `*` é um espaço reservado para zero ou mais caracteres ou números. Então, se você digitar

`cat *.txt > tudo-junto.txt`

e apertar Enter, uma combinação de todos os ficheiros .txt no diretório atual são combinados em ordem alfabética como `tudo-junto.txt`. Isto pode ser muito útil se você precisa combinar um número elevado de pequenos ficheiros no interior um diretório para que você possa trabalhar com eles em um programa de análise de texto. Outra _wildcard_ que vale a pena ser memorizada é `?` que é um espaço reservado para um único caractere ou número.

## Editando ficheiros de texto diretamente na linha de comando

Se você quiser ler um arquivo inteiro sem sair da linha de comando, você pode iniciar o [vim](http://en.wikipedia.org/wiki/Vim_%28text_editor%29) (em inglês). O Vim é um editor de texto muito poderoso, perfeito para usar com programas como [Pandoc](http://johnmacfarlane.net/pandoc/) para fazer processamento de texto ou para editar seu código sem ter que mudar para outro programa. O melhor de tudo é que ele vem incluído no bash tanto no SO X quanto no Windows. O Vim tem uma curva de aprendizado bastante acentuada, então vamos apenas abordar alguns pontos menores.

Digite

`vim machado.txt`

Você verá o vim ganhar vida diante de você, um editor de texto baseado em linha de comando.

{% include figure.html filename="vim.png" caption="Vim" %}

Se você realmente quer se aprofundar no Vim, há um [bom guia do Vim](http://vimdoc.sourceforge.net/htmldoc/quickref.html) (em inglês) disponível.

Utilizar o Vim para ler ficheiros é relativamente simples. Você pode utilizar as setas para navegar e poderia teoricamente ler *Memórias Póstumas* através da linha de comando. Alguns comandos básicos de navegação rápidos são os seguintes:

`Ctrl+F` (ou seja, pressionar e segurar a tecla 'Ctrl' e pressionar a tecla F) irá lhe mover uma página abaixo (`Shift+SetaParaCima` no Windows).

`Ctrl+B` irá lhe mover uma página acima (`Shift+SetaParaBaixo` para usuários do Windows).

Se você deseja se mover rapidamente para o final de uma linha, pode pressionar: `$`, e para se mover para o início de uma linha, `0`. Você também pode se mover entre sentenças digitando `)` (para frente) ou `(` (para trás). Para parágrafos, use `}` e `{`. Como você está fazendo tudo com o teclado, em vez de ter que segurar a tecla de seta para se mover em um documento, isso permite que você se mova rapidamente para frente e para trás.

Vamos rolar até o topo e fazer uma alteração mínima, como adicionar um campo `Leitor` no cabeçalho. Mova o cursor entre **o título** e **Texto-fonte:**, assim:

{% include figure.html filename="pronto-para-inserir.png" caption="Pronto para inserir um campo" %}

Se você simplesmente começar a digitar, receberá uma mensagem de erro ou o cursor começará a pular. Isso ocorre porque você precisa especificar que deseja fazer uma edição. Pressione a tecla

`a`

Na parte de baixo da tela, você verá

`-- INSERÇÃO --`

Isso significa que você está no modo de inserção. Agora você pode digitar e editar o texto como se estivesse em um editor de texto padrão. Pressione `Enter` duas vezes, depois `seta para cima` e digite:

`Leitor: Um Historiador Programador`

Quando terminar, pressione `ESC` para retornar ao modo de leitura.

Para sair do Vim ou salvar alterações, você precisa inserir uma série de comandos. Pressione `:` e você será levado para a linha de entrada de comandos do Vim. Você pode digitar vários comandos aqui. Se você quiser salvar o ficheiro, digite `w` para 'escrever' (_write_ em inglês) o ficheiro. Se você executar esse comando, verá:

>> "machado.txt" 7952L, 371667B gravado(s)

{% include figure.html filename="apos-escrever.png" caption="Após Escrever o Ficheiro, com nossas Pequenas Alterações" %}

Se você quiser sair, digite `:` novamente e depois `q`. Isso o levará de volta à linha de comando. Assim como no restante do bash, você também poderia ter combinado os dois comandos. Pressionar `:` e depois digitar `wq` teria salvado o ficheiro e depois saído do Vim. Ou, se você quisesse sair **sem** salvar, `q!` teria encerrado o vim e substituído a preferência padrão para salvar suas alterações.

Vim é diferente do que você está acostumado(a) e exigirá mais esforço e prática para se tornar fluente nele. Mas se você estiver fazendo pequenos ajustes em ficheiros, é uma boa maneira de começar. À medida que você se sentir mais confortável, talvez até comece a escrever trabalhos finais de disciplinas com ele, aproveitando o poder das [notas de rodapé e formatação do Pandoc e Markdown](/pt/licoes/autoria-sustentavel-texto-simples-pandoc-markdown).

## Mover, Copiar e Deletar Ficheiros

Digamos que você terminou este diretório e gostaria de mover `machado.txt` para outro lugar. Primeiro, você deve criar uma cópia de backup. O shell é bastante implacável com erros, e o backup é ainda mais importante do que com GUIs. Se você excluir algo aqui, não haverá lixeira para retirá-lo. Para criar um backup, você pode digitar

`cp machado.txt machado-backup.txt`

Agora, quando você executar um comando `ls`, verá cinco arquivos, dois dos quais são iguais: `machado.txt` e `machado-backup.txt`.

Vamos mover o primeiro deles para outro lugar. Como exemplo, vamos criar um segundo diretório na sua área de trabalho. Vá para a área de trabalho (`cd ..`) e use o comando `mkdir` para criar outro diretório. Vamos chamá-lo de `proghist-dest`.

Para copiar o arquivo `machado.txt`, você tem algumas opções diferentes. Você pode executar esses comandos de qualquer lugar no terminal ou pode visitar os diretórios de origem ou destino. Para este exemplo, vamos executar o comando a partir daqui. O formato básico do comando de cópia é `cp [origem] [destino]`. Ou seja, você digita `cp` primeiro e, em seguida, insere o arquivo ou arquivos que deseja copiar, seguido pelo local para onde eles devem ir.


In this case, the command

`cp /home/ebn/"Área de Trabalho"/proghist-text/machado.txt /home/ebn/"Área de Trabalho"/proghist-dest/`

copiará Machado do primeiro diretório para o segundo. Você terá que inserir seu próprio nome de usuário no lugar de 'ebn'. Isso significa que agora você tem três cópias do romance em seu computador. O original, o backup e a nova cópia no segundo diretório. Se você quiser **mover** o ficheiro, ou seja, não deixar uma cópia para trás, você pode rodar o comando novamente, trocando `cp` por `mv`; não vamos fazer isso ainda.

Você também pode copiar vários ficheiros com um único comando. Se você deseja copiar **ambos** o ficheiro original e o ficheiro de backup, você pode usar o comando de _wildcard_ (curinga).

`cp /home/ebn/"Área de trabalho"/proghist-text/*.txt /home/ebn/"Área de trabalho"/proghist-dest/`

Este comando copia **todos** os arquivos de texto do diretório de origem para o diretório de destino.

Se você estiver no diretório para o qual deseja mover as coisas, não é necessário digitar toda a estrutura do diretório. Vamos fazer dois exemplos rápidos. Altere seu diretório para o diretório `ProgHist-text`. A partir deste local, se você quiser copiar esses dois arquivos para `proghist-dest`, este comando funcionará:

`cp *.txt /home/ebn/"Área de Trabalho"/proghist-dest/` (no SO X e Linux, substitua o diretório no Windows).

Como alternativa, se você estivesse no diretório `proghist-dest`, este comando funcionaria:

`cp /home/ebn/"Área de Trabalho"/proghist-text/*.txt ./`

O comando `./` refere-se ao diretório **atual** em que você está. **Este é um comando realmente valioso.**

Por fim, se você quiser excluir um arquivo, por qualquer motivo, o comando é `rm`, ou remove. **Tenha cuidado com o comando `rm`**, pois você não quer excluir arquivos que não pretende. Ao contrário da exclusão dentro da sua interface gráfica, não há lixeira ou opções de desfazer. Por essa razão, se você estiver em dúvida, é recomendado ter cautela ou fazer backups regulares dos seus dados.

Vá para `proghist-text` e exclua o arquivo original digitando

`rm machado.txt`

Verifique se o arquivo foi removido usando o comando `ls`.

Se você deseja excluir um diretório inteiro, tem duas opções. Você pode usar `rmdir`, o oposto de `mkdir`, para deletar um diretório **vazio**. Para excluir um diretório com ficheiros, você pode usar na área de trabalho:

`rm -r proghist-text`

## Conclusões

Você pode querer fazer uma pausa no terminal neste momento. Para fazer isso, digite `exit` e você fechará sua sessão.

Há mais comandos para tentar à medida que você se familiariza com a linha de comando. Alguns de nossos outros favoritos são `du`, que é uma maneira de descobrir quanta memória está sendo usada em um diretório ou ficheiro (`du -h` o torna legível por humanos - como com outros comandos). Para aqueles de vocês no SO X ou Linux, `top` fornece uma visão geral de quais processos estão sendo executados (`mem` no Windows) e `touch NOMEDOFICHEIRO` pode criar um ficheiro de texto básico em ambos os sistemas.

A esta altura, esperamos que você tenha uma boa compreensão básica de como se movimentar usando a linha de comando, mover arquivos básicos e fazer pequenas edições aqui e ali. Esta lição de nível iniciante foi projetada para dar a você alguma fluência e confiança básicas. No futuro, você pode querer se envolver com scripts.

Divirta-se! Antes que perceba, você pode acabar gostando da conveniência e precisão da linha de comando - para determinadas aplicações, pelo menos - muito mais do que a interface gráfica pesada fornecida pelo seu sistema. O seu conjunto de ferramentas acabou de ficar maior.

## Reference Guide

Para sua conveniência, aqui estão os comandos que você aprendeu nesta lição:

| Command              | What It Does                                                                                                                                           |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `pwd`                | Imprime o 'diretório de trabalho atual', informando onde você está.                                                                                    |
| `ls`                 | Lista os ficheiros do diretório atual                                                                                                                  |
| `man *`              | Lista o manual do comando, substituído pelo `*`                                                                                                        |
| `cd *`               | Muda o diretório atual para `*`                                                                                                                        |
| `mkdir *`            | Cria um diretório chamado `*`                                                                                                                          |
| `open` ou `explorer` | No SO X e no Linux, `open`, seguido por um arquivo, o abre; no Windows, o comando `explorer` seguido de um nome de arquivo faz a mesma coisa.          |
| `cat *`              | `cat` é um comando versátil. Ele lerá um ficheiro para você se você substituir um ficheiro por `*`, mas também pode ser usado para combinar ficheiros. |
| `head *`             | Mostra as primeiras dez linhas de `*`                                                                                                                  |
| `tail *`             | Mostra as últimas dez linhas de `*`                                                                                                                    |
| `mv`                 | Movimenta um ficheiro                                                                                                                                  |
| `cp`                 | Copia um ficheiro                                                                                                                                      |
| `rm`                 | Deleta um ficheiro                                                                                                                                     |
| `vim`                | Abre o editor de documentos `vim`.                                                                                                                     |

