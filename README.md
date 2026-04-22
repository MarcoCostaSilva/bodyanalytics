<<<<<<< HEAD
# bodyanalytics
=======
# BodyAnalytics — Composição Corporal Avançada

> Plataforma web profissional para avaliação antropométrica clínica. 10 protocolos científicos, 21 índices clínicos com classificação por percentil, relatórios PDF completos — 100% no navegador, sem servidor, sem armazenamento de dados.

![Version](https://img.shields.io/badge/versão-24-blue)
![License](https://img.shields.io/badge/licença-MIT-green)
![Stack](https://img.shields.io/badge/stack-HTML%20%2B%20CSS%20%2B%20JS-orange)
![LGPD](https://img.shields.io/badge/LGPD-conforme-success)

---

## Sumário

- [Visão Geral](#visão-geral)
- [Demonstração](#demonstração)
- [Funcionalidades](#funcionalidades)
- [Protocolos](#protocolos)
- [Índices Clínicos](#índices-clínicos)
- [Medidas Coletadas](#medidas-coletadas)
- [Arquitetura](#arquitetura)
- [Dependências Externas](#dependências-externas)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Deploy no Vercel](#deploy-no-vercel)
- [Uso Local](#uso-local)
- [Privacidade e LGPD](#privacidade-e-lgpd)
- [Roadmap](#roadmap)
- [Referências Bibliográficas](#referências-bibliográficas)

---

## Visão Geral

O **BodyAnalytics** é uma aplicação web de arquivo único (`body-analytics-v24.html`) que implementa o fluxo completo de avaliação antropométrica clínica. Desenvolvida para nutricionistas, educadores físicos, equipes hospitalares e pesquisadores.

**Características principais:**

- Arquivo HTML único e autocontido — sem build, sem dependências locais
- Executa 100% no navegador — zero dados enviados a servidores
- 10 protocolos de composição corporal validados pela literatura
- 21 índices clínicos com interpretação automática
- Tabelas de percentil de Frisancho (1990) embutidas no código
- Exportação de relatório em PDF (jsPDF) e Word (HTML blob)
- Gráfico interativo de composição corporal (Chart.js)
- Suporte bilíngue PT/EN com toggle dinâmico
- 8 temas de cor personalizáveis
- Responsivo para desktop, tablet e mobile

---

## Demonstração

```
https://bodyanalytics.vercel.app        ← landing page
https://bodyanalytics.vercel.app/app    ← aplicação
```

---

## Funcionalidades

### Identificação do Paciente
- Nome, data de nascimento, sexo, etnia, peso atual, peso desejado, peso habitual, estatura
- Cálculo automático de IMC, classificação OMS, faixa de peso ideal
- Estimativa de peso corporal para pacientes acamados — Chumlea, Guo, Roche & Steinbaugh (1988)
- Estimativa de estatura por altura do joelho — Chumlea, Roche & Mukherjee (1987)

### Avaliação Antropométrica
- 11 dobras cutâneas com descrição anatômica de cada ponto
- 6 perímetros de tronco (medida única): pescoço, ombro, tórax, cintura, abdominal, quadril
- 9 perímetros de membros bilaterais (direito + esquerdo): braço relaxado, braço contraído, antebraço, punho, coxa proximal, coxa medial, coxa distal, panturrilha, tornozelo
- 3 diâmetros ósseos: punho, cotovelo, joelho
- Força de preensão palmar (mão dominante e não dominante)

### Composição Corporal
Calculada automaticamente após protocolo e dobras:

| Variável | Método |
|---|---|
| % Gordura (Siri) | `(4,95/DC − 4,50) × 100` — Siri (1961) |
| % Gordura (Brozek) | `(4,57/DC − 4,142) × 100` — Brozek et al. (1963) |
| Gordura Corporal (kg) | `% gordura × peso` |
| Massa Magra Total (kg e %) | `peso − gordura` |
| Massa Muscular (kg e %) | Matiegka (1921) |
| Peso Ósseo (kg e %) | Von Dobeln modificado por Rocha (1975) |
| Peso Residual (kg e %) | Würch (1974) — ♂ 24,1% / ♀ 20,9% |
| Água Corporal Total (L e %) | Watson et al. (1980) |
| Compleição Óssea | Razão Estatura ÷ Circunferência do Punho |

### Índices Clínicos
21 índices calculados automaticamente com checkboxes de seleção para exportação.

### Avaliação Energética
- Taxa Metabólica Basal: Mifflin-St Jeor (1990), Harris-Benedict (1919), FAO/OMS (1985)
- Gasto Energético Total (GET) com 5 fatores de atividade
- Necessidade Energética Estimada — IOM (2005)
- Meta calórica diária com objetivo (manutenção, perda, ganho)
- Todos os itens com checkboxes — exportação seletiva para o relatório

### Relatório PDF
- **Simples**: 1–2 páginas — Estado nutricional + composição corporal + gráfico (opcional)
- **Completo**: até 4 páginas — todas as seções, índices clínicos, energética, laudo, medidas aferidas
- Gráfico de composição em barras (cores derivadas do tema)
- Bolinhas de classificação coloridas 🟢🟡🔴 em cada resultado
- Campo de laudo livre para o profissional
- Assinatura profissional com nome, título, número do conselho e especialidade
- Exportação Word (`.doc`) como alternativa

---

## Protocolos

| # | Protocolo | Sexo | Dobras |
|---|---|---|---|
| 01 | Pollock & Jackson (1978/1980) | ♂♀ separados | 3 dobras |
| 02 | Pollock & Jackson (1978/1980) | ♂♀ separados | 7 dobras |
| 03 | Durnin & Womersley (1974) | ♂♀ | 4 dobras |
| 04 | Guedes (1985) | ♂♀ | 3 dobras |
| 05 | Petroski (1995) | ♂♀ | 4 dobras |
| 06 | Faulkner (1968) | ♂♀ | 4 dobras |
| 07 | Weltman et al. (1988) | ♀ | Perímetros |
| 08 | Katch & McArdle (1973) | ♂♀ | 3 dobras |
| 09 | Chumlea et al. (1988) | ♂♀ | Estimativa — idosos |
| 10 | Yuhasz (1974) | ♂♀ | 6 dobras |

---

## Índices Clínicos

| Índice | Referência | Classif. |
|---|---|---|
| Índice de Massa Corporal | OMS, 1995 | Categórica |
| Relação Cintura-Quadril | WHO, 2008 | Por sexo |
| Relação Cintura-Altura | Ashwell & Hsieh, 2005 | Ponto de corte |
| Índice de Conicidade | Valdez, 1991 | Ponto de corte |
| Índice de Adiposidade Corporal | Bergman et al., 2011 | Faixas % |
| Circunferência da Cintura | WHO, 2008 | Por sexo |
| Circunferência do Pescoço | Ben-Noun et al., 2001 | Por sexo |
| Circunferência da Panturrilha | WHO, 1995 | Ponto de corte |
| Índice de Massa Livre de Gordura | VanItallie et al., 1990 | Por sexo |
| Índice de Massa de Gordura | VanItallie et al., 1990 | Por sexo |
| Circunferência do Braço | Frisancho, 1990 | **Percentil** P5–P95 |
| Circunferência Muscular do Braço | Frisancho, 1981 | **Percentil** P5–P95 |
| Área Muscular do Braço corrigida | Heymsfield et al., 1982 | **Percentil** P5–P95 |
| Área de Gordura do Braço | Frisancho, 1990 | **Percentil** P5–P95 |
| Prega Cutânea Triciptal | Frisancho, 1990 | **Percentil** P5–P95 |
| Prega Cutânea Subescapular | Frisancho, 1990 | **Percentil** P5–P95 |
| Força de Preensão Palmar — Direita | Referência clínica | 5 níveis |
| Força de Preensão Palmar — Esquerda | Referência clínica | 5 níveis |
| Espessura Músculo Adutor do Polegar — Direito | Gonzalez et al., 2010 | Ponto de corte |
| Espessura Músculo Adutor do Polegar — Esquerdo | Gonzalez et al., 2010 | Ponto de corte |
| Compleição Óssea | Referência clínica | 3 categorias |

**Percentis Frisancho (1990):** tabelas completas embutidas no JS para 28 faixas etárias (1,0–74,9 anos), ambos os sexos, percentis P5, P10, P15/P25, P50, P75, P85/P90, P95.

---

## Medidas Coletadas

### Dobras Cutâneas (mm)
`Bíceps · Tríceps · Subescapular · Suprailíaca · Abdominal · Coxa Medial · Panturrilha Medial · Peitoral · Axilar Média · EMAP Direito · EMAP Esquerdo`

### Perímetros de Tronco — medida única (cm)
`Pescoço · Ombro · Tórax · Cintura · Abdominal · Quadril`

### Perímetros de Membros Superiores — bilateral D/E (cm)
`Braço relaxado (CB) · Braço contraído · Antebraço · Punho`

### Perímetros de Membros Inferiores — bilateral D/E (cm)
`Coxa proximal · Coxa medial · Coxa distal · Panturrilha · Tornozelo`

### Diâmetros Ósseos (cm)
`Punho · Cotovelo · Joelho`

### Força
`Preensão palmar dominante (kgf) · Preensão palmar não-dominante (kgf) · Seleção de dominância`

**Total: 38 campos + 9 bilaterais = 47 pontos de coleta**

---

## Arquitetura

```
body-analytics-v24.html          (215 KB — arquivo único)
│
├── <style>                      CSS3 — design system completo
│   ├── Variáveis CSS custom properties (8 temas de cor)
│   ├── Layout: CSS Grid + Flexbox
│   ├── Responsivo: breakpoints 380px / 540px / 768px
│   └── Componentes: cards, stepper, dual-input, CI table
│
├── <body>                       HTML5 semântico
│   ├── Header com stepper de navegação (5 etapas)
│   ├── Seção 1: Identificação do paciente
│   ├── Seção 2: Dobras cutâneas + grade dinâmica por protocolo
│   ├── Seção 3: Perímetros + diâmetros + força
│   ├── Seção 4: Avaliação energética
│   ├── Seção 5: Laudo + opções de exportação
│   └── Cards de resultado (composição + índices clínicos)
│
└── <script>                     JavaScript ES6+
    ├── Estado global (objeto S)
    ├── SKINFOLDS_DEF[]          11 dobras com metadados
    ├── FRISANCHO_CB/CMB/AMB/AGB/PCT/PCSE  tabelas de percentil
    ├── FPP_CUTOFFS              pontos de corte por sexo/lado
    ├── EMAP_CUTOFFS             Gonzalez (2010) por sexo/idade
    ├── CLINICAL_INDICES[]       19 índices com calc() + interp()
    ├── Funções de cálculo       calcSkinfolds, calcBMI, calcEnergy...
    ├── displaySFResults()       composição corporal + gráfico
    ├── exportPDF()              jsPDF — relatório completo
    └── exportWord()             HTML blob — relatório Word
```

### Fluxo de dados

```
Entrada do usuário
      │
      ▼
calcSkinfolds()         ← protocolo + dobras → densidade corporal
      │
      ▼
displaySFResults()      ← % gordura Siri/Brozek + composição absoluta
      │
      ▼
calcAllClinicalIndices() ← todos os 19 índices em paralelo
      │
      ▼
renderCompositionChart() ← Chart.js: barras empilhadas
      │
      ▼
exportPDF() / exportWord() ← relatório final
```

### Funções JavaScript principais

| Função | Descrição |
|---|---|
| `calcSkinfolds()` | Calcula densidade e % gordura pelo protocolo selecionado |
| `displaySFResults(fatPct, density, sum, weight, sex, age)` | Preenche todos os cards de composição corporal |
| `calcAllClinicalIndices()` | Roda todos os 19 índices e atualiza a tabela |
| `calcEnergy()` | Calcula TMB, GET, EER e meta calórica |
| `calcBMI()` | IMC, classificação OMS, faixa de peso ideal |
| `calcFrameSize()` | Compleição óssea por razão estatura/punho |
| `calcGrip()` | Classificação EWGSOP2 da força de preensão |
| `calcChumlea()` | Estimativa de estatura por altura do joelho |
| `calcPesoEstimado()` | Estimativa de peso — Chumlea (1988) |
| `buildCITable()` | Constrói dinamicamente a tabela de índices clínicos |
| `buildSFGrid()` | Gera a grade de dobras para o protocolo selecionado |
| `renderCompositionChart()` | Gráfico Chart.js de composição em barras |
| `exportPDF()` | Gera e baixa o relatório em PDF via jsPDF |
| `exportWord()` | Gera e baixa o relatório em formato Word |
| `lookupPercentile(val, table, sex, age)` | Consulta tabelas de Frisancho e retorna classificação |

---

## Dependências Externas

Carregadas via CDN — sem instalação local necessária:

| Biblioteca | Versão | Uso | CDN |
|---|---|---|---|
| jsPDF | 2.5.1 | Geração do relatório PDF | cdnjs.cloudflare.com |
| Chart.js | 4.4.1 | Gráfico de composição corporal | cdnjs.cloudflare.com |
| Google Fonts | — | Fraunces + Instrument Sans | fonts.googleapis.com |

> **Offline:** o app funciona sem as fontes e sem o gráfico caso não haja internet. O PDF usa Helvetica (fonte nativa do jsPDF).

---

## Estrutura do Projeto

Para deploy no Vercel, organizar assim:

```
bodyanalytics/
├── index.html              ← landing page (bodyanalytics-landing-v2.html)
├── app/
│   └── index.html          ← aplicação (body-analytics-v24.html)
├── vercel.json             ← configuração de rotas
└── README.md
```

### vercel.json

```json
{
  "rewrites": [
    { "source": "/app", "destination": "/app/index.html" },
    { "source": "/app/(.*)", "destination": "/app/index.html" }
  ]
}
```

---

## Deploy no Vercel

### Método 1 — Interface web (recomendado para iniciantes)

**1. Crie o repositório no GitHub**

```bash
# Clone ou crie novo repo
git init bodyanalytics
cd bodyanalytics

# Crie a estrutura
mkdir app
cp body-analytics-v24.html app/index.html
cp bodyanalytics-landing-v2.html index.html
```

**2. Crie o `vercel.json`**

```json
{
  "rewrites": [
    { "source": "/app", "destination": "/app/index.html" }
  ]
}
```

**3. Suba para o GitHub**

```bash
git add .
git commit -m "feat: initial BodyAnalytics deployment"
git branch -M main
git remote add origin https://github.com/seu-usuario/bodyanalytics.git
git push -u origin main
```

**4. Conecte ao Vercel**

1. Acesse [vercel.com](https://vercel.com) e faça login com sua conta GitHub
2. Clique em **"Add New Project"**
3. Importe o repositório `bodyanalytics`
4. Configurações de build: deixe tudo em branco (projeto estático)
5. Clique em **"Deploy"**
6. Em ~30 segundos: `https://bodyanalytics.vercel.app` ✅

### Método 2 — Vercel CLI

```bash
# Instalar CLI
npm install -g vercel

# Na pasta do projeto
vercel

# Seguir as perguntas:
# ? Set up and deploy "bodyanalytics"? → Y
# ? Which scope? → sua conta
# ? Link to existing project? → N
# ? Project name: → bodyanalytics
# ? In which directory is your code? → ./
# ? Want to override settings? → N
```

### Domínio personalizado (opcional)

1. No painel do Vercel: **Settings → Domains**
2. Adicione `bodyanalytics.com.br` (ou o domínio que preferir)
3. Configure os DNS no seu registrador:
   - `A 76.76.21.21`
   - `CNAME www cname.vercel-dns.com`

### Atualizações futuras

Qualquer `git push` na branch `main` faz deploy automático:

```bash
# Atualizar a aplicação
cp nova-versao.html app/index.html
git add .
git commit -m "feat: update app to v25"
git push
# Deploy automático em ~30s
```

---

## Uso Local

```bash
# Opção 1: abrir direto no navegador
open app/index.html   # macOS
start app/index.html  # Windows

# Opção 2: servidor local simples
python3 -m http.server 8000
# Acesse: http://localhost:8000/app/
```

Não requer Node.js, npm, pip ou qualquer outra ferramenta.

---

## Privacidade e LGPD

O BodyAnalytics foi projetado com privacidade por padrão:

- **Zero persistência:** nenhum dado é salvo em localStorage, sessionStorage, cookies ou servidor
- **Zero telemetria:** sem Google Analytics, sem scripts de rastreamento
- **Zero backend:** não existe servidor que receba dados
- **Processamento local:** todos os cálculos ocorrem no JavaScript do navegador do profissional
- **Sessão volátil:** ao fechar a aba, todos os dados desaparecem

Cada uso é uma sessão isolada e efêmera. O arquivo PDF gerado é criado e baixado diretamente no dispositivo do usuário, sem passar por nenhum servidor.

---

## Roadmap

### v1.0 — MVP atual ✅
- 10 protocolos de composição corporal
- 21 índices clínicos
- Exportação PDF e Word
- Gráfico de composição
- Responsivo

### v1.1 — Em desenvolvimento
- [ ] Alertas de risco nutricional cruzado (sarcopenia, desnutrição, risco cardiometabólico)
- [ ] Resumo clínico automático por templates parametrizados
- [ ] Metas terapêuticas pré-prontas clicáveis
- [ ] Triagem de sarcopenia (SARC-F, SARC-CalF)

### v2.0 — SaaS (planejado)
- [ ] Autenticação por profissional (Supabase Auth)
- [ ] Banco de dados de pacientes (PostgreSQL via Supabase)
- [ ] Histórico de avaliações seriadas
- [ ] Comparação evolutiva entre avaliações
- [ ] Resumo clínico por IA (Claude API)

### v3.0 — Plataforma clínica completa (futuro)
- [ ] Protocolos de triagem nutricional: MAN, NRS-2002, ASG
- [ ] Escalas de fragilidade e funcionalidade
- [ ] Algoritmo diagnóstico de sarcopenia disfágica
- [ ] API para integração com prontuários eletrônicos

---

## Referências Bibliográficas

| Referência | Uso no sistema |
|---|---|
| Siri WE (1961). *Body composition from fluid spaces and density.* | % Gordura corporal |
| Brozek J et al. (1963). *Densitometric Analysis of Body Composition.* | % Gordura corporal |
| Pollock ML, Jackson AS (1978/1980). | Protocolos 3 e 7 dobras |
| Durnin JVGA, Womersley J (1974). *Body fat assessed from total body density.* | Protocolo 4 dobras |
| Guedes DP (1985). *Composição Corporal: princípios, técnicas e aplicações.* | Protocolo |
| Petroski EL (1995). *Desenvolvimento e validação de equações.* | Protocolo |
| Matiegka J (1921). *The testing of physical efficiency.* | Massa muscular |
| Von Dobeln W, modificado por Rocha (1975). | Peso ósseo |
| Würch A (1974). *La femme et le sport.* | Peso residual |
| Watson PE et al. (1980). *Total body water volumes.* | Água corporal total |
| Frisancho AR (1990). *Anthropometric Standards for the Assessment of Growth and Nutritional Status.* | Tabelas de percentil |
| Heymsfield SB et al. (1982). *Anthropometric measurement of muscle mass.* | Área Muscular do Braço corrigida |
| Valdez R (1991). *A simple model-based index of abdominal adiposity.* | Índice de Conicidade |
| Bergman RN et al. (2011). *A better index of body adiposity.* | Índice de Adiposidade Corporal |
| VanItallie TB et al. (1990). *Height-normalized indices of the body's fat-free mass.* | FFMI e FMI |
| Ashwell M, Hsieh SD (2005). *Six reasons why the waist-to-height ratio is a rapid and effective global indicator.* | Relação Cintura-Altura |
| WHO (2008). *Waist circumference and waist-hip ratio: report of a WHO expert consultation.* | RCQ e Circunferência da Cintura |
| Ben-Noun L et al. (2001). *Relationship between neck circumference and cardiovascular risk factors.* | Circunferência do Pescoço |
| Gonzalez MC et al. (2010). *Adductor pollicis muscle: Reference values of its thickness in a healthy population.* | EMAP |
| Chumlea WC, Guo SS, Roche AF, Steinbaugh ML (1988). *Prediction of body weight for the nonambulatory elderly.* | Estimativa de peso |
| Chumlea WC, Roche AF, Mukherjee D (1987). *Nutritional Assessment of the Elderly.* | Estimativa de estatura |
| Mifflin MD et al. (1990). *A new predictive equation for resting energy expenditure.* | Taxa Metabólica Basal |
| Harris JA, Benedict FG (1919). *A Biometric Study of Human Basal Metabolism.* | Taxa Metabólica Basal |
| FAO/WHO/UNU (1985). *Energy and protein requirements.* | Taxa Metabólica Basal |
| IOM (2005). *Dietary Reference Intakes for Energy.* | Necessidade Energética Estimada |
| Gallagher D et al. (2000). *Healthy percentage body fat ranges.* | Classificação % gordura |

---

## Licença

MIT License — livre para uso, modificação e distribuição.

---

## Contato

Desenvolvido por **BodyAnalytics**  
📧 contato@bodyanalytics.com.br  
🌐 [bodyanalytics.vercel.app](https://bodyanalytics.vercel.app)

---

*BodyAnalytics — Composição Corporal Avançada · © 2026*
>>>>>>> 653f6df (Primeiro commit - projeto bodyanalytics)
