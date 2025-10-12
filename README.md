# 🔍 Uptime Kuma - Seu primeiro projeto de monitoramento na nuvem

## 👶 Para quem é este guia?
Este tutorial foi feito para **iniciante em Cloud Computing** que quer subir sua **primeira aplicação na nuvem**.  
Você não precisa ter experiência com AWS, Oracle ou Docker — o guia mostra **passo a passo com prints**.

Ao final, você terá:
- Uma instância (máquina virtual) rodando na nuvem (AWS ou Oracle).
- O **Uptime Kuma** instalado em container Docker.
- Monitoramento básico de sites, APIs e serviços, com alertas no **Telegram**.

## 📋 O que é o Uptime Kuma?
O **Uptime Kuma** é uma ferramenta self-hosted de monitoramento de uptime, parecida com o Uptime Robot.  
Com ele você pode:
- ✅ Monitorar sites, APIs e serviços
- 📊 Ver um painel visual com gráficos
- 🔔 Receber alertas em tempo real (Telegram, Discord, e-mail, etc.)
- 🐳 Deploy fácil com Docker

## 🗂️ Etapas do projeto

- **Fase 1:** Criar conta em um provedor de nuvem   
- **Fase 2:** Criar uma instância Linux na nuvem  
- **Fase 3:** Fazer o deploy do Uptime Kuma com Docker  
- **Fase 4:** Configurar alertas e monitoramento

Neste tutorial, usaremos a AWS.

## ☁️ Fase 1 - Criando sua conta na nuvem

- Acesse o link: [https://aws.amazon.com/free](https://aws.amazon.com/free).  
- Clique no botão **"Criar uma conta gratuita"**.  
- Em **Root user email address**, insira um **e-mail válido**.  
- Em **AWS account name**, insira o nome da conta. Pode ser seu nome, sua empresa ou um apelido (ex: `meu-projeto-cloud`).  
- Clique em **Verify email address**. A AWS enviará um código de verificação para seu e-mail.  
- Verifique sua caixa de entrada e cole o código.  
- Clique em **Verify**.  
- Em **Root user password**, digite uma senha forte.  
  💡 Dica: misture letras maiúsculas, minúsculas, números e símbolos.  
- ⚠️ Observações importantes:
  - Esta senha será usada para **entrar na AWS** como usuário root.  
  - Guarde a senha em um local seguro, pois é o acesso principal da sua conta.  
- Após preencher os campos, clique em **Continue**.  

---

### Escolhendo o plano

- Selecione a opção **Gratuito**:  
  - Benefícios iniciais por até **6 meses**.  
  - Créditos de até **USD $200** para testar e experimentar serviços.  
  - Inclui serviços selecionados que podem ser usados sem custo, como instâncias `t2.micro`.  

---

### Informações sobre uso da conta

- No campo **Como você planeja usar a AWS?**, escolha a opção **Pessoal**.  
- Preencha os campos com seus **dados pessoais** (nome, telefone, endereço, etc.).  
- Marque a caixa: **Li e concordo com os termos do Contrato de Cliente da AWS**.  
- Clique em **Concordar e continuar (etapa 2 de 5)**.  

---

### Informações de faturamento (etapa 3 de 5)

- A AWS pede dados de pagamento para **verificação e prevenção de fraudes**, mesmo para o plano gratuito.  
- A AWS retém temporariamente **USD $1** (ou equivalente) para verificar o cartão.  
  ⚠️ Certifique-se de que seu cartão permite compras internacionais.  
- Não haverá cobrança para o plano gratuito, a menos que você faça upgrade para um plano pago.  
- Preencha todos os campos obrigatórios sobre faturamento e clique em **Verificar e continuar**.  

---

### Verificação de telefone (etapa 4 de 5)

- A AWS pedirá para **confirmar seu número de telefone**.  
- Você receberá um **código via SMS ou chamada de voz**.  
- Digite o código na tela para concluir a verificação.  
⚠️ Sem essa verificação, sua conta não será ativada.  

---

### Escolha do plano de suporte (etapa 5 de 5)

- A AWS oferece planos pagos de suporte, mas para iniciantes escolha **Basic (grátis)**.  
- O plano gratuito permite criar instâncias e usar serviços sem custo extra, perfeito para aprendizado.  

---

### Confirmação e login

- Após concluir a verificação de telefone e escolher o plano de suporte, sua conta será ativada.  
- Você poderá entrar na **AWS Management Console** usando o **e-mail** e a **senha** que criou. 🎉





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
