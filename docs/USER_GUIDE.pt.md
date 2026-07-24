# Elyvo Assist — Guia do Utilizador

> 🌐 Este guia também está disponível em: [English](USER_GUIDE.md) · [Беларуская](USER_GUIDE.be.md) · [Deutsch](USER_GUIDE.de.md) · [Español](USER_GUIDE.es.md) · [Français](USER_GUIDE.fr.md) · [Italiano](USER_GUIDE.it.md) · **Português** · [Русский](USER_GUIDE.ru.md) · [Українська](USER_GUIDE.uk.md)

Elyvo Assist é um assistente de IA para desktop destinado a reuniões, pesquisa e brainstorming. Funciona como uma sobreposição translúcida por cima de qualquer janela, invocada através de um atalho de teclado. Consegue ouvir o seu microfone e o áudio do sistema, transcrever em tempo real, ver o seu ecrã e responder a perguntas em contexto — mantendo-se oculto na partilha e na gravação de ecrã.

Este guia aborda a instalação e uma visão geral das principais funcionalidades.

- [Instalação](#instalação)
- [Primeiro arranque](#primeiro-arranque)
- [Permissões](#permissões)
- [A sobreposição e os atalhos de teclado](#a-sobreposição-e-os-atalhos-de-teclado)
- [Visão geral das funcionalidades](#visão-geral-das-funcionalidades)
- [Definições](#definições)
- [Atualização](#atualização)
- [Desinstalação](#desinstalação)
- [Resolução de problemas](#resolução-de-problemas)

---

## Instalação

Os instaladores e binários são publicados através do [GitHub Releases](https://github.com/pdasilem/elyvo-assist/releases). Descarregue o ficheiro correspondente à sua plataforma a partir da versão mais recente. Todas as compilações são de 64 bits (`x86_64` / Apple Silicon).

Cada versão contém, para a versão `X.Y.Z`:

| Plataforma | Ficheiro |
|----------|------|
| Windows (recomendado) | `elyvo-assist-X.Y.Z-windows-x64-setup.exe` |
| Windows (MSI) | `elyvo-assist-X.Y.Z-windows-x64.msi` |
| macOS (Intel) | `elyvo-assist-X.Y.Z-macos-x64.dmg` |
| macOS (Apple Silicon) | `elyvo-assist-X.Y.Z-macos-arm64.dmg` |
| Debian / Ubuntu | `elyvo-assist-X.Y.Z-linux-x86_64.deb` |
| Arch / Manjaro | `elyvo-assist-X.Y.Z-1-x86_64.pkg.tar.zst` (+ `install.sh`) |

### Windows

1. Descarregue o instalador `...-setup.exe` (NSIS) — ou o `.msi` se a sua organização preferir implementação via MSI.
2. Execute-o e siga as instruções. A aplicação é instalada em `Program Files\Elyvo Assist`.
3. Inicie o **Elyvo Assist** a partir do menu Iniciar.

### macOS

1. Descarregue o `.dmg` correspondente ao seu chip — `macos-x64` para Intel, `macos-arm64` para Apple Silicon (M1/M2/M3 e posteriores).
2. Abra a imagem de disco e arraste o **Elyvo Assist** para **Applications**.
3. No primeiro arranque, o macOS pode avisar que a aplicação é de um programador não identificado. Clique com o botão direito na aplicação → **Open** → **Open** para a permitir.

> **Requisitos no Linux.** O Elyvo Assist destina-se ao ambiente de trabalho **KDE Plasma** sobre **Wayland**. A proteção contra captura de ecrã da sobreposição é implementada através do KWin (o compositor do KDE), pelo que o comportamento de ocultação na partilha de ecrã só funciona em KDE/KWin. Outros ambientes de trabalho (GNOME, etc.) conseguem executar a aplicação, mas as garantias de proteção contra captura não se aplicam. Também precisa de uma sessão **PipeWire** em execução para a captura de microfone e de áudio do sistema.

### Linux — Debian / Ubuntu

```bash
sudo apt install ./elyvo-assist-X.Y.Z-linux-x86_64.deb
```

O `apt` resolve as dependências de runtime (WebKitGTK 4.1, OpenSSL 3, PipeWire). Em versões mais antigas do `apt`, utilize `sudo dpkg -i ...` seguido de `sudo apt -f install` para obter as dependências em falta.

### Linux — Arch / Manjaro

A forma mais rápida é utilizar o script de instalação publicado, que descarrega o pacote, instala as bibliotecas de sistema necessárias e executa o `pacman` por si:

```bash
curl -fsSL https://github.com/pdasilem/elyvo-assist/releases/latest/download/install.sh -o install.sh
bash install.sh
```

O script só suporta sistemas baseados em `pacman` e instala quaisquer pacotes de runtime em falta (GTK3, WebKit2GTK 4.1, PipeWire, libayatana-appindicator, entre outros).

Prefere fazê-lo manualmente? Descarregue o `.pkg.tar.zst` e instale-o diretamente:

```bash
sudo pacman -U elyvo-assist-X.Y.Z-1-x86_64.pkg.tar.zst
```

---

## Primeiro arranque

1. **Iniciar sessão.** Inicie sessão com **email e palavra-passe**, um **código de acesso único por email** ou com o **Google**. As contas novas são criadas a partir do mesmo ecrã (email → código de verificação → definir uma palavra-passe).
2. **Integração inicial (onboarding).** Um pequeno assistente de configuração guia-o por alguns passos — incluindo as **permissões** e a **criação do seu primeiro projeto** — e termina com um passo **Sobre si**, onde pode opcionalmente anexar um ficheiro (`.pdf`, `.doc`, `.docx`, `.md`, `.txt`) para dar ao assistente mais contexto sobre si. Pode editar isto mais tarde a partir do seu **Perfil**.
3. **Comece a utilizar.** Após a integração inicial, o **Dashboard** abre-se. Invoque a sobreposição de chat a qualquer momento com o atalho de alternância (predefinição `Ctrl+\`).

---

## Permissões

Para ouvir e ver o seu ecrã, o Elyvo Assist precisa de duas permissões ao nível do sistema operativo, pedidas durante a integração inicial:

- **Microfone** — para captar o que diz.
- **Captura de ecrã** — para que a função *Perguntar sobre o meu ecrã* consiga ver a janela ativa.

No **Windows** e no **macOS**, estas são geridas através dos pedidos normais do sistema operativo. No **Linux**, conceda-as quando forem pedidas; se negar alguma por engano, conceda-a nas definições de privacidade do seu sistema operativo.

As definições de áudio e microfone em si não podem ser configuradas dentro da aplicação — o Elyvo utiliza sempre o dispositivo **predefinido** do seu sistema.

> No Linux, a captura de microfone e de áudio do sistema utiliza o PipeWire e o portal do ambiente de trabalho. Certifique-se de que o PipeWire está em execução (é a predefinição no Manjaro e no Ubuntu atuais).

---

## A sobreposição e os atalhos de teclado

O Elyvo Assist é comandado quase inteiramente pelo teclado, para que o possa usar sem sair da sua reunião. A sobreposição de chat flutua por cima de outras janelas, pode ser arrastada e está **oculta na partilha e na gravação de ecrã** (consulte [proteção da janela](../README.md#window-protection-from-screen-sharing)).

Atalhos predefinidos (todos redefiníveis em **Definições → Atalhos de teclado**):

| Ação | Predefinição | O que faz |
|--------|---------|--------------|
| Alternar visibilidade | `Ctrl+\` | Mostrar / ocultar a sobreposição do Elyvo |
| Perguntar ao Elyvo | `Ctrl+Enter` | Perguntar sobre o seu ecrã ou o áudio atual |
| Limpar chat | `Ctrl+R` | Limpar a conversa atual |
| Iniciar / terminar sessão | `Ctrl+Shift+\` | Iniciar ou terminar uma sessão de escuta |
| Mover sobreposição | `Ctrl+↑ / ↓ / ← / →` | Reposicionar a janela no ecrã |
| Deslocar resposta | `Ctrl+Shift+↑ / ↓` | Deslocar a resposta para cima / para baixo |

Para redefinir um atalho, abra **Definições → Atalhos de teclado**, clique num atalho e prima a nova combinação.

---

## Visão geral das funcionalidades

### Sessões

Uma **sessão** é o período em que o Elyvo está a ouvir ativamente e a manter contexto. Inicie ou termine uma sessão com `Ctrl+Shift+\`. Durante uma sessão, o Elyvo capta o seu microfone e o áudio do sistema, transcreve-o em tempo real e mantém a transcrição em curso como contexto para as suas perguntas. O Elyvo utiliza o dispositivo de entrada **predefinido** do seu sistema (não é possível alterá-lo dentro da aplicação); nas Definições pode ver o dispositivo detetado e testar os níveis do microfone e do áudio do sistema com medidores em tempo real.

### Perguntar sobre o seu ecrã ou áudio

Prima **Perguntar ao Elyvo** (`Ctrl+Enter`) e o Elyvo responde utilizando como contexto o que está atualmente no seu ecrã e o áudio/transcrição recentes — útil para "resuma o que acabou de ser dito", "o que é este erro" ou "redija uma resposta a isto". Também pode, a qualquer momento, escrever uma mensagem normal na caixa de chat.

### Ações rápidas

Durante uma sessão, o chat oferece cinco ações de um clique. Elas são **sensíveis ao papel**: cada uma retira o seu significado da situação e do objetivo do modo ativo, pelo que o mesmo botão ajuda de forma diferente consoante esteja a responder, a avaliar, a negociar ou a aprender.

- **Assist** — a substância que o momento exige: a resposta ao que lhe acabaram de perguntar; uma resposta de referência ou uma avaliação rápida quando quem avalia é *você*; a solução completa quando a captura de ecrã contém uma tarefa. É material para pensar, não palavras para dizer em voz alta.
- **What should I say?** — a próxima frase a dizer em voz alta, na sua voz, pronta a usar tal como está.
- **Follow-up questions** — um conjunto de 3–4 perguntas que pode fazer a seguir para fazer avançar o seu objetivo: um menu para escolher, não uma única frase.
- **What did they mean?** — descodifica a última intervenção da outra parte: a ideia, a intenção e qualquer preocupação implícita não dita.
- **Recap** — até três pontos sobre o que mudou, foi decidido ou perguntado desde a última vez que fez o ponto de situação.

Como funciona a rotação: num modo de candidato, o Assist responde à pergunta que lhe é dirigida; num modo de avaliador, entrega-lhe a resposta de referência para julgar o que ouve; num modo de negociação, as Follow-up questions tornam-se perguntas de sondagem. Num modo de aula ou webinar, em que sobretudo ouve, o Assist explica em termos mais simples o ponto acabado de expor, as Follow-up questions passam a perguntas para o orador ou verificações da sua própria compreensão, e o Recap põe-no a par depois de uma distração. Tudo isto é conduzido pelo prompt de sistema do modo ativo — os botões mantêm-se (ver **Modos de IA** abaixo).

### Modos de IA

Os **Modos** permitem-lhe adaptar o comportamento do assistente a diferentes situações. Cada modo tem o seu próprio prompt de sistema e um modelo de notas opcional. Faça a gestão em **Modos**:

- Comece pela **Galeria de Modelos** — os modelos são fornecidos pelo servidor e mudam ao longo do tempo — ou crie um modo de raiz.
- Edite o prompt de sistema para definir o tom, o papel e as regras adequados a essa situação.
- Anexe **ficheiros de modo** — material de referência que o assistente deve ter em conta para esse modo.
- Marque um modo como ativo; existe sempre um modo geral/predefinido disponível.

### Chat de IA ambiente

O chat ambiente é um chat leve e sempre disponível que o acompanha em toda a aplicação e pode ser delimitado a um projeto. Faz parte do plano pago (consulte **Definições → Faturação**).

### Projetos

Os **Projetos** agrupam sessões relacionadas e dão ao assistente um contexto partilhado e persistente. Dentro de um projeto pode gerir:

- **Membros** — veja quem está no projeto e convide outras pessoas por email (cada convidado aparece como *pendente* até aceitar).
- **Memória** — factos e contexto que o assistente deve recordar entre sessões nesse projeto.
- **Regras** — orientações que o assistente segue nesse projeto.
- **Definições** — um **modo**, um **idioma de resposta** e um **idioma de transcrição** por projeto, além de **Enriquecer contexto** — um interruptor (desativado por predefinição) que permite ao assistente obter contexto relevante das suas *outras* sessões no mesmo projeto (recuperação entre sessões).

Quando alguém o convida para o projeto dele, o convite aparece no topo de **Projetos** com botões **Aceitar** / **Rejeitar**. O chat ambiente pode ser delimitado a um projeto, de modo a que as respostas se baseiem na memória e nas regras desse projeto.

### Documentos

O Elyvo pode manter uma biblioteca pessoal de documentos de referência que pode abrir como a sua própria sobreposição enquanto trabalha — útil para ter notas, um briefing ou uma checklist à mão durante uma chamada.

- **Gerir os seus documentos.** Em **Definições → Recursos**, adicione ficheiros Markdown (`.md`) — até **1 MB** cada — em *Os seus documentos*, ou elimine os que já não precisa. Os documentos são privados à sua conta.
- **Ativar por projeto.** No projeto ativo, assinale os documentos que quer ter à mão. Os documentos ativados **abrem automaticamente como separadores** no visualizador de Documentos sempre que o abrir para esse projeto. Ativar um documento controla o que o visualizador mostra para esse projeto; não introduz o conteúdo do ficheiro nas respostas do assistente.
- **Abrir o visualizador.** No menu de sessão da sobreposição de chat (o botão `···`), escolha **Documentos**. Abre-se como uma janela própria, arrastável, que, tal como a sobreposição principal, está **oculta na partilha e na gravação de ecrã**. O mesmo item de menu alterna o seu fecho.
- **Ler e alternar.** Cada documento abre no seu próprio separador. Utilize o separador **+** para abrir qualquer um dos seus documentos, clique num separador para mudar e em **×** para o fechar. O conteúdo é apresentado como Markdown formatado e segue o tema e o tamanho de letra do seu chat.

### Calendário e reuniões

Ligue o **Google Calendar** (em **Definições → Geral**) para ver as suas próximas reuniões dentro do Elyvo. No cartão de uma reunião, **"Entrar na reunião →"** limita-se a abrir a ligação da chamada (Zoom/Meet/Teams) no navegador, enquanto **"Fazer anotações"** inicia uma sessão de escuta. Pouco antes de uma reunião, o Elyvo também mostra um lembrete dentro da aplicação com o seu próprio botão **"Fazer anotações"**, que faz as duas coisas ao mesmo tempo — inicia a sessão e abre a ligação da chamada — para que o assistente esteja a ouvir desde o momento em que entra.

### Dashboard e histórico

O **Dashboard** é a sua base principal: lista as sessões anteriores numa lista pesquisável e agrupada por data (o campo de pesquisa está no cabeçalho da aplicação) e permite abrir o detalhe de uma sessão, que tem três separadores — **Resumo** (o resumo da reunião), **Transcrição** (a transcrição captada) e **Utilização** (as perguntas que fez ao Elyvo durante a sessão e as respectivas respostas). Utilize-o para rever ou fazer o acompanhamento depois de uma reunião.

### Memória e autoaprendizagem

O Elyvo melhora com o uso. No seu **Perfil** pode rever e editar:

- **Memória do utilizador** — factos duradouros sobre si e as suas preferências que o assistente aplica em todo o lado.
- **Desambiguações** — esclarecimentos que o assistente aprendeu (por exemplo, a que "John" ou a que projeto se refere) para deixar de adivinhar de forma errada.

### Proteção da janela na partilha de ecrã

A sobreposição é deliberadamente invisível à captura, para que a possa usar durante uma chamada partilhada sem que apareça na transmissão. A cobertura varia consoante a plataforma — o [README principal](../README.md#window-protection-from-screen-sharing) é a matriz de referência. Em resumo:

- **Windows 11** — oculta de todos os tipos de captura por predefinição.
- **Windows 10** — mesma proteção, mas **não garantida**: uma limitação conhecida do sistema operativo pode mostrar a sobreposição como um retângulo preto na captura, em vez de a ocultar corretamente.
- **Linux (KDE / KWin)** — oculta na *gravação e partilha* de ecrã por predefinição. No **KWin 6.7.0+ (Plasma 6.7+)** as *capturas de ecrã* estáticas também ficam ocultas por predefinição — não é necessário patch. Em KWin mais antigos (≤ 6.6.x), ocultá-la em *capturas de ecrã* estáticas (Spectacle/PrintScreen) requer um patch pontual do KWin, que deve ser reaplicado após atualizações do KWin.
- **macOS** — utiliza o mesmo mecanismo nativo de proteção de conteúdo. Fiável no **macOS 14 e anteriores**; no **macOS 15 e posteriores** a não deteção **não é garantida** e a sobreposição pode aparecer nas capturas.

---

## Definições

Abra as Definições a partir do menu do utilizador. Os separadores são:

- **Geral** — preferências principais, o dispositivo de entrada de áudio detetado e os medidores de teste de microfone/áudio do sistema, ligação ao Google Calendar, opções de captura de ecrã e **Verificar atualizações**.
- **Atalhos de teclado** — ver e redefinir todos os atalhos.
- **Perfil** — as suas respostas da integração inicial, memória do utilizador e desambiguações.
- **Segurança** — opções de segurança da conta.
- **Idioma** — idioma da interface / das respostas.
- **Recursos** — carregue e faça a gestão dos seus documentos Markdown, e escolha quais estão ativados para o projeto ativo (consulte [Documentos](#documentos)).
- **Faturação** — a sua subscrição e plano (controla o acesso a funcionalidades pagas, como o chat de IA ambiente).

---

## Atualização

O Elyvo Assist **não** se atualiza sozinho, mas a verificação de versão é automática: o servidor consulta periodicamente o GitHub (aproximadamente a cada 8 horas, mais uma vez ao arrancar o servidor) à procura de novas versões e, se encontrar uma mais recente, envia para o seu Dashboard um aviso que pode fechar, **"New version!"** (o título mantém-se em inglês), com uma ligação para descarregar. Também pode acionar manualmente **Verificar atualizações** em **Definições → Geral** a qualquer momento para abrir diretamente a página [Releases](https://github.com/pdasilem/elyvo-assist/releases) no seu navegador.

Para atualizar, descarregue o instalador mais recente para a sua plataforma a partir de [Releases](https://github.com/pdasilem/elyvo-assist/releases) e execute-o sobre a instalação existente — as definições e a sessão iniciada são preservadas.

- **Arch / Manjaro:** volte a executar o `install.sh` da versão mais recente, ou faça `sudo pacman -U` ao novo `.pkg.tar.zst`.
- **Debian / Ubuntu:** `sudo apt install ./elyvo-assist-<nova-versão>-linux-x86_64.deb`.
- **Windows / macOS:** execute o novo instalador / abra o novo DMG.

> Utilizadores de Linux KDE com KWin anterior à 6.7.0: reaplique o patch de captura de ecrã do KWin após uma atualização do sistema KWin, caso dependa da proteção contra capturas de ecrã. Se a atualização o levar ao KWin 6.7.0 ou mais recente, o patch deixa de ser necessário — a proteção está integrada.

---

## Desinstalação

- **Windows** — *Definições → Aplicações → Aplicações instaladas → Elyvo Assist → Desinstalar*.
- **macOS** — arraste o **Elyvo Assist** de *Applications* para o Lixo.
- **Debian / Ubuntu** — `sudo apt remove elyvo-assist`.
- **Arch / Manjaro** — `sudo pacman -R elyvo-assist`.

---

## Resolução de problemas

**A sobreposição não aparece.** Certifique-se de que a aplicação está em execução (verifique o tabuleiro do sistema/barra de menu) e prima o atalho de alternância (`Ctrl+\`). No macOS, confirme que a permissão de Acessibilidade está concedida, caso contrário os atalhos globais não funcionam.

**Não é captado áudio.** Verifique o acesso ao microfone e à captura de ecrã nas definições de privacidade do seu sistema operativo e, em seguida, utilize o teste de microfone/áudio do sistema em **Definições → Geral** para confirmar os níveis. O Elyvo utiliza o dispositivo de entrada predefinido do seu sistema, pelo que deve definir o predefinido correto nas definições de som do seu sistema operativo. No Linux, confirme que o PipeWire está em execução.

**A sobreposição continua a aparecer em capturas de ecrã no Linux.** A *gravação/partilha* de ecrã está oculta por predefinição. No KWin 6.7.0+ (Plasma 6.7+) as capturas de ecrã ficam ocultas por predefinição; em KWin mais antigos, as capturas de ecrã estáticas requerem o patch pontual do KWin descrito no [README](../README.md#window-protection-from-screen-sharing) — reaplique-o após atualizações do KWin.

**Problemas ao iniciar sessão.** Experimente o método alternativo (email/palavra-passe versus Google) e certifique-se de que o relógio do seu sistema está correto — a validação OAuth e de tokens é sensível ao tempo.

Para qualquer outra questão, abra uma issue no [repositório de releases](https://github.com/pdasilem/elyvo-assist/issues).
