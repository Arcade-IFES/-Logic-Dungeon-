# Logic  Dungeon

**Logic Dungeon: O Grimório de Cristal** é um jogo educativo arcade desenvolvido em HTML, CSS e JavaScript. O jogador controla um mago dentro de uma arena, lê uma pergunta exibida no alto da tela e atira somente na runa que contém a resposta correta.

O projeto combina revisão de conteúdos escolares com uma dinâmica de ação: cada pergunta gera uma onda de criaturas, e o jogador precisa mirar, desviar e responder antes que os inimigos alcancem o personagem.

## Funcionalidades

- Arena 2D renderizada com HTML Canvas.
- Perguntas de Matemática, Física, Química, Biologia, Português, História, Geografia, Filosofia, Inglês, Programação, Desenvolvimento Web, Dados, Redes e Sistemas.
- Alternativas embaralhadas a cada rodada.
- Uma alternativa correta identificada pela runa ciano.
- Sistema de pontuação e combo.
- Progressão por níveis com aumento gradual da velocidade dos inimigos.
- Barra de vida, experiência e nível.
- Dash com invulnerabilidade temporária.
- Power-ups de cura e escudo.
- Efeitos sonoros sintetizados pelo navegador com Web Audio API.
- Efeitos visuais de partículas, brilho, tremor de tela e feedback de acerto ou erro.
- Layout redimensionável para diferentes tamanhos de tela.
- Banco de perguntas separado da lógica do jogo.

## Como jogar

1. Abra o arquivo `dungeon_do_saber.html` em um navegador moderno.
2. Clique em **ENTRAR NA MASMORRA**.
3. Leia a pergunta no topo da arena.
4. Mova o mago e mire com o mouse.
5. Atire na runa ciano, que representa a resposta correta.
6. Evite as runas coloridas incorretas e o contato com os inimigos.
7. Continue acertando para aumentar o combo e avançar de nível.

### Controles

| Ação | Controle |
|---|---|
| Mover para cima | `W` |
| Mover para a esquerda | `A` |
| Mover para baixo | `S` |
| Mover para a direita | `D` |
| Mirar | Mouse |
| Atirar | Botão esquerdo do mouse |
| Usar dash | Barra de espaço |

## Regras do jogo

- Cada onda contém uma pergunta e até quatro runas com alternativas.
- A resposta correta é sempre a primeira alternativa do campo `a` no banco de perguntas.
- As alternativas são embaralhadas antes de aparecerem na arena.
- A runa correta aparece na cor ciano.
- Acertar a resposta:
  - destrói a onda;
  - aumenta a pontuação;
  - aumenta o combo;
  - concede experiência;
  - pode gerar um power-up.
- Acertar uma resposta errada causa dano e reinicia o combo.
- Ser atingido por um inimigo também causa dano.
- Ao completar a experiência necessária, o jogador sobe de nível, recupera a vida e aumenta a vida máxima.
- O jogo termina quando a vida chega a zero.

A pontuação de um acerto é calculada com base no combo atual:

```text
pontos = 100 × combo
```

## Estrutura do projeto

```text
Jogos Arcade/
├── dungeon_do_saber.html   # Interface, estilos, renderização e lógica do jogo
├── perguntas.js            # Banco de perguntas e respostas
└── README.md               # Documentação do projeto
```

### `dungeon_do_saber.html`

É o arquivo principal e pode ser aberto diretamente no navegador. Ele contém:

- Estrutura HTML da tela inicial, HUD e tela de game over.
- Estilos CSS da arena e dos elementos de interface.
- Canvas de `1000 x 700` usado para desenhar o jogo.
- Controle do jogador e movimentação com teclado.
- Mira e disparos com o mouse.
- Criação e atualização dos inimigos.
- Detecção de colisões com runas, pilares e jogador.
- Sistema de pontuação, combo, experiência e níveis.
- Power-ups, partículas, efeitos sonoros e animações.
- Loop principal baseado em `requestAnimationFrame`.

O HTML carrega o banco externo antes do código principal:

```html
<script src="perguntas.js"></script>
```

### `perguntas.js`

Contém o array global `PERGUNTAS`, que é consumido pelo jogo quando uma nova onda é criada.

O campo `a[0]` deve ser sempre a resposta correta. O jogo usa os demais itens como respostas incorretas e embaralha todas as opções antes de exibi-las.

## Formato de uma pergunta

```javascript
{
  q: "Qual é a capital do Brasil?",
  a: ["Brasília", "Rio", "São Paulo", "Salvador"],
  e: "Brasília é a capital federal desde 1960.",
  m: "geografia"
}
```

### Campos disponíveis

| Campo | Descrição | Uso atual |
|---|---|---|
| `q` | Enunciado da pergunta | Exibido no topo da arena |
| `a` | Lista de alternativas | `a[0]` é a correta; todas são usadas no jogo |
| `e` | Explicação da resposta | Reservado para feedback ou revisão futura |
| `m` | Nome da matéria | Reservado para filtros ou sorteio equilibrado futuro |

As alternativas devem ser curtas, preferencialmente com até 12 caracteres, pois aparecem acima das runas dentro da arena.

## Como adicionar perguntas

1. Abra `perguntas.js`.
2. Copie uma pergunta existente.
3. Altere o enunciado, as alternativas, a explicação e a matéria.
4. Coloque a resposta correta na primeira posição do array `a`.
5. Mantenha a vírgula entre os objetos.
6. Salve o arquivo e recarregue o jogo.

Exemplo:

```javascript
{
  q: "Quanto é 2 + 2?",
  a: ["4", "3", "5", "6"],
  e: "A soma de 2 com 2 é 4.",
  m: "matematica"
}
```

Não é necessário modificar o HTML para adicionar ou editar perguntas, desde que `perguntas.js` permaneça na mesma pasta de `dungeon_do_saber.html`.

## Tecnologias utilizadas

- **HTML5**: estrutura da aplicação.
- **CSS3**: layout, HUD, telas, cores e efeitos visuais.
- **JavaScript**: regras, eventos, animações e gerenciamento do estado.
- **Canvas 2D**: desenho da arena, jogador, inimigos, partículas e projéteis.
- **Web Audio API**: geração dos efeitos sonoros.
- **Google Fonts**: fontes `Fira Code` e `Press Start 2P`.

## Fluxo principal do jogo

```text
Tela inicial
    ↓
Iniciar partida
    ↓
Sortear pergunta em PERGUNTAS
    ↓
Separar resposta correta e alternativas erradas
    ↓
Embaralhar e criar as runas
    ↓
Jogador atira em uma runa
    ↓
Acerto? ── sim ──> Pontos, combo, XP e nova onda
    │
    não
    ↓
Dano, perda do combo e remoção da runa
    ↓
Vida chega a zero?
    ├── não ──> Continuar partida
    └── sim ──> Tela de game over
```

## Execução local

O projeto não exige instalação de dependências ou processo de compilação.

### Opção 1: abrir diretamente

Abra `dungeon_do_saber.html` em um navegador como Chrome, Edge ou Firefox.

### Opção 2: usar um servidor local

Um servidor local pode ser útil durante o desenvolvimento. Exemplos:

```bash
python -m http.server 8000
```

Depois, acesse:

```text
http://localhost:8000/dungeon_do_saber.html
```

O servidor deve ser iniciado dentro da pasta do projeto.

## Desenvolvimento e manutenção

Para alterar a aparência ou as regras do jogo, edite `dungeon_do_saber.html`.

Para alterar o conteúdo educacional, edite somente `perguntas.js`.

Ao modificar a lógica, os pontos principais são:

- `spawnWave()`: sorteia a pergunta e cria as runas.
- `processHit()`: decide o que acontece quando um disparo atinge uma runa.
- `resetGame()`: reinicia os dados da partida.
- `update()`: atualiza movimentação, colisões, inimigos e efeitos.
- `draw()`: renderiza a arena e todos os elementos visuais.
- `loop()`: executa o ciclo contínuo do jogo.

## Observações

- O arquivo `perguntas.js` deve permanecer com esse nome e na mesma pasta do HTML.
- O banco é carregado como um script JavaScript comum no navegador.
- As perguntas são sorteadas aleatoriamente.
- Atualmente, o campo `m` não força uma distribuição equilibrada entre matérias.
- Atualmente, o campo `e` não é exibido em uma tela de explicação após a resposta; ele está preparado para uma futura expansão pedagógica.
- O jogo depende de um navegador com suporte a Canvas, ES6 e Web Audio API.

## Possíveis evoluções

- Exibir a explicação `e` depois de cada resposta.
- Criar seleção de matéria usando o campo `m`.
- Implementar sorteio equilibrado entre as disciplinas.
- Adicionar ranking e armazenamento de recordes com `localStorage`.
- Criar tela de pausa.
- Adicionar suporte a toque para dispositivos móveis.
- Separar o código JavaScript do HTML em módulos independentes.
- Adicionar testes automatizados para o banco de perguntas e para as regras de pontuação.
