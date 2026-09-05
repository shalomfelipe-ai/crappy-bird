# Crappy Bird — build web

Pasta pronta para publicar no GitHub Pages. **Todo o conteudo aqui e gerado**:
nao edite nada por dentro. Para refazer:

    godot --headless --path . --export-release "Web" "build/web/index.html"
    python tools/empacotar.py     # (o zip de teste, separado)

## Como publicar

1. Crie um repositorio no GitHub (pode ser publico ou privado com Pages ligado).
2. Suba **o conteudo desta pasta na raiz do repositorio**, nao a pasta em si.
3. Settings -> Pages -> Source: `Deploy from a branch`, branch `main`, pasta `/`.
4. O endereco sai em ate um minuto: `https://<usuario>.github.io/<repo>/`

## Detalhes que importam

- **`.nojekyll` precisa ir junto.** Sem ele o GitHub roda o Jekyll, que ignora
  arquivos e pastas comecando com `_` e pode engolir parte do build.
- **Build sem threads, de proposito.** A versao com threads exige os cabecalhos
  COOP/COEP, que o GitHub Pages nao envia — a pagina simplesmente nao abriria.
- **`index.wasm` tem ~38 MB.** Passa no limite de 100 MB por arquivo do GitHub,
  mas cada republicacao guarda outra copia no historico do git. Se voce for
  publicar muitas vezes, considere `git gc` de vez em quando, ou um repositorio
  so para a build.
- **Retrato mostra "ROTATE YOUR DEVICE".** O jogo e paisagem; o aviso e CSS
  injetado pelo `html/head_include` do preset, nao editavel aqui.

## Testar antes de subir

    python -m http.server 8099 --directory build/pages

Abrir http://localhost:8099 — precisa ser por HTTP. Abrir o `index.html` como
arquivo (file://) nao funciona: o navegador recusa carregar o wasm assim.
