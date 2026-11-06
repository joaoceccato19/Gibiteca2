# Guia: gerar o APK pelo GitHub e instalar no celular

Você não precisa de Android Studio. O GitHub compila o APK para você, de graça.

## 1. Criar a conta e o repositório
1. Crie uma conta em github.com (se ainda não tiver).
2. Toque em **New repository**. Nome sugerido: `quadrinhos`. Pode deixar **Private**.
3. Marque **Add a README file** (isso cria a branch `main`) e crie.

## 2. Enviar os arquivos deste zip
Descompacte o zip. Você precisa enviar **tudo** para o repositório, incluindo a pasta oculta `.github`.

**Pelo computador (mais fácil):** abra o repositório, toque em **Add file > Upload files**, arraste todo o conteúdo da pasta `quadrinhos-apk` (inclusive `.github`, `www` e `debug.keystore`) e confirme em **Commit changes**.

**Pelo terminal:**
```bash
cd quadrinhos-apk
git init
git add .
git commit -m "Quadrinhos"
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/quadrinhos.git
git push -u origin main
```

**Se a pasta `.github` não subir** (comum pelo celular): em **Add file > Create new file**, digite o nome `.github/workflows/apk.yml` (as barras criam as pastas), cole o conteúdo do arquivo `apk.yml` do zip e confirme.

## 3. Gerar o APK
1. Abra a aba **Actions** do repositório. O processo **Gerar APK** começa sozinho depois do envio.
2. Se não começar: **Gerar APK > Run workflow**.
3. Aguarde de 5 a 10 minutos até aparecer o ícone verde ✓. Se ficar vermelho ✗, abra a execução e leia o erro (veja a seção de problemas).

## 4. Baixar o APK
1. Na página principal do repositório, abra **Releases** (lado direito, ou aba Code > Releases).
2. Abra **Quadrinhos (APK)** e toque em **Quadrinhos.apk** para baixar direto no celular.

## 5. Instalar
1. Abra o arquivo baixado.
2. Se o Android pedir, permita **Instalar apps desconhecidos** para o app que você usou (Chrome, Arquivos etc.).
3. Se o Play Protect avisar que o app não é verificado, toque em **Instalar mesmo assim**. Isso é normal em apps feitos por você.

## 6. Usar
- Toque em **+** para escolher vários quadrinhos (`.cbz` e `.cbr`) de uma vez.
- O botão **📁** tenta escolher uma pasta. Em alguns Androids ele abre o seletor normal de arquivos; nesse caso, selecione vários arquivos de uma vez.
- Abra um quadrinho e use o **⚙** para trocar entre **Horizontal**, **Página dupla** e **Vertical**, e ativar o modo **Mangá**.
- Toque no centro da tela para esconder ou mostrar os controles. O progresso de cada quadrinho fica salvo.

## 7. Atualizar o app
Mude o arquivo `www/index.html` no GitHub (ícone do lápis, depois Commit). O APK novo é gerado sozinho e substitui o da aba Releases. Instale por cima do antigo: sua biblioteca é mantida, porque a chave de assinatura é fixa (`debug.keystore`).

## Problemas comuns
- **Falha na etapa "Criar projeto Android":** confira se o arquivo `package.json` e a pasta `www` estão na raiz do repositório.
- **Falha em "Usar chave fixa":** o arquivo `debug.keystore` não foi enviado. Envie de novo.
- **Falha ao publicar na Releases:** em Settings > Actions > General > Workflow permissions, marque **Read and write permissions** e rode de novo.
- **"App não instalado":** já existe uma versão com outra assinatura. Desinstale a antiga e instale a nova (a biblioteca do app antigo será apagada).
- **`.cbr` não abre e aparece aviso:** o arquivo usa compressão RAR, que o app ainda não lê. Converta para `.cbz` (por exemplo, extraia e compacte como ZIP).
