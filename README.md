# Projeto Bigodes — Gerador de Arte de Adoção 🐾

Editor online para gerar as artes de adoção do **Projeto Bigodes** nos modelos oficiais:
preencha os dados uma vez (foto, sexo, castração, idade, contato) e baixe os dois formatos —
o **Story (1080×1920)** e o **Post de feed (1080×1350)** — prontos para WhatsApp e Instagram.

## Arquivos

| Arquivo | O que é |
|---|---|
| `index.html` | **O editor** (publicado no GitHub Pages). Autocontido — os dois modelos SVG já estão embutidos. |
| `story-src.html` | Código-fonte do editor, com os marcadores `<!--SVG_MODELO_STORY-->` e `<!--SVG_MODELO_FEED-->` no lugar dos SVGs. |
| `modelo/modelo-post-story.svg` | Modelo oficial do story, exportado do editor de design. |
| `modelo/modelo-post-feed.svg` | Modelo oficial do post de feed (4:5), exportado do editor de design. |
| `cartao.html` | Protótipo antigo do cartão quadrado (layout próprio, não usa os modelos). |

## Como atualizar o editor quando um modelo SVG mudar

O `index.html` é gerado injetando os SVGs dentro do `story-src.html`:

```powershell
$src = [System.IO.File]::ReadAllText("story-src.html")
$story = [System.IO.File]::ReadAllText("modelo\modelo-post-story.svg")
$feed = [System.IO.File]::ReadAllText("modelo\modelo-post-feed.svg")
$final = $src.Replace('<!--SVG_MODELO_STORY-->', $story).Replace('<!--SVG_MODELO_FEED-->', $feed)
[System.IO.File]::WriteAllText("index.html", $final, (New-Object System.Text.UTF8Encoding($false)))
```

> Atenção: o editor troca a foto e apaga os textos variáveis localizando estruturas
> específicas dos SVGs (a imagem JPEG e os grupos/glifos de texto vetorizado, identificados
> pelos transforms exatos definidos em `STORY` e `FEED` no código). Se um modelo for
> re-exportado, essas coordenadas mudam — ajuste as constantes e teste antes de publicar.
