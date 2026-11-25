# minha ideia do projeto 
# JOJO-OS é um projeto de desktop temático inspirado em JoJo’s Bizarre Adventure, feito em Python com Tkinter. Ele combina uma área de trabalho visual com aplicativos locais, cadastro, efeitos sonoros, ferramentas de jogo e integrações opcionais.

Importante: JOJO-OS é um aplicativo de fã executado dentro do Windows/Linux, não é um sistema operacional. Alguns recursos dependem de serviços externos ou de arquivos que precisam ser baixados separadamente. A interface e os testes automatizados foram verificados no ambiente de desenvolvimento; isso não substitui testes em um computador Windows e telefone reais.

Conteúdo
Recursos
Requisitos
Instalação no Windows
Instalação no Linux
Configuração opcional de IA e voz
Cadastro e perfis
IKEMEN GO e pacote Android
Controle pelo celular
Dados, segurança e backups
Testes
Estrutura do projeto
Solução de problemas
Créditos e licenças
Recursos
Desktop temático: interface Tkinter com skins JoJo e Cleiton OS, grade de ícones e janelas para ferramentas do projeto.
Aplicativos: calculadora, navegador, terminal, gerenciador de arquivos, debugger, batalha de Stands, ferramentas de jogos e outras janelas locais. A disponibilidade de recursos pode variar conforme o sistema e as dependências opcionais instaladas.
Assistente de IA opcional: a janela Heaven’s Door pode conversar por meio da API Groq quando uma chave válida estiver configurada.
Fala opcional: pode usar uma voz instalada no computador com pyttsx3 ou, quando configurado, um provedor online de fala. O texto enviado a um provedor online sai do computador.
Cleiton Store: disponível no perfil Cleiton OS; contém 20 utilitários locais, instaláveis pela própria Store. As ferramentas e notas/listas usam dados locais e não são pré-instaladas no desktop.
Cadastro e contas locais: primeiro cadastro com fluxo de despertar de Stand; os dados ficam no computador.
IKEMEN GO: o hub de jogos instala a release oficial compatível com a plataforma, verifica o hash publicado antes de extrair e oferece opções de personagens e conteúdo que existam no projeto.
Requisitos
Python 3.11 ou mais recente, de 64 bits recomendado.
Tkinter/Tcl-Tk instalado junto com o Python.
Conexão com a internet para instalar as dependências e usar as funções online, como IA ou download oficial do IKEMEN GO.
Espaço em disco para o ambiente virtual, dependências e jogos baixados.
Instalação no Windows
Abra o Prompt de Comando na pasta do projeto e execute:

py -3.11 -m venv .venv
.venv\Scripts\activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
copy .env.example .env
python main_gui.py
Se o comando py -3.11 não existir, instale Python 3.11+ de 64 bits e selecione Add Python to PATH e tcl/tk and IDLE no instalador. Edite o arquivo .env somente se for ativar os serviços online.

Para abrir o receptor de controle USB no Windows, há também o arquivo INICIAR_CONTROLE_USB.bat. Consulte Controle pelo celular antes de usar essa integração.

Instalação no Linux
Em distribuições baseadas em Debian/Ubuntu, instale o suporte Tkinter caso ainda não esteja disponível. Em seguida, a partir da pasta do projeto:

sudo apt install python3-tk python3-venv
python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python main_gui.py
Se sua distribuição não tiver Python 3.11 instalado, use uma versão suportada igual ou superior e ajuste o comando python3.11.

Navegador opcional com Chromium
A interface principal continua usando Tkinter. Para habilitar a implementação opcional do navegador baseada em Qt WebEngine, instale também:

python -m pip install -r requirements-optional.txt
Esse componente não é necessário para iniciar o aplicativo principal.

Configuração opcional de IA e voz
O projeto inclui .env.example. Copie-o para .env na pasta principal e preencha somente as chaves dos serviços que decidir usar. Exemplo:

GROQ_API_KEY=sua_chave_groq
GROQ_MODEL=llama-3.3-70b-versatile
JOJO_TTS_PROVIDER=local
FISH_AUDIO_API_KEY=
FISH_AUDIO_MODEL=drama-3
FISH_AUDIO_REFERENCE_ID=ed45c9bdc3d74548bf4987c9987f218b
GROQ_API_KEY: necessária para as respostas da IA online. Sem ela, as demais partes do desktop podem ser abertas, mas a integração online de IA não estará disponível.
JOJO_TTS_PROVIDER: use local, fish ou auto. auto escolhe Fish Audio se houver chave configurada; caso contrário, tenta usar a voz local.
FISH_AUDIO_API_KEY: opcional. Quando a fala online for ativada, o texto enviado para leitura será transmitido ao provedor Fish Audio.
A fala local depende de uma voz compatível instalada no sistema. O resultado e o idioma dependem das vozes disponíveis no computador.
Não coloque chaves reais no código, em commits, capturas de tela ou arquivos ZIP. O .gitignore está configurado para ignorar .env.

Cadastro e perfis
No primeiro uso, o aplicativo apresenta uma cerimônia de despertar. A pessoa pode escolher despertar um Stand, continuar sem Stand ou selecionar o perfil visual Cleiton OS. Quando escolhe despertar, um dos 33 Stands do catálogo é sorteado e revelado com animação e efeitos sonoros originais deste projeto.

O perfil Cleiton OS é uma identidade visual e não concede privilégios administrativos nem transforma o aplicativo em ferramenta de invasão. A Cleiton Store e seus 20 utilitários aparecem nesse perfil; ao voltar para JoJo OS, a Store fica oculta. Contas já existentes continuam podendo entrar pelo fluxo de login.

IKEMEN GO e pacote Android
O executável do IKEMEN GO não é incorporado ao código-fonte. Pelo hub de jogos, o instalador consulta a release oficial e baixa o pacote correspondente à plataforma compatível. A instalação verifica os metadados/hash publicados e valida a estrutura antes de disponibilizar o jogo.

O projeto também contém core/games/JoJo_OS_Android_DataPack.zip, um pacote de dados separado para acompanhar o APK oficial. O manifesto incluído no pacote identifica 44 personagens presentes nos arquivos fornecidos para o projeto; não se deve interpretar isso como 60 personagens nem como inclusão de personagens que não foram enviados. O APK permanece oficial e não é modificado ou resignado.

O procedimento Android é separado do download do APK: instale e abra o APK uma vez, escolha a pasta de jogo pelo seletor do Android, feche o aplicativo e extraia/mescle o conteúdo do pacote de dados na mesma pasta escolhida. O arquivo LEIA-ME_ANDROID.txt dentro do pacote contém os passos e avisos detalhados. O pacote é grande, ocupa centenas de megabytes e precisa de espaço livre no telefone.

Limitação: o procedimento foi conferido pelo código do wrapper e pela inspeção dos arquivos, mas não foi testado em um aparelho Android físico. Uma atualização do APK que refaça a extração dos dados poderá exigir reaplicar o pacote.

O motor oficial tem suas próprias licenças e avisos. Personagens e outros assets de fãs não são automaticamente autorizados para redistribuição comercial; confira ANIME_ASSET_SOURCES.md e as licenças incluídas em cada pacote.

Controle pelo celular
O JoJo-OS inclui um receptor experimental de controle no projeto desktop. No Windows, INICIAR_CONTROLE_USB.bat abre a janela do receptor. A ponte USB foi projetada para funcionar com um aplicativo companheiro Android e encaminhamento ADB; ela aceita apenas os controles definidos pelo projeto, não comandos arbitrários enviados pelo telefone.

A integração Bluetooth depende do aplicativo Android companheiro e de suporte nativo do Android. A comunicação com um telefone real por USB ou Bluetooth ainda precisa ser testada no aparelho e computador de destino. O receptor de desktop sozinho não transforma o telefone em controle: é necessário o companion compatível.

Dados, segurança e backups
Contas, configurações e dados de aplicativos são mantidos localmente na pasta data/.
O armazenamento de contas usa verificação de integridade e hashes de senha; isso não substitui a segurança física do computador nem um backup.
Faça cópias de segurança da pasta data/ antes de atualizar ou reinstalar. Mantenha juntos o banco e os arquivos de chave necessários para validar os dados.
Não apague, edite manualmente ou compartilhe data/jojo_os.db, data/system_key.json ou outros arquivos de conta sem um backup confiável.
O antivírus/scanner do projeto é uma ferramenta do aplicativo e não substitui o Microsoft Defender ou outro produto de segurança reconhecido.
O arquivo .env pode conter credenciais. Não o envie a terceiros nem o inclua em commits ou ZIPs públicos.
Testes
Com o ambiente virtual ativado, a partir da pasta principal:

python -m unittest discover -s tests -v
python -m compileall -q .
O lint Ruff pode ser executado se estiver instalado:

python -m pip install ruff
ruff check .
Os testes automatizados e os smokes com Tk/Xvfb não substituem a validação de áudio, Bluetooth, USB, APIs externas ou interface em um Windows/Android reais. Não execute arquivos de jogo/personagens para validar o código-fonte.

Estrutura do projeto
main_gui.py                 Entrada principal do desktop
core/                       Login, banco, segurança, IA e janelas
core/games/                 Hub, IKEMEN GO, personagens e controle
ui/                         Temas, grade, efeitos e componentes visuais
battle/                     Interface e recursos de batalha
soms/stand_reveal/          Efeitos originais da revelação dos Stands
tests/                      Testes automatizados
 data/                       Dados locais de execução (não compartilhar)
Solução de problemas
A janela não abre
Ative o ambiente virtual e confirme que as dependências foram instaladas com python -m pip install -r requirements.txt. No Linux, instale o pacote de Tkinter da distribuição. No Windows, reinstale o Python habilitando Tcl/Tk.

A IA não responde
Confirme que GROQ_API_KEY está preenchida corretamente no .env, sem aspas desnecessárias ou espaços extras. A IA requer internet e uma chave válida; não compartilhe o arquivo .env.

Não há som
Confirme o dispositivo de áudio do computador e as vozes locais instaladas. Se o mixer não inicializar, a aplicação pode continuar sem efeitos sonoros. A fala Fish Audio exige uma chave e conexão com o serviço.

O IKEMEN não inicia
Use o hub para completar ou reparar a instalação. Não mova apenas o executável: mantenha juntos o executável e as pastas do jogo. Verifique se a release oficial baixada corresponde à arquitetura/sistema operacional.

O banco local não abre ou informa falha de integridade
Não apague nem sobrescreva arquivos em data/. Feche o aplicativo e restaure, juntos, o banco e a respectiva chave a partir do mesmo backup confiável. Se não houver backup, preserve uma cópia dos arquivos atuais antes de qualquer tentativa de reparo.
