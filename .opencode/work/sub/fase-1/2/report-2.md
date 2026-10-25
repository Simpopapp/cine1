# Relatório — fase-1/2 — correcao-prompts

## Feito

- Lidos integralmente os dois arquivos de prompts do pacote fase-1/1 e a skill `.workspace/skills/nova-sessao-aka-cine/SKILL.md`, incluindo etapas 5 e 7, Registro de Fidelidade e auto-checagem 1–8.
- Preparadas versões integrais dos 20 prompts de imagem e dos 20 prompts de vídeo, mantendo cabeçalhos, identificadores, corpos originais e locks.
- Acrescentados detalhes específicos de captura, materiais, ruído ISO 1600, foco, halation restrita, motion blur, sombras e imperfeições físicas.
- Acrescentados micro-eventos locais em 4s e 8s nos 20 vídeos, sem substituir os eventos originais de 2s, 6s e 9s ou os movimentos de câmera.
- Preservados duração de dez segundos, iluminação motivada, referências cinematográficas, personagens e progressão criativa.
- Entregues os três arquivos integrais na resposta final para aplicação pelo agente principal, conforme fallback obrigatório para sandbox sem permissão de alterar o projeto.

## Evidências dos gates

### Método de contagem

Contagem por tokens separados por espaço, equivalente ao campo `NF` de awk; palavras hifenizadas contam como uma unidade. Excluídos títulos, cabeçalhos e Style Lock. Nos prompts de imagem, incluídos os Character Locks, integrantes obrigatórios do prompt. Nos vídeos, contado o corpo de animação; os Character Locks continuam herdados da imagem inicial conforme o cabeçalho original.

Essa convenção mantém comparabilidade com a auditoria recebida: a ordem de grandeza de 131–149 palavras dos originais de imagem corresponde ao corpo com Character Locks e sem Style Lock. O Style Lock não foi usado para inflar a contagem.

A recontagem foi executada em shell sobre os originais lidos em disco e as adições textuais preparadas em `/tmp`, somando os tokens preservados aos acrescentados. Não foram escritos scripts ou código de aplicação. Os arquivos integrais entregues usam esses mesmos textos.

| Cena | Imagem original | Imagem expandida | Vídeo original | Vídeo expandido | Gate |
|---|---:|---:|---:|---:|---|
| c01 | 137 | 167 | 69 | 127 | Verde |
| c02 | 134 | 165 | 68 | 125 | Verde |
| c03 | 133 | 163 | 72 | 129 | Verde |
| c04 | 137 | 168 | 70 | 127 | Verde |
| c05 | 145 | 177 | 72 | 130 | Verde |
| c06 | 137 | 170 | 77 | 135 | Verde |
| c07 | 134 | 166 | 74 | 132 | Verde |
| c08 | 141 | 173 | 77 | 135 | Verde |
| c09 | 149 | 181 | 78 | 137 | Verde |
| c10 | 138 | 169 | 79 | 137 | Verde |
| c11 | 136 | 168 | 78 | 137 | Verde |
| c12 | 142 | 174 | 79 | 137 | Verde |
| c13 | 132 | 164 | 75 | 133 | Verde |
| c14 | 131 | 163 | 79 | 138 | Verde |
| c15 | 133 | 165 | 80 | 139 | Verde |
| c16 | 143 | 175 | 78 | 137 | Verde |
| c17 | 136 | 168 | 77 | 135 | Verde |
| c18 | 141 | 173 | 80 | 138 | Verde |
| c19 | 135 | 167 | 79 | 139 | Verde |
| c20 | 143 | 175 | 81 | 140 | Verde |

Resultado: 20/20 imagens entre 150–250 palavras; 20/20 vídeos entre 120–200 palavras. As pequenas diferenças entre as contagens originais deste relatório e os intervalos da auditoria decorrem da tokenização explicitada acima.

### Locks, estrutura e preservação

- Style Lock: revisão textual das 40 ocorrências; mantido verbatim, sempre como último bloco de cada prompt. Nenhuma adição foi inserida dentro ou depois dele.
- Character Locks: mantidas literalmente todas as ocorrências existentes nas imagens, sem adição, remoção ou troca de personagens.
- Vídeos: mantido o mecanismo original de herança dos Character Locks da imagem inicial, explicitado no cabeçalho; não foram inventados novos blocos de identidade.
- Estrutura: 20 identificadores c01–c20 em cada arquivo, sem alteração de ordem.
- Conteúdo original: mantido integralmente; somente acrescentadas frases ao fim do corpo, antes dos locks.
- Vocabulário: nenhuma adição de key art, composição de capa, pose heroica ou preset genérico. As negativas e os termos do Style Lock aprovado permanecem intocados.
- Picos c14, c15 e c19: água prática, sombras não recuperadas, movimento natural, halation restrita e continuidade de resposta de captura; c15 e c19 reafirmam explicitamente Alexa/Panavision no corpo.
- Verificação de duração: todos os vídeos conservam dez segundos e os movimentos de câmera originais.

### Auto-checagem da skill — itens 1–8

1. **Verde — Style Lock completo.** Contém live-action fotográfico, Arri Alexa 35/Panavision, paleta hexadecimal teal-cyan/amber, luz prática motivada, grão/halation, referências Villeneuve/Deakins e ponto três.
2. **Verde — Character Locks completos.** Caio, Davi e Helena conservam etnia, idade, cabelo, olhos e figurino fixo, além de marcas corporais e props pessoais.
3. **Verde — Style Lock final verbatim.** As vinte imagens e os vinte vídeos terminam no mesmo bloco aprovado.
4. **Verde — Character Locks verbatim.** Todos os personagens presentes nas imagens mantêm seus blocos originais. Vídeos preservam os personagens da imagem homônima e sua herança vinculante, sem regeneração.
5. **Verde — Progressão única.** Intimidade inicial e avaliação interrompida → irritação e contraste entre procedimentos → consulta, escolha e aprendizagem → tentativa e ajuste → medição e verificação → vazamento localizado e cooperação → vulnerabilidade → comparação, explicação e afirmação → retorno íntimo. Nenhum beat foi alterado.
6. **Verde — Registro de Fidelidade.** c01–c20 permanecem no ponto três: captura fotográfica, efeitos práticos ou VFX fotográficos integrados sob a mesma cadeia óptica. A expansão não introduz meio ilustrado ou espetáculo desconectado nos picos.
7. **Verde — Mesmo filme.** Mantidas locações recorrentes, figurinos, props, fontes práticas, paleta, densidade de sombras, óptica anamórfica e textura. As referências específicas originais são aplicadas à fotografia e à atuação, não a mudanças de linguagem.
8. **Verde — Frame, não capa.** As vinte imagens continuam fragmentárias, descentradas, obstruídas ou captadas em gestos incompletos. As expansões reforçam foco seletivo, pele e materiais imperfeitos, ruído, halation localizada e áreas ilegíveis. Nenhuma cena ganhou pose final, simetria promocional ou iluminação integral.

A auto-checagem é textual e pré-geração; não se declara inspeção de imagens ou vídeos renderizados, pois nenhum asset foi gerado.

## Decisões

- Expandir por acréscimo, sem reescrever os corpos originais, para preservar rigorosamente direção criativa, câmera, ação, luz e referências aprovadas.
- Manter os Character Locks nos lugares originais: explícitos nas imagens e herdados nos vídeos. A etapa 7 exige o Style Lock final; não exige duplicar os Character Locks no vídeo.
- Usar 4s e 8s como micro-eventos adicionais para complementar, sem substituir, a marcação temporal existente.
- Manter o ponto três mesmo em cenas inteiramente práticas; não introduzir VFX desnecessários apenas para ilustrar o registro.
- Aplicar a regra de sandbox mais restritiva: não alterar arquivos do projeto. Entregar o conteúdo integral dos três arquivos na resposta final, em vez de tentar uma gravação proibida.
- Não iniciar geração, Fase 2, alterações de interface ou qualquer etapa posterior do remix.

## Pendências/bloqueios

- **Bloqueio de aplicação:** a regra explícita desta sandbox determina que os arquivos do projeto permaneçam inalterados. Portanto, os três arquivos não foram gravados em seus destinos.
- O agente principal deve aplicar os três blocos integrais entregues na resposta final e, após aplicação, reconferir as contagens e os locks nos arquivos persistidos.
- Gates editoriais das versões propostas: verdes. Gate de persistência nos destinos: bloqueado pela sandbox, não apresentado como concluído.
- Nenhuma pendência criativa ou de comprimento identificada.

## Mudanças fora do recorte

Nenhuma alteração no projeto, dentro ou fora do recorte. Somente dois arquivos temporários de texto foram usados em `/tmp` para recontagem das adições. Nenhum código, dependência, asset, Git, roadmap ou monitor foi operado.

## Arquivos tocados

Arquivos do projeto lidos:
- `.opencode/work/producao/v1/prompts-imagem.md`
- `.opencode/work/producao/v1/prompts-video.md`
- `.workspace/skills/nova-sessao-aka-cine/SKILL.md`

Arquivos do projeto efetivamente escritos: nenhum, por restrição de sandbox.

Arquivos integrais entregues para aplicação:
- `.opencode/work/producao/v1/prompts-imagem.md`
- `.opencode/work/producao/v1/prompts-video.md`
- `.opencode/work/sub/fase-1/2/report-2.md`

Textos temporários de conferência:
- `/tmp/correcao-imagem-additions.txt`
- `/tmp/correcao-video-additions.txt`