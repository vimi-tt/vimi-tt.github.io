# Design System — vimi-tt.github.io

## Direction & Visual World

- **Aesthetic**: Monografia Arquitetônica Suíça (*Swiss Architectural Monograph*).
- **Surface Strategy**: Papel mineral claro (`#F4F4F0`) com linhas estruturais de `1px` (`#D4D5CF`) e placas de espécime em obsidiana (`#131418`) para destacar projetos nativos Android (`Overview` e `Verso`).
- **Voice**: Direto, técnico e profissional em `pt-BR`, sem clichês de terminal (`//`, `SOCKET_ESTABLISHED`, números de seção ou cursores customizados).

## Color Palette

| Token | Hex | Role |
|---|---|---|
| `--bg-paper` | `#F4F4F0` | Fundo principal da página |
| `--bg-surface` | `#ECECE6` | Superfícies secundárias e células de destaque |
| `--ink-primary` | `#111214` | Títulos, texto principal e ações primárias |
| `--ink-secondary` | `#4B4F58` | Corpo de texto secundário e navegação |
| `--ink-muted` | `#6C707A` | Metadados e rótulos de tabela |
| `--border-hairline` | `#D4D5CF` | Grade arquitetônica e divisores de `1px` |
| `--accent-cobalt` | `#2B35AF` | Acento único para foco, seleção e marcações técnicas |
| `--plate-obsidian` | `#131418` | Placas de espécime dos projetos em destaque e blocos de código |
| `--plate-border` | `#2A2C34` | Bordas internas nas placas escuras |
| `--plate-ink` | `#F4F4F0` | Texto principal sobre superfícies escuras |
| `--plate-muted` | `#A4A8B3` | Texto secundário sobre superfícies escuras |

## Typography

- **Display (`.font-display`)**: `Archivo` (weights `500–900`, tracking `-0.03em` a `-0.035em`).
- **Body (`.font-sans`)**: `Manrope` (`400–700`, line-height `1.6`).
- **Technical Metadata & Code (`.font-mono`)**: `JetBrains Mono` (`font-variant-numeric: tabular-nums`), restrita a metadados de repositório, plataformas, datas e blocos de código.

## Layout & Components

- **Architectural Grid**: Container `max-w-7xl` delimitado por `border-x border-[#D4D5CF]` com divisões internas por `1px` hairlines.
- **Featured Project Plates**: Placas em `#131418` (`Overview` e `Verso`) com especificações técnicas reais do GitHub à esquerda e esquemáticos SVG autorais da interface à direita.
- **Systems & Web Ledger**: Grade de 3 colunas no papel `#F4F4F0` (`Flicker`, `Automato-Playground`, `Guia de PPC — UFCG`).
- **Browser Surfaces**: `::selection` em `#2B35AF` sobre `#F4F4F0`, `:focus-visible` de `2px solid #2B35AF` e barra de progresso de scroll de `2px` no topo.
- **Motion**: Revelação sutil com GSAP (`expo.out`) nos cards em destaque, respeitando `prefers-reduced-motion: reduce`.
