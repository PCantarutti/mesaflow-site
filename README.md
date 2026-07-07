# mesaflow-site

Site estático do MesaFlow: landing page (placeholder) + página de convite da mesa.

## Páginas

- `index.html` — landing page (TODO: desenvolver).
- `entrar/index.html` — convite da mesa. Recebe `?restaurante_id=<uuid>&mesa=<n>&code=<5 chars>`:
  1. Tenta abrir o app via deep link `mesaflow://entrar?...` (scheme do app Expo).
  2. Se o app não abrir em ~1,6s, mostra os botões das lojas + o código para entrada manual.

O link é gerado pelo app em `mesaflow-cardapio/src/features/cliente/hooks/useCompartilharCodigo.ts`,
com base configurável via `EXPO_PUBLIC_SHARE_URL`. O deep link é tratado em
`src/hooks/useDeepLinkMesa.ts`.

## Deploy

Estático puro — qualquer host serve (Vercel/Netlify/GitHub Pages/Cloudflare Pages).
Depois do deploy, definir `EXPO_PUBLIC_SHARE_URL=https://<dominio>` no `.env` do app.

Teste local: `npx serve .` e abrir
`http://localhost:3000/entrar/?restaurante_id=<uuid>&mesa=12&code=ABC12`.

## TODOs

- [ ] Domínio publicado → atualizar `EXPO_PUBLIC_SHARE_URL` no app.
- [ ] App publicado → preencher `PLAY_STORE_URL` / `APP_STORE_URL` em `entrar/index.html`.
- [ ] Deferred deep link Android: página já manda os params no `referrer` da Play Store;
      falta o app ler o Install Referrer (`expo-application` `getInstallReferrerAsync`)
      no primeiro launch. iOS não tem equivalente — fallback é o código na página.
- [ ] App Links / Universal Links verificados (abrir o link https direto no app, sem
      passar pela página): `.well-known/assetlinks.json` (SHA-256 do certificado EAS) +
      `apple-app-site-association`, e `intentFilters`/`associatedDomains` no `app.json`.
- [ ] Landing page real em `index.html`.
