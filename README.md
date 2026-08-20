# Projeto Bigodes — Gerador de Arte de Adoção 🐾

Editor online para gerar as artes de adoção do **Projeto Bigodes** no modelo oficial:
troque a foto do gato e os textos (sexo, castração, idade) e baixe **os dois formatos** —
o story (1080×1920, o modelo original) e o quadrado do WhatsApp (1080×1080, remontado
com recortes do próprio modelo) — junto com a mensagem pronta pra colar como legenda.

## Arquivos

| Arquivo | O que é |
|---|---|
| `index.html` | **O editor** (publicado no GitHub Pages). Autocontido — o modelo SVG já está embutido. |
| `story-src.html` | Código-fonte do editor, com o marcador `<!--SVG_MODELO-->` no lugar do SVG. |
| `modelo/modelo-post-story.svg` | O modelo oficial da arte, exportado do editor de design. |
| `cartao.html` | Protótipo antigo do cartão quadrado (layout próprio, não usa o modelo). |

## Como atualizar o editor quando o modelo SVG mudar

O `index.html` é gerado injetando o SVG dentro do `story-src.html`:

```powershell
$src = [System.IO.File]::ReadAllText("story-src.html")
$svg = [System.IO.File]::ReadAllText("modelo\modelo-post-story.svg")
[System.IO.File]::WriteAllText("index.html", $src.Replace('<!--SVG_MODELO-->', $svg), (New-Object System.Text.UTF8Encoding($false)))
```

> Atenção: o editor troca a foto e apaga os textos variáveis localizando estruturas
> específicas do SVG (a imagem JPEG do círculo e os grupos de texto vetorizado).
> Se o modelo for re-exportado, essas posições podem mudar — teste antes de publicar.
