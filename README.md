# christianbeninca.github.io

Repositório de extensões [Mihon](https://mihon.app) hospedado via GitHub Pages.

## Instalar no Mihon

1. **Settings → Browse → Extension repos → Add repository**
2. URL: `https://christianbeninca.github.io`
3. Aba **Extensions** → filtrar `pt-BR` → instalar **Manga Online Green**
4. A fonte é marcada com conteúdo +18 misto: ative "Show sources with adult content" em Settings → Browse se não aparecer.

## Extensões

| Nome | Fonte | Versão |
|------|-------|--------|
| Manga Online Green | [mangaonline.green](https://mangaonline.green) | 1.6.1 (code 1) |

## Estrutura

- `index.min.json` / `index.json` — índice consumido pelo app
- `apk/` — APKs assinados (debug key local)
- `icon/` — ícones por package name
- `index.html` — página humana do repositório

## Build da extensão

Código-fonte em `.ai-work/mihon/extensions-source/src/pt/mangaonlinegreen/` (clone keiyoushi).

```powershell
$env:JAVA_HOME = "C:\Program Files\Java\jdk-25"
.\gradlew.bat :src:pt:mangaonlinegreen:assembleDebug
# APK em src/pt/mangaonlinegreen/build/outputs/apk/debug/
```

Ao atualizar: incrementar `versionCode` no `build.gradle.kts`, rebuildar, copiar o APK para `apk/`,
renomear entrada no `index.json`/`index.min.json` (code, version, apk) e commitar.
