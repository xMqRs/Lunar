<div align="center">

<img src=".github/assets/banner-lunar.png" alt="Lunar" width="720">

</div>

<div align="center">

<a href="https://lunarbot.dev">
  <img src=".github/assets/card-lunar.png" alt="Lunar: bot open source para Discord com música, economia e moderação" width="560">
</a>

</div>

---

<div align="center">

<img src=".github/assets/tags.png" alt="discord.js, TypeScript, Node.js, PostgreSQL, Prisma ORM, Redis, Docker" width="720">

</div>

---

<h3 align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset=".github/assets/title-sobre-dark.png">
    <img src=".github/assets/title-sobre-light.png" alt="Sobre" height="76">
  </picture>
</h3>

<div align="center">

<img src=".github/assets/px-note.png" alt="" height="18"> **Música**: fila, loop, volume, letras e playlists salvas por servidor.

<img src=".github/assets/px-coin.png" alt="" height="18"> **Economia de estrelas**: saldo, recompensa diária, loja, ranking e minigames.

<img src=".github/assets/px-shield.png" alt="" height="18"> **Moderação**: ban, kick, timeout, avisos com histórico e canal de logs.

<img src=".github/assets/px-book.png" alt="" height="18"> **Utilidades**: lembretes, enquetes, perfil e boas-vindas personalizáveis.

Lunar é um bot open source para o Discord, escrito em TypeScript e organizado em módulos independentes. Cada módulo pode ser ligado ou desligado por servidor, e novos comandos entram só criando um arquivo na pasta da categoria.

</div>

---

<h3 align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset=".github/assets/title-estrutura-dark.png">
    <img src=".github/assets/title-estrutura-light.png" alt="Estrutura" height="76">
  </picture>
</h3>

```text
lunar/
  src/
    commands/
      music/          # play, skip, queue, loop, volume, lyrics
      economy/        # saldo, diario, pagar, loja, ranking, slots
      moderation/     # ban, kick, timeout, avisos, limpar
      utility/        # ajuda, ping, perfil, lembrete, enquete
      fun/            # dado, ppt, ship, 8ball, sorteio
    events/           # ready, messageCreate, interactionCreate, guildMemberAdd
    modules/
      player/         # fila de áudio, filtros e cache de streams
      economy/        # carteira, extrato e regras de recompensa
      logger/         # logs estruturados e canal de auditoria
    handlers/         # carregador de comandos e eventos com hot reload
    config/           # leitura e validação das variáveis de ambiente
    index.ts          # ponto de entrada
  prisma/
    schema.prisma     # modelos: Guild, Wallet, Ledger, Warning, Playlist
    migrations/       # migrações SQL do PostgreSQL
  locales/            # traduções (pt-BR, en-US)
  tests/              # testes unitários dos módulos e comandos
  docker-compose.yml  # PostgreSQL + Redis para desenvolvimento
  .env.example        # modelo das variáveis de ambiente
```

---

<h3 align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset=".github/assets/title-como-executar-dark.png">
    <img src=".github/assets/title-como-executar-light.png" alt="Como executar" height="76">
  </picture>
</h3>

<div align="center">

Instale o [Node.js](https://nodejs.org) 20 ou superior e o [Docker](https://www.docker.com) antes de começar.

</div>

```sh
git clone https://github.com/seu-usuario/lunar.git
cd lunar
npm install
cp .env.example .env
docker compose up -d
npx prisma migrate dev
```

<div align="center">

Preencha o `.env` com as variáveis abaixo:

</div>

<div align="center">

<table align="center">
  <thead>
    <tr><th align="center">Variável</th><th align="center">Obrigatória</th><th align="center">Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td align="center"><code>DISCORD_TOKEN</code></td><td align="center">sim</td><td align="center">Token do bot no Developer Portal.</td></tr>
    <tr><td align="center"><code>CLIENT_ID</code></td><td align="center">sim</td><td align="center">ID da aplicação, usado para registrar os slash commands.</td></tr>
    <tr><td align="center"><code>DATABASE_URL</code></td><td align="center">sim</td><td align="center">String de conexão do PostgreSQL.</td></tr>
    <tr><td align="center"><code>REDIS_URL</code></td><td align="center">não</td><td align="center">Cache de filas e cooldowns. Sem ele, usa memória local.</td></tr>
    <tr><td align="center"><code>PREFIX</code></td><td align="center">não</td><td align="center">Prefixo padrão. O valor inicial é <code>l.</code></td></tr>
  </tbody>
</table>

</div>

```sh
npm run dev         # inicia com recarga automática de comandos
npm run build       # compila o TypeScript para dist/
npm start           # executa a versão compilada
npm test            # roda os testes
npm run deploy      # registra os slash commands no Discord
npm run lint        # confere o estilo do código
```

---

<h3 align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset=".github/assets/title-comandos-dark.png">
    <img src=".github/assets/title-comandos-light.png" alt="Comandos" height="76">
  </picture>
</h3>

<div align="center">

O prefixo padrão é `l.` e todos os comandos também existem como slash commands (`/play`, `/saldo`, `/ban`). Ao mencionar `@Lunar` sem texto extra, ela responde com o prefixo atual.

</div>

<div align="center">

<img src=".github/assets/px-note.png" alt="" height="18"> **Música**

<table align="center">
  <thead>
    <tr><th align="center">Comando</th><th align="center">Aliases</th><th align="center">Argumentos</th><th align="center">Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td align="center"><code>l.play</code></td><td align="center"><code>p</code> <code>tocar</code></td><td align="center"><code>&lt;nome ou link&gt;</code></td><td align="center">Toca ou adiciona uma música à fila.</td></tr>
    <tr><td align="center"><code>l.skip</code></td><td align="center"><code>s</code> <code>pular</code></td><td align="center">-</td><td align="center">Pula para a próxima música.</td></tr>
    <tr><td align="center"><code>l.queue</code></td><td align="center"><code>q</code> <code>fila</code></td><td align="center"><code>[página]</code></td><td align="center">Mostra a fila com paginação por botões.</td></tr>
    <tr><td align="center"><code>l.loop</code></td><td align="center"><code>repetir</code></td><td align="center"><code>off</code> <code>faixa</code> <code>fila</code></td><td align="center">Define o modo de repetição.</td></tr>
    <tr><td align="center"><code>l.volume</code></td><td align="center"><code>vol</code></td><td align="center"><code>&lt;0-100&gt;</code></td><td align="center">Ajusta o volume do player.</td></tr>
    <tr><td align="center"><code>l.lyrics</code></td><td align="center"><code>letra</code></td><td align="center"><code>[música]</code></td><td align="center">Busca a letra da música atual.</td></tr>
  </tbody>
</table>

<img src=".github/assets/px-coin.png" alt="" height="18"> **Economia**

<table align="center">
  <thead>
    <tr><th align="center">Comando</th><th align="center">Aliases</th><th align="center">Argumentos</th><th align="center">Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td align="center"><code>l.saldo</code></td><td align="center"><code>bal</code> <code>carteira</code></td><td align="center"><code>[@usuário]</code></td><td align="center">Mostra o saldo de estrelas.</td></tr>
    <tr><td align="center"><code>l.diario</code></td><td align="center"><code>daily</code></td><td align="center">-</td><td align="center">Resgata a recompensa diária.</td></tr>
    <tr><td align="center"><code>l.pagar</code></td><td align="center"><code>pay</code> <code>enviar</code></td><td align="center"><code>@usuário &lt;quantidade&gt;</code></td><td align="center">Transfere estrelas para outro usuário.</td></tr>
    <tr><td align="center"><code>l.loja</code></td><td align="center"><code>shop</code></td><td align="center"><code>comprar &lt;item&gt;</code></td><td align="center">Lista e compra itens da loja do servidor.</td></tr>
    <tr><td align="center"><code>l.ranking</code></td><td align="center"><code>top</code> <code>ricos</code></td><td align="center"><code>[página]</code></td><td align="center">Mostra quem tem mais estrelas.</td></tr>
    <tr><td align="center"><code>l.slots</code></td><td align="center"><code>cassino</code></td><td align="center"><code>&lt;aposta&gt;</code></td><td align="center">Aposta estrelas no caça-níquel lunar.</td></tr>
  </tbody>
</table>

<img src=".github/assets/px-shield.png" alt="" height="18"> **Moderação**

<table align="center">
  <thead>
    <tr><th align="center">Comando</th><th align="center">Aliases</th><th align="center">Argumentos</th><th align="center">Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td align="center"><code>l.ban</code></td><td align="center"><code>banir</code></td><td align="center"><code>@usuário [motivo]</code></td><td align="center">Bane um usuário do servidor.</td></tr>
    <tr><td align="center"><code>l.kick</code></td><td align="center"><code>expulsar</code></td><td align="center"><code>@usuário [motivo]</code></td><td align="center">Expulsa um usuário do servidor.</td></tr>
    <tr><td align="center"><code>l.timeout</code></td><td align="center"><code>mute</code> <code>silenciar</code></td><td align="center"><code>@usuário &lt;duração&gt; [motivo]</code></td><td align="center">Silencia um usuário por tempo determinado.</td></tr>
    <tr><td align="center"><code>l.aviso</code></td><td align="center"><code>warn</code></td><td align="center"><code>@usuário &lt;motivo&gt;</code></td><td align="center">Registra um aviso no histórico do usuário.</td></tr>
    <tr><td align="center"><code>l.limpar</code></td><td align="center"><code>clear</code> <code>purge</code></td><td align="center"><code>&lt;1-100&gt;</code></td><td align="center">Apaga mensagens do canal em massa.</td></tr>
  </tbody>
</table>

<img src=".github/assets/px-star.png" alt="" height="18"> **Utilidades e diversão**

<table align="center">
  <thead>
    <tr><th align="center">Comando</th><th align="center">Aliases</th><th align="center">Argumentos</th><th align="center">Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td align="center"><code>l.ajuda</code></td><td align="center"><code>help</code> <code>cmds</code></td><td align="center"><code>[comando]</code></td><td align="center">Lista os comandos ou detalha um deles.</td></tr>
    <tr><td align="center"><code>l.ping</code></td><td align="center"><code>latencia</code></td><td align="center">-</td><td align="center">Mostra a latência do bot e da API.</td></tr>
    <tr><td align="center"><code>l.perfil</code></td><td align="center"><code>profile</code></td><td align="center"><code>[@usuário]</code></td><td align="center">Exibe o cartão de perfil com nível e estrelas.</td></tr>
    <tr><td align="center"><code>l.lembrete</code></td><td align="center"><code>remind</code></td><td align="center"><code>&lt;tempo&gt; &lt;texto&gt;</code></td><td align="center">Agenda um lembrete por mensagem.</td></tr>
    <tr><td align="center"><code>l.enquete</code></td><td align="center"><code>poll</code></td><td align="center"><code>&lt;pergunta&gt;</code></td><td align="center">Cria uma enquete com reações.</td></tr>
    <tr><td align="center"><code>l.dado</code> <code>l.ppt</code> <code>l.ship</code> <code>l.8ball</code> <code>l.sorteio</code></td><td align="center">vários</td><td align="center">-</td><td align="center">Comandos de diversão em <code>src/commands/fun/</code>.</td></tr>
  </tbody>
</table>

</div>

---

<h3 align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset=".github/assets/title-contribuir-dark.png">
    <img src=".github/assets/title-contribuir-light.png" alt="Contribuir" height="76">
  </picture>
</h3>

<div align="center">

Contribuições são bem-vindas! Para criar um comando novo, copie um arquivo da categoria desejada em `src/commands/` e ajuste o nome, os aliases e a função `execute`.

</div>

```ts
// src/commands/fun/dado.ts
import { defineCommand } from "../../handlers/define";

export default defineCommand({
  name: "dado",
  aliases: ["dice", "d6"],
  description: "Rola um dado de 6 lados.",
  async execute(ctx) {
    const n = Math.floor(Math.random() * 6) + 1;
    await ctx.reply(`🎲 Saiu **${n}**!`);
  },
});
```

<div align="center">

Faça um fork, crie uma branch (`feat/nome-do-recurso`), rode `npm run lint` e `npm test`, e abra um pull request. Mensagens de commit seguem o padrão [Conventional Commits](https://www.conventionalcommits.org/pt-br/).

</div>

---

<div align="center">

Licença [MIT](LICENSE) · histórico de versões em [CHANGELOG.md](CHANGELOG.md)

</div>

---

<div align="center">
  <img src=".github/assets/made-by-xmqr.png" alt="Made by xMqR" height="26">
</div>
