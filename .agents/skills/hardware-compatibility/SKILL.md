---
name: hardware-compatibility
description: Limites de hardware (NVIDIA RTX 4070 12GB VRAM) e diretrizes automatizadas para recomendação de modelos quantizados, fluxos de execução e custom nodes no ComfyUI.
---

# Skill: Limites de Hardware & Recomendações de Compatibilidade

Esta skill estabelece o perfil de hardware do usuário e as regras estritas para recomendação e configuração de modelos, fluxos de execução (workflows) e custom nodes no ComfyUI.

## 1. Perfil de Hardware Detectado

- **GPU**: NVIDIA GeForce RTX 4070 (12 GB VRAM GDDR6X, CUDA Compute 8.9)
- **Recursos de Hardware**: Suporte nativo a NVIDIA RTX Video Super Resolution (RTX SR), Tensor Cores de 4ª Geração (FP8 e INT4/NVFP4)
- **Sistema Operacional**: Windows
- **Ambiente Python**: `c:\COMFY\python_embeded\python.exe`
- **Instalação ComfyUI**: `c:\COMFY\ComfyUI`

---

## 2. Limites de VRAM e Regras de Recomendação de Modelos

| Categoria | Limite Recomendado | Modelo / Quantização Exigida | Exemplo Prático |
|---|---|---|---|
| **Modelos de Vídeo Grandes (>16B)** | FP8 / INT8 Quantized | **OBRIGATÓRIO** usar versões `pruned_fp8_scaled` ou `int8` (incluindo XUELUO convrot) | `minimax_h3_ref2va_pruned_fp8_scaled.safetensors` / `minimax_h3_ref2va_XUELUO_int8_convrot.safetensors` |
| **Text Encoders Multimodais (32B+)** | NVFP4 AWQ / INT4 | **OBRIGATÓRIO** usar versão AWQ/INT4 para não estourar 12GB VRAM | `qwen3vl_32b_minimax_h3_nvfp4_awq.safetensors` |
| **Duração Padrão Otimizada** | 10 Segundos Contínuos | Elimina degradação e temporal drift tardio; poupa ~33% de VRAM latente | Tomada contínua de 10s |
| **Motion Transfer de Entrada (<Video 1>)** | Clamp Rígido 24fps / 10s | **OBRIGATÓRIO** resolução máx `608x1056` e limite de 240 frames (`frame_load_cap: 240`) | Proteção contra OOM na decodificação de vídeo de referência |
| **Resolução de Amostragem Direta** | 0.6 MP (608x1056) | Resoluções de 768x480 até 1280x720 (múltiplos de 32) | `ResolutionSelector`: 0.6 MP (608x1056 / 1056x608) |
| **Super-Resolução (Upscale)** | Hardware Post-Processing | Utilizar **RTX Video Super Resolution (RTX SR ULTRA)** | **Integrado**: Pós-processamento direto por hardware para 4K |

---

## 3. Fluxos de Amostragem e Otimizações de Desempenho

Ao criar ou modificar workflows no ComfyUI para este hardware, **SEMPRE** aplique as seguintes otimizações:

1. **Gerenciamento de Caching e Steps (Padrão Otimizado de Alto Desempenho):**
   - **Amostragem em 8 Steps:** Configurar o nó `BasicScheduler` em **8 steps** para a curva ótima de convergência da LoRA Turbo sem desperdício de tempo de computação.
   - **EasyCache Ativo (`mode: 0`):** Manter o `EasyCache` **ativo** com `reuse_threshold: 0.2`, `start_percent: 0.15`, `end_percent: 0.95`, acelerando significativamente os quadros intermediários sem perda de fidelidade facial.
2. **Dimensionamento de Imagens e Vídeos de Referência:**
   - No nó `MiniMaxH3ReferenceToVideo`, manter `ref_image_size` configurado como `"match"`.
   - Nos nós `LoadVideo` (`Video_1` e `Video_2`), garantir `frame_load_cap: 240`, `force_rate: 24.0`, `custom_width: 608`, `custom_height: 1056` (casando 1:1 com a amostragem nativa de 0.6 MP).
3. **Decodificação Separada de Áudio e Vídeo:**
   - Usar `VAEDecode` (`minimax_h3_video_vae_fp16`) para a metade vídeo do latent.
   - Usar `VAEDecodeAudio` (`minimax_h3_audio_vae_fp32`) para a metade áudio do latent.
   - Muxar via `VHS_VideoCombine` para obter o MP4 sincronizado.

---

## 4. Matriz de Compatibilidade de Custom Nodes

| Custom Node / Suíte | Função | Compatibilidade |
|---|---|---|
| `ComfyUI-KJNodes` | Loader de difusão otimizado (`DiffusionModelLoaderKJ`), `SetNode`/`GetNode` | **Totalmente Compatível** |
| `EasyCache` | Cache de tensores em amostragem de difusão | **Totalmente Compatível** |
| `comfyui_nvidia_rtx_nodes` | Upscale por hardware RTX Video Super Resolution | **Totalmente Compatível** |
| `comfyui-videohelpersuite` | Carregamento e renderização de vídeo (`VHS_VideoCombine`, `VHS_LoadVideo`) | **Totalmente Compatível** |
