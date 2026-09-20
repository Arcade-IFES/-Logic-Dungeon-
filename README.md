# Logic Dungeon

**Logic Dungeon: O Grimório de Cristal** é um jogo educativo arcade feito com HTML, CSS e JavaScript. Responda perguntas, destrua as runas corretas e sobreviva às ondas de inimigos.

## Como jogar

Abra [logic_dungeon.html](logic_dungeon.html) em um navegador moderno e clique em **ENTRAR NA MASMORRA**.

| Ação | Controle |
|---|---|
| Mover | `W`, `A`, `S`, `D` |
| Mirar | Mouse |
| Atirar | Botão esquerdo do mouse |
| Usar dash | Barra de espaço |

Leia a pergunta no topo da tela e atire apenas na runa que representa a resposta correta. Runa errada e contato com inimigos causam dano.

## Recursos

- Perguntas de diversas áreas do conhecimento.
- Sistema de pontos, combo, experiência e níveis.
- Dificuldade progressiva por fase.
- Fase especial de chefe a cada 10 fases.
- Chefes com três estágios e novas perguntas.
- Dash, escudo e power-ups de cura.
- Ranking local com iniciais, pontos, fase e combo.

## Estrutura

```text
.
├── logic_dungeon.html       # Jogo, interface e lógica principal
├── perguntas.js             # Banco de perguntas
├── .github/workflows/       # Versionamento e releases automáticos
└── README.md
```

## Banco de perguntas

As perguntas ficam em `perguntas.js`. A resposta correta deve ser sempre o primeiro item do campo `a`:

```javascript
{
  q: "Qual é a capital do Brasil?",
  a: ["Brasília", "Rio de Janeiro", "São Paulo", "Salvador"],
  e: "Brasília é a capital federal do Brasil.",
  m: "geografia"
}
```

Para adicionar uma pergunta, copie esse formato e mantenha a resposta correta na posição `a[0]`.

## Execução local

Não é necessário instalar dependências. O arquivo pode ser aberto diretamente no navegador.

Para usar um servidor local:

```bash
python -m http.server 8000
```

Depois, acesse `http://localhost:8000/logic_dungeon.html`.

## Versionamento

O workflow em `.github/workflows/autotag.yml` cria automaticamente uma nova tag e uma Release a cada push na branch `main`:

```text
v0.0.1 -> v0.0.2 -> v0.0.3
```

O ranking é salvo no navegador com `localStorage` e não é compartilhado entre dispositivos.

## Tecnologias

- HTML5 e CSS3
- JavaScript
- Canvas 2D
- Web Audio API
