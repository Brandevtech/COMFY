# Vocabulário Cinematográfico de Movimentação e Ângulos de Câmera (42 Movimentos)

Este guia serve como referência técnica obrigatória para o agente ao estruturar os blocos de câmera (`[3. Camera Movement]`) em prompts do MiniMax H3.

---

## Princípio Fundamental: Fim do Ângulo Frontal Genérico
- **Proibição:** É estritamente vedado o uso de ângulos frontais estáticos genéricos (`static frontal shot`, `front view camera`, `eye-level front shot`). Câmeras estáticas frontais empobrecem a estética, deixam a geração com aparência de "estátua de cera / IA amadora" e subutilizam o motor de atenção espacial do MiniMax H3.
- **Diretriz de Seleção Dramática:** Toda escolha de ângulo e movimento DEVE ser intencional, servindo à emoção, ao gênero narrativo e à proposta dramática da cena.

---

## As 15 Categorias e 42 Movimentos Oficiais

### 1. Dolly Moves (Translação no Eixo Z - Profundidade e Conexão)
- **`slow dolly in`**: Aproximação física sutil e contínua em direção ao sujeito.  
  *Emoção:* Conexão íntima, revelação de segredo, foco em pensamento ou suspense crescente.
- **`slow dolly out`**: Recuo físico suave da câmera, afastando-se do sujeito.  
  *Emoção:* Sentimento de solidão, abandono, isolamento ou choque diante da magnitude do ambiente.
- **`fast dolly in`**: Avanço físico veloz da câmera em direção ao ponto de interesse.  
  *Emoção:* Surpresa imediata, urgência, choque súbito ou momento de epifania.
- **`vertigo effect` (Dolly Zoom / Zolly)**: Avanço físico da câmera enquanto as lentes realizam zoom out (ou vice-versa). O sujeito mantém as dimensões relativas enquanto o fundo deforma e se distorce elasticamente.  
  *Emoção:* Vertigem, desespero psicológico, pânico, crise existencial ou perda súbita de controle.

### 2. Infinite Scale Continuity (Escala Infinita - Transições Macroscópicas)
- **`extreme macro zoom`**: Mergulho contínuo da visão geral para detalhes microscópicos da pele, pupila, gota de suor ou fibra de tecido.  
  *Emoção:* Hiper-realismo, tensão fisiológica, sensibilidade tátil e revelação orgânica.
- **`cosmic hyper zoom`**: Recuo colossal acelerado saindo do nível dos olhos até a estratosfera ou órbita planetária.  
  *Emoção:* Grandiosidade cósmica, insignificância humana, transcendência e ficção científica.

### 3. Character-Mounted & Framing (Câmera Atrelada ao Personagem)
- **`over the shoulder` (OTS)**: Enquadramento capturando o sujeito pelo ombro/costas de um interlocutor.  
  *Emoção:* Tridimensionalidade humana, engajamento em conversação, cumplicidade ou confronto interpessoal.
- **`fisheye or peephole lens`**: Distorção esférica ultra-ampla com bordas curvadas, simulando olho mágico ou câmera corporal *Snorricam*.  
  *Emoção:* Paranoia, claustrofobia, vigilância clandestina ou distorção mental induzida.

### 4. Obstacle & Environmental Interaction (Interação com o Cenário)
- **`reveal from behind wide movement`**: A tomada inicia com a visão obstruída por uma pilastra, tronco ou parede e se desloca lateralmente revelando a cena.  
  *Emoção:* Mistério, descoberta voyeurística, senso de espionagem ou introdução impactante de cenário.
- **`through shot`**: A câmera transpassa uma barreira física real (janela entreaberta, vegetação densa, cortina ou arco arquitetônico).  
  *Emoção:* Acesso proibido, imersão profunda e transição entre mundos interno/externo.
- **`fly through aperture`**: Mergulho suave e milimétrico da câmera através de frestas diminutas (fechadura, grades ou fendas).  
  *Emoção:* Curiosidade investigativa, tensão de invasão furtiva e perspectiva microscópica.

### 5. Focus & Lens Manipulation (Foco Seletivo e Óptica)
- **`reveal from blur fade in`**: O plano inicia em desfoque completo com círculos de *bokeh* volumétricos e ganha nitidez gradativa.  
  *Emoção:* Despertar de sono/coma, recuperação de consciência, atmosfera onírica e poética.
- **`rack focus foreground to background`**: O plano focal transita suavemente de um elemento nítido em primeiro plano para um elemento secundário ao fundo (ou o inverso).  
  *Emoção:* Revelação de ameaça oculta, desvio narrativo de atenção e diálogo visual sem cortes.

### 6. Tripod Moves (Movimentos Angulares em Eixo Fixo)
- **`tilt up`**: A base permanece fixa enquanto o cabeçote da câmera se inclina para cima (do chão para o céu).  
  *Emoção:* Sensação de poder, imponência de arquiteturas/monstros, esperança ou reverência.
- **`tilt down`**: A base permanece fixa enquanto a lente desce (do céu para o chão/pés).  
  *Emoção:* Derrota, vulnerabilidade, tristeza, vergonha ou foco em pistas no solo.

### 7. Slider Moves (Deslocamento Lateral - Eixo X)
- **`camera truck left`**: Movimento físico paralelo em trilho para o lado esquerdo, gerando ricas camadas de paralaxe entre primeiro plano e fundo.  
  *Emoção:* Exploração ambiental rítmica, revelação de múltiplos elementos em fila e dinamismo visual.
- **`lateral truck right`**: Movimento físico lateral para o lado direito.  
  *Emoção:* Continuidade narrativa, acompanhamento de caminhada e contemplação estética.

### 8. Orbital Movements (Movimentos Circulares ao Redor do Eixo)
- **`orbit 180`**: Giro em semicírculo contínuo contornando o personagem de um perfil ao outro.  
  *Emoção:* Tomada de decisão, contemplação panorâmica e tridimensionalidade de figurino/rosto.
- **`fast 360 orbit`**: Rotação completa e veloz em 360 graus ao redor do centro da cena.  
  *Emoção:* Clímax heroico, transformação mágica, confusão mental ou cerco por inimigos.
- **`slow cinematic arc`**: Deslocamento suave em curva/arco amplo com iluminação volumétrica e mudança gradual de luz e sombra na face do sujeito.  
  *Emoção:* Elegância cinematográfica, drama romântico sofisticado e alta estética visual.

### 9. Vertical Movements (Crane & Pedestal - Eixo Y)
- **`pedestal down`**: A câmera inteira desce em linha reta vertical (mantendo a linha de horizonte nivelada).  
  *Emoção:* Aproximação ao nível humano, aterrisagem emocional e quebra de solenidade.
- **`pedestal up`**: A câmera sobe inteira em linha reta vertical sem reclinar o ângulo.  
  *Emoção:* Elevação social, triunfo sereno e amplitude de visão.
- **`crane up high angle reveal`**: Movimento de grua mecânica subindo enquanto aponta suavemente para baixo (*high-angle*).  
  *Emoção:* Conclusão épica, visão estratégica do campo de batalha e revelação da imensidão do ambiente.
- **`crane down landing`**: Descida majestosa de grua partindo do teto/copa das árvores e pousando no nível dos olhos dos atores.  
  *Emoção:* Boas-vindas à narrativa, transição fluida do ambiente macro para o drama interpessoal.

### 10. Optical Lens Effects (Variação de Distância Focal)
- **`smooth optical zoom in`**: Aproximação ótica pura sem deslocar a base da câmera (comprime o plano de fundo contra o sujeito).  
  *Emoção:* Sensação de sufocamento, vigilância à distância e foco clínico na expressão.
- **`smooth optical zoom out`**: Afastamento ótico abrindo a lente grande-angular.  
  *Emoção:* Contextualização súbita, perda de intimidade e revelação de múltiplos atores no quadro.
- **`snap zoom` (Crash Zoom)**: Zoom violento e instantâneo em alta velocidade em um detalhe específico.  
  *Emoção:* Estética de filmes de ação, comédia satírica, choque tarantinesco ou susto (*jump cut* visual).

### 11. Drone & Aerial Views (Tomadas Aéreas e Cinematografia de Voo)
- **`drone flyover`**: Voo linear fluido em média altitude sobrevoando o relevo, tráfego ou multidão.  
  *Emoção:* Estabelecer escala geográfica, abertura de ato ou jornada épica.
- **`epic drone reveal`**: Drone parte rente ao chão ou atrás de um penhasco e emerge no ar revelando o sol poente ou um castelo/cidade imensa.  
  *Emoção:* Deslumbramento, vitória e libertação.
- **`large scale drone orbit`**: Voo circular de longo raio contornando montanhas, fortalezas ou veículos em alta velocidade.  
  *Emoção:* Grandiosidade orquestrada e poder institucional.
- **`top down God's eye view`**: Visão zenital perpendicular a 90 graus apontando diretamente para o chão.  
  *Emoção:* Destino pré-determinado, padrão geométrico do mundo, labirinto e despersonalização.
- **`FPV drone aggressive drone dive`**: Mergulho acrobático de alta velocidade com curvas acentuadas e rasantes violentos.  
  *Emoção:* Adrenalina extrema, esportes radicais e ação frenética.

### 12. Stylized & Dynamic Movements (Câmera Orgânica e Efeitos Visuais)
- **`handheld documentary style`**: Operação de câmera na mão com respiração humana, micro-tremores e imperfeição realista.  
  *Emoção:* Realismo documental, intimismo cru, autenticidade e tensão jornalística/de guerra.
- **`whip pan`**: Giro horizontal tão rápido que o quadro se dissolve em *motion blur* dinâmico, servindo de transição cinética entre dois sujeitos ou ações.  
  *Emoção:* Ritmo frenético, corte invisível de alta energia e humor dinâmico.
- **`Dutch angle`**: Horizonte intencionalmente inclinado em ângulo oblíquo.  
  *Emoção:* Loucura, conspiração criminosa, desconforto, estado de embriaguez ou pesadelo.

### 13. Subject Tracking (Acompanhamento e Perseguição)
- **`leading shot backward tracking`**: A câmera recua de costas mantendo o enquadramento do sujeito enquanto ele caminha resoluto em sua direção.  
  *Emoção:* Liderança, determinação heróica e tensão do que está prestes a acontecer.
- **`following shot forward tracking`**: A câmera segue imediatamente atrás do personagem em movimento contínuo.  
  *Emoção:* Condução da audiência através de territórios desconhecidos e identificação direta com o protagonista.
- **`side tracking parallel`**: Câmera emparelhada lateralmente acompanhando a passada de corrida ou veículos em velocidade sincronizada.  
  *Emoção:* Ritmo atlético, corrida contra o tempo e perseverança física.
- **`POV walk first person walk`**: Câmera em primeira pessoa com o balanço realista dos passos e visão direta dos olhos do sujeito.  
  *Emoção:* Imersão absoluta em jogos/simulações e identificação psicológica total.

### 14. Time & Speed Manipulation (Manipulação Temporal Cinematográfica)
- **`hyperlapse moving`**: Deslocamento espacial contínuo em longa distância com compressão temporal acelerada.  
  *Emoção:* Ritmo urbano caótico, passagem de horas em segundos e vertigem do progresso.
- **`timelapse`**: Ângulo fixo mostrando a movimentação rápida de luzes, sol, estrelas ou crescimento de plantas.  
  *Emoção:* Ciclos da natureza, brevidade da vida e beleza cósmica.
- **`bullet time frozen moment`**: Congelamento da ação física enquanto a câmera se desloca tridimensionalmente pelo espaço (combinar com `embedding:minimaxh3_bullet_time`).  
  *Emoção:* Suspensão do tempo, reflexão no auge do impacto e estética de ficção de alto nível.

### 15. Extreme Orientation & Perspective (Perspectivas Não Convencionais)
- **`barrel roll vortex`**: Rotação contínua em 360 graus sobre o próprio eixo óptico (rolagem de barril).  
  *Emoção:* Desorientação espacial absoluta, perda de gravidade e combate aeroespacial.
- **`inception shot`**: Câmera que inverte a linha de gravidade ou curva o horizonte sobre si mesmo.  
  *Emoção:* Realidade distorcida, universos paralelos e surrealismo de sonho.
- **`worm's eye tracking ground level`**: Câmera rasteira colada ao chão, acompanhando passos na poeira, folhas secas ou rodas de veículos em alta velocidade.  
  *Emoção:* Tensão de emboscada, vulnerabilidade, perseguição implacável e grandiosidade do que está acima.

---

## Tabela de Decisão: Emoção da Cena vs. Combinação de Ângulo e Movimento

| Emoção Predominante da Cena | Ângulo de Início (0s - 3s) | Movimento Central (3s - 7s) | Desfecho Dinâmico (7s - 10s) |
|---|---|---|---|
| **Intimidade & Revelação** | `Reveal from blur fade in` | `Over the shoulder (OTS)` com `slow rack focus` | `Slow dolly in` em direção ao olhar do sujeito |
| **Tensão, Perigo & Suspense** | `Dutch angle` em plano médio | `Through shot` por fresta / janela com `handheld documentary style` | `Fast dolly in` ou `Vertigo effect` |
| **Épico, Abertura & Conquista** | `High-angle establishing shot` com `crane up high angle reveal` | `Drone flyover` ou `large scale drone orbit` | `Crane down landing` para plano médio |
| **Ação, Perseguição & Urgência** | `Worm's eye tracking ground level` | `Leading shot backward tracking` ou `side tracking parallel` | `Whip pan` para impacto ou `FPV drone aggressive dive` |
| **Diálogo Dramático (2 Pessoas)** | `Over the shoulder (OTS)` pelo ombro de A focando B | Corte dinâmico para OTS reverso de B focando A | `Slow cinematic arc` contornando os dois sujeitos |
| **Desorientação ou Sobrenatural** | `Barrel roll vortex` ou `Inception shot` | `Bullet time frozen moment` (`embedding:minimaxh3_bullet_time`) | `Cosmic hyper zoom` ou `extreme macro zoom` |
