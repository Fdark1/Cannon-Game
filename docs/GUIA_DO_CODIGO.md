# Entendendo o Cannon Game

## O que acontece quando você toca?

1. `CannonView.onTouchEvent()` recebe as coordenadas do dedo.
2. A posição fica em `pendingTouch`, uma AtomicReference. Isso permite entregar um toque à thread do jogo sem a UI mexer diretamente nos alvos.
3. `CannonThread.run()` chama `updateGame()` a cada frame.
4. `GameEngine.aimAndFire()` orienta o canhão e tenta criar uma bola.
5. `Cannon.align()` usa `Math.atan2()` para descobrir o ângulo entre o canhão e o dedo.
6. `Cannon.fireCannonball()` só dispara se não houver outra bola. Cosseno calcula a parte horizontal da velocidade; seno, a vertical.
7. `SoundManager` toca o áudio do disparo se o carregamento já terminou.

## Por que usar outra thread?

A thread principal trata botões, toque e diálogos. Um laço infinito nela impediria a interface de responder. `CannonThread` mantém o ciclo: medir tempo, atualizar posições, desenhar e aguardar. `running` é `volatile` para que o pedido de parada feito pela UI seja observado pela thread.

## Como a animação acontece?

A tela não contém objetos que se movem sozinhos. O programa apaga o fundo e desenha tudo novamente em outra posição. Essa repetição forma a animação quadro a quadro.

`posição nova = posição anterior + velocidade × tempo`

A velocidade está em pixels por segundo; `dt` está em segundos. O tempo é medido com `System.nanoTime()`. A espera busca aproximadamente 60 frames por segundo, mas não garante exatamente esse valor. Frames excessivamente longos são limitados a 50 ms para evitar saltos violentos; por isso o relógio simulado pode desacelerar em um aparelho muito sobrecarregado.

## Canvas, Paint, SurfaceView e SurfaceHolder

- **SurfaceView:** a área de desenho do jogo.
- **SurfaceHolder:** controla o acesso à superfície de desenho.
- **Canvas:** oferece operações como desenhar círculo, retângulo, linha e texto.
- **Paint:** informa cor, espessura e tamanho do texto.

`lockCanvas()` obtém uma tela para desenhar. `unlockCanvasAndPost()` publica o frame. O bloco `finally` garante a devolução do Canvas mesmo que o desenho seja interrompido por uma exceção.

## Herança

`Target` e `Blocker` herdam de `GameElement`: reutilizam posição, tamanho e movimento. O alvo acrescenta o bônus; o bloqueador, a penalidade. `Cannonball` usa geometria circular própria em vez de herdar um retângulo: é uma adaptação intencional para uma colisão mais precisa.

## Colisão

`Cannonball.collidesWith()` acha o ponto do retângulo mais próximo do centro da bola. Se a distância até esse ponto for menor ou igual ao raio, há contato. A comparação usa distâncias ao quadrado e dispensa a raiz quadrada.

O `GameEngine` divide cada atualização em passos de até aproximadamente 1/480 de segundo para verificar contatos durante o deslocamento. Ao tocar o bloqueador, a bola é colocada à esquerda dele, passa a viajar para a esquerda e recebe a marca `reflected`. Isso evita descontar tempo repetidamente enquanto ainda está encostada.

## Sons

Os três WAV estão em `app/src/main/res/raw`. Android gera os identificadores `R.raw.cannon_fire`, `R.raw.target_hit` e `R.raw.blocker_hit`. SoundPool carrega os efeitos de maneira assíncrona; o listener registra quais estão prontos. Ao destruir a interface, `release()` libera o recurso.

## Pausa e reinício

`onPause()` para o loop, espera a thread encerrar e limpa toques pendentes. O tempo não continua correndo no fundo. `onResume()` retoma a mesma partida se a janela e o processo ainda existirem. Reiniciar cria um novo `GameEngine`, sem precisar reabrir o aplicativo. A tela de resultados é aberta na UI por um Handler.

## Extras

`streak` conta acertos consecutivos. `score` soma 100 vezes o multiplicador, limitado a 5. O maior resultado fica em SharedPreferences e continua salvo ao fechar o aplicativo. A precisão é alvos acertados divididos pelos tiros realizados, vezes 100; não há divisão quando nenhum tiro foi dado.

## Perguntas para apresentação

**Qual parte faz o desenho?** `CannonView.drawGame()`.

**Qual parte controla as regras?** `GameEngine`.

**Por que não contar apenas o número de frames?** Aparelhos podem renderizar em velocidades diferentes; usamos tempo decorrido para calcular o deslocamento.

**Por que uma lista de alvos?** Cada alvo tem posição e velocidade próprias, e pode ser removido ao receber um tiro.

**O que acontece quando o tempo acaba?** O motor marca `finished`; a View pausa a simulação e pede que a UI apresente o resultado.

**Como evitar duas threads desenhando?** Antes de criar outro loop, o código solicita a parada do anterior e espera seu término com `join()`.

**O que falta para chamar de validado?** Compilar o APK e executar os casos manuais em um dispositivo real ou emulador.
