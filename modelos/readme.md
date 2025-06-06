# 📊 Diagramas UML do Sistema

> Visão Geral

<br>

## 🔹 [DIAGRAMA DE CASOS DE USO (PNG)](./DiagramaCasodeUso/Diagrama%20Caso%20de%20Uso.png)

> Ferramenta: LucidChart

> ### [Detalhamento dos Casos de Uso](./modelos/CasosUsoDescricao.md)

| Nome                   | Ator    | Descrição breve                        |
| ---------------------- | ------- | -------------------------------------- |
| Fazer Login            | Jogador | Permite acesso ao sistema              |
| Fazer Cadastro         | Jogador | Permite acesso ao sistemas             |
| Editar Perfil          | Jogador | Permite inserir informações no sistema |
| Buscar Jogadores       | Jogador | Permite integração entre usuários      |
| Visualizar Perfil      | Jogador | Permite obter informações de usuários  |
| Verificar Login        | Sistema | Permite validar o acesso ao sistema    |
| Cadastrar Jogos        | Jogador | Permite listar preferências            |
| Cadastrar Estilos      | Jogador | Permite listar preferências            |
| Cadastrar Horários     | Jogador | Permite listar preferências            |
| Cadastrar Plataformas  | Jogador | Permite listar preferências            |
| Filtrar por Plataforma | Jogador | Permite selecionar preferências        |
| Filtrar por Região     | Jogador | Permite selecionar preferências        |
| Filtrar por Jogos      | Jogador | Permite selecionar preferências        |
| Enviar Convites        | Jogador | Permite comunicação entre usuários     |
| Conversar com Jogadores| Jogador | Permite comunicação entre usuários     |
| Avaliar Jogadores      | Jogador | Permite rankear usuários               |
| Bloquear Jogadores     | Jogador | Permite gerenciar preferências         |
| Sugerir Jogadores      | Sistema | Permite integração entre usuários      |
| Gerenciar Chat         | Sistema | Permite boa experiência ao usuário     |
| Eviar Notificações     | Sistema | Permite integração entre usuários      |

<br>

## 🔹 [DIAGRAMA DE ATIVIDADE](./DiagramaDeAtividade)

### Fluxo de Ações

> Ferramenta: LucidChart

<br>

| Nome                                                                            | Obs                               |
| ----------------------------------------------------------------------------    | --------------------------------- |
| [Buscar Jogadores](./DiagramaDeAtividade/DiagramaDeATVbuscarJogador.png)        | Filtro, Sugestões e Notificações  |
| [Editar Perfil](./DiagramaDeAtividade/DiagramaDeATVeditarPerfil.png)            | Preferências                      |
| [Acessar](./DiagramaDeAtividade/DiagramaDeATVloginCadastro.png)                 | Cadastro, Login                   |
| [Enviar Mensagem](./DiagramaDeAtividade/DiagramaDeATVenviarMensagem.png)        | Chat                              |
| [Enviar Notificação](./DiagramaDeAtividade/DiagramaDeATVenviarNotificação.png)  | Notificação                       |
| [Vizualizar Perfil](./DiagramaDeAtividade/DiagramaDeATVvisualizarPerfil.png)    | Vizualização, Bloqueio, Avaliação |

<br>

## 🔹 [DIAGRAMA DE CLASSE](./DiagramaDeClasses)

### Módulo de Usuário

# Documentação do Diagrama de Classes - Sistema de Matchmaking e Jogos

<br>

## 🧍‍♂️ Classe Usuario
*Atributos:*
- nome: String
- email: String
- dataNasc: LocalDate
- senha: String

*Métodos:*
- login(email: String, senha: String): boolean
- modificarSenha(senhaAtual: String, novaSenha: String): boolean
- recuperarSenha(email: String): void

*Relacionamentos:*
- Herança: Jogador herda de Usuário
- Associado à ServicoDeUsuario (Dependência)

---

## 🧑‍💻 Classe Jogador
*Atributos:*
- nickname: String
- statusPresenca: String
- horariosDisponiveis: List<String>
- isBloqueadoSistema: boolean

*Métodos:*
-editarPerfil(dadosAtualizacao: Map): void
- buscarMeusJogos(filtro: String): List<Jogo>
- iniciarConversa(outroJogador: Jogador): Chat
- enviarConvite(destino: Jogador, jogo: Jogo, texto: String, chat: Chat): Convite
- receberSugestao(servicoMatchmaking: ServicoDeMatchmaking): List<Sugestao>
- adicionarJogoAoPerfil(j: Jogo): void
- removerJogoDoPerfil(j: Jogo): void
- definirEstilosDeJogo(estilos: List<EstiloDeJogo>): void
- atualizarHorarios(novosHorarios: List<String>): void
- registrarLoginParaHorarioAutomatico(): void
- receberNotificacao(notificacao: Notificacao): void
- bloquearJogador(jogadorParaBloquear: Jogador): void
- desbloquearJogador(jogadorParaDesbloquear: Jogador): void


*Relacionamentos:*
- Envia/recebe Convites, Notificações, Avaliações e Mensagens
- Participa de Chats
- Associado ao ServicoDeMatchmaking

---

## 💬 Classe Chat
*Atributos:*
- idChat: String
- dataCriacao: LocalDateTime
- ultimaAtividade: LocalDateTime

*Relacionamentos:*
- Contém múltiplas Mensagem
- 2 Jogadores participam no mínimo

*Métodos:*
- adicionarMensagem(mg: Mensagem, servico: ServicoDeNotificacao): void
- carregarHistoricoMensagem(quant: int, offset: int): List<Mensagem>
- verificarInteracaoEntreJogadores(A: Jogador, B: Jogador): boolean

---

## ✉️ Classe Mensagem
*Atributos:*
- idMensagem: String
- conteudo: String
- momentoEnvio: LocalDateTime
- statusLeitura: Map

*Métodos:*
- marcarComoLida(j: Jogador): void
- statusLeituraParaJogador(j: Jogador): boolean

---

## 🤝 Classe Convite
*Atributos:*
- conteudo: String
- statusConvite: String
- dataHoraEnvio: LocalDateTime
- dataHoraExpiracao: LocalDateTime

*Métodos:*
- aceitarConvite(servicoNotificacao: ServicoDeNotificacao): void
- recusarConvite(servicoNotificacao: ServicoDeNotificacao): void

---

## 📩 Classe Notificacao
*Atributos:*
- idNotificacao: String
- tipoNotificacao: String
- titulo: String
- mensagemCurta: String
- dataHoraCriacao: LocalDateTime
- Lida: boolean


*Métodos:*
- marcarComoLida(): void

---

## 🌟 Classe Sugestao
*Atributos:*
- pontuacaoCompatibilidade: Double
- criteriosRelevantes: Map
- dataGeracao: LocalDateTime

*Relacionamentos:*
- Gerada por ServicoDeMatchmaking

---

## 🌟 Classe Avaliacao
*Atributos:*
- nota: int
- comentario: String
- dataHoraAvaliacao: LocalDateTime

*Relacionamentos:*
- Enviada de um Jogador para outro

---

## ⚙️ Classe ServicoDeMatchmaking
*Responsabilidades:*
- Gerar sugestões de partidas entre jogadores

*Métodos:*
- gerarSugestoesPara(j: Jogador, filtros: Map): List<Sugestao>
- calcularPontosDeCompatibilidade(A: Jogador, B: Jogador): Double

  *Relacionamentos:*
- Associada a Sistema e Jogador (dependência)

---

## 📤 Classe ServicoDeNotificacao
*Métodos:*
- enviarNotificacao(messagem: Notificacao): void
- criarNotificaoNovaMensagem(c: Chat, m: Messagem, j: Jogador): Notificacao

*Relacionamentos:*
- Associada a Sistema (dependência)

---

## ⚙️ Classe ServicoDeUsuario
*Métodos:*
- cadastrarUsuario(dados: Map): Usuario
- autenticarUsuario(email: String, senha: String): Object
- solicitarRecuperacaoSenha(email: String): void

*Relacionamentos:*
- Associada a Sistema e Usuario (dependência)

---

## 👮‍♀️ Classe ServicoDeModeracao
*Métodos:*
- bloquearJogadorSistema(nick: String, motivo: String, adminResponsavel: Usuario): boolean
- desbloquearJogadorSistema(nick: String, adminResponsavel: Usuario): boolean

  *Relacionamentos:*
- Associada a Sistema e Jogador (dependência)

---

## 🎮 Classe Jogo
*Atributos:*
- nome: String
- descricao: String

*Métodos:*
-obterDetalhes(): String

*Relacionamentos:*
- Associada Plataforma (dependência)

---

## 🎮 Classe EstiloDeJogo
*Atributos:*
- tipo: String
- descricao: String

  *Relacionamentos:*
- Associada Jogo (dependência)

---

## 🕹️ Classe Plataforma
*Atributos:*
- nome: String

*Métodos:*
- listarJogos(catalogo: ServicoDeCatalogo): List<Jogos>

*Relacionamentos:*
- Associada a múltiplos Jogos

---

## 🗂️ Classe ServicoDeCatalogo
*Métodos:*
- cadastrarNovaPlataforma(nome: String): Plataforma
- cadastrarNovoJogo(dadosJogo: Map): Jogo
- cadastrarNovoEstiloJogo(tipo: String, descricao: String): EstiloDeJogo
- listarTodosJogos(filtros: Map): List<Jogo>
- listarTodosEstilos(): List<EstiloDeJogo>

*Relacionamentos:*
- Associada a Sistema, Plataforma, Jogo e EstiloDeJogo

---

## 🧠 Classe Sistema
*Atributos:*
- servicoUsuario: ServicoDeUsuario
- servicoJogador: ServicoDeJogador
- servicoMatchmaking: ServicoDeMatchmaking
- servicoNotificacao: ServicoDeNotificacao
- servicoCatalogo: ServicoDeCatalogo
- servicoModeracao: ServicoDeModeracao

*Relacionamentos:*
- Associada a todas as classes de Serviço

---

## ✅ Classe ServicoDoJogador
*Métodos:*
- atualizaPerfilJogador(nick: String, dadosPerfil: Map): Jogador
- obterPerfilPublico(nickname: String): Object

*Relacionamentos:*
- Associada a Sistema e Jogador

<br>

## 🔹 [DIAGRAMA DE ESTADOS](./DiagramaDeEstados)

### TITULO DO DIAGRAMA

> Mostra os estados possíveis de cada entidade [ex: login] e as transições entre eles.

<br>

| Nome                            | Finalidade / Obs  |
| ------------------------------- | ----------------- |
| [Status Usuário](./DE_login.md) | Status do usuário |
| A2                              | B2                |
| A3                              | B3                |

