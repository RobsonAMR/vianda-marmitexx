# 🍱 Vianda Marmitex

Site de cardápio e pedidos do restaurante **Vianda Marmitex** — comida caseira feita na hora, em Vicente Pires (DF).

O cliente navega pelo cardápio, monta a sacola, escolhe entre **entrega** ou **retirada** e envia o pedido pronto, com total calculado, direto para o **WhatsApp** do restaurante.

Feito apenas com **HTML, CSS e JavaScript puro** — sem frameworks, sem build e sem backend.

---

## ✨ Funcionalidades

- **Cardápio em cards**: Marmitas (9 opções) e Bebidas (9 opções), com foto, descrição e preço.
- **Sacola de pedidos**: botão **+** adiciona o item; dentro da sacola dá para aumentar ou diminuir a quantidade (chegando a 0, o item sai da sacola).
- **Entrega ou retirada**
  - *Entrega*: soma a taxa de **R$ 5,00** e exige o endereço.
  - *Retirada*: esconde o campo de endereço, zera a taxa e mostra o endereço da loja com link para o mapa.
- **Envio pelo WhatsApp**: monta a mensagem com itens, subtotal, taxa, total, nome, endereço, forma de pagamento (Pix, Cartão ou Dinheiro) e observações, e abre o `wa.me` em nova aba.
- **Busca no cardápio**: filtra pelo nome do prato, sem diferenciar maiúsculas nem acentos (digitar "agua" encontra "Água"). Seções sem resultado somem e aparece o aviso "Nenhum item encontrado".
- **Cardápio do dia**: pratos com o atributo `data-dias` ficam marcados como indisponíveis nos dias em que não são servidos e não podem ser adicionados à sacola (ex.: Feijoada só às sextas).
- **Layout responsivo**: tema escuro, com ajustes para telas até 980 px e até 600 px.

---

## 🗂️ Estrutura do projeto

```
vianda-marmitexx/
├── index.html            # Página única: cabeçalho, cardápio, sacola e formulário
├── style.css             # Estilos (tema escuro, variáveis de cor, responsivo)
├── script.js             # Sacola, busca, cardápio do dia e envio pelo WhatsApp
├── cardapio_planilha.tsv # Planilha de referência do cardápio (não é lida pelo site)
├── logo.jpg / logo_horizontal.jpg / favicon.jpg / vianda_marmitex icone.jpg
├── cardapio_opcoes.jpg   # Imagem do banner
└── *.jpg / *.jpeg        # Fotos dos pratos e bebidas
```

Todos os arquivos ficam na raiz, e o HTML referencia as imagens pelo nome (ex.: `src="feijoada.jpg"`).

---

## 🚀 Como rodar

Não precisa instalar nada.

**Opção 1 — abrir direto**

```bash
git clone https://github.com/RobsonAMR/vianda-marmitexx.git
cd vianda-marmitexx
```

Depois é só abrir o `index.html` no navegador (dois cliques no arquivo).

**Opção 2 — servidor local (recomendado)**

Com a extensão **Live Server** do VS Code: clique com o botão direito no `index.html` → *Open with Live Server*.

Ou, com Python instalado:

```bash
python3 -m http.server 8000
```

E acesse `http://localhost:8000`.

> Os ícones vêm do Font Awesome via CDN, então é preciso estar conectado à internet para o ícone do WhatsApp aparecer.

---

## 🌐 Publicar no GitHub Pages

1. No repositório, vá em **Settings → Pages**.
2. Em *Source*, escolha **Deploy from a branch**.
3. Selecione a branch `main` e a pasta `/ (root)` e clique em **Save**.
4. Em alguns minutos o site fica disponível em `https://robsonamr.github.io/vianda-marmitexx/`.

---

## 🛠️ Como fazer manutenção

### Adicionar ou alterar um prato

Copie um bloco `.prod` no `index.html` e ajuste nome, descrição, preço e foto:

```html
<div class="prod">
    <div class="info">
        <h4>Nome do Prato</h4>
        <div class="desc">Descrição curta.</div>
        <div class="preco">R$ 24,00</div>
    </div>
    <div class="foto">
        <img src="nome_da_foto.jpg" alt="Nome do Prato">
        <a class="add" href="https://wa.me/556132538736?text=Quero%201%20Nome%20do%20Prato" target="_blank">+</a>
    </div>
</div>
```

- O **preço** precisa seguir o formato `R$ 00,00` — o JavaScript lê esse texto para calcular o total.
- O nome que vai para a sacola e para a mensagem do WhatsApp é o texto do `<h4>`.
- Para bebidas, use `class="foto clara"` (fundo claro para fotos de produto).
- Etiquetas opcionais: `<div class="tags"><span class="tag">Com ovo</span></div>` ou `class="tag hot"` para destaque.

### Definir em quais dias o prato é servido

Adicione `data-dias` ao card, com os dias separados por vírgula:

| 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| dom | seg | ter | qua | qui | sex | sáb |

```html
<div class="prod" data-dias="5">   <!-- só às sextas -->
```

Sem `data-dias`, o prato fica disponível todos os dias. O dia é verificado pelo relógio do aparelho do cliente.

### Alterar taxa de entrega ou número do WhatsApp

No início do `script.js`:

```js
const TAXA_ENTREGA = 5;
```

E na parte do envio:

```js
const WHATSAPP = "556132538736";   // 55 + DDD + número, só dígitos
```

Se trocar o número, atualize também os links `wa.me` do `index.html` (botão do topo e botões **+** dos cards).

### Alterar cores

As cores ficam em variáveis no topo do `style.css`:

```css
:root {
    --fundo: #120f0e;
    --vermelho: #e3262b;
    --laranja: #ff7a1a;
    --verde: #25d366;
    /* ... */
}
```

---

## 🧰 Tecnologias

- HTML5
- CSS3 (variáveis, Grid, Flexbox, media queries)
- JavaScript (vanilla, sem bibliotecas)
- [Font Awesome 6](https://fontawesome.com/) via CDN
- API de links do WhatsApp (`wa.me`)

---

## 📍 Contato do restaurante

- **Telefone / WhatsApp:** (61) 3253-8736
- **Endereço para retirada:** Rua 5, Chácara 100, Loja 1 — Vicente Pires, DF
- **Horário das marmitas:** todos os dias, das 11h às 14h30

---

## 👤 Autor

Desenvolvido por **Robson** — [@RobsonAMR](https://github.com/RobsonAMR)

© Vianda Marmitex
