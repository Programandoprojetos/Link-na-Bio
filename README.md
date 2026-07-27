# Link na Bio - Luis Henrique

Landing page estilo link na bio criada para reunir servicos, redes sociais, portfolio e contatos em uma unica pagina responsiva.

O projeto foi desenvolvido em HTML, CSS e JavaScript puro, com visual premium em tema escuro, cards animados, contador global mensal com Firebase e assets personalizados.

## Recursos

- Layout responsivo para desktop e mobile.
- Cards de servicos com animacao no hover, foco, toque e rolagem mobile.
- Links diretos para WhatsApp, Instagram e portfolio.
- Card de Portfolio com link externo.
- Card de Suporte e Consultoria.
- Botao de musica com audio local.
- Musica pausa automaticamente ao sair da pagina ou trocar de aba.
- Contador global de visitas do mes usando Firebase Firestore.
- Reset automatico do contador quando o mes muda.
- Favicons e manifesto PWA basico.

## Estrutura

```text
.
|-- index.html
|-- styles.css
|-- site.webmanifest
|-- favicon.ico
`-- assets/
    |-- Luis Henrique.jpg
    |-- pro-elite-montagens.png
    |-- programando-projetos.png
    |-- prime-design.png
    |-- portfolio-logo.png
    |-- support-logo.png
    |-- thunder.mp3
    `-- favicons/
```

## Como Abrir

Abra o arquivo `index.html` diretamente no navegador.

Tambem e possivel publicar o projeto em plataformas como GitHub Pages, Vercel, Netlify ou Firebase Hosting.

## Personalizacao

### Foto do Perfil

A foto principal fica em:

```text
assets/Luis Henrique.jpg
```

Para trocar, substitua esse arquivo por outra imagem mantendo o mesmo nome, ou altere o caminho no `index.html`.

### Logos dos Cards

As logos ficam em:

```text
assets/pro-elite-montagens.png
assets/programando-projetos.png
assets/prime-design.png
assets/portfolio-logo.png
assets/support-logo.png
```

### Links

Os links dos cards e contatos ficam no `index.html`, dentro dos atributos `href`.

Principais destinos configurados:

- WhatsApp: contato direto para orcamento.
- Instagram principal: `@xxluisxx.tw300f`
- Pro Elite: `@pro_elite_montagem`
- Programando Projetos: `@programando_projetos`
- Prime Design: `@prime_design_ofc`
- Portfolio: `https://devportfolio-nu-vert.vercel.app/`

### Musica

O audio fica em:

```text
assets/thunder.mp3
```

O navegador pode bloquear autoplay com som. Por isso existe um botao para tocar ou pausar a musica.

## Contador de Visitas com Firebase

O contador usa Firebase Firestore para registrar visitas globais do mes.

Documento usado:

```text
siteStats/monthlyVisits
```

Campos gravados:

- `month`: mes atual no formato `YYYY-MM`
- `count`: quantidade de visitas do mes
- `updatedAt`: data da ultima atualizacao

Quando o mes muda, o proprio codigo reinicia o contador automaticamente na primeira visita do novo mes.

### Configuracao do Firebase

1. Crie um projeto no Firebase.
2. Adicione um aplicativo Web.
3. Ative o Firestore Database.
4. Use o banco com ID `(default)`.
5. Configure as regras abaixo.

### Regras do Firestore

Use estas regras em Firebase > Firestore Database > Regras:

```js
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    match /siteStats/monthlyVisits {
      allow read: if true;

      allow create: if request.resource.data.month is string
        && request.resource.data.count == 1
        && request.resource.data.updatedAt == request.time;

      allow update: if request.resource.data.month is string
        && request.resource.data.updatedAt == request.time
        && (
          request.resource.data.count == resource.data.count + 1
          || request.resource.data.count == 1
        );
    }
  }
}
```

### Zerar Manualmente

No Firebase:

1. Acesse Firestore Database.
2. Abra a colecao `siteStats`.
3. Abra o documento `monthlyVisits`.
4. Altere o campo `count` para `0`.
5. Salve.

Na proxima visita, o contador volta para `1`.

## Publicacao

Este projeto pode ser publicado como pagina estatica.

Opcoes recomendadas:

- GitHub Pages
- Vercel
- Netlify
- Firebase Hosting

Para publicar, envie todos os arquivos da raiz e a pasta `assets/`.

## Tecnologias

- HTML5
- CSS3
- JavaScript
- Firebase Firestore
- Lucide Icons
- Google Fonts

## Observacoes

Este projeto nao depende de backend proprio. A unica integracao externa e o Firebase Firestore para o contador global de visitas.

Para evitar custos inesperados, acompanhe o uso do Firestore no painel do Firebase, principalmente se a pagina receber muitas visitas.
