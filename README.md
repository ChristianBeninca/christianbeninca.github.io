# christianbeninca.github.io

Hub de projetos no GitHub Pages. A raiz (`index.html`) indexa os projetos; cada projeto é um repositório próprio com Pages, exceto as extensões Mihon, que ficam na subpasta `mihon/` deste repositório.

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
4. Aba **Extensions** → filtrar `pt-BR` → instalar as extensões desejadas.
5. As fontes marcadas como **+18** (Manga Online) só aparecem com "Show sources with adult content" ligado em Settings → Browse.

## Extensões

| Nome | Fonte | Versão |
|------|-------|--------|
| Manga Online | [mangaonline.love](https://mangaonline.love) | 1.6.3 (code 3) |
| Manga Livre Blog | [mangalivre.blog](https://mangalivre.blog) | 1.6.3 (code 3) |

## Build

O código vive no clone do keiyoushi em `.ai-work/mihon/extensions-source/src/pt/<extensao>/`.
As extensões deste repo estão registradas no `settings.gradle.kts` desse clone.

```powershell
cd ..\.ai-work\mihon\extensions-source
$env:JAVA_HOME = "C:\Program Files\Java\jdk-25"
.\gradlew.bat :src:pt:mangaonlinegreen:assembleDebug   # Manga Online
.\gradlew.bat :src:pt:mangalivreblog:assembleDebug    # Manga Livre Blog
# APKs em src/pt/<modulo>/build/outputs/apk/debug/
```

Para publicar uma versão:

1. Aumentar o `versionCode` no `build.gradle.kts` do módulo.
2. Compilar e copiar o APK para `mihon/apk/` (o nome já traz a versão) e o ícone de
   `res/mipmap-xxxhdpi/ic_launcher.png` para `mihon/icon/<packageName>.png`.
3. Atualizar `name`, `versionCode`, `versionName` e as URLs em `mihon/index.json`, copiar
   para `mihon/index.min.json` e regerar o protobuf:
   `python tools/gen_index_pb.py mihon/index.json mihon/index.pb`
   (o `id` da fonte é o gerado pelo KSP em `build/generated/ksp/.../ExtensionGenerated.kt`).
4. `python tools/pbtools.py mihon/index.pb` para conferir.

O `signingKey` no `index.json` é o fingerprint SHA-256 do certificado que assina os APKs — o
Mihon usa isso para confiar nas atualizações. Conferir com
`apksigner verify --print-certs mihon\apk\<arquivo>.apk` (a chave de debug local já bate).
