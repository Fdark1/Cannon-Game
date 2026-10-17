# Validação realizada

Data: 08/10/2026.

## Resultado

1. Motor de jogo e teste independente compilados com o compilador Java 17 (`jdk.compiler`).
2. Execução de `GameEngineChecks`: **23 verificações aprovadas**. Abrange inicialização, tiro único, recompensas, pontuação, reflexão, penalidade única, vitória, derrota, limite do relógio, bola fora da tela, geometria de colisão, bordas, diferentes frequências de atualização e contato em frame longo.
3. Recursos Android compilados com **AAPT2 8.7.3-12006047** e vinculados contra a API 35, sem erros. Para esta verificação isolada, uma cópia temporária do manifesto recebeu o package normalmente injetado pelo Android Gradle Plugin. O manifesto do projeto mantém a configuração correta para AGP moderno, com namespace no build.gradle.
4. Todas as classes da aplicação compiladas contra Android API 35 e a classe `R` efetivamente gerada pelo AAPT2, sem erros. Avisos: uso intencional do Fragment nativo e da API imersiva antiga no ramo de compatibilidade.
5. Os três WAV foram abertos e conferidos byte a byte contra os anexos fornecidos.
6. O ZIP foi conferido para conter a estrutura do projeto e nenhum arquivo local de SDK, cache ou resultado temporário.

## O que esta validação não comprova

Não houve geração completa do APK pelo Android Gradle Plugin, execução de Android Lint, instalação, captura de tela ou teste em aparelho/emulador. A tentativa `./gradlew testDebugUnitTest assembleDebug --no-daemon` parou no download do Gradle com `UnknownHostException: services.gradle.org`. O ambiente não tinha SDK Android completo instalado.

Compilar Java e vincular os recursos reduz a chance de erros de código e XML, mas não substitui a compilação integral nem a execução do aplicativo. O fluxo GitHub Actions está preparado, mas ainda não foi executado. Execute os comandos do README e o roteiro manual antes de entregar.
