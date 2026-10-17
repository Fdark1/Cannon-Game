# Publicação no GitHub

## Forma recomendada: GitHub Desktop

1. Extraia o arquivo recebido. A pasta `CannonGame` precisa conter `app`, `gradle`, `README.md` e `settings.gradle`.
2. Abra e teste essa pasta no Android Studio antes de publicar.
3. Preencha os integrantes no README. Confirme com o professor como registrar o apoio de IA e a composição da dupla.
4. Instale/abra o GitHub Desktop e entre na sua conta.
5. Use **File → Add local repository** e selecione `CannonGame`. Se ele informar que a pasta não é um repositório, use o link para criar um repositório nessa pasta. Confira o caminho para não criar outra subpasta vazia.
6. Confira os arquivos detectados. Na raiz devem estar `settings.gradle`, `build.gradle`, `gradlew`, `gradlew.bat`, `README.md`, `.gitignore`, além de `app/`, `gradle/`, `docs/` e `.github/`.
7. No resumo do primeiro commit, descreva honestamente o que está sendo adicionado, por exemplo: **Adiciona implementação inicial do Cannon Game com apoio de IA**. Clique em **Commit to main**.
8. Clique em **Publish repository**. Nome sugerido: `cannon-game-programacao-iii`. Desmarque **Keep this code private**, porque o enunciado exige repositório público.
9. Abra o repositório no navegador e vá à aba **Actions**. Espere a execução do fluxo Android. Só considere a compilação verificada quando ele ficar verde. Em caso de falha, abra o passo com erro e leia o log.
10. Na execução bem-sucedida, o artifact `CannonGame-debug` contém o APK de depuração. Baixe-o e teste em aparelho ou rode o projeto no emulador do Android Studio.
11. Inclua, se possível, uma captura real do jogo em execução no README. Não use uma ilustração como se fosse screenshot do aplicativo.
12. Entregue a URL do repositório no Moodle. Confira se ela abre sem estar logada.

## Sobre o botão Add file do site

Enviar somente um arquivo Java não basta. O Android Studio precisa da estrutura completa. O envio por navegador pode omitir pastas ocultas e tem limites de tamanho/quantidade; o GitHub Desktop é a opção mais simples para preservar tudo, inclusive `.github` e `.gitignore`.

## Participação e commits

Cada pessoa deve usar a própria conta para registrar mudanças que efetivamente fez. Exemplos de participação real: executar o roteiro de testes, corrigir um erro encontrado, explicar e revisar uma classe ou melhorar a documentação. Não crie autores fictícios, datas retroativas ou commits simulando uma divisão de trabalho que não aconteceu.

O repositório público ainda não foi criado por esta ferramenta. Nenhum commit foi publicado na sua conta.
