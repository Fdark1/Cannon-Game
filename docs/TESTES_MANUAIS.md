# Roteiro de testes no Android

Estas verificações precisam ser executadas; as caixas vazias não são resultados aprovados.

- [ ] Abrir no Android Studio e sincronizar sem erros.
- [ ] Executar `testDebugUnitTest assembleDebug lintDebug` com sucesso.
- [ ] Instalar o APK em Android 6/API 23 e em uma versão recente, quando houver ambos disponíveis.
- [ ] Tela inicial legível; o tempo só começa ao tocar em Jogar.
- [ ] Tela horizontal e barras do sistema ocultas; swipe permite recuperá-las temporariamente.
- [ ] Tocar acima/abaixo muda a mira; arrastar também funciona.
- [ ] Nunca há dois projéteis simultâneos.
- [ ] Ouvir disparo, alvo e bloqueador com volume de mídia habilitado.
- [ ] Acertar um alvo remove-o e acrescenta cerca de 3 s ao valor anterior, descontado o tempo do frame.
- [ ] Acertar o bloqueador rebate a bola e desconta apenas 2 s por tiro.
- [ ] Deixar a bola sair da tela quebra a sequência sem penalidade extra de tempo.
- [ ] Conferir multiplicadores 1×, 2×, 3×, 4×, 5×; limite de 500 pontos por acerto.
- [ ] Ficar sem disparar leva à derrota, com zero tiros e precisão 0%, sem erro.
- [ ] Acertar os 9 alvos leva à vitória.
- [ ] Reiniciar restaura os 9 alvos, 10 s e contadores zerados.
- [ ] Pressionar Home por alguns segundos e retornar: partida retoma sem descontar o tempo fora do app.
- [ ] Bloquear/desbloquear a tela durante a partida: não há desenho duplicado nem travamento.
- [ ] Sair e voltar com a tela de resultado aberta: resultado continua acessível.
- [ ] Fechar e reabrir: recorde permanece salvo.
- [ ] Mudar tamanho da janela em tablet/multijanela: nova rodada é iniciada pela tela de instruções.
- [ ] Conferir HUD sem corte em telas pequenas e com recorte de câmera.

Registre dispositivo, versão do Android, resultado e falhas reais. Se não houver acesso a duas versões, registre em qual foi testado. Não declare como testado um aparelho que não foi utilizado.
