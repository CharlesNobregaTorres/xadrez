# Atelier Chess — Multiplayer Online (salas privadas)

## O que vem neste pacote
- `index.html`: Atelier Chess com interface para criar/entrar em salas Firebase e sincronizar posição/lances em tempo real.
- `database.rules.json`: regras iniciais para o Realtime Database, com acesso condicionado à participação na sala.
- `firebase-config.example.js`: referência dos campos de configuração (copie os valores para o objeto `firebaseConfig` dentro de `index.html`).

## 1. Criar o projeto Firebase
1. Acesse https://console.firebase.google.com/ e crie um projeto.
2. Em **Adicionar app**, registre um app Web (`</>`). Copie `apiKey`, `authDomain`, `databaseURL`, `projectId` e `appId`.
3. No `index.html`, encontre `const firebaseConfig = {...}` e substitua os valores `COLE_API_KEY`, `SEU-PROJETO` e `SEU-BANCO` pelos valores reais.
4. Em **Authentication → Sign-in method**, habilite **Anonymous**.
5. Em **Realtime Database**, crie um banco de dados. Copie sua URL para `databaseURL`.
6. Na área **Realtime Database → Rules**, cole o conteúdo de `database.rules.json` e publique. Não use regras abertas de teste em produção.

## 2. Publicar o site
1. Instale Node.js LTS: https://nodejs.org/
2. Extraia este ZIP para uma pasta.
3. Abra o terminal nessa pasta e execute:
   ```bash
   npm install -g firebase-tools
   firebase login
   firebase init hosting
   ```
4. Escolha o projeto criado no Firebase. Defina `public` como diretório público; copie `index.html` para `public/` (ou indique a pasta atual se o assistente permitir). Para uma configuração simples, mantenha `index.html` na pasta `public`.
5. Execute:
   ```bash
   firebase deploy --only hosting
   ```
6. Abra a URL `https://SEU-PROJETO.web.app` e envie o código da sala ao seu amigo. Ambos precisam abrir a mesma versão publicada.

## Como usar
- Clique em **Sala online**.
- Em um navegador, clique **Criar sala** e copie o código de 8 caracteres.
- No outro dispositivo, abra o mesmo site, clique em **Sala online**, digite o código e escolha **Entrar na sala**.
- A pessoa que criou joga de brancas; quem entra joga de pretas.

## Notas importantes
- A configuração Firebase é específica do seu projeto e não pode ser preenchida sem os dados fornecidos no Console.
- Não cole chaves privadas ou service-account JSON no navegador. A configuração de app Web (`apiKey` etc.) é pública por desenho; a segurança depende das regras e autenticação.
- As regras fornecidas permitem que usuários autenticados leiam os registros de salas para viabilizar a entrada por código; trate os códigos como convites privados e não os publique. Regras de banco precisam ser testadas com os dois navegadores antes de divulgar o site. Configure limites/alertas de uso no Firebase.
- Este é um protótipo multiplayer: o estado da posição é sincronizado; relógios, reconexão, abandono, reivindicação de empate e validação autoritativa no servidor ainda precisam de testes e endurecimento antes de torneios públicos.
