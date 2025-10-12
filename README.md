# 🔍 Uptime Kuma - Sistema de Monitoramento

Projeto de monitoramento de serviços usando Uptime Kuma com Docker.

## 📋 Sobre o projeto

Uptime Kuma é uma ferramenta self-hosted de monitoramento de uptime, similar ao Uptime Robot. Este projeto configura o Uptime Kuma para monitorar serviços locais e externos, como o FileBrowser.

## ✨ Funcionalidades

- ✅ Monitoramento HTTP/HTTPS
- 📊 Dashboard visual com gráficos
- 🔔 Alertas em múltiplos canais (Telegram, Discord, e-mail, etc)
- 📱 Interface responsiva
- 🐳 Deploy fácil com Docker

## 🚀 Instalação

### Pré-requisitos

- Docker e Docker Compose instalados
- Porta 3001 liberada no firewall

### Passo a passo

Para rodar este projeto na instância em nuvem, siga os passos:

### ☁️ Rodando em uma instância na nuvem (ex: AWS EC2, Oracle Cloud, etc.)

1.  **Crie a instância:**
    * Escolha uma imagem Linux (Ubuntu recomendado).
    * Libere a porta `3001` no grupo de segurança/firewall.

2.  **Acesse a instância via SSH:**
    ```bash
    ssh usuario@ip-da-instancia
    ```

3.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/JoaoLuizDev/kuma.git](https://github.com/JoaoLuizDev/kuma.git)
    cd kuma
    ```

4.  **Inicie o container:**
    ```bash
    docker-compose up -d
    ```

5.  **Acesse a interface pelo navegador:**
    ```
    http://<ip-da-instancia>:3001
    ```

6. **Configure sua conta** na primeira vez que acessar

## 📊 Configuração de monitores

### Exemplo: Monitorar um serviço HTTP

1. Clique em "Add New Monitor"
2. Preencha:
   - **Monitor type:** HTTP(s)
   - **Friendly name:** Nome do serviço
   - **URL:** http://seu-ip:porta
   - **Heartbeat interval:** 60 segundos
3. Clique em "Save"

## 🔔 Configuração de alertas no Telegram

### Passo 1: Criar o bot

1. Abra o Telegram e busque por [@BotFather](https://t.me/BotFather)
2. Envie o comando: `/newbot`
3. Escolha um nome para o bot (ex: `Uptime Monitor`)
4. Escolha um username único que termine com `bot` (ex: `uptime_monitor_seunome_bot`)
5. **Copie e guarde o token** que o BotFather fornecer (exemplo de saída: `123456789:ABCdefGHIjklMNOpqrsTUVwxyz`)

### Passo 2: Obter seu chat ID

1. Busque por [@userinfobot](https://t.me/userinfobot) no Telegram
2. Envie qualquer mensagem (ex: `/start`)
3. **Copie o número do ID** fornecido (ex: `123456789`)

### Passo 3: Iniciar conversa com seu bot

⚠️ **IMPORTANTE:** Antes de configurar no Uptime Kuma, você DEVE:
1. Buscar seu bot pelo username no Telegram (ex: `@uptime_monitor_seunome_bot`)
2. Clicar em **START** ou enviar `/start`
3. Sem isso, o bot não conseguirá enviar mensagens!

### Passo 4: Configurar no Uptime Kuma

1. Acesse o Uptime Kuma e clique no ícone de **Settings** ⚙️
2. Vá em **Notifications** → **Setup Notification**
3. Selecione **Telegram**
4. Preencha:
   - **Friendly name:** insira um nome (exemplo: `Telegram Alerts`)
   - **Bot token:** cole o token do BotFather
   - **Chat ID:** cole o ID do userinfobot
5. Clique em **Test** (deve chegar uma mensagem de teste!)
6. Clique em **Save**

### Passo 5: Associar ao monitor

1. Volte ao **Dashboard**
2. Clique no monitor que deseja adicionar alertas
3. Clique em **Edit**
4. Na seção **Notifications**, marque a checkbox **Telegram Alerts**
5. Clique em **Save**

### Testando os alertas

Para verificar se está funcionando:

```bash
# Derruba o serviço monitorado. Exemplo:
docker stop filebrowser

# Aguarde 60-90 segundos
# Você receberá: 🔴 [FileBrowser] is DOWN

# Sobe o serviço novamente
docker start filebrowser

# Aguarde 60-90 segundos
# Você receberá: 🟢 [FileBrowser] is UP
```

### Outros canais suportados para envio de notificações

- Discord Webhook
- Email (SMTP)
- Slack
- Microsoft Teams
- WhatsApp
- Webhook genérico
- E mais de 90 opções!

## 🛠️ Comandos úteis

### Ver logs:
```bash
docker-compose logs -f uptime-kuma
```

### Parar o serviço:
```bash
docker-compose down
```

### Atualizar para última versão:
```bash
docker-compose pull
docker-compose up -d
```

### Backup dos dados:
```bash
tar -czf uptime-kuma-backup.tar.gz data/
```

## 📁 Estrutura do projeto

```
kuma/
├── docker-compose.yml    # Configuração do Docker
├── data/                 # Dados persistentes (criado automaticamente)
└── README.md             # Este arquivo
```

## 🔒 Segurança

- ⚠️ **IMPORTANTE:** Altere a senha padrão no primeiro acesso
- 🔐 Recomendado: Configure um proxy reverso (nginx) com SSL
- 🛡️ Limite o acesso por IP se possível

## 📈 Monitoramento Recomendado

Serviços sugeridos para monitorar:

- ✅ Aplicações web
- ✅ APIs
- ✅ Bancos de dados (via HTTP check)
- ✅ Servidores de arquivo
- ✅ Containers Docker

## 🐛 Troubleshooting

### Container não inicia:
```bash
docker logs uptime-kuma
```

### Porta já em uso

Se ao iniciar o container você receber erro de que a porta **3001 já está em uso**, significa que algum outro serviço na sua máquina já está ocupando essa porta.

No `docker-compose.yml`, a configuração de portas funciona assim:

```yaml
porta-do-host : porta-do-container
```

- **porta-do-host** → a porta que você vai usar para acessar pelo navegador  
- **porta-do-container** → a porta que o Uptime Kuma usa internamente (sempre `3001`)  

Neste caso, o Uptime Kuma continua rodando na porta 3001 dentro do container, mas você acessa pelo navegador em:

```yaml
http://seu-ip:3002
```

💡 Dica: se precisar, pode trocar para qualquer porta livre no host, como 8080:3001, 4000:3001, etc.

#### Exemplo: alterar para a porta 3002 no host

```yaml
ports:
  - "3002:3001"
```

### Perda de dados:
Os dados ficam em `./data` - faça backup regularmente!  <br><br>

---
   

**Feito com ❤️ para monitorar tudo que você precisa! 🚀**
