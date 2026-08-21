# christianbeninca.github.io

Hub de projetos no GitHub Pages. A raiz lista os projetos; cada subpasta/repo tem seu próprio conteúdo.

## Projetos

| Projeto | URL |
|---------|-----|
| Hub (esta raiz) | https://christianbeninca.github.io/ |
| Repo de extensões Mihon | https://christianbeninca.github.io/mihon/ |
| Dashboard Pessoal | https://christianbeninca.github.io/CustomDashboard/ |
| NLW eSports AI Agent | https://christianbeninca.github.io/NLW20-GameCoachAi/ |
| SNES Space Shooter | https://christianbeninca.github.io/RetroSpaceShooter/ |
| Megaman Arena Tribute | https://thegamerspub.github.io/MegamanArenaTribute-Website/ |

---

# Repo de extensões Mihon (`/mihon`)

## Instalar no Mihon

1. **Settings → Browse → Extension repos → Add repository**
2. Nome: `Christian Beninca` (ou o que preferir)
3. URL: `https://christianbeninca.github.io/mihon/index.pb` (formato protobuf canônico; index.min.json em JSON também funciona)
4. Aba **Extensions** → filtrar `pt-BR` → instalar **Manga Online Green**
5. A fonte é marcada com conteúdo +18 misto: ative "Show sources with adult content" em Settings → Browse se não aparecer.

## Extensões

| Nome | Fonte | Versão |
|------|-------|--------|
| Manga Online Green | [mangaonline.green](https://mangaonline.green) | 1.6.1 (code 1) |

## Estrutura (`mihon/`)

- `index.pb` — índice protobuf canônico (mesmo formato do Keiyoushi)
- `index.min.json` / `index.json` — mesmo Store em JSON (objeto único com
  `name`, `badgeLabel`, `signingKey`, `contact`, `extensionList`), não mais o array legado
- `apk/` — APKs assinados (debug key local)
- `icon/` — ícones por package name
- `index.html` — página humana do repositório

O `signingKey` é o fingerprint SHA-256 (hex minúsculo) do certificado que assina os APKs —
o Mihon usa para confiar automaticamente nas instalações. Se mudar a chave de assinatura,
regenerar com: `apksigner verify --print-certs <apk>` e atualizar aqui.

## Build da extensão

Código-fonte em `.ai-work/mihon/extensions-source/src/pt/mangaonlinegreen/` (clone keiyoushi).

```powershell
$env:JAVA_HOME = "C:\Program Files\Java\jdk-25"
.\gradlew.bat :src:pt:mangaonlinegreen:assembleDebug
# APK em src/pt/mangaonlinegreen/build/outputs/apk/debug/
```

Ao atualizar: incrementar `versionCode` no `build.gradle.kts`, rebuildar, copiar o APK para `mihon/apk/`,
renomear entrada no `index.json`/`index.min.json` (code, version, apk) e commitar.
