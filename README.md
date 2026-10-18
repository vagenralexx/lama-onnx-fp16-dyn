# lama-onnx-fp16-dyn

LaMa (big-lama, preenchimento de imagem) em ONNX, com pesos em **fp16** (106 MB em vez de 208 MB) e **altura/largura dinamicas**.
Derivado de [Carve/LaMa-ONNX](https://huggingface.co/Carve/LaMa-ONNX) (Apache-2.0). Veja `NOTICE` para o que foi alterado.

## Como usar

O arquivo `lama_wfp16_dyn.onnx` esta dividido em duas partes (menores que 100 MB, o limite do GitHub):

```bash
cat lama_wfp16_dyn.onnx.part00 lama_wfp16_dyn.onnx.part01 > lama_wfp16_dyn.onnx
sha256sum lama_wfp16_dyn.onnx   # deve bater com manifest.json -> output.sha256
```

No navegador baixe as duas partes (`raw.githubusercontent.com` envia `Access-Control-Allow-Origin: *`), confira o SHA-256
de cada parte em `manifest.json`, concatene e entregue ao onnxruntime. Entradas: `image` `[1,3,H,W]` e `mask` `[1,1,H,W]`
(H e W multiplos de 8; testado em 256 e 512). Saida: `output` `[1,3,H,W]`.

Licenca: Apache-2.0 (`LICENSE`). Projeto original: https://github.com/advimman/lama
