
# 🗺️ Brasil — Mapa Socioepidemiológico Interativo

Projeto desenvolvido por Vinícius Reis de Lemos motivado e co-participado pela Nutricionista residente em Neonatologia programa da Universidade Federal da Bahia (UFBA) Raquel Natali Cardoso Rebelo.

Aplicação web interativa que exibe indicadores socioepidemiológicos dos 27 estados brasileiros (incluindo o Distrito Federal) em um mapa SVG navegável. Desenvolvida em HTML, CSS e JavaScript puros, sem dependências externas, sem frameworks, sem build step. A aplicação foi feita inline para facilitar o uso em dispositivos móveis de forma offline.

---

## 📸 Visão Geral

Ao clicar em qualquer estado do mapa, um painel lateral (ou modal em dispositivos móveis) exibe um perfil completo com IDH, raça predominante, composição racial, mortalidade, doenças infecciosas, saneamento básico e um contexto epidemiológico narrativo.

---

## ✨ Funcionalidades

- **Mapa SVG interativo** do Brasil com hover, seleção ativa e tooltip com o nome do estado
- **Painel lateral** (desktop) e **modal balloon** (mobile) com perfil socioepidemiológico completo
- **IDH em destaque** com classificação semafórica (Muito Alto / Alto / Médio / Baixo) e cor dinâmica
- **Raça predominante** com indicador colorido por categoria racial (branco, pardo, preto, indígena, amarelo)
- **Barras de composição racial** animadas com transição suave ao selecionar cada estado
- **Codificação por cor** verde / amarelo / vermelho em todos os indicadores para leitura rápida de risco
- **Layout totalmente responsivo**: painel lateral em telas grandes, modal em tablets e smartphones
- **Fechamento de modal** por clique no overlay, botão ✕ ou tecla `Escape`

---

## 📊 Indicadores por Estado

Cada perfil estadual reúne dados de múltiplas fontes organizados em seis blocos temáticos:

### 🧬 IDH & Identidade Racial
| Indicador | Descrição |
|---|---|
| IDH (2022) | Índice de Desenvolvimento Humano com classificação qualitativa |
| Raça Predominante | Categoria racial majoritária com percentual populacional |
| Composição Racial | Distribuição percentual de branco, pardo, preto, indígena e amarelo |

### 💔 Mortalidade & Expectativa de Vida
| Indicador | Unidade |
|---|---|
| Esperança de vida ao nascer | Anos (ambos os sexos) |
| Mortalidade infantil | Óbitos por 1.000 nascidos vivos |
| Mortalidade materna | Óbitos por 100.000 nascidos vivos |
| Cobertura SUS | % da população dependente exclusiva do SUS |

### 🫀 Causas de Óbito
Taxas por 100.000 habitantes para: doenças cardiovasculares, neoplasias malignas (câncer), doenças respiratórias (DPOC, pneumonias, asma) e diabetes mellitus.

### 🦠 Doenças Infecciosas
Incidência por 100.000 habitantes para: tuberculose, dengue, sífilis adquirida e leitos psiquiátricos disponíveis.

### 🚰 Saneamento Básico
| Indicador | Descrição |
|---|---|
| Saneamento adequado | % de domicílios com esgoto e coleta de resíduos |
| Água tratada | % de domicílios com abastecimento de água |

### 📋 Contexto Epidemiológico
Texto narrativo por estado descrevendo os principais desafios sanitários, padrões regionais de morbidade e características do sistema de saúde local.

---

## 🗂️ Fontes de Dados

| Fonte | Dados |
|---|---|
| **IBGE — Censo 2022** | Composição racial, população por estado |
| **DATASUS / SIM** | Mortalidade geral, causas de óbito |
| **SVS/MS — SINAN** | Incidência de tuberculose, dengue, sífilis |
| **ANS (2023)** | Cobertura SUS, leitos psiquiátricos |
| **IPEA / Atlas Brasil** | IDH estadual (2022) |

> Os dados são referentes ao período 2022–2024 e estão embutidos diretamente no arquivo HTML como objeto JavaScript (`stateData`).

---

## 🏗️ Arquitetura

```
mapa_socioepidemiologico.html
│
├── <style>              # CSS inline — variáveis, layout, componentes, responsividade
│   ├── Variáveis CSS    # Paleta de cores, tipografia, espaçamentos
│   ├── Header           # Barra de título e badge de fonte
│   ├── Map Area         # Área SVG com estados interativos
│   ├── Side Panel       # Painel lateral (desktop)
│   ├── Data Card        # Cards de métricas e barras de composição
│   ├── Modal Balloon    # Overlay modal (mobile)
│   └── Responsividade   # Breakpoints: 1024px, 768px, 480px
│
├── <svg id="brazil-map"> # Mapa SVG com paths por estado (data-state="UF")
│
└── <script>
    ├── stateData{}      # Objeto com todos os dados dos 27 estados
    ├── buildCard()      # Gera HTML do painel/modal dinamicamente
    ├── cls_*()          # Funções de classificação semafórica por indicador
    └── Event listeners  # Hover (tooltip), click (painel/modal), Escape, overlay
```

---

## 🎨 Design System

A interface usa um tema dark com grain texture e as seguintes variáveis de cor:

```css
--bg:       #0a0f1a   /* Fundo principal */
--surface:  #111827   /* Superfície do painel */
--surface2: #1a2235   /* Cards de métricas */
--accent:   #3dd68c   /* Verde — indicador positivo / bom */
--warn:     #ffb347   /* Âmbar — indicador médio / atenção */
--danger:   #ff5f5f   /* Vermelho — indicador crítico / ruim */
--accent2:  #5b8dee   /* Azul — hover do mapa */
```

Tipografia: **Syne** (títulos e valores numéricos) + **DM Sans** (corpo de texto) — Google Fonts.

---

## 🚀 Como Usar

Por ser um arquivo HTML único sem dependências locais, basta abrir no navegador:

```bash
# Clone o repositório
git clone https://github.com/viniR15/Mapa_interativo.git

# Abra o arquivo
open mapa_socioepidemiologico.html
# ou arraste o arquivo para qualquer navegador moderno
```

Não é necessário servidor local, npm, pip ou qualquer outra ferramenta.

---

## 🌐 Compatibilidade

Testado nos navegadores modernos que suportam CSS Custom Properties, `dvh` units e `backdrop-filter`:

- Google Chrome 90+
- Mozilla Firefox 90+
- Safari 15+
- Microsoft Edge 90+

## 🔄 Como Atualizar os Dados

Os dados estão no objeto `stateData` dentro do `<script>`, organizados por sigla de UF:

```javascript
const stateData = {
  SP: {
    name: "São Paulo",
    region: "Região Sudeste",
    uf: "SP",
    pop: 46.6,                      // Milhões de habitantes
    idh: 0.826,
    raca: { branco:55, pardo:30, preto:11, indigena:1, amarelo:3 },
    raca_pred: "Branco",
    esperanca_vida: 77.8,           // Anos
    mortalidade_infantil: 9.2,      // Por 1.000 NV
    mortalidade_materna: 38.4,      // Por 100.000 NV
    cobertura_sus: 67,              // %
    cobertura_psiquiatrica: 7.2,    // Leitos por 100k hab.
    obitos_cardiovascular: 174,     // Por 100k hab.
    obitos_cancer: 116,
    obitos_respiratorio: 68,
    obitos_diabetes: 48,
    incidencia_tuberculose: 36.8,   // Por 100k hab.
    incidencia_dengue: 384,
    incidencia_sifilis: 54.6,
    saneamento_basico: 92,          // %
    agua_tratada: 96,               // %
    nota: "Texto narrativo..."
  },
  // ... demais estados
};
```

---

## 📜 Licença

MIT — livre para uso, modificação e distribuição com atribuição.

---

## 🙏 Créditos

Dados compilados a partir de fontes públicas do governo brasileiro. Este projeto não representa posicionamento institucional de nenhum órgão governamental.
