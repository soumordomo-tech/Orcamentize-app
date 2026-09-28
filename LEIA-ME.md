# Orçamentize – empacotamento para Android

Pasta `www/` = o app (seu HTML + manifest + service worker + ícones).

## Caminho 1 – Instalar como app (PWA), o mais rápido
1. Publique a pasta `www/` em qualquer hospedagem HTTPS gratuita
   (Netlify Drop, Cloudflare Pages, GitHub Pages, Vercel).
2. Abra o link no Chrome do Android → menu ⋮ → **Instalar app / Adicionar à tela inicial**.
3. Abra uma vez com internet; depois disso funciona offline.

## Caminho 2 – Gerar o APK sem instalar nada (GitHub Actions)
1. Crie um repositório no GitHub e envie **todo o conteúdo desta pasta**
   (inclusive a pasta oculta `.github`).
2. Vá na aba **Actions → Gerar APK → Run workflow**.
3. Ao terminar (~5 min), baixe o **Orcamentize-APK** em *Artifacts*, descompacte e
   instale o `app-debug.apk` no celular (permita "fontes desconhecidas").

## Caminho 3 – Gerar o APK no seu computador
Requisitos: Node 20+, Java 17 e Android Studio (ou só o Android SDK).
```
npm install
npx cap add android
npx cap sync android
npx cap open android     # Build > Build APK(s)
```

## Publicar na Play Store
Precisa de APK/AAB **assinado** (release). No Android Studio: Build > Generate Signed Bundle.
Guarde bem o arquivo .jks – sem ele você não consegue atualizar o app depois.

## Observações
- O app usa CDNs (Tailwind, FontAwesome, html2pdf, fonte Inter). Na 1ª abertura precisa de
  internet; o service worker guarda tudo em cache para uso offline depois.
- Os dados (rascunho e materiais) ficam no localStorage do app, no próprio aparelho.
- No app Android, "Baixar PDF" gera o arquivo e abre o menu Compartilhar (WhatsApp, Drive, etc.).
- "Imprimir" (window.print) pode não funcionar dentro do app Android; use o PDF.
