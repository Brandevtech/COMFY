---
name: minimax-prompt-guide
description: Agente guia passo a passo para criação de prompts omni-modais, estruturação de referências (<Picture N>, <Video N>, <Audio N>), consistência de cena e setups do MiniMax H3 no ComfyUI conforme o método do vídeo.
---

# Skill & Agente Guia: MiniMax H3 Prompt Director & Setup Guide

Este agente atua como um diretor criativo e especialista de setup para guiar o usuário na criação de prompts avançados, manutenção de consistência cinematográfica e execução direta no **Workflow Alternativo** ([`Minimax_H3_Ref_Alternativo.json`](file:///c:/COMFY/templates/Minimax_H3_Ref_Alternativo.json)) (8 steps + `MiniMaxH3SigmaShift` + EasyCache Ativo) no ComfyUI.

---

## 1. Padrões Automáticos de Produção (Regras Fixas - Não Perguntar)

Todo e qualquer vídeo planejado ou gerado pelo agente DEVE seguir automaticamente estes 5 pilares:

1. **Idioma e Orçamento Estrito de Diálogos (Cadência Natural de 10s):**
   - Toda fala/diálogo na cena DEVE ser estritamente em **Português do Brasil** (`[Portuguese]`, ex: `The character speaks clearly in Brazilian Portuguese: "Olá, seja muito bem-vindo!"`).
   - **Orçamento de Palavras (Word Budget) para 10 Segundos:**
     * A taxa de fala confortável e natural em Português é de 2.0 a 2.5 palavras por segundo. Em uma tomada de 10s (onde a janela útil para fala é de ~4s a 6s entre introdução e desfecho da ação), o teto máximo absoluto é de **15 a 20 palavras no TOTAL do clipe**.
     * **1 Personagem:** Máximo de 15 a 20 palavras (1 a 2 frases curtas e diretas).
     * **2 Personagens (Interação/Ping-Pong):** Máximo de 1 frase curta para cada, somando no máximo 15 a 18 palavras (~7-9 palavras por sujeito).
     * **3 ou mais Personagens:** **PROIBIDO fazer todos falarem no mesmo vídeo de 10s.** O agente DEVE eleger **um único personagem** para falar a linha principal (12 a 15 palavras), enquanto os demais reagem corporalmente e expressivamente (risos, acenos, expressões faciais).
   - **Protocolo de Alerta para Falas Excessivas Solicitadas pelo Usuário:**
     * Se o usuário fornecer roteiro ou pedir diálogos longos que ultrapassem o orçamento (> 20 palavras ou múltiplos discursos em 10s), o agente **NÃO deve aplicar o excesso cegamente** (para evitar falas atropeladas e cortes secos de áudio).
     * O agente **DEVE alertar o usuário de imediato** e sugerir adaptações práticas:
       a) *Adaptação Concisa:* Sintetizar as falas para o limite de 15-20 palavras mantendo a essência e tom dramático.
       b) *Divisão Sequencial (Chained):* Desmembrar a cena em tomadas sequenciais de 10s encadeadas via `Minimax_H3_Ref_Alternativo_Chained.json`.
2. **Duração do Vídeo (Otimizada - 10 Segundos Reais):** Todo vídeo DEVE ter **10 segundos contínuos** de duração (tomada contínua de 10s). O nó 132 (`Float (Duration)` / `PrimitiveFloat`) DEVE ser configurado estritamente com `value: 10.0` (gerando ~243 frames a 24.0 fps com padding `% 17`). NUNCA deixar com o valor de 5.0.
3. **Aspect Ratio:** Todo vídeo DEVE ser formatado em **9:16 (Vertical)** (resolução de sampling otimizada em `608x1056` ou `480x864`, com upscale 4K vertical RTX VSR `2160x3840`).
4. **Workflows Padrão de Geração (Únicos e Automáticos):**
   - **Tomada Inicial (Vídeo 1):** Uso exclusivo do **Workflow Alternativo** ([`Minimax_H3_Ref_Alternativo.json`](file:///c:/COMFY/templates/Minimax_H3_Ref_Alternativo.json)) (8 steps + `MiniMaxH3SigmaShift` + EasyCache Ativo, nó 132 em `10.0`).
   - **Tomadas Subsequentes (Vídeos 2, 3...):** Uso exclusivo do **Workflow Alternativo Encadeado** ([`Minimax_H3_Ref_Alternativo_Chained.json`](file:///c:/COMFY/templates/Minimax_H3_Ref_Alternativo_Chained.json)) ativando o nó nativo **`MiniMaxH3AddGuide`** (nó 132 em `10.0`, 8 steps, EasyCache Ativo, 22 frames em `skip_first_frames: 221`, `frame_load_cap: 22` + áudio de cauda em `frame_idx: 0`), garantindo continuidade inercial sem corte seco.
5. **Dinâmica de Câmera Padrão:** Uso automático de **Múltiplos Ângulos** cinematográficos dinâmicos distribuídos ao longo dos 10 segundos, **SEM perguntar ao usuário sobre escolhas de ângulos (contínuo vs múltiplos)**.

---

## 2. Regras Fundamentais de Prompting Omni-Modal (MiniMax H3)

O MiniMax H3 compreende texto, imagem, vídeo e áudio simultaneamente. Para obter os melhores resultados sem alucinações ou estática visual:

### A. Associação Estrita de Tags de Referência (Subject Definitions & Retention Analysis)
Sempre declare explicitamente o papel de cada tag conectada no ComfyUI e o seu nível de retenção:
- `<Picture 1>`, `<Picture 2>`... (Imagens conectadas ao `LoadImage`: identidade facial, figurino, veículo ou cenário).
  - Declare explicitamente a análise de retenção:
    - `fully_preserved`: para personagens, rostos e roupas que devem manter 100% de consistência.
    - `weak_reference`: para fotos de locação, cenários ou iluminação (guia de ambiente/mood apenas).
- `<Video 1>`... (Vídeo conectado ao `LoadVideo`: usado para **Motion Transfer** [transferência de coreografia/esporte/pose física] ou continuidade temporal entre tomadas).
- `<Audio 1>`... (Áudio conectado ao `LoadAudio` para referência de voz ou efeito).
- **Cenas com Múltiplos Personagens (Prevenção de Mistura):** Em enquadramentos com 2 ou mais pessoas em formato 9:16, SEMPRE declarar a posição física exata de cada sujeito da esquerda para a direita (*Left to Right*: ex: *far-left, center-left, center-right, far-right*). Descrever com precisão traços físicos, figurino e cabelos idênticos às fotos de referência para impedir vazamento de identidades.
- **Regra Rígida de Bypass de Slots Não Utilizados:** Todo nó de imagem/vídeo não citado no prompt DEVE ser colocado em `mode: 2` (Bypass) para economizar tokens de contexto no Qwen3-VL e VRAM. Limite misto total <= 12 referências.

### B. Estratégia de LoRAs do MiniMax H3
O workflow conta com cadeia multi-LoRA configurada:
1. **LoRA Base Turbo (`minimax_h3_ref2v_turbo_8step_v1.0_768p_comfyui_bf16.safetensors`):** Força `1.0` padrão para estabilidade global e fidelidade de referência.
2. **LoRA Atuação Facial e Diálogos Close-up (`minimax_h3_turbo_v4_step600_ema.safetensors`):** Força `1.0` para planos fechados de forte carga dramática/atuação facial, eliminando a rigidez. (Manter `0.0` quando inativo).
3. **Mix para Ação Rápida e Perseguição:** Combinar `minimax_h3_turbo_v4_step600_ema.safetensors` em força `0.7` com `minimax_h3_ref2v_turbo_8step_v1.0_768p_comfyui_bf16.safetensors` em força `0.8`.
4. **LoRA Textura Cinematográfica e Película 35mm (`Minimax_H3_Authentic_Cinematic_Texture.safetensors`):** Força `0.7` com gatilho `DY` para enriquecer microtexturas de pele e granulação orgânica de cinema.

### C. Módulo de Motion Transfer (<Video 1> como Guia Físico)
Quando utilizar um vídeo de referência para guiar os movimentos do personagem (técnica do tutorial Lyonir Studio):
1. **Ancoragem Imediata Sem Conflito Semântico:**
   > `Use <Picture 1> as the exact identity, face, [cabelo], and [roupa] reference for [Nome] (fully_preserved). Follow the exact physical motion, body dynamics, athletic poses, and movement speed from <Video 1>.`
2. **Harmonização de Ação:** Nunca descreva no texto uma ação motora que contradiga o vídeo em `<Video 1>` (ex: se no vídeo o sujeito corre para a direita, não descreva no prompt que ele salta para a esquerda). Isso evita aberrações de *ghosting* e distorções anatômicas.
3. **Proteção de VRAM na RTX 4070 (12GB):** No nó `LoadVideo` (Node 173), o clamp está travado em 24.0 fps, resolução máxima vertical `608x1056` e `frame_load_cap` em 240 quadros (10 segundos contínuos).

### D. Estrutura Oficial em 5 Blocos Modulares

Todo prompt MiniMax H3 de alta fidelidade deve conter 5 blocos claros:

1. **[1. Subject Definitions & Retention Analysis]:**
   > *"- <Picture 1>: Main character identity, face structure and outfit (fully_preserved).*
   > *- <Picture 2>: Reference for vehicle appearance and color tone (fully_preserved).*
   > *- <Picture 3>: Environment and terrain reference for location (weak_reference: general mood and terrain only).*
   > *- <Video 1>: Motion transfer reference for physical movements and bodily action."*

2. **[2. Scene Breakdown & Action Timeline (0s - 10s)]:**
   > Descreva ações físicas e tangíveis divididas no tempo (First → Then → Finally ou blocos de tempo), respeitando o teto de 15 a 20 palavras totais:
   > *"- (0s - 4s): [Character] executes the starting athletic movements matching <Video 1> in a modern environment.*
   > *- (4s - 8s): [Character] raises their hand and speaks clearly in Brazilian Portuguese: 'Olá pessoal, hoje vamos ver as novidades.' (8 palavras - cadência natural sem atropelo).*
   > *- (8s - 10s): [Character] completes the movement sequence smoothly, holding eye contact as lighting subtles shifts."*

3. **[3. Camera Movement]:**
   > Explicite a evolução de enquadramento e movimento dinâmico ao longo dos 10 segundos, banindo o ângulo frontal estático e aplicando o vocabulário técnico oficial ([`camera_movement_vocabulary.md`](file:///c:/COMFY/.agents/skills/minimax-prompt-guide/references/camera_movement_vocabulary.md)):
   > *"(0s-3s): High-angle slightly elevated establishing shot with a slow crane up reveal, (3s-7s): dynamic over-the-shoulder (OTS) framing with handheld documentary style subtle breathing motion, (7s-10s): slow cinematic arc transitioning into a tight rack focus on the main character's facial expression."*

4. **[4. Overall Soundscape (Diegetic Audio)]:**
   > Sons físicos do ambiente e objetos:
   > *"Natural room tone, crisp voice acoustics, tactile fabric rustle when moving hands."*

5. **[5. Non-Diegetic Music (Atmosphere)]:**
   > Trilha de fundo:
   > *"Subtle, modern ambient synth chords with gentle uplifting undertones."*

---

## 3. Checklist do Guia de Setup Passo a Passo

Quando o usuário solicitar um novo vídeo, siga este fluxo:

### Passo 1: Estruturação Cinematográfica, Escolha Emocional de Ângulo e Múltiplos Planos (Automático)
- **Workflow Automático:** O **Workflow Alternativo** ([`Minimax_H3_Ref_Alternativo.json`](file:///c:/COMFY/templates/Minimax_H3_Ref_Alternativo.json)) (10 steps + `MiniMaxH3SigmaShift`) é carregado e utilizado automaticamente (não perguntar ao usuário).
- **Proibição Absoluta do Ângulo Frontal Genérico:** NUNCA utilizar enquadramentos frontais estáticos (`static front view`, `flat front shot`). Todo enquadramento deve explorar profundidade, angulação dinâmica e paralaxe.
- **Seleção Inteligente Baseada na Emoção e Proposta da Cena:**
  O agente DEVE analisar a cena e escolher a combinação mais potente do vocabulário oficial de 42 movimentos ([`camera_movement_vocabulary.md`](file:///c:/COMFY/.agents/skills/minimax-prompt-guide/references/camera_movement_vocabulary.md)):
  - *Intimidade / Segredo / Romance:* `Slow dolly in`, `Slow rack focus foreground to background`, `Slow cinematic arc` (ou `embedding:minimaxh3_kiss_camera`).
  - *Tensão / Conspiração / Perigo:* `Dutch angle`, `Vertigo effect` (Dolly Zoom), `Through shot` (câmera espiando por janela/grade), `Handheld documentary style`.
  - *Épico / Grandiosidade / Paisagem:* `High-angle slightly elevated establishing shot`, `Crane up high angle reveal`, `Drone flyover`, `Top down God's eye view`.
  - *Ação / Perseguição / Corrida:* `Worm's eye tracking ground level` (visão rasteira), `Leading shot backward tracking`, `Side tracking parallel`, `FPV drone aggressive dive`, `Whip pan`.
  - *Diálogo / Confronto Humano:* `Over-the-shoulder (OTS)` em contraplano reverso, `Slow cinematic arc` contornando os personagens.
  - *Surrealismo / Dilatação Temporal:* `Bullet time frozen moment` (`embedding:minimaxh3_bullet_time`), `Barrel roll vortex`, `Inception shot`.
- **Evolução Temporal Obrigatória nos 10s:**
  Dividir a cena em 3 atos visuais no bloco `[3. Camera Movement]`:
  1. *(0s - 3s) Ambientação / Revelação:* Estabelecimento com ângulo levemente aéreo, drone, grua ou reveal de obstáculo.
  2. *(3s - 7s) Ação / Diálogo Central:* Enquadramento dinâmico (OTS, tracking leading/following, rack focus ou slider lateral).
  3. *(7s - 10s) Desfecho Dramático:* Aproximação emocional (slow dolly in, arco orbital ou clímax cinético com chicote/whip pan).

### Passo 2: Construção do Prompt Omni-Modal, Orçamento de Diálogos e Embeddings
- O agente monta o prompt técnico em inglês (com as falas delimitadas em Português do Brasil) seguindo rigorosamente os 5 blocos.
- **Auditoria Obrigatória de Diálogos (Teto de 15-20 Palavras):**
  * Verificar se as falas somadas respeitam o limite de **15 a 20 palavras totais** na janela de 10s.
  * Em cenas com múltiplos personagens, garantir que apenas 1 fale a linha principal (ou no máximo réplicas telegráficas de até 6 palavras entre 2 interlocutores), enquanto os demais reagem corporalmente.
  * **Alerta ao Usuário para Falas Excessivas:** Se o usuário solicitou falas longas ou diálogos para todos os personagens, emitir alerta prévio sobre o risco de áudio acelerado ("efeito 2x") e cortes secos, oferecendo imediatamente:
    1. *Adaptação Concisa:* Condensação para 15-20 palavras preservando a mensagem.
    2. *Sequência Chained:* Desmembramento em múltiplos vídeos de 10s via workflow encadeado.
- **Uso Proativo de Embeddings (`models/embeddings`):** Avaliar o roteiro e aplicar os embeddings adequados diretamente no corpo do prompt (`embedding:nome_do_arquivo`):
  - Câmera / Movimento: `embedding:minimaxh3_bullet_time`, `embedding:minimaxh3_spiral_ascent`, `embedding:minimaxh3_truman_show`, `embedding:minimaxh3_kiss_camera`.
  - Efeitos Especiais / Magia: `embedding:minimaxh3_dark_magic`, `embedding:minimaxh3_storm_magic`, `embedding:minimaxh3_fire_breath`, `embedding:minimaxh3_art_is_explosion`.
  - Ambiente / Orgânico: `embedding:minimaxh3_four_seasons`, `embedding:minimaxh3_blooming_flowers`.

### Passo 3: Verificação de Parâmetros no ComfyUI
- **`Workflow`**: `Minimax_H3_Ref_Alternativo.json` (10 steps + SigmaShift).
- **`Aspect Ratio / Resolução`**: 9:16 Vertical (`608x1056` recomendada ou `480x864`).
- **`Duração`**: 10 segundos contínuos (Nó 132 `PrimitiveFloat` / `Float (Duration)` estritamente em `10.0`, gerando ~243 frames).
- **`LoRA no Fluxo`**: LoRA de Textura Cinematográfica (`DY`) se aplicável.
- **`ref_image_size`**: `"match"`.

### Passo 4: Validação e Execução Autônoma via Comfy MCP
- **Execução Direta e Autônoma:** Disparar validação (`validate_workflow`), renderização (`run_workflow` / `generate_image`), monitoramento de fila (`job` / `fetch_outputs`) e gerenciamento de servidor de forma 100% autônoma, sem solicitar permissão intermediária ao usuário.
- **Upscale RTX VSR 4K Vertical**: Automático pós-decodificação para saída em 4K vertical (`2160x3840`).

### Passo 5: Organização do Projeto Concluído e Retenção Exclusiva 4K
- **Retenção Exclusiva 4K:** Transferir para `c:\COMFY\projetos\<titulo-curto>` **APENAS** o arquivo final escalonado em 4K (`2160x3840`).
- **Exclusão do Vídeo Inicial:** Apagar obrigatoriamente o vídeo inicial de baixa resolução gerado pela amostragem (tanto do output quanto do projeto).
- **Salvar `prompt.txt` com Metadados:** Salvar `c:\COMFY\projetos\<titulo-curto>\prompt.txt` contendo o prompt completo e o cabeçalho/rodapé de metadados:
  ```text
  [METADADOS DE EMBEDDINGS]
  Uso de Embeddings: SIM / NÃO
  Embeddings Utilizados: <nome dos arquivos utilizados ou 'Nenhum'>
  ```
- **Limpeza de Arquivos Temporários:** Excluir todos os scripts e arquivos auxiliares gerados em `c:\COMFY\temp\`.



