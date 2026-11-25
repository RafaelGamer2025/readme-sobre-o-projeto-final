# JOJO-OS

O **JOJO-OS** é um projeto de desktop temático inspirado em *JoJo’s Bizarre Adventure*, desenvolvido em Python utilizando o framework **Tkinter**. Ele combina uma área de trabalho visual e imersiva com aplicativos locais, cadastro de usuários, efeitos sonoros, ferramentas de jogos e integrações opcionais.

> **Importante:** O JOJO-OS é um aplicativo de fã executado dentro do Windows ou Linux, **não sendo um sistema operacional real**. Alguns recursos dependem de serviços externos ou de arquivos que devem ser baixados separadamente. A interface e os testes automatizados foram verificados no ambiente de desenvolvimento, o que não substitui testes práticos em computadores Windows e telefones reais.

---

## 📋 Conteúdo

- [Recursos](#-recursos)
- [Requisitos](#-requisitos)
- [Instalação no Windows](#-instalação-no-windows)
- [Instalação no Linux](#-instalação-no-linux)
- [Configuração Opcional de IA e Voz](#-configuração-opcional-de-ia-e-voz)
- [Cadastro e Perfis](#-cadastro-e-perfis)
- [IKEMEN GO e Pacote Android](#-ikemen-go-e-pacote-android)
- [Controle pelo Celular](#-controle-pelo-celular)
- [Dados, Segurança e Backups](#-dados-segurança-e-backups)
- [Testes](#-testes)
- [Estrutura do Projeto](#-estrutura-do-projeto)
- [Solução de Problemas](#-solução-de-problemas)
- [Créditos e Licenças](#-créditos-e-licenças)

---

## 🌟 Recursos

* **Desktop Temático:** Interface gráfica em Tkinter com skins inspiradas em *JoJo* e no *Cleiton OS*, grade de ícones e janelas personalizadas.
* **Aplicativos Integrados:** Calculadora, navegador, terminal, gerenciador de arquivos, debugger, batalha de Stands, ferramentas de jogos e outras utilidades locais. *(A disponibilidade pode variar conforme o sistema e dependências opcionais)*.
* **Assistente de IA Opcional:** Janela *Heaven’s Door* capaz de conversar utilizando a API Groq quando configurada com uma chave válida.
* **Sistema de Voz Opcional:** Suporte a voz local instalada no computador (`pyttsx3`) ou provedores online de fala (o texto enviado a provedores online sai do seu computador).
* **Cleiton Store:** Disponível no perfil *Cleiton OS*, contendo 20 utilitários locais instaláveis pela própria loja. Ferramentas e listas utilizam dados locais e não vêm pré-instaladas no desktop padrão.
* **Cadastro e Contas Locais:** Fluxo inicial de "despertar de Stand". Todos os dados de usuário permanecem salvos localmente.
* **IKEMEN GO:** Hub de jogos que localiza a release oficial compatível, valida o hash de segurança antes de extrair e oferece suporte a personagens e conteúdos do projeto.

---

## ⚙️ Requisitos

* **Python:** Versão **3.11** ou mais recente (recomenda-se a versão de 64 bits).
* **Tkinter/Tcl-Tk:** Geralmente já vem integrado com o instalador oficial do Python.
* **Conexão com a Internet:** Necessária para baixar dependências, utilizar recursos de IA ou realizar o download oficial do IKEMEN GO.
* **Espaço em Disco:** Espaço livre adequado para o ambiente virtual, bibliotecas e os jogos baixados.

---

## 🪟 Instalação no Windows

Abra o **Prompt de Comando (CMD)** ou **PowerShell** na pasta raiz do projeto e execute os comandos abaixo:

```bash
py -3.11 -m venv .venv
.venv\Scripts\activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
copy .env.example .env
python main_gui.py
```

* **Nota:** Se o comando `py -3.11` não funcionar, instale o Python 3.11+ de 64 bits marcando as opções **"Add Python to PATH"** e **"tcl/tk and IDLE"** no instalador oficial.
* Edite o arquivo `.env` apenas se desejar ativar os serviços online.
* Para iniciar o receptor de controle USB no Windows, você também pode utilizar o atalho `INICIAR_CONTROLE_USB.bat`. Consulte a seção [Controle pelo Celular](#-controle-pelo-celular).

---

## 🐧 Instalação no Linux

Em distribuições baseadas em Debian/Ubuntu, certifique-se de instalar o suporte ao Tkinter. Em seguida, abra o terminal na pasta do projeto e execute:

```bash
sudo apt install python3-tk python3-venv
python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python main_gui.py
```

* Se a sua distribuição não possuir o Python 3.11 nativo, utilize uma versão compatível equivalente ou superior ajustando o comando `python3.11`.

### 🌐 Navegador Opcional com Qt WebEngine

A interface principal roda nativamente em Tkinter. Caso queira habilitar a implementação opcional de navegador baseada em Qt WebEngine, instale os pacotes opcionais:

```bash
python -m pip install -r requirements-optional.txt
```

*(Este componente não é obrigatório para iniciar o sistema principal).*

---

## 🤖 Configuração Opcional de IA e Voz

O projeto disponibiliza um arquivo modelo chamado `.env.example`. Copie-o para `.env` na pasta principal do projeto e preencha apenas as chaves dos serviços que deseja utilizar:

```env
GROQ_API_KEY=sua_chave_groq_aqui
GROQ_MODEL=llama-3.3-70b-versatile
JOJO_TTS_PROVIDER=local
FISH_AUDIO_API_KEY=
FISH_AUDIO_MODEL=drama-3
FISH_AUDIO_REFERENCE_ID=ed45c9bdc3d74548bf4987c9987f218b
```

* **`GROQ_API_KEY`:** Obrigatória caso queira utilizar as respostas da IA online (*Heaven's Door*). Sem ela, o restante do desktop funcionará normalmente, exceto as consultas online.
* **`JOJO_TTS_PROVIDER`:** Aceita `local`, `fish` ou `auto` (o modo `auto` prioriza o Fish Audio se houver chave configurada, recorrendo à voz local caso contrário).
* **Segurança:** Nunca compartilhe suas chaves reais, não as envie em commits públicos e mantenha o arquivo `.env` fora do controle de versão (já configurado no `.gitignore`).

---

## 👤 Cadastro e Perfis

* **Cerimônia de Despertar:** No primeiro acesso, o aplicativo exibe um fluxo temático onde você pode despertar um Stand, continuar sem Stand ou escolher o perfil visual *Cleiton OS*. Se optar por despertar, um dos 33 Stands do catálogo será sorteado com animações e efeitos sonoros exclusivos.
* **Perfil Cleiton OS:** Funciona como uma identidade visual alternativa e não concede privilégios de sistema ou funções de invasão. É neste perfil que a *Cleiton Store* e seus 20 utilitários aparecem (ficando ocultos no modo padrão do JoJo OS).

---

## 🎮 IKEMEN GO e Pacote Android

* **IKEMEN GO (Desktop):** O executável do motor de jogos não vem embutido no repositório. O hub de jogos do JOJO-OS consulta a release oficial, valida os metadados/hash de segurança e faz o download automatizado do pacote correspondente à sua plataforma.
* **Pacote Android (`JoJo_OS_Android_DataPack.zip`):** Localizado em `core/games/`, serve para acompanhar o APK oficial. O manifesto identifica 44 personagens presentes nos arquivos disponibilizados.
  * *Instalação no Android:* Instale o APK oficial, escolha a pasta do jogo pelo seletor de arquivos do aplicativo, feche-o e extraia/mescle o conteúdo do pacote de dados nessa exata pasta. O arquivo `LEIA-ME_ANDROID.txt` dentro do pacote detalha o procedimento.

---

## 📱 Controle pelo Celular

O JOJO-OS possui um receptor experimental de controle integrado ao ambiente desktop:

* No Windows, execute o arquivo `INICIAR_CONTROLE_USB.bat` para abrir o receptor.
* A ponte USB foi desenhada para interagir com um aplicativo companheiro no Android através de encaminhamento ADB, aceitando estritamente os comandos definidos pelo projeto.
* A integração Bluetooth e USB depende de testes práticos no seu hardware e aparelho celular de destino, sendo obrigatório o uso do aplicativo Android correspondente.

---

## 🔒 Dados, Segurança e Backups

* **Armazenamento Local:** Contas, configurações e dados internos são salvos na pasta `data/`.
* **Integridade:** O sistema de contas utiliza hashes de senha, o que não substitui a segurança física do seu computador.
* **Cuidados com Backups:** Faça cópias de segurança periódicas da pasta `data/` antes de realizar atualizações ou reinstalações. Mantenha sempre o banco de dados (`data/jojo_os.db`) e os arquivos de chave (`data/system_key.json`) juntos. Não edite esses arquivos manualmente sem ter um backup seguro.

---

## 🧪 Testes

Para executar os testes automatizados do projeto com o ambiente virtual ativo, utilize os comandos na raiz da pasta:

```bash
python -m unittest discover -s tests -v
python -m compileall -q .
```

Se desejar executar o linter Ruff (caso instalado):

```bash
python -m pip install ruff
ruff check .
```

> **Nota:** Testes automatizados e *smokes* com Tk/Xvfb ajudam a validar a base de código, mas não substituem testes manuais de áudio, conexão USB/Bluetooth ou comportamentos em sistemas operacionais reais.

---

## 📁 Estrutura do Projeto

```text
├── main_gui.py                 # Ponto de entrada principal do desktop
├── core/                       # Lógica de login, banco, segurança, IA e janelas
├── core/games/                 # Hub de jogos, integração IKEMEN GO e controle
├── ui/                         # Temas, grades, efeitos e componentes visuais
├── battle/                     # Interface e mecânicas de batalha de Stands
├── soms/stand_reveal/          # Efeitos sonoros originais da revelação dos Stands
├── tests/                      # Conjunto de testes automatizados
└── data/                       # Dados locais de execução (ignorado pelo Git)
```

---

## 🛠️ Solução de Problemas

* **A janela não abre:** Certifique-se de que o ambiente virtual (`.venv`) está ativado e que as dependências foram instaladas corretamente (`pip install -r requirements.txt`). No Linux, confirme a instalação do pacote de Tkinter da sua distribuição.
* **A IA não responde:** Verifique se a variável `GROQ_API_KEY` está configurada corretamente no arquivo `.env` (sem espaços sobrando ou aspas desnecessárias) e se há conexão ativa com a internet.
* **Sem som no sistema:** Confira as configurações de áudio do seu computador e as vozes locais instaladas. Se o mixer falhar ao inicializar, o app funcionará sem os efeitos sonoros.
* **O IKEMEN não inicia:** Utilize o hub interno para reparar ou completar a instalação. Mantenha o executável e as pastas do jogo sempre juntas na mesma estrutura baixada.
* **Erro de integridade no banco local:** Caso ocorra falha ao abrir o banco de dados, evite sobrescrever a pasta `data/`. Restaure conjuntamente o banco e a chave de sistema a partir de um backup confiável anterior.

---

## 📜 Créditos e Licenças

* Projeto desenvolvido por fãs, inspirado no universo de **JoJo’s Bizarre Adventure** (propriedade de Hirohiko Araki / Shueisha).
* O motor de jogos e assets de terceiros possuem suas próprias licenças descritas em seus respectivos pacotes ou no arquivo `ANIME_ASSET_SOURCES.md`.
