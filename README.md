# Projeto Bigodes — Gerador de Arte de Adoção 🐾

Editor online para gerar a arte de adoção do **Projeto Bigodes** no modelo oficial
(story 1080×1920): troque a foto do gato e os textos (sexo, castração, idade),
baixe o JPG e envie no WhatsApp com a mensagem pronta.

## Arquivos

| Arquivo | O que é |
|---|---|
| `index.html` | **O editor** (publicado no GitHub Pages). Autocontido — o modelo SVG já está embutido. |
| `story-src.html` | Código-fonte do editor, com o marcador `<!--SVG_MODELO-->` no lugar do SVG. |
| `modelo/modelo-post-story.svg` | O modelo oficial da arte, exportado do editor de design. |
| `cartao.html` | Versão alternativa em formato quadrado 1080×1080 (layout próprio). |

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
