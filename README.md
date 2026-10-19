# Simulados

Simulados de questões de provas anteriores, como páginas estáticas. HTML + JS puro:
sem build, sem dependências, sem servidor. Hospedado no GitHub Pages.

**Acesse:** https://SEU-USUARIO.github.io/simulados/

## Simulados

### `veterinaria/`

Conhecimentos Específicos de três provas Cesgranrio para Analista Ambiental — 128 questões.

| Prova | Cargo | Questões |
|---|---|---|
| Transpetro 2023 | Analista Ambiental Júnior | 49 |
| Petrobras 2011 | Analista Ambiental Júnior – Biologia | 49 |
| Petrobras Biocombustível 2010 | Analista Ambiental Júnior | 30 |

Apenas Conhecimentos Específicos — Língua Portuguesa e Inglesa ficaram de fora.

Blocos temáticos: Ecologia e Biodiversidade (17) · Biologia, Química e Métodos
Quantitativos (15) · Monitoramento Ambiental e Ecotoxicologia (8) · Poluição Atmosférica
e Mudanças Climáticas (9) · Recursos Hídricos e Efluentes (11) · Resíduos Sólidos (5) ·
Solos e Áreas Contaminadas (9) · Legislação Ambiental e Unidades de Conservação (15) ·
Licenciamento e Avaliação de Impacto Ambiental (6) · Gestão Ambiental e Normas
Técnicas (9) · Gestão de Riscos e Emergências (7) · Petróleo, Gás e Biocombustíveis (7) ·
Educação Ambiental e Sustentabilidade (10).

Dificuldade: 29 Fácil · 67 Média · 32 Difícil.

## Funcionalidades de cada simulado

- Filtros por bloco temático, prova e dificuldade.
- Quantidade configurável (10/20/30/50/todas) e ordem aleatória (Fisher–Yates).
- Resposta em dois cliques: escolher a alternativa, depois **Responder**.
- Progresso salvo em `localStorage` — dá para fechar e retomar de onde parou.
- Relatório com % geral, desempenho por bloco, por dificuldade e por prova,
  lista das questões erradas e opção de refazer só os erros.
- Modo escuro automático; coluna única que funciona no celular.

## Estrutura

```
.
├── index.html          hub com os cartões dos simulados
└── veterinaria/
    ├── index.html      interface, lógica e relatório
    └── questoes.js     window.QUESTOES = [ ... ]
```

## Formato dos dados

Os dados ficam em `.js` (e não `.json`) de propósito: assim a página funciona também
aberta direto do disco, sem servidor — `file://` bloqueia `fetch` de JSON.

```js
window.QUESTOES = [
  {
    "id": "Q001",
    "prova": "Transpetro 2023",
    "empresa": "Transpetro",
    "ano": 2023,
    "cargo": "Analista Ambiental Júnior",
    "num": 21,
    "categoria": "1. Ecologia e Biodiversidade",   // prefixo numérico ordena os filtros
    "tema": "Serviços ambientais",
    "dificuldade": "Fácil",                        // "Fácil" | "Média" | "Difícil"
    "dependeFigura": false,
    "enunciado": "Texto completo...\ncom quebras de linha",
    "alternativas": ["A...", "B...", "C...", "D...", "E..."],
    "gabarito": "D"
  }
]
```

A página monta os filtros a partir dos valores encontrados no array, então acrescentar
provas ou corrigir uma classificação é só editar `questoes.js`. Se uma prova tiver 4
alternativas em vez de 5, a interface já funciona (itera sobre o array); só o relatório
de letras usa a constante `LETRAS`.

As questões vêm da camada de texto dos cadernos oficiais. 18 delas se apoiam em figuras
ou quadros do caderno impresso que não estão reproduzidos aqui: essas exibem um aviso e
podem ser escondidas pelo filtro "ocultar questões que dependem de figura".

## Acrescentar um novo simulado

1. Crie a subpasta da área (ex.: `ambiental/`).
2. Copie `index.html` de um simulado existente e ajuste o `<h1>` e o subtítulo.
3. Gere o `questoes.js` no formato acima.
4. Adicione um cartão em `index.html` da raiz.

## Rodar localmente

Abra `index.html` com duplo clique — não precisa de servidor.
