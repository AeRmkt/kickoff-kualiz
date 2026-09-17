# Kick-off de Implantação Kualiz — apresentação web

Apresentação de uma página só, em HTML, usada nas reuniões de kick-off da Kualiz.
No ar em: **https://kickoff-kualiz.vercel.app**

## O que tem aqui

| Arquivo | O que é |
| --- | --- |
| `index.html` | A apresentação inteira: conteúdo, estilo, animações e scripts. Não depende de build nem de framework. |
| `logo-kualiz.png` | Logo completo (fundo transparente). |
| `logo-icon.png` | Só o símbolo dos balões (fundo transparente). |

Só isso. Para ver na sua máquina, dê duplo clique no `index.html`.

## Como usar em uma reunião

1. Abra o link.
2. Clique em **Editar informações** (ou no menu **⋯** no topo) e preencha cliente, contato, responsáveis, apresentador e as datas.
3. Clique em **Copiar link com os dados** — esse é o link para mandar ao cliente, já preenchido.
4. Na reunião, clique em **Apresentar**.

Os dados preenchidos viajam dentro do link (`?cliente=...&apresentador=...`), então não existe banco de dados
e cada cliente tem o seu próprio link. O menu **⋯** também tem **Baixar PDF** (15 páginas, 16:9) e **Limpar informações**.

## Modo apresentação

- **Apresentar** abre em tela cheia, um slide por tela, sempre no mesmo quadro 16:9 (1600x900).
- Navegação: setas, espaço, Page Up/Down, clique nos botões de baixo, ou deslizar o dedo no celular. **Esc** sai.
- O conteúdo abaixo do título é reduzido por inteiro quando não cabe — **nunca achate um mockup para fazer caber**.

## Como editar o conteúdo

Tudo está em `index.html`, em três blocos:

1. `<style>` — todo o visual. O bloco do fim, com `body.presenting` e `body.printing`, é o do modo apresentação e do PDF.
2. O HTML dos slides — cada slide é uma `<section id="s1">` … `<section id="s15">`.
3. `<script>` — campos editáveis, animações, simulador de WhatsApp, modo apresentação e PDF.

### Regras deste projeto (combinadas com o Gabriel)

- **O texto é o do documento original do Gamma**, incluindo maiúsculas, colchetes (`Semanas [1–2]`) e os erros de digitação. Não "melhore" o texto.
- **Nada de emoji.** Todo ícone é um `<svg>` que aponta para um `<symbol>` no topo do arquivo (`#i-cal`, `#i-check`, …).
- **Cores da marca:** branco predominante, laranja `#D65F3B` nos destaques, azul `#4472A3` nos detalhes, amarelo `#F5B93B` em pequenos toques.
- **Magic UI:** os efeitos (brilho na borda, entrada suave, feixes animados, spotlight nos cards) fazem parte do padrão.
- **Mockups** (celulares, telas do Kualiz, kanban) são desenhados em HTML/CSS. Mexer neles com cuidado: eles substituem os prints do documento original.

### Campos editáveis

Qualquer texto dentro de `<span data-f="cliente">` é trocado automaticamente pelo valor do formulário.
Para criar um campo novo:

1. Acrescente a chave em `DEFAULTS` (dentro do `<script>`).
2. Use `<span data-f="minhaChave">valor padrão</span>` onde ele deve aparecer.
3. Acrescente um `<label>` com `<input name="minhaChave">` no formulário `#edForm`.

### Simulador de WhatsApp (slide 10)

É 100% roteirizado, sem nenhuma API. A lógica está na função `reply()`: especialidades, dias, horários e
as frases de resposta. Para mudar o que a "IA" diz, mexa ali.

## Como publicar

Precisa da conta Vercel que é dona do projeto:

```bash
cd kickoff-prosaude
npx vercel deploy --prod --yes --scope 7otonis-projects
```

O link `kickoff-kualiz.vercel.app` continua o mesmo; quem abrir depois vê a versão nova.

> Sem acesso a essa conta, rode `npx vercel deploy --prod` sem o `--scope`: cai na conta de quem está logado
> e gera outro link.

## Como criar uma apresentação nova com este mesmo padrão

1. Copie a pasta com outro nome (o nome da pasta vira o nome do projeto na Vercel).
2. Troque o conteúdo das `<section>` mantendo a estrutura (`.head` com `h2` + `.lead`, e o resto do conteúdo abaixo).
3. Publique com `npx vercel deploy --prod --yes`.

Para o **mesmo** kick-off com outro cliente não copie nada: é só preencher o formulário e copiar o link.
