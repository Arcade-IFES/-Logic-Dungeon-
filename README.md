# Logic Dungeon

**Logic Dungeon: Mulheres que Mudaram o Mundo** é um jogo educativo arcade feito com HTML, CSS e JavaScript. Responda perguntas sobre mulheres protagonistas da história, destrua as runas corretas e sobreviva às ondas de inimigos.

## Como jogar

Abra [index.html](index.html) em um navegador moderno e clique em **ENTRAR NA MASMORRA**.

| Ação | Controle |
|---|---|
| Mover | `W`, `A`, `S`, `D` |
| Mirar | Mouse |
| Atirar | Botão esquerdo do mouse |
| Usar dash | Barra de espaço |

Leia a pergunta no topo da tela e atire apenas na runa que representa a resposta correta. Runa errada e contato com inimigos causam dano.

## Recursos

- 100 perguntas sobre mulheres revolucionárias, cientistas, artistas, atletas e ativistas.
- Sistema de pontos, combo, experiência e níveis.
- Dificuldade progressiva por fase.
- Fase especial de chefe a cada 10 fases.
- Chefes com três estágios e novas perguntas.
- Dash, escudo e power-ups de cura.
- Ranking local com iniciais, pontos, fase e combo.

## Estrutura

```text
.
├── index.html               # Jogo completo em uma única página
├── game.json                # Manifesto do jogo
├── questoes.json            # Banco documentado com 100 questões
├── capa.png                 # Imagem de capa
├── CREDITOS.md              # Autoria e créditos
├── .github/workflows/       # Versionamento e releases automáticos
└── README.md
```

## Banco de perguntas

O banco oficial desta versão fica em `questoes.json` e contém 100 questões sobre mulheres, cada uma com quatro alternativas, resposta correta, explicação e fonte. O `index.html` carrega esse arquivo por `fetch` antes de liberar o botão de início.

## Execução local

Não é necessário instalar dependências. O arquivo pode ser aberto diretamente no navegador.

Para usar um servidor local:

```bash
python -m http.server 8000
```

Depois, acesse `http://localhost:8000/index.html`.

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
