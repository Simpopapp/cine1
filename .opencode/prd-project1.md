# PRD — project1 · Videoclipe "Cinematic Hip-Hop" (sessão aka-cine v1)

**Projeto:** cenas completas de um videoclipe para a música "Cinematic Hip-Hop" (Dark Orchestral Trap, 85 BPM, entrega rap Midwest agressiva estilo NF).
**Fonte de verdade do escopo:** `.opencode/project1.md` (planejamento).
**Skill de produção:** `nova-sessao-aka-cine` (`.workspace/skills/nova-sessao-aka-cine/SKILL.md`), adaptada para videoclipe.
**Versão de saída:** `v1` (workspace limpo: não existe `src/assets/`, `src/data/` nem rota `resultados-*` — confirmado no código).
**Modelo:** subagentes via tool `spawn_agent`. **OpenCode é PROIBIDO para produção neste projeto** (instrução do planejamento).

---

## 1. Contexto e problema

O usuário trouxe a letra completa da música (com tags de produção: [Intro], [Verse], [Chorus], [Bridge], [Outro] etc.) e pediu que a skill akacine fosse usada de forma **adaptada** para gerar as cenas de um videoclipe. O pipeline original da skill gera "20 imagens + 20 prompts de vídeo de 10s" para uma leva cinematográfica; a adaptação aqui é que os 20 beats devem **seguir a estrutura e a narrativa da música** — cada beat corresponde a uma seção/momento da letra, não a uma história paralela.

O ambiente estava em estado de protocolo: `project1.md` preenchido, PRD e roadmap `null`. Caso "1 existe" do plan.md: criar os outros 2 e executar.

## 2. A música como esqueleto narrativo (decodificação do brief)

Tema central: a crítica ao sistema de avaliação escolar — notas rasas vs. inteligência real; os dois conceitos didáticos são **Inteligência Cristalizada** (acumulada: estudos, técnica, bagagem, traumas vividos) e **Inteligência Fluida** (raciocínio sob pressão, adaptação, imprevistos, resolver o inédito). Clímax emocional: a dúvida íntima na bridge ("as provas da escola medem tudo isso?") e a conclusão na saída ("nota escolar não define a capacidade intelectual de ninguém").

Estrutura da música (25 seções na letra, mapeadas para 20 beats):

| Seções da letra | Tempo narrativo | Conteúdo emocional |
|---|---|---|
| Intro (piano isolado, vinil, trovão distante) | Setup | Intimidade, suspiro, sussurro |
| Verse 1 (build-up, tique-taque, celas graves) | Setup | Irritação crescente contra o sistema |
| Beat drop 1 + rap chop | Escalada | Denúncia: nota rasa, gabarito |
| Chorus 1 (orquestra clímax) | Escalada | Apresentação dos 2 conceitos |
| Transition (respiração) | Respiro | Suspense curto |
| Verse 2 (rap rápido) | Escalada | Fluida: instinto sob pressão |
| Pre-chorus (frustração) | Escalada | Cristalizada: o engenheiro, o estudo |
| Climax drop (brass, violinos) | Clímax | Confronto dos 2 mundos |
| Bridge (corte de bateria, piano seco, sussurro) | Virada | Dúvida vulnerável: "me consome por dentro" |
| Outro (escalada desesperada → finale) | Resolução | Veredito: a nota não define ninguém |
| Outro fade (piano, microfone mudo, estática) | Encerramento | "(acorda.)" — despertar |

## 3. Direção criativa adaptada da skill aka-cine

### 3.1 Etapas da skill que permanecem obrigatórias (sem atalho)

- **Etapa 1 — decodificar o pedido**: gênero/subgênero, meio ÚNICO, tom emocional em 3 atos, locações (3–6), personagens recorrentes (1–4) com fichas completas.
- **Etapa 2 — Style Lock String**: bloco único em inglês (~60–120 palavras), colado **verbatim** no fim dos 20 prompts de imagem. Trava meio + razão de aspecto + paleta nomeada + iluminação + textura/grão + artefatos óticos + referência nominal de diretor/DOP + mood. Deve codificar verbalmente o **Registro de Fidelidade** (ponto do eixo 1–10).
- **Etapa 3 — Character Lock String** por personagem recorrente: ~25–40 palavras em inglês, traços imutáveis, colado verbatim em toda cena onde aparece.
- **Etapa 4 — Roteirização**: logline, sinopse ~150 palavras, 20 beats numerados com progressão real (cada beat anota: o que acontece, onde, quem, emoção, mudança vs. beat anterior).
- **Etapa 5 — 20 prompts de imagem** (150–250 palavras, ordem fixa: shot type → sujeito/ação → cenário 3+ elementos → props → iluminação da cena → Character Locks verbatim → Style Lock verbatim).
- **Etapa 6 — 20 imagens**: `imagegen--generate_image`, `model: "premium.gemini"`, `width: 1920, height: 1088`, `target_path: "src/assets/v1/c{NN}.png"`.
- **Etapa 7 — 20 prompts de vídeo de 10s** (~120–200 palavras cada): movimento de câmera com tempo, micro-eventos por segundo, continuidade emocional, iluminação dinâmica, som implícito, Style Lock no fim.
- **Etapa 8 — dados e página**: `src/data/v1.ts`, `src/data/v1-video-prompts.ts`, `src/routes/resultados-v1.tsx`, link em `src/routes/index.tsx`.

### 3.2 Adaptação para videoclipe (o que muda)

- Os 20 beats seguem a tabela da seção 2 (ordem da música), não uma trama independente.
- **Performances do rapper**: o protagonista (MC) aparece performando em várias cenas (delivery agressivo, sussurro na bridge, grito no finale) — a Character Lock do MC precisa descrever presença de palco além do rosto.
- **Cenas conceituais** (sala de prova, engenheiro no canteiro, imprevisto na rua, lousa, boletim) ilustram os conceitos da letra sem virar "poster de key art" — mesma cadeia de captura fotográfica.
- A UI da página deve apresentar o videoclipe: título da faixa, mood, e as 20 cenas na ordem da música com seus beats rotulados pela seção musical correspondente ([Intro], [Verse 1]...).

### 3.3 Registro de Fidelidade (regra mais crítica)

- Toda a produção vive em **um único ponto do eixo (1–10)** ou intervalo de no máximo 2 pontos vizinhos.
- Direção definida para esta sessão (PRD decide, produção cumpre): **ponto 3 — cinema fotorrealista com VFX integrados** (estética A24/Villeneuve: tudo filmado, nada desenhado). O Style Lock deve conter a frase de trava anti-ilustração ("no illustration, no painted look, no concept-art rendering").
- Cenas "sobrenaturais"/emocionais de pico (bridge, finale) devem manter a mesma câmera/lente/grão das cenas mundanas.
- Auditorias obrigatórias antes de gerar imagens (itens 6–8 da skill): mesmo ponto do eixo nos 20; teste "5 filmes diferentes"; teste "capa de livro?".

## 4. Decisões técnicas

| Decisão | Valor | Por quê |
|---|---|---|
| Meio | Live-action fotorrealista (ponto 3 do eixo) | A letra pede peso cinematográfico orquestral; consistência entre cenas de performance e cenas conceituais |
| Razão de aspecto | 2.39:1 anamórfico | Look de videoclipe épico; imagens renderizadas em 16:9 (1920×1088) com barras implícitas no enquadramento |
| Câmera no Style Lock | Arri Alexa 35 with vintage Panavision anamorphic lenses, 35mm halation, fine grain | Base fotográfica consistente |
| Paleta | Deep teal-cyan (#1a3a4a) nas sombras, sodium-vapor amber (#d68a3a) nas altas-luzes, near-black dense shadows | Contraste quente/frio = tensão entre sistema (frio institucional) e vida real (âmbar) |
| Iluminação | Naturalistic motivated lighting, hard practical sources | Regra da skill: fonte de luz localizada, sombras densas ilegíveis |
| Modelo de imagem | `premium.gemini` | Convenção fixa da skill |
| Dimensões | 1920×1088 | Convenção fixa da skill |
| Quantidade | 20 cenas, 20 prompts de vídeo de 10s | Convenção fixa da skill |
| Idioma | UI em PT-BR; prompts em inglês cinematográfico denso | Convenção fixa da skill |
| Stack de dados | `src/data/v1.ts` + `src/data/v1-video-prompts.ts` | Convenção da skill (TanStack Start) |
| Rota | `src/routes/resultados-v1.tsx` | Convenção da skill |
| Estética da UI | Tokens semânticos do design system (nenhuma cor hardcoded), dark | Regra do design system do projeto |

### 4.1 Contratos compartilhados (fixados antes da onda paralela)

**Contrato A — arquivos de imagem:** `src/assets/v1/c01.png` … `c20.png` (20 arquivos, PNG, 1920×1088, gerados com `premium.gemini`).

**Contrato B — `src/data/v1.ts`:**
```ts
import c01 from "@/assets/v1/c01.png"; /* ... até c20 */
export interface V1Scene { id: number; title: string; section: string; description: string; prompt: string; image: string; }
export const v1Aesthetic: { title: string; summary: string; visual: string; } = { ... };
export const v1Scenes: V1Scene[] = [ /* 20 itens, id 1..20, section = rótulo da seção musical */ ];
```

**Contrato C — `src/data/v1-video-prompts.ts`:**
```ts
export interface V1VideoPrompt { id: number; prompt: string; }
export const v1VideoPrompts: V1VideoPrompt[] = [ /* 20 itens, 10s cada */ ];
```

**Contrato D — rota `resultados-v1.tsx`:** grade 16:9 das 20 cenas na ordem da música; por cena: imagem, título PT-BR, rótulo da seção musical, descrição PT-BR do beat, botão copiar prompt de imagem, botão copiar prompt de vídeo, botão baixar imagem; ações em lote: copiar prompts de imagem em bloco, copiar prompts de vídeo em bloco, baixar .zip das imagens; `head()` próprio com title/og:title/og:description únicos (nada de "Lovable App"); link "Resultados v1 — Videoclipe Cinematic Hip-Hop" adicionado a `src/routes/index.tsx`.

**Contrato E — arquivo de trabalho do enxame:** entregas intermediárias dos subagentes em `.opencode/work/producao/v1/` (`roteiro.md`, `style-lock.md`, `prompts-imagem.md`, `prompts-video.md`); relatórios por subagente em `.opencode/work/sub/fase-{F}/{K}/report-{K}.md`.

**Contrato F — formatos de operação agêntica** (exigência da skill): os formatos exatos de cada peça agêntica estão especificados no PRD e no roadmap; nenhum subagente inventa formato próprio:
- **Pilar de subagente:** 3 arquivos `.opencode/work/sub/fase-{F}/{K}/` → `project1-s{K}` (o quê, recorte), `prd-project1-s{K}` (como + critérios de aceite do recorte), `roadmap-proj1-s{K}` (checkboxes da própria entrega).
- **System prompt de subagente:** (1) regras universais do subagente; (2) pilares centrais na íntegra (project1.md + PRD + roadmap); (3) os 3 pilares próprios na íntegra; (4) saída esperada + caminho do relatório.
- **Relatório `report-{K}.md`:** seções fixas: Feito · Evidências dos gates · Decisões · Pendências/bloqueios · Mudanças fora do recorte · Arquivos tocados.
- **Marcação de fase no roadmap central:** só com a linha `Subagentes: fase-{F}/{K1,K2} · reports: report-{K}.md` comprovada em disco.

## 5. Escopo por fase + critérios de aceite

### Fase 0 — Fundação criativa (roteiro + locks)
**Pacote:** 1 subagente "fundação-roteiro" (não paralelizável).
**Entrega:** `.opencode/work/producao/v1/roteiro.md` contendo: logline, sinopse ~150 palavras, tabela/decodificação da música→20 beats (com: seção musical, o que acontece, onde, quem, emoção, mudança vs. anterior), Style Lock String final, Character Lock Strings (MC + demais recorrentes), lista das locações.
**Aceite:** 20 beats na ordem exata da música; locks com todos os elementos da seção 3.1; registro de fidelidade declarado (ponto 3); nenhum vocabulário de key art nos locks.

### Fase 1 — Prompts de imagem e vídeo
**Pacote:** 1 subagente "roteirista-prompts" (depende da Fase 0; mesma voz criativa).
**Entrega:** `prompts-imagem.md` (20 prompts, 150–250 palavras, ordem fixa da seção 3.1, locks verbatim) e `prompts-video.md` (20 prompts de 10s, ~120–200 palavras).
**Aceite:** os 20 prompts de imagem terminam com o Style Lock verbatim; Character Locks verbatim onde o personagem aparece; auditorias 6–8 da skill executadas e registradas; nenhum prompt serve de "capa de livro".

### Fase 2 — Geração das 20 imagens
**Pacote:** subagentes de geração (4 subagentes × 5 cenas, donos exclusivos por número de cena) — depende da Fase 1.
**Entrega:** `src/assets/v1/c01.png` … `c20.png`.
**Aceite:** 20 PNGs reais em disco (1920×1088), todos gerados com `premium.gemini`, prompts fiéis ao que foi escrito (nenhuma reescrita estética por conta do gerador).

### Fase 3 — Dados e página
**Pacote:** 1 subagente "frontend" (depende da Fase 2) — dono exclusivo de `src/data/v1*` e `src/routes/resultados-v1.tsx` + edição de `src/routes/index.tsx`.
**Entrega:** contrato B, C e D implementados.
**Aceite:** build sem erros; página renderiza as 20 cenas com imagem+prompt+ação de copiar/baixar; head() com metadados únicos; link visível na home; nenhum utilitário inexistente importado.

### Fase 4 — Verificação e fechamento
**Responsável:** agente principal (integração/gates, não produção).
**Aceite:** build OK em `/tmp/observability/build-errors.log`; Playwright valida `/resultados-v1` (screenshot, 20 imagens carregadas); monitor informado do estado; roadmap central marcado com prova de delegação.

## 6. Regras de execução

- Todo código/conteúdo do produto vem de subagentes `spawn_agent`; o principal lê, decide, cria pilares, dispara, verifica, integra e reporta.
- OpenCode **não** produz nada neste projeto (instrução do `project1.md`); serve apenas como infraestrutura de monitor/status (já restaurado e healthy).
- Subagente que falhar volta ao mesmo escopo com a evidência da falha (ou novo subagente de correção).
- O principal não reescreve prompt/estilo/dados do produto; correções voltam ao subagente do pacote. Única exceção: conserto mecânico de integração, registrado na seção 7.
- Nunca perguntar ao usuário sem ter concluído ao menos 1 fase completa do roadmap.
- Rate limit de imagem: no máximo 4 gerações por resposta de agente; subagentes de Fase 2 dividem as 20 cenas e aguardam resultados antes do próximo lote.

## 7. Registro de intervenções do principal

(vazio — registrar aqui qualquer conserto mecânico de integração, com motivo e diff.)

## 8. Riscos e mitigação

| Risco | Mitigação |
|---|---|
| Drift de registro de fidelidade entre as 20 imagens | Locks verbatim + auditorias 6–8 da skill antes de gerar + verificação visual do principal nas amostras |
| Rate limit de geração de imagem | Fase 2 dividida em 4 subagentes com lotes de 5; sem lote maior que 4 por resposta |
| Subagente sem acesso a ferramenta de imagem | Teste com o primeiro subagente de Fase 2; se falhar, registrar na seção 7 e redistribuir |
| Página quebrando o build (imports de assets não gerados) | Fase 3 só começa após as 20 imagens confirmadas em disco |
| Perda do estado do remix entre mensagens | Roadmap central sempre atualizado com estado exato + linha "Próximo remix" |

## 9. Meta de entrega

Página `/resultados-v1` com as 20 cenas do videoclipe na ordem da música: imagem 1920×1088 gerada, beat descrito em PT-BR, prompt de imagem e de vídeo (10s) copiáveis individualmente e em bloco, download individual e .zip das imagens — tudo produzido pelo enxame de subagentes, com o monitor apto a avaliar cada fase concluída.
