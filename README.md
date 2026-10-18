# Beira OS

Sistema de gestão de ordens de serviço da Beira Premium Garage (Beira, Moçambique). App instalável (PWA), derivada do WR OS, com marca, cores e serviços próprios da Beira.

## Estado atual

- Funciona já em **modo local** (os dados ficam só no aparelho) até o Firebase ser configurado.
- A base de dados da WR (`wr-oficina`) **não** é usada aqui. A Beira tem de ter o seu próprio projeto Firebase.

## A preencher

1. `index.html` → `var OFICINA`: telefone, morada e horário reais da oficina.
2. `firebase-config.js`: configuração do projeto Firebase da Beira + chave VAPID.
3. Regras da base de dados: Firebase Console → Firestore → *Regras*: cole `firestore.rules` e publique.

## Ecrãs e instalação

Funciona em iPhone, Android, tablet e computador. O ecrã adapta-se: telemóvel com barra de separadores em baixo, tablet com duas colunas, computador com menu lateral. As margens de segurança do notch, da ilha dinâmica, do furo da câmara e da barra inicial são respeitadas em retrato e em paisagem (`env(safe-area-inset-*)`, nas variáveis `--sat/--sab/--sal/--sar`).

Para instalar no ecrã inicial: no Android, menu do Chrome → *Instalar app*; no iPhone/iPad, *Partilhar* → *Adicionar ao ecrã inicial*. O ícone é o da Beira Premium Garage (`icon-192/512`, com versão *maskable* para o Android recortar sem cortar o carro).

## Avisos com a app fechada (push)

Um robô gratuito do GitHub (Actions) corre de hora em hora, das 07h às 18h (Maputo), vê as O.S. na base de dados e envia push para os aparelhos registados. Avisa: entrega atrasada / hoje / amanhã, lembretes vencidos, viatura pronta há 2+ dias sem levantar, orçamento sem resposta há 2+ dias.

### Configuração (uma vez)

1. **Chave VAPID**: Firebase Console → Definições do projeto → *Cloud Messaging* → *Certificados Web Push* → *Gerar par de chaves*. Copie a chave pública para `window.WR_VAPID_KEY` em `firebase-config.js`.
2. **Conta de serviço**: Firebase Console → Definições do projeto → *Contas de serviço* → *Gerar nova chave privada*. No GitHub: *Settings → Secrets and variables → Actions → New repository secret*, nome `FIREBASE_SERVICE_ACCOUNT`, valor = o conteúdo completo do ficheiro JSON. **Nunca** coloque este ficheiro no repositório.
3. **Em cada aparelho**: abra a app, entre, toque no sino → *Ativar notificações* e aceite. No iPhone/iPad: primeiro *Partilhar → Adicionar ao ecrã inicial*.

### Testar

- GitHub → *Actions → Avisos push → Run workflow* (com `forcar = 1` para ignorar o horário).
- Lógica dos avisos: `npm test`.
