# Quadro de Demandas

Aplicação web para gestão de tarefas semanais de equipe pequena, hospedada no GitHub Pages com dados persistidos no próprio repositório via GitHub Contents API.

---

## ⚠️ Aviso de privacidade importante

> **O arquivo `data/tarefas.json` fica publicamente acessível** via a URL do GitHub Pages, mesmo que o repositório seja privado.
>
> O código-fonte e o histórico de commits ficam ocultos num repositório privado, mas **todos os arquivos servidos pelo GitHub Pages são públicos** — qualquer pessoa com a URL pode ler o JSON.
>
> **Não inclua no JSON:**
> - CPFs, RGs ou documentos pessoais
> - Valores financeiros, contratos ou orçamentos
> - Senhas, tokens ou credenciais
> - Endereços completos ou dados de contato pessoal
>
> Use o sistema apenas para textos de tarefas e nomes de obras que possam ser públicos.

---

## Pré-requisitos

- Conta GitHub com plano **Pro**, **Team** ou **Enterprise** (GitHub Pages em repositório privado exige plano pago)
- Se sua conta for gratuita, o repositório precisará ser **público** — o conteúdo do JSON continuará público de qualquer forma, mas o código-fonte também ficará visível

---

## 1. Criar o repositório

1. Acesse [github.com/new](https://github.com/new)
2. Escolha um nome (ex: `quadro-demandas`)
3. Marque **Private** (ou Public se sua conta for gratuita)
4. **Não** inicialize com README (você vai fazer upload dos arquivos)
5. Clique em **Create repository**

---

## 2. Fazer upload dos arquivos

### Opção A — Interface web (mais simples)

1. Na página do repositório recém-criado, clique em **uploading an existing file**
2. Arraste `index.html`
3. Commit: `initial: add app`
4. Crie a pasta `data/` clicando em **Add file → Create new file**, digite `data/tarefas.json` e cole o conteúdo do arquivo
5. Commit: `initial: add data file`

### Opção B — Git na linha de comando

```bash
git init
git add index.html data/tarefas.json
git commit -m "initial: add app and data"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/quadro-demandas.git
git push -u origin main
```

---

## 3. Ativar o GitHub Pages

1. No repositório, vá em **Settings → Pages**
2. Em **Source**, selecione **Deploy from a branch**
3. Branch: `main` | Pasta: `/ (root)`
4. Clique em **Save**
5. Aguarde 1–2 minutos. A URL aparecerá no topo da página, no formato:
   ```
   https://SEU-USUARIO.github.io/quadro-demandas/
   ```

> Se o repositório for privado e você não tiver plano pago, o GitHub vai mostrar erro "GitHub Pages is not available for private repositories on your current plan". Nesse caso, torne o repositório público ou faça upgrade do plano.

---

## 4. Gerar o Personal Access Token (PAT)

O PAT permite que a aplicação leia e grave o JSON sem que você precise fazer login.

1. Acesse **GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)**
   - URL direta: [github.com/settings/tokens](https://github.com/settings/tokens)
2. Clique em **Generate new token (classic)**
3. Dê um nome descritivo: `quadro-demandas`
4. Expiration: escolha um prazo (90 dias é razoável; lembre de renovar)
5. Scopes: marque apenas **`repo`** (acesso completo a repositórios privados)
6. Clique em **Generate token**
7. **Copie o token agora** — ele não será exibido novamente

> O token fica salvo apenas no `localStorage` do seu navegador, nunca em commits ou logs.

---

## 5. Primeira abertura da aplicação

1. Acesse a URL do GitHub Pages
2. Um modal de configuração vai aparecer automaticamente
3. Preencha:
   - **GitHub Owner**: seu usuário ou organização (ex: `minha-org`)
   - **Repositório**: nome do repositório (ex: `quadro-demandas`)
   - **Branch**: `main`
   - **Personal Access Token**: o token copiado no passo anterior
4. Clique em **Salvar e conectar**

As configurações ficam salvas no `localStorage` do navegador. Para redefinir, clique no botão **Configurar** no canto superior direito.

---

## 6. Uso em vários dispositivos / navegadores

Como as configurações ficam no `localStorage`, cada dispositivo ou navegador precisa configurar o PAT separadamente. Os dados em si ficam no JSON do repositório e são compartilhados automaticamente.

---

## Fluxo de trabalho sugerido

1. **Inbox**: jogue tudo que precisa ser feito, sem pensar em detalhes
2. Periodicamente (ex: toda segunda-feira), abra cada item do Inbox e clique em **Organizar**: defina responsável, semana e tipo
3. Na aba **Semana**, acompanhe o andamento marcando tarefas como concluídas
4. Use tarefas do tipo **Lote** para atividades que se repetem por obra (ex: "enviar relatório para todas as obras")

---

## Solução de problemas

| Problema | Solução |
|---|---|
| "Erro ao carregar dados" na primeira abertura | Verifique Owner, Repositório e Token. Confirme que o arquivo `data/tarefas.json` existe no repositório |
| "HTTP 401" | Token inválido ou expirado — gere um novo |
| "HTTP 403" | Token sem escopo `repo` ou repositório não encontrado |
| "HTTP 409 Conflict" | Conflito de SHA — alguém (outro dispositivo) salvou enquanto você também editava. Recarregue a página |
| Mudanças não aparecem em outro dispositivo | Recarregue a página — a leitura acontece sempre no carregamento inicial |
| GitHub Pages não ativa | Verifique se a conta tem plano Pro/Team para repositório privado |
