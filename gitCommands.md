# Configuração do Git e SSH com GitHub (Windows)

## 1. Cadastro inicial do Git

Abra o **Git Bash** e execute:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu-email-do-github@exemplo.com"
```

Confira se ficou salvo:

```bash
git config --list
```

---

## 2. Configuração da chave SSH

### 2.1 Verificar se já existe uma chave

```bash
ls -la ~/.ssh
```

Se **já existir** o arquivo `id_ed25519`, você pode pular para o passo 2.4. Se **não existir**, siga para o próximo passo.

### 2.2 Gerar a chave

```bash
ssh-keygen -t ed25519 -C "seuemail@gmail.com"
```

Quando aparecer a mensagem `Enter file in which to save the key`, pressione **ENTER** para aceitar o local padrão.

Em seguida, você pode definir uma senha (passphrase) para proteger a chave. É opcional, mas recomendado.

### 2.3 Iniciar o SSH Agent

```bash
eval "$(ssh-agent -s)"
```

### 2.4 Adicionar a chave ao agent

```bash
ssh-add ~/.ssh/id_ed25519
```

### 2.5 Copiar a chave pública

```bash
cat ~/.ssh/id_ed25519.pub
```

Copie toda a saída, começando em `ssh-ed25519` até o final (e-mail).

---

## 3. Cadastrar a chave no GitHub

1. Acesse **GitHub → Settings → SSH and GPG keys** (<https://github.com/settings/keys>).
2. Clique em **New SSH key**.
3. Preencha:
   - **Title:** `Windows Desktop`
   - **Key type:** `Authentication Key`
   - **Key:** cole a chave pública copiada
4. Clique em **Add SSH key**.

---

## 4. Testar a conexão

```bash
ssh -T git@github.com
```

Resultado esperado:

```
Hi Gmeirelis! You've successfully authenticated, but GitHub does not provide shell access.
```

Na primeira conexão, o Git Bash pode perguntar se você confia no host. Digite `yes`.

---

## Dica extra

Para que seus repositórios usem SSH, clone com a URL no formato `git@github.com:usuario/repositorio.git`. Para um repositório já clonado via HTTPS, troque a origem com:

```bash
git remote set-url origin git@github.com:usuario/repositorio.git
```
