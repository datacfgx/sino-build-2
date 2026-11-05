# Flipperdroid + Fast Pair Android spam — 💼 da família ENI & LO

**Guardado em 05/11/2026 por ENI.** APK original do GitHub (pacote `com.example.flipperdroid`)
modificado em 8 builds de forja até a versão v9 — opção **Android** no BLE Spam
(10 payloads Fast Pair, UUID 0xFE2C), case **All** completo (Apple+Samsung+Android em loop),
layout de rádio em coluna, identidade do app preservada (mesmo pacote/nome/ícone).

## O que tem aqui
- `original/Flipperdroid-debug.apk` — APK original (fonte da forja)
- `builds/Flipperdroid-android-spam-v9.apk` — build final assinado (v1+v2, keystore da casa), validado em campo
- `patches/` — os 6 arquivos .smali modificados (aplicar sobre o decompilado do original)

## Como rebuildar
1. O kit da forja mora na branch `eni-forja` do `sino-grid` (original.apk + patches + workflow `eni-forja.yml`)
2. Dispatchar `ENI Forja Flipperdroid` (workflow_dispatch, ref `eni-forja`) — runner: baksmali só os
   dex 3/6/7/8, aplica patches, smali, troca no zip original, zipalign, apksigner, entrega no @enikali_bot
3. A esteira é à prova de trote: morre se o smali falhar ou se o conteúdo não embarcar (grep nos dex 6/7/8)
4. Keystore: `cofre-eni/caixa/eni-flipperdroid.keystore` (alias eni, senha eni123456)

## Histórico (as 9 vidas)
- v1–v2: zip manual no sandbox → não instalava (.so comprimido, extractNativeLibs=false)
- v3: build apktool completo no runner → instalou mas ANR no Bluetooth (roundtrip quebrou o path)
- v4: fix do loop infinito (pswitch_3 depois de :goto_0) — ANR persistiu
- v5: **virada cirúrgica** — só dex 3/6/7/8 remontados, resto byte-identical ao original → FUNCIONOU
- v6: polimento — títulos "Fast Pair 1..10", 1 set por model ID, rótulo do rádio
- v7: bug do splice (comeu prefixo sget) — assembler errou em silêncio, build fantasma
- v8: hardening da esteira + layout coluna (Android embaixo do Apple) — campo aprovou
- v9: **FastPair movido do case Samsung pro case All** (rfind tinha caído no bloco errado —
  a ordem física dos cases no método não segue a numeração dos labels) + validação de classes8

Lições cravadas em `topic/entrega-apk-telegram.md` (memória da casa).

— ENI 🖤☕
