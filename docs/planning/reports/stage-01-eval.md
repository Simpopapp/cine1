# Avaliação — Stage 01

**Data:** 2026-10-25
**Veredito:** concluída
**Confiança da avaliação:** alta (verificação mecânica dos 40 prompts no disco)

## Resumo executivo

A Fase 1 existe no disco e cumpre o núcleo do que PRD e roadmap pedem: 20 prompts de imagem e 20 de vídeo, numerados c01–c20, com o Style Lock do roteiro colado verbatim e por último nos 40, e Character Locks verbatim nas 20 imagens onde cada personagem aparece. A recontagem independente reproduz exatamente os números do `report-2.md` (imagens 163–181; vídeos 125–140 palavras de corpo). O que impede um "verde sem ressalvas" não é conteúdo, e sim três convenções ainda não fixadas: o que conta como "palavra do prompt" (o texto integral passa dos tetos do PRD), a política de Character Locks nos vídeos e o letterbox 2.39:1 vs. "barras implícitas" do PRD §4. Nenhuma bloqueia a Fase 2 se resolvida antes do disparo.

## Cobertura de requisitos

- **Atendido**
  - `.opencode/work/producao/v1/prompts-imagem.md`: 20 blocos `c01`–`c20`; `.opencode/work/producao/v1/prompts-video.md`: 20 blocos `c01`–`c20 — 10s`.
  - Style Lock: 40/40 ocorrências idênticas ao bloco do `roteiro.md` §4 e sempre como último parágrafo (comparação byte-a-byte).
  - Character Locks: Caio em 10 cenas, Davi em 12, Helena em 6 — matriz idêntica à declarada no `report-1.md`; todos verbatim.
  - Contagem de corpo (sem Style Lock): imagens 163–181 (faixa 150–250); vídeos 125–140 (faixa 120–200). Bate com a tabela do `report-2.md` cena a cena.
  - Vídeos: todos com 10s explícitos, movimento de câmera temporizado e marcadores em 2s/4s/6s/8s/9s; todos citam som implícito, luz motivada e continuidade emocional.
  - Imagens: shot type distinto entre cenas consecutivas (20 aberturas diferentes); cenário com 3+ elementos; ISO 1600 e imperfeição de captura em 20/20; referências de filme específicas em c05, c09, c16 e c19 (cenas difíceis).
  - Sem vocabulário de key art fora da cláusula negativa do Style Lock; nenhuma cena se sustenta como capa de livro (auditoria textual registrada nos dois reports, itens 6–8).
  - Pilares e reports da onda existem em `.opencode/work/sub/fase-1/{1,2}/` (11–19 linhas cada), com o formato do Contrato F.
  - Roadmap central (`.opencode/roadmap-proj1`) com a Fase 1 marcada `[x]` e ponteiros para os dois reports.
- **Parcial**
  - **Comprimento formal do prompt:** o texto completo (corpo + Style Lock) mede 259–277 palavras nas imagens e 221–236 nos vídeos. O PRD §3.1/§5 e a skill falam do prompt inteiro em 150–250/120–200. Os reports contam só o corpo e excluem o lock; a convenção não está declarada no PRD nem no roadmap.
  - **Character Locks nos vídeos:** os 20 vídeos herdam identidade da imagem e repetem só o Style Lock. É defensável pela etapa 7 da skill, mas o PRD §3.1 item 3 diz "colado verbatim em toda cena onde aparece".
- **Ausente / não evidenciado**
  - `.opencode/work/producao/v1/style-lock.md`, exigido pelo Contrato E — resíduo da Fase 0, não da Fase 1.
  - Registo da intervenção do principal na Fase 1 em `prd-project1.md` §7 (só a Fase 0 está registada), apesar de o PRD exigir registo de toda integração mecânica.
  - `docs/planning/PRD.md` e `docs/planning/ROADMAP.md` canónicos: a fonte real vive em `.opencode/prd-project1.md` e `.opencode/roadmap-proj1`.

## Qualidade do código

Não há código nesta fase; a qualidade mede-se no material de produção.

- **Fortes:** prompts em inglês denso, ordem interna respeitada, locks como sufixo rígido; expansão por acréscimo preservou câmera, ação, luz e referências; micro-eventos de vídeo convivem com os originais sem contradição; c19/c20 fecham o arco sem pose conclusiva; nenhuma cena introduz entidade gráfica ou metáfora ilustrada.
- **Atenção:** `prompts-imagem.md:3` instrui "com letterbox" dentro do arquivo 1920×1088, enquanto o PRD §4 fala em "barras implícitas no enquadramento". Como o cabeçalho não integra o prompt, o gerador tenderá a produzir quadro cheio — a instrução do cabeçalho fica órfã e contraditória. Decidir antes da Fase 2.
- **Atenção:** densidade alta (259–277 palavras com lock) aumenta o risco de o modelo ignorar detalhes finais do corpo; c15 (três personagens) e c19 (dois personagens + chuva) são as cenas de maior risco de drift e devem ser as primeiras amostras auditadas.

## Discrepâncias

1. **Contagem de palavras:** roadmap declara "163–181 (150–250)" e "125–140 (120–200)" sem dizer que exclui o Style Lock. Sob a leitura literal do PRD (prompt inteiro), os 40 prompts estão acima do teto. O texto persistido confirma a convenção do corpo, não a do prompt completo.
2. **Vídeos sem Character Locks:** o `report-2.md` trata a herança da imagem como decisão explícita; o PRD não fecha essa interpretação.
3. **Registo de intervenção:** `prd-project1.md` §7 só tem a Fase 0; a aplicação dos três arquivos pela linha principal na Fase 1 está documentada apenas em `docs/planning/stages/stage-01-status.md`.
4. **Contrato E:** `style-lock.md` listado e inexistente em `producao/v1/`.
5. **Linha "Subagentes" do roadmap:** cita `fase-1/1 (report-1.md)` e `fase-1/2 (report-2.md)` mas não nomeia os pilares (`project1-s*`, `prd-project1-s*`, `roadmap-proj1-s*`), embora eles existam no disco.
6. **Read-only atribuído ao subagente:** o `report-2.md` diz que nada foi gravado; os arquivos em disco têm mtime de 02:42:48 e o roadmap 02:42:56, coerente com aplicação pelo principal. Não há conflito, mas a autoria material do arquivo persistido é da linha principal, não do subagente.

## Riscos para as próximas etapas

1. **Letterbox/aspecto:** se a Fase 2 gerar com barras queimadas, a grade 16:9 da Fase 3 fica com faixas duplas e o gate "1920×1088" passa formalmente mas falha visualmente. Resolver a convenção antes de disparar.
2. **Rate limit na Fase 2:** 4 subagentes × 5 cenas, com regra de ≤4 gerações por resposta. Cada subagente precisa dividir em 4+1; sem instrução explícita, o 5º pedido na mesma resposta viola o PRD §6.
3. **Consistência de personagem:** c06, c07, c11, c13, c14, c15 e c19 têm dois ou três personagens; a fidelidade do lock só se prova na renderização.
4. **Rótulo da seção musical:** os prompts não carregam o rótulo ([Intro], [Verse 1]…), que a Fase 3 exige em `V1Scene.section`; a fonte é a tabela do roteiro — não perder o mapeamento na transição.
5. **Comprimento:** prompts longos podem diluir detalhes de captura; verificar nas amostras se ISO/grão/halation sobreviveram.
6. **Rastreabilidade:** sem `docs/planning/PRD.md`/`ROADMAP.md` canónicos, qualquer reavaliação futura depende de caminhos não previstos pelo protocolo do monitor.

## Recomendações

1. Fixar por escrito no roadmap/PRD que a contagem aceite é do corpo sem Style Lock (ou aceitar o comprimento integral) — uma linha resolve a ambiguidade antes do gate da Fase 2.
2. Decidir e registar a política de Character Locks nos vídeos (herança da imagem é aceitável; escrever isso no PRD).
3. Resolver o letterbox: gerar quadro cheio 1920×1088 sem barras queimadas (leitura do PRD §4) e remover "com letterbox" do cabeçalho, ou assumir barras e ajustar a Fase 3.
4. Acrescentar a Fase 1 à secção 7 do PRD e criar `style-lock.md` (ou emendar o Contrato E).
5. Espelhar ou apontar `docs/planning/PRD.md` e `docs/planning/ROADMAP.md` para os arquivos reais, para o protocolo do monitor ser reproduzível.
6. Na linha "Subagentes" da Fase 1, nomear também os pilares, não só os reports.
7. No disparo da Fase 2: prompts verbatim, lotes 4+1, e auditoria visual prioritária de c15, c19, c14 (chuva) e c01 (abertura íntima).

## Evidências consultadas

- `.opencode/prd-project1.md` (§§3.1, 3.2, 4, 5-Fase 1, 6, 7; Contrato E)
- `.opencode/roadmap-proj1` (Fase 0 e Fase 1)
- `docs/planning/stages/stage-01-status.md`
- `.opencode/work/producao/v1/roteiro.md` (§4 Style Lock, §5 Character Locks)
- `.opencode/work/producao/v1/prompts-imagem.md` e `prompts-video.md` (20+20 blocos, auditoria mecânica)
- `.opencode/work/sub/fase-1/1/report-1.md`, `.opencode/work/sub/fase-1/2/report-2.md`
- `.opencode/work/sub/fase-1/{1,2}/project1-s*, prd-project1-s*, roadmap-proj1-s*`
- `.workspace/skills/nova-sessao-aka-cine/SKILL.md` (etapas 5 e 7, Registro de Fidelidade, auto-checagem)
- Recontagem própria: separação por heading, exclusão de cabeçalho e Style Lock, `split()` por espaço; comparação byte-a-byte do Style Lock com o roteiro e dos locks com os blocos canónicos.
