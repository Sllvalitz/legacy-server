<div align="center">
  <img width="2560" height="328" alt="Ansi Labs Banner GitHub" src="https://github.com/user-attachments/assets/fcb5ab82-46e5-4571-b4c2-d6cc3556e024" />
  <img src="https://img.shields.io/badge/Status-Ativo-success?style=for-the-badge" alt="Status Ativo">
  <img src="https://img.shields.io/badge/versão-1.0.0-blue?style=for-the-badge" alt="Versão 1.0.0">
  <img src="https://img.shields.io/badge/Debian-13-a81d33?style=for-the-badge&logo=debian" alt="Debian 13">
  <img src="https://img.shields.io/badge/Docker-Containers-2496ed?style=for-the-badge&logo=docker" alt="Docker">
  <img src="https://img.shields.io/badge/Consumo-%7E10W-yellow?style=for-the-badge" alt="10W">
  <img src="https://img.shields.io/badge/Uptime-24%2F7-brightgreen?style=for-the-badge" alt="24/7">

<h1>Legacy Server</h1>
</div>

<div align="center">
  <img src="imagem.png" alt="Servidor Legacy NAS em funcionamento" width="600">
  <br>
  <em>Servidor operando 24/7 no gabinete customizado impresso em 3D.</em>
</div>
<br>

<div align="justify">
Um servidor doméstico construído a partir de uma placa-mãe de um notebook que viria a ser descartada (Acer Aspire ES1-511), rodando 24/7 com consumo ínfimo de ~10W. O projeto prova que hardware legado possui vida útil real e escalável para hospedar mídia, diversos serviços locais e um portfólio web próprio, dispensando infraestruturas externas de nuvem.
</div>

> 📺 Este projeto é documentado em série no YouTube — links dos episódios ao final.


## Hardware

<div align="justify">
O dispositivo foi escolhido com o objetivo estrito de reaproveitamento total do hardware. Pois, para tarefas comuns do dia-a-dia ele já estava no limite, seja assistir vídeo no youtube ou ter mais de uma guia aberta no navegador. O Celeron N2840 é fraco para transcodificação de vídeo, mas é exatamente o que se precisa para um servidor NAS: baixíssimo consumo, poder computacional suficiente para servir arquivos, filtrar DNS e gerenciar containers leves.
</div>
&nbsp;

<div align="center">
<table>
  <tr>
    <th align="center">Componente</th>
    <th align="center">Especificação</th>
  </tr>
  <tr>
    <td align="left"><strong>Processador</strong></td>
    <td align="left">Intel Celeron N2840</td>
  </tr>
  <tr>
    <td align="left"><strong>RAM</strong></td>
    <td align="left">8 GB (HyperX Impact DDR3L 1600 MHz)</td>
  </tr>
  <tr>
    <td align="left"><strong>Sistema</strong></td>
    <td align="left">Rise Mode Gamer Line 120 GB (SSD via USB 3.0)</td>
  </tr>
  <tr>
    <td align="left"><strong>Dados</strong></td>
    <td align="left">2× HGST 500 GB 7200 RPM 2.5" SATA</td>
  </tr>
  <tr>
    <td align="left"><strong>Rede</strong></td>
    <td align="left">Intel 7260HMW (Wi-Fi Dual Band AC + Bluetooth)</td>
  </tr>
  <tr>
    <td align="left"><strong>Gabinete</strong></td>
    <td align="left">Case customizado impresso em 3D (modelos na pasta <code>/modelos-3d</code>)</td>
  </tr>
</table>
</div>


## Stack de Infraestrutura

<div align="justify">
A infraestrutura base é o <strong>Debian 13 (Trixie)</strong> puro, escolhido por sua estabilidade, uso mínimo de RAM e suporte de longo prazo. Sobre ele, o <strong>CasaOS</strong> atua como uma camada de abstração visual para a engine do <strong>Docker</strong>, agilizando o monitoramento e o deploy de containers sem restringir o acesso nativo ao terminal.
</div>

<br>

<div align="justify">
A topologia de rede é gerenciada por dois componentes críticos: o <strong>Tailscale</strong> cria uma malha VPN criptografada via WireGuard, provendo acesso remoto seguro à gerência sem expor portas na WAN. Em paralelo, o <strong>Nginx Proxy Manager (NPM)</strong> orquestra as requisições HTTP/HTTPS, roteando o tráfego interno e sendo a peça-chave para expor e hospedar o portfólio web pessoal diretamente neste hardware, com renovação automatizada de certificados SSL via Let's Encrypt.
</div>
&nbsp;

<div align="center">
<table>
  <tr>
    <th align="center">Camada</th>
    <th align="center">Tecnologia</th>
  </tr>
  <tr>
    <td align="left"><strong>Sistema Operacional</strong></td>
    <td align="left">Debian 13 Trixie</td>
  </tr>
  <tr>
    <td align="left"><strong>Engine de Containers</strong></td>
    <td align="left">CasaOS + Docker</td>
  </tr>
  <tr>
    <td align="left"><strong>Túnel e VPN</strong></td>
    <td align="left">Tailscale</td>
  </tr>
  <tr>
    <td align="left"><strong>Proxy Reverso e Web Server</strong></td>
    <td align="left">Nginx Proxy Manager</td>
  </tr>
  <tr>
    <td align="left"><strong>Resolução Local de DNS</strong></td>
    <td align="left">AdGuard Home</td>
  </tr>
</table>
</div>


## Serviços ativos

<div align="justify">
Os serviços foram escolhidos conforme preferência e praticidade, sempre observando as restrições de CPU e o consumo reduzido de memória RAM. Nenhum container faz transcodificação sob demanda; o Jellyfin opera apenas em <em>Direct Play</em>.
</div>
&nbsp;

<div align="center">
<table>
  <tr>
    <th align="center">Serviço</th>
    <th align="center">Função</th>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://github.com/tailscale/tailscale" target="_blank" rel="noopener noreferrer">Tailscale</a></strong></td>
    <td align="left">VPN gerenciada (acesso remoto seguro a todos os serviços privados)</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://github.com/crowdsecurity/crowdsec" target="_blank" rel="noopener noreferrer">CrowdSec</a></strong></td>
    <td align="left">Detecção de intrusão e bloqueio de IPs maliciosos</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://github.com/CISOfy/lynis" target="_blank" rel="noopener noreferrer">Lynis</a></strong></td>
    <td align="left">Auditoria de segurança e hardening do sistema operacional</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://github.com/Cisco-Talos/clamav" target="_blank" rel="noopener noreferrer">ClamAV</a></strong></td>
    <td align="left">Antivírus open-source para varredura de arquivos e detecção de malwares</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://github.com/AdguardTeam/AdGuardHome" target="_blank" rel="noopener noreferrer">AdGuard Home</a></strong></td>
    <td align="left">Filtragem de DNS e bloqueio de anúncios para toda a rede</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://github.com/NginxProxyManager/nginx-proxy-manager" target="_blank" rel="noopener noreferrer">Nginx Proxy Manager</a></strong></td>
    <td align="left">Reverse proxy com HTTPS e SSL automático via Let's Encrypt</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://github.com/samba-team/samba" target="_blank" rel="noopener noreferrer">Samba</a></strong></td>
    <td align="left">Compartilhamento de arquivos na rede local e via Tailscale</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://github.com/rclone/rclone" target="_blank" rel="noopener noreferrer">Rclone</a></strong></td>
    <td align="left">Sincronização e backup criptografado para o Google Drive</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://github.com/binwiederhier/ntfy" target="_blank" rel="noopener noreferrer">ntfy</a></strong></td>
    <td align="left">Notificações push para iPhone via ntfy.sh</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://github.com/Stirling-Tools/Stirling-PDF" target="_blank" rel="noopener noreferrer">Stirling PDF</a></strong></td>
    <td align="left">Ferramentas PDF (juntar, dividir, OCR, converter e etc)</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://github.com/LibreOffice/core" target="_blank" rel="noopener noreferrer">LibreOffice headless</a></strong></td>
    <td align="left">Conversão de arquivos de escritório (PDF ↔ Word e similares)</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://github.com/jellyfin/jellyfin" target="_blank" rel="noopener noreferrer">Jellyfin</a></strong></td>
    <td align="left">Servidor de mídia (Direct Play — H.264 + AAC)</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://github.com/qbittorrent/qBittorrent/" target="_blank" rel="noopener noreferrer">qBittorrent</a></strong></td>
    <td align="left">Cliente de downloads com agendamento de banda</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://github.com/Suwayomi/Suwayomi-Server" target="_blank" rel="noopener noreferrer">Suwayomi-Server</a></strong></td>
    <td align="left">Servidor e Leitor de mangás (atua como fonte para Paperback no iOS)</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="URL_DO_SEU_SITE" target="_blank" rel="noopener noreferrer">Site estático</a></strong></td>
    <td align="left">Portfólio pessoal em HTML/CSS/JS servido pelo Nginx</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://gitlab.com/crafty-controller/crafty-4" target="_blank" rel="noopener noreferrer">Minecraft Bedrock</a></strong></td>
    <td align="left">Servidor Bedrock via Crafty Controller</td>
  </tr>
  <tr>
    <td align="left"><strong><a href="https://gitlab.com/crafty-controller/crafty-4" target="_blank" rel="noopener noreferrer">Minecraft Java</a></strong></td>
    <td align="left">Servidor Paper 1.20.1 via Crafty Controller</td>
  </tr>
</table>
</div>

## Documentação

<details>
  <summary>📌 EP 01 — Do Zero ao Servidor de Pé</summary>

### EP 01 — Do Zero ao Servidor de Pé

**Pré-requisitos:**

> - Pendrive de no mínimo 4 GB disponível
> - Acesso ao painel do roteador da rede local
> - Computador Windows para geração de chaves SSH e acesso remoto

---

**Visão Geral:**

<div align="center">
<table>
  <tr>
    <th align="center">Etapa</th>
    <th align="center">Ferramenta</th>
    <th align="center">Função</th>
  </tr>
  <tr>
    <td align="left"><a href="#ep01-etapa1">Pendrive bootável</a></td>
    <td align="left">Rufus + ISO Debian</td>
    <td align="left">Prepara a mídia de instalação do sistema operacional.</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep01-etapa2">Instalação do Debian</a></td>
    <td align="left">Debian 13 Installer</td>
    <td align="left">Instala o sistema mínimo sem interface gráfica.</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep01-etapa3">Sistema de Arquivos</a></td>
    <td align="left">Btrfs</td>
    <td align="left">Configura os discos extras utilizando o sistema de arquivos Btrfs.</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep01-etapa4">Conexão via SSH</a></td>
    <td align="left">OpenSSH + chaves Ed25519</td>
    <td align="left">Configura acesso remoto seguro por chave criptográfica.</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep01-etapa5">CasaOS + AdGuard</a></td>
    <td align="left">CasaOS + Docker</td>
    <td align="left">Instala o painel de containers e o filtro DNS da rede.</td>
  </tr>
</table>
</div>

---

**Convenções Utilizadas Neste Documento**

<div align="justify">
Este guia utiliza variáveis de template representadas pelo formato >NOME_DA_VARIAVEL<. Sempre que encontrar uma delas em comandos, arquivos de configuração ou exemplos, substitua pelo valor correspondente ao seu ambiente antes de prosseguir.
</div>

> ⚠️ Quando uma etapa exigir atenção especial a essa substituição, um aviso como este será exibido.

<div align="center">
<table>
  <tr>
    <th align="center">Variável</th>
    <th align="center">Descrição</th>
  </tr>
  <tr>
    <td align="left"><code>>SEU_USUARIO<</code></td>
    <td align="left">Nome do usuário comum configurado na instalação do Debian.</td>
  </tr>
  <tr>
    <td align="left"><code>>IP_DO_SERVIDOR<</code></td>
    <td align="left">Endereço IP local fixo atribuído ao servidor na rede interna.</td>
  </tr>
  <tr>
    <td align="left"><code>>NOME_DA_CHAVE<</code></td>
    <td align="left">Nome personalizado para o par de chaves SSH gerado no Windows.</td>
  </tr>
  <tr>
    <td align="left"><code>>NOME_SERVIDOR<</code></td>
    <td align="left">Alias configurado no SSH config do Windows para acesso rápido.</td>
  </tr>
</table>
</div>

---

### Etapas Documentadas

<details id="ep01-etapa1">
  <summary>🪨 Etapa 1 — Preparar o Pendrive Bootável</summary>

**Passo 1 — Baixar os recursos necessários**

<div align="justify">
Baixe a ISO do Debian 13 e o Rufus, a ferramenta que gravará a imagem no pendrive em modo compatível com UEFI.
</div>

- ISO: [debian.org/download](https://www.debian.org/download)
- Rufus: [rufus.ie](https://rufus.ie)

---

**Passo 2 — Gravar o pendrive**

<div align="justify">
Abra o Rufus, selecione o pendrive e a ISO baixada. Configure os parâmetros abaixo antes de iniciar.
</div>

- **Esquema de partição:** `GPT`
- **Sistema de destino:** `UEFI (não CSM)`

Clique em `Iniciar` e selecione o modo `Imagem DD` quando solicitado. Aguarde a conclusão e conecte o pendrive ao servidor.

---

</details>

<details id="ep01-etapa2">
  <summary>🪨 Etapa 2 — Instalar o Debian 13</summary>

**Passo 1 — Configurar a BIOS**

<div align="justify">
Ligue o servidor e pressione <code>ESC</code>, <code>DEL</code> OU <code>F2</code> para entrar na BIOS. Os ajustes abaixo são necessários antes de iniciar pelo pendrive.
</div>

> ⁉️ Em outras máquinas a tecla de acesso à BIOS pode ser diferente, consulte o manual do modelo.

- Ajuste data e hora se necessário
- Desative o `Secure Boot`
- Defina a ordem de boot: `USB` como primeiro, dispositivo que receberá o Sitema Operacional como segundo
> ⁉️ Em alguns notebooks é necessário criar uma senha de administrador para desativar o secure boot.

---

**Passo 2 — Executar o instalador**

<div align="justify">
Selecione <code>Install</code> (sem interface gráfica) e siga a sequência abaixo. Para Wi-Fi, selecione a interface <code>wlan...</code> quando solicitado.
</div>

- **Nome da máquina:** `legacy-server` (sugestão)
- **Nome de domínio:** deixar em branco
- **Método de particionamento:** `Usar disco inteiro`
- **Partição:** `Todos os arquivos em uma única partição`
- **Espelho dos repositórios:** Brasil → `deb.debian.org`
- **Proxy HTTP:** deixar em branco
- **Concurso de utilização de pacotes:** `Não`
- **Seleção de software:** marcar apenas `Servidor SSH` e `Utilitários de sistema padrão`

> ⁉️ Quando a tela apagar ao final da instalação, remova o pendrive antes de o sistema reiniciar.

---

**Passo 3 — Primeiros comandos**

<div align="justify">
Ao iniciar, faça login com o usuário configurado na instalação. Em seguida, eleve para root e prepare o sistema.
</div>

> ⚠️ Ao digitar senhas no terminal, nada aparecerá na tela, isso é comportamento normal do Linux.

```bash
su -
apt update && apt upgrade -y
apt install -y curl wget sudo net-tools network-manager
```

---

</details>

<details id="ep01-etapa3">
  <summary>🪨 Etapa 3 — Criar o Sistema de Arquivos</summary>

**Passo 1 — Identificar os discos**

```bash
lsblk -o NAME,SIZE,TYPE,MOUNTPOINT,MODEL
```

---

**Passo 2 — Instalar as ferramentas do Btrfs**

<div align="justify">
O Debian não inclui as ferramentas de gerenciamento do Btrfs por padrão. Elas precisam ser instaladas antes de formatar o disco.
</div>

```bash
sudo apt update
sudo apt install -y btrfs-progs
```

---

**Passo 3 — Formatar o disco em Btrfs**

<div align="justify">
Este passo cria o sistema de arquivos Btrfs diretamente no disco, com um rótulo (label) que facilita a identificação posterior.
</div>

> ⚠️ A variável `>DISCO<` deve ser substituída pelo identificador confirmado no Passo 1. Todos os dados existentes no disco serão apagados.

```bash
sudo mkfs.btrfs -L Storage /dev/>DISCO<
```

---

**Passo 4 — Obter o UUID do disco**
<div align="justify">
O uso do UUID em vez do nome do dispositivo (ex: <code>/dev/sdb</code>) garante que a montagem funcione mesmo que a ordem de identificação dos discos mude após uma reinicialização.
</div>

> ⚠️ A variável `>DISCO<` deve ser substituída pelo identificador confirmado no Passo 1.

```bash
sudo blkid /dev/>DISCO<
```

> 💡 Anote o valor de `UUID` retornado. Ele será usado no próximo passo para a variável `>UUID_DISCO<`.

---

### Passo 5 — Criar o ponto de montagem e montar

<div align="justify">
Aqui é criada a pasta que servirá como ponto de acesso ao armazenamento e o disco é montado nela.
</div>

> ⚠️ A variável `>DISCO<` deve ser substituída pelo identificador confirmado no Passo 1.

```bash
sudo mkdir -p /mnt/storage
sudo mount /dev/>DISCO</mnt/storage
```

---

### Passo 6 — Tornar a montagem permanente

<div align="justify">
Esta entrada no <code>fstab</code> garante que o disco seja montado automaticamente sempre que o servidor for reiniciado, usando o UUID identificado no Passo 4.
</div>

> ⚠️ A variável `>UUID_DISCO<` deve ser substituída pelo UUID obtido no Passo 4.

```bash
echo 'UUID=>UUID_DISCO</mnt/storage btrfs defaults 0 0' | sudo tee -a /etc/fstab
```

---

### Passo 7 — Validar a montagem

<div align="justify">
Por fim, é recomendado recarregar as configurações de montagem e confirmar que tudo foi aplicado corretamente antes de seguir para o próximo bloco.
</div>

```bash
sudo mount -a
df -hT /mnt/storage
sudo btrfs filesystem show
```

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>df -hT /mnt/storage</code></td>
    <td align="left">Disco listado com sistema de arquivos <strong>btrfs</strong> montado em <code>/mnt/storage</code></td>
  </tr>
  <tr>
    <td align="left"><code>sudo btrfs filesystem show</code></td>
    <td align="left">Exibe o label <strong>Storage</strong> e o disco associado sem erros</td>
  </tr>
</table>
</div>

</details>

<details id="ep01-etapa4">
  <summary>🪨 Etapa 4 — Configurar Acesso SSH</summary>

**Passo 1 — Gerar par de chaves no Windows**

<div align="justify">
Abra o PowerShell no computador principal e gere o par de chaves Ed25519.
</div>

> ⚠️ A variável `>NOME_DA_CHAVE<` deve ser substituída por um nome personalizado para identificar esta chave (ex: `legacy-server`).

```powershell
ssh-keygen -t ed25519 -C ">NOME_DA_CHAVE<"
```

- Quando perguntar o diretório: pressione `Enter` para manter o padrão
- Quando pedir senha da chave: pressione `Enter` duas vezes para deixar sem senha

---

**Passo 2 — Exibir a chave pública**

```powershell
Get-Content C:\Users\Admin\.ssh\id_ed25519.pub
```

> ⚠️ Copie todo o conteúdo retornado. Não compartilhe essa chave com ninguém.

---

**Passo 3 — Descobrir o IP do servidor**

<div align="justify">
Acesse o painel do roteador (geralmente <code>192.168.1.1</code> ou <code>192.168.15.1</code> — credenciais na etiqueta do aparelho). Localize o hostname do servidor na seção <code>Rede Local</code> e copie o IP atribuído.
</div>

---

**Passo 4 — Primeira conexão e instalação da chave**

> ⚠️ A variável `>SEU_USUARIO<` deve ser substituída pelo usuário configurado na instalação do Debian. A variável `>IP_DO_SERVIDOR<` deve ser substituída pelo IP copiado no passo anterior.

```powershell
ssh >SEU_USUARIO<@>IP_DO_SERVIDOR<
```

Digite `yes` quando solicitado e então a senha do usuário. Já dentro do servidor:

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
nano ~/.ssh/authorized_keys
```

Cole o conteúdo da chave pública. Salve: `Ctrl+O` → `Enter` → `Ctrl+X`

```bash
chmod 600 ~/.ssh/authorized_keys
```

---

**Passo 5 — Configurar o sshd_config**

```bash
nano /etc/ssh/sshd_config
```

Use `Ctrl+W` para localizar e ajustar cada parâmetro:

<div align="center">
<table>
  <tr>
    <th align="center">Parâmetro</th>
    <th align="center">Valor</th>
    <th align="center">Motivo</th>
  </tr>
  <tr>
    <td align="left"><code>Port</code></td>
    <td align="left"><code>2242</code></td>
    <td align="left">Muda a porta padrão, reduzindo ataques de bots automáticos</td>
  </tr>
  <tr>
    <td align="left"><code>PermitRootLogin</code></td>
    <td align="left"><code>no</code></td>
    <td align="left">Desativa login direto como root via SSH</td>
  </tr>
  <tr>
    <td align="left"><code>PasswordAuthentication</code></td>
    <td align="left"><code>no</code></td>
    <td align="left">Permite apenas login via chave SSH criptografada</td>
  </tr>
</table>
</div>

Salve: `Ctrl+O` → `Enter` → `Ctrl+X`

```bash
systemctl restart ssh
```

> ⚠️ Não feche o terminal atual. Se algo der errado, você ainda está logado e pode corrigir antes de testar.

---

**Passo 6 — Testar a nova configuração**

Abra um novo terminal no Windows e conecte pela nova porta:

> ⚠️ As variáveis `>SEU_USUARIO<` e `>IP_DO_SERVIDOR<` devem ser substituídas pelos valores do seu ambiente.

```powershell
ssh -i C:\Users\Admin\.ssh\id_ed25519 -p 2242 >SEU_USUARIO<@>IP_DO_SERVIDOR<
```

---

**Passo 7 — Configurar atalho SSH no Windows**

> ⚠️ As variáveis `>NOME_SERVIDOR<`, `>IP_DO_SERVIDOR<` e `>SEU_USUARIO<` devem ser substituídas pelos valores do seu ambiente.

```powershell
@'
Host >NOME_SERVIDOR<
    HostName >IP_DO_SERVIDOR<
    User >SEU_USUARIO<
    Port 2242
    IdentityFile C:\Users\Admin\.ssh\id_ed25519
'@ | Out-File C:\Users\Admin\.ssh\config -Encoding ascii
```

Após salvar, conecte com:

```powershell
ssh >NOME_SERVIDOR<
```

---

**Passo 8 — Reservar o IP fixo no roteador**

<div align="justify">
No painel do roteador, localize a opção para reservar o IP pelo hostname do servidor. Isso garante que o endereço não mude após reinicializações.
</div>

> 💡 O nome da opção varia por fabricante: na Vivo aparece como `Criar Reserva no DHCP`; em outros roteadores pode ser `IP Estático` ou `IP-MAC Binding`.

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>ssh >NOME_SERVIDOR<</code></td>
    <td align="left">Conexão estabelecida sem solicitar senha</td>
  </tr>
  <tr>
    <td align="left">Porta 22 recusada</td>
    <td align="left">Conexão na porta padrão deve ser recusada</td>
  </tr>
</table>
</div>

---

</details>

<details id="ep01-etapa5">
  <summary>🪨 Etapa 5 — Instalar CasaOS e AdGuard Home</summary>

**Passo 1 — Instalar o CasaOS**

```bash
curl -fsSL https://get.casaos.io | sudo bash
```

> ⁉️ Após a instalação, o terminal exibirá um endereço de acesso. Não acesse ainda — é necessário ajustar a porta antes.

---

**Passo 2 — Ajustar a porta do CasaOS**

<div align="justify">
O Nginx Proxy Manager (instalado no EP 02) exige as portas 80 e 443 livres. Se o CasaOS permanecer na porta 80, os dois serviços vão conflitar. A solução é mover o CasaOS para a porta 5000.
</div>

```bash
sudo nano /etc/casaos/gateway.ini
```

Altere o valor de `port` de `80` para `5000`. Salve: `Ctrl+O` → `Enter` → `Ctrl+X`

```bash
sudo systemctl restart casaos-gateway
```

---

**Passo 3 — Primeiro acesso ao CasaOS**

<div align="justify">
Abra o navegador e acesse o painel. Crie um login para administração.
</div>

> ⚠️ A variável `>IP_DO_SERVIDOR<` deve ser substituída pelo IP do servidor na rede local.

```
http://>IP_DO_SERVIDOR<:5000
```

---

**Passo 4 — Preparar o sistema para o AdGuard Home**

<div align="justify">
O Debian vem com o <code>systemd-resolved</code> ativo, ocupando a porta 53. O AdGuard Home em modo HOST precisa assumir essa porta exclusivamente. O script abaixo desativa essa trava de forma limpa.
</div>

```bash
bash -c "$(wget -qLO - https://raw.githubusercontent.com/bigbeartechworld/big-bear-scripts/master/generate-adguard-home-config/run.sh)"
```

---

**Passo 5 — Instalar o AdGuard Home pelo CasaOS**

1. No painel do CasaOS, clique em `App Store`
2. Busque por `AdGuard Home (HOST)`
3. Clique para instalar e em seguida clique em `Next Steps`

> ⁉️ O aviso sobre execução de script no terminal deve ter sido resolvido no passo anterior. Se o instalador ainda reportar erro na porta 53, execute o script novamente.

---

**Passo 6 — Reiniciar o servidor**

```bash
sudo reboot
```

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left">Acesso ao CasaOS</td>
    <td align="left"><code>http://>IP_DO_SERVIDOR<:5000</code> abre o painel normalmente</td>
  </tr>
  <tr>
    <td align="left">AdGuard Home visível</td>
    <td align="left">Container com status <strong>Running</strong> no CasaOS</td>
  </tr>
</table>
</div>

</details>
</details>

---

<details>
  <summary>📌 EP 02 — Segurança</summary>

### EP 02 — Segurança

**Pré-requisitos:**

> - EP 01 concluído — Debian instalado, Conexão SSH estabelecida, CasaOS operacional

---

**Visão Geral:**

<div align="center">
<table>
  <tr>
    <th align="center">Etapa</th>
    <th align="center">Ferramenta</th>
    <th align="center">Função</th>
  </tr>
  <tr>
    <td align="left"><a href="#ep02-etapa1">AdGuard Home</a></td>
    <td align="left">AdGuard Home</td>
    <td align="left">Configura filtragem DNS, listas de bloqueio e cache para toda a rede.</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep02-etapa2">Firewall UFW</a></td>
    <td align="left">UFW</td>
    <td align="left">Define política de deny-all e abre apenas as portas necessárias.</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep02-etapa3">Nginx + CrowdSec</a></td>
    <td align="left">Nginx Proxy Manager + CrowdSec</td>
    <td align="left">Proxy reverso com SSL e detecção/bloqueio automático de intrusos.</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep02-etapa4">Tailscale</a></td>
    <td align="left">Tailscale</td>
    <td align="left">VPN WireGuard gerenciada para acesso remoto seguro sem expor portas.</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep02-etapa5">Antivírus e Auditoria</a></td>
    <td align="left">ClamAV + Lynis</td>
    <td align="left">Varredura antivírus agendada e auditoria de hardening do sistema.</td>
  </tr>
</table>
</div>

---

**Convenções Utilizadas Neste Documento**

<div align="justify">
Este guia utiliza variáveis de template representadas pelo formato >NOME_DA_VARIAVEL<. Sempre que encontrar uma delas em comandos, arquivos de configuração ou exemplos, substitua pelo valor correspondente ao seu ambiente antes de prosseguir.
</div>

> ⚠️ Quando uma etapa exigir atenção especial a essa substituição, um aviso como este será exibido.

<div align="center">
<table>
  <tr>
    <th align="center">Variável</th>
    <th align="center">Descrição</th>
  </tr>
  <tr>
    <td align="left"><code>>IP_DO_SERVIDOR<</code></td>
    <td align="left">Endereço IP local fixo atribuído ao servidor na rede interna.</td>
  </tr>
  <tr>
    <td align="left"><code>>SEU_DOMINIO<</code></td>
    <td align="left">Domínio próprio utilizado para os Proxy Hosts do NPM.</td>
  </tr>
  <tr>
    <td align="left"><code>>SEU_USUARIO<</code></td>
    <td align="left">Nome do usuário comum utilizado para administração do sistema.</td>
  </tr>
  <tr>
    <td align="left"><code>>IP_TAILSCALE<</code></td>
    <td align="left">IP virtual atribuído ao servidor pelo Tailscale (formato 100.x.x.x).</td>
  </tr>
  <tr>
    <td align="left"><code>>NOME_SERVIDOR<</code></td>
    <td align="left">Alias configurado no SSH config do Windows.</td>
  </tr>
</table>
</div>

---

### Etapas Documentadas

<details id="ep02-etapa1">
  <summary>🪨 Etapa 1 — AdGuard Home (Configuração Definitiva)</summary>

**Passo 1 — Ajustar portas no CasaOS**

<div align="justify">
O AdGuard Home precisa de dois ajustes de porta antes de ser configurado: a interface web deve rodar na porta 3000, e o servidor DNS interno deve usar a porta 3001 (liberando a 80 para o Nginx Proxy Manager).
</div>

1. No painel do CasaOS, clique nos três pontinhos do AdGuard Home → `Configurações`
2. Verifique se o campo `Web UI` está na porta `:3000`. Corrija se necessário e salve.

**Passo 2 — Instalador inicial**

1. Siga o assistente de instalação
2. Quando perguntar a porta de escuta, troque `80` para `3001`
3. Crie usuário e senha

**Passo 3 — Listas de bloqueio de DNS**

<div align="justify">
Vá em <code>Filtros → Listas de bloqueio de DNS → Adicionar lista de bloqueio → Escolher na lista</code> e marque as seguintes:
</div>

- `AdAways Default Blocklist`
- `Phishing URL Blocklist (PhishTank and OpenPhish)`
- `Dandelion Sprout's Anti-Malware List`
- `Phishing Army`
- `ShadowWhisperer's Malware List`
- `The Big List of Hacked Malware Web Sites`

**Passo 4 — Apontar o DNS do roteador para o AdGuard**

1. Acesse o painel do roteador → seção `DHCP`
2. Substitua o `DNS Primário` pelo IP do servidor
3. Deixe o `DNS Secundário` em branco
4. Salve e aplique

> ⚠️ Com o DNS Secundário em branco, se o servidor for desligado toda a rede perde resolução de nomes. Para manutenções, adicione temporariamente `1.1.1.1` como secundário e remova após religar.

**Passo 5 — Configurações gerais**

<div align="justify">
Acesse <code>Configurações → Configurações Gerais</code> e ajuste os parâmetros abaixo:
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Parâmetro</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Tamanho do cache</td>
    <td align="left"><code>4194304</code> (4 MB)</td>
  </tr>
  <tr>
    <td align="left">TTL mínimo</td>
    <td align="left"><code>300</code> segundos (5 minutos)</td>
  </tr>
  <tr>
    <td align="left">Logs de consultas</td>
    <td align="left"><code>24 horas</code></td>
  </tr>
  <tr>
    <td align="left">Estatísticas</td>
    <td align="left"><code>24 horas</code></td>
  </tr>
</table>
</div>

> 💡 O TTL mínimo de 300s garante que domínios já visitados sejam resolvidos diretamente do cache local, eliminando a latência do DNS upstream para consultas repetidas.

**Passo 6 — Servidores DNS upstream**

<div align="justify">
Acesse <code>Configurações → Configurações de DNS</code> e substitua os servidores upstream por:
</div>

```
https://cloudflare-dns.com/dns-query
https://dns.google/dns-query
1.1.1.1
```

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>nslookup google.com >IP_DO_SERVIDOR<</code></td>
    <td align="left">Retorna resposta válida com endereço IP resolvido</td>
  </tr>
</table>
</div>

</details>

---

<details id="ep02-etapa2">
  <summary>🪨 Etapa 2 — Firewall de Perímetro (UFW)</summary>

**Passo 1 — Configurar as regras**

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 80/tcp comment 'HTTP - renovacao de certificados e redirect HTTPS'
sudo ufw allow 443/tcp comment 'HTTPS - trafego criptografado via Nginx Proxy Manager'
sudo ufw allow 5000/tcp comment 'CasaOS - painel de gerenciamento'
sudo ufw allow 2242/tcp
sudo ufw enable
```

> ⚠️ A regra da porta `2242` sem restrição de interface é temporária. Ela será substituída pela regra exclusiva do Tailscale no Bloco 4.

**Passo 2 — Port Forwarding no roteador**

<div align="justify">
No painel do roteador, crie regras de redirecionamento de porta para expor apenas os serviços web na internet pública.
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Porta externa</th>
    <th align="center">Protocolo</th>
    <th align="center">IP de destino</th>
    <th align="center">Porta interna</th>
  </tr>
  <tr>
    <td align="left"><code>80</code></td>
    <td align="left">TCP</td>
    <td align="left"><code>>IP_DO_SERVIDOR<</code></td>
    <td align="left"><code>80</code></td>
  </tr>
  <tr>
    <td align="left"><code>443</code></td>
    <td align="left">TCP</td>
    <td align="left"><code>>IP_DO_SERVIDOR<</code></td>
    <td align="left"><code>443</code></td>
  </tr>
</table>
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>sudo ufw status</code></td>
    <td align="left">Regras listadas com status <code>active</code></td>
  </tr>
</table>
</div>

</details>

---

<details id="ep02-etapa3">
  <summary>🪨 Etapa 3 — Nginx Proxy Manager e CrowdSec</summary>

**Passo 1 — Instalar o Nginx Proxy Manager**

1. No CasaOS, abra a `App Store` e pesquise por `Nginx Proxy Manager`
2. Clique em `Instalação Personalizada` e verifique o mapeamento de portas:

<div align="center">
<table>
  <tr>
    <th align="center">Porta do Host</th>
    <th align="center">Porta do Container</th>
    <th align="center">Função</th>
  </tr>
  <tr>
    <td align="left"><code>80</code></td>
    <td align="left"><code>80</code></td>
    <td align="left">Tráfego HTTP e validação de certificados Let's Encrypt</td>
  </tr>
  <tr>
    <td align="left"><code>443</code></td>
    <td align="left"><code>443</code></td>
    <td align="left">Tráfego HTTPS criptografado</td>
  </tr>
  <tr>
    <td align="left"><code>81</code></td>
    <td align="left"><code>81</code></td>
    <td align="left">Painel web de administração do NPM</td>
  </tr>
</table>
</div>

3. Clique em `Instalar` e aguarde

**Passo 2 — Primeiro acesso**

> ⚠️ A variável `>IP_DO_SERVIDOR<` deve ser substituída pelo IP do servidor na rede local.

```
http://>IP_DO_SERVIDOR<:81
```

Crie a conta com um e-mail válido (usado para alertas de renovação SSL) e uma senha forte.

**Passo 3 — Criar um Proxy Host**

<div align="justify">
No menu superior, vá em <code>Hosts → Proxy Hosts → Add Proxy Host</code>. Exemplo de configuração para o CasaOS:
</div>

> ⚠️ A variável `>SEU_DOMINIO<` deve ser substituída pelo seu domínio próprio.

<div align="center">
<table>
  <tr>
    <th align="center">Campo</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Domain Names</td>
    <td align="left"><code>casaos.>SEU_DOMINIO<</code></td>
  </tr>
  <tr>
    <td align="left">Scheme</td>
    <td align="left"><code>http</code></td>
  </tr>
  <tr>
    <td align="left">Forward Name/IP</td>
    <td align="left"><code>>IP_DO_SERVIDOR<</code></td>
  </tr>
  <tr>
    <td align="left">Forward Port</td>
    <td align="left"><code>5000</code></td>
  </tr>
</table>
</div>

Marque `Block Common Exploits` e `Websockets Support`. Clique em `Save`.

**Passo 4 — Teste local do Proxy Host**

<div align="justify">
Antes de apontar o DNS real, valide o Proxy Host localmente editando o arquivo <code>hosts</code> do Windows. Abra o Bloco de Notas como Administrador e abra o arquivo:
</div>

```
C:\Windows\System32\drivers\etc\hosts
```

Adicione a linha:

```
>IP_DO_SERVIDOR<    casaos.>SEU_DOMINIO<
```

Acesse `http://casaos.>SEU_DOMINIO<` em aba anônima para validar. Remova a linha após confirmar.

**Passo 5 — Instalar o CrowdSec (Agente)**

```bash
curl -s https://packagecloud.io/install/repositories/crowdsec/crowdsec/script.deb.sh | sudo bash
sudo rm /etc/apt/sources.list.d/crowdsec_crowdsec.list
sudo apt update
sudo apt install crowdsec -y
```

> 💡 O repositório do packagecloud é removido logo após a instalação pois não oferece suporte ao Debian 13 (Trixie). O pacote já estará instalado corretamente.

```bash
sudo systemctl status crowdsec
```

**Passo 6 — Instalar o Bouncer**

<div align="justify">
O pacote do bouncer não está disponível via apt para Debian 13. A instalação é feita via tarball oficial do GitHub.
</div>

```bash
wget https://github.com/crowdsecurity/cs-firewall-bouncer/releases/download/v0.0.34/crowdsec-firewall-bouncer.tgz
tar xzvf crowdsec-firewall-bouncer.tgz
cd crowdsec-firewall-bouncer-v0.0.34/
sudo ./install.sh
```

Quando perguntar qual firewall usar, digite `iptables`.

```bash
sudo systemctl status crowdsec-firewall-bouncer
```

**Passo 7 — Instalar coleções de detecção**

```bash
sudo cscli hub update
sudo cscli collections install crowdsecurity/sshd --force
sudo cscli collections install crowdsecurity/nginx
sudo cscli collections install crowdsecurity/base-http-scenarios
sudo systemctl restart crowdsec
sudo cscli hub list | grep -E "sshd|nginx|base-http"
```

> ⁉️ As três coleções devem aparecer com status `✔️ enabled`. Se alguma não aparecer, reexecute o comando de instalação individual.

**Passo 8 — Apontar o CrowdSec para os logs do NPM**

```bash
sudo mkdir -p /etc/crowdsec/acquis.d
sudo nano /etc/crowdsec/acquis.d/npm.yaml
```

Cole o conteúdo abaixo e salve com `Ctrl+O`, `Enter`, `Ctrl+X`:

```yaml
filenames:
  - /DATA/AppData/nginx-proxy-manager/data/logs/*.log
  - /DATA/AppData/nginx-proxy-manager/data/logs/proxy-host-*_access.log
  - /DATA/AppData/nginx-proxy-manager/data/logs/proxy-host-*_error.log
labels:
  type: nginx
```

```bash
sudo systemctl restart crowdsec
```

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>sudo cscli bouncers list</code></td>
    <td align="left">Bouncer listado como autenticado</td>
  </tr>
  <tr>
    <td align="left">Teste de banimento manual</td>
    <td align="left">IP de teste aparece no ipset após <code>decisions add</code></td>
  </tr>
  <tr>
    <td align="left"><code>systemctl status crowdsec</code></td>
    <td align="left"><code>active (running)</code></td>
  </tr>
  <tr>
    <td align="left"><code>systemctl status crowdsec-firewall-bouncer</code></td>
    <td align="left"><code>active (running)</code></td>
  </tr>
</table>
</div>

</details>

---

<details id="ep02-etapa4">
  <summary>🪨 Etapa 4 — Tailscale</summary>

**Passo 1 — Instalar e autenticar**

```bash
sudo apt install tailscale -y
sudo systemctl status tailscaled
sudo tailscale up
```

<div align="justify">
Uma URL será exibida no terminal. Abra no navegador, faça login com sua conta Tailscale e autorize o dispositivo.
</div>

**Passo 2 — Obter o IP virtual**

```bash
tailscale ip -4
```

> ⚠️ Anote o IP retornado (formato `100.x.x.x`) — ele é o `>IP_TAILSCALE<` usado nos passos seguintes.

**Passo 3 — Atrelar SSH à interface Tailscale**

```bash
sudo ufw allow in on tailscale0 to any port 2242 proto tcp comment 'SSH - apenas via tunel Tailscale'
```

**Passo 4 — Testar conexão pelo Tailscale**

Sem fechar o terminal atual, abra um segundo terminal e teste:

> ⚠️ As variáveis `>SEU_USUARIO<` e `>IP_TAILSCALE<` devem ser substituídas pelos valores do seu ambiente.

```powershell
ssh -p 2242 >SEU_USUARIO<@>IP_TAILSCALE<
```

**Passo 5 — Atualizar o SSH config no Windows**

> ⚠️ As variáveis `>NOME_SERVIDOR<`, `>IP_TAILSCALE<` e `>SEU_USUARIO<` devem ser substituídas pelos valores do seu ambiente.

```
Host >NOME_SERVIDOR<
    HostName >IP_TAILSCALE<
    User >SEU_USUARIO<
    Port 2242
    IdentityFile C:\Users\Admin\.ssh\id_ed25519
```

**Passo 6 — Remover a regra global de SSH**

```bash
sudo ufw delete allow from 192.168.15.0/24 to any port 2242 proto tcp
sudo ufw delete allow 2242/tcp
sudo ufw status numbered
```

**Estado final esperado do UFW:**

```
[1] 443/tcp                     ALLOW IN    Anywhere
[2] 5000/tcp                    ALLOW IN    Anywhere
[3] 2242/tcp on tailscale0      ALLOW IN    Anywhere
[4] 80/tcp                      ALLOW IN    Anywhere
```

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>ssh >NOME_SERVIDOR<</code> pelo Tailscale</td>
    <td align="left">Conexão estabelecida sem solicitar senha</td>
  </tr>
  <tr>
    <td align="left">SSH pela rede local sem Tailscale</td>
    <td align="left">Conexão recusada — porta 2242 não acessível fora do túnel</td>
  </tr>
  <tr>
    <td align="left"><code>sudo ufw status</code></td>
    <td align="left">Porta 2242 visível apenas na interface <code>tailscale0</code></td>
  </tr>
</table>
</div>

</details>

---

<details id="ep02-etapa5">
  <summary>🪨 Etapa 5 — Antivírus e Auditoria de Segurança</summary>
 
**Passo 1 — ClamAV — Instalação e atualização do banco de definições**
 
```bash
sudo apt install clamav clamav-daemon -y
 
sudo systemctl stop clamav-freshclam
sudo freshclam
sudo systemctl start clamav-freshclam
```
 
Verifique:
 
```bash
sudo systemctl status clamav-freshclam
```
 
Deve retornar `active (running)` com os três bancos `up-to-date`:
- `daily.cvd`
- `main.cvd`
- `bytecode.cvd`
> ℹ️ O aviso `Clamd was NOT notified: Can't connect to clamd` é esperado e inofensivo — o daemon em tempo real (`clamd`) não é usado neste setup. A varredura é feita via cron, sem impacto de memória contínuo.
 
---
 
**Passo 2 — ClamAV — Teste de funcionamento**
 
Baixe um arquivo de teste padrão da indústria (inofensivo — apenas uma assinatura conhecida):
 
```bash
curl -o /tmp/eicar.txt https://www.eicar.org/download/eicar.com.txt
sudo clamscan /tmp/eicar.txt
```
 
O retorno deve conter:
 
```
/tmp/eicar.txt: Eicar-Signature FOUND
```
 
Remova o arquivo de teste:
 
```bash
rm /tmp/eicar.txt
```
 
---
 
**Passo 3 — ClamAV — Script de varredura diária**
 
```bash
sudo nano /usr/local/bin/clamav-scan.sh
```
 
Cole o conteúdo:
 
```bash
#!/bin/bash
LOG="/var/log/clamav/scan-$(date +%Y-%m-%d).log"
PASTAS="/DATA/Storage/Media"
 
echo "=== Varredura ClamAV - $(date) ===" >> "$LOG"
sudo clamscan --recursive --infected --log="$LOG" $PASTAS
echo "=== Fim da varredura ===" >> "$LOG"
```
 
Salve com `Ctrl+O`, `Enter`, `Ctrl+X` e torne o script executável:
 
```bash
sudo chmod +x /usr/local/bin/clamav-scan.sh
```
 
---
 
**Passo 4 — ClamAV — Agendar varredura via Cron (diariamente às 3h)**
 
```bash
sudo crontab -e
```
 
Na primeira execução, escolha o editor `1` (nano). Adicione ao final do arquivo:
 
```
0 3 * * * /usr/local/bin/clamav-scan.sh
```
 
Salve e confirme que foi registrado:
 
```bash
sudo crontab -l
```
 
---
 
**Passo 5 — Lynis — Auditoria de segurança**
 
#### Instalação
 
```bash
sudo apt install lynis -y
```
 
#### Primeira auditoria
 
```bash
sudo lynis audit system
```
 
A varredura leva alguns minutos e ao final exibe um **Hardening index** (nota de 0 a 100), warnings e sugestões de melhoria.
 
---
 
**Passo 6 — Correções aplicadas com base no relatório Lynis**
 
#### Pacotes de segurança adicionais
 
```bash
sudo apt install needrestart debsums apt-show-versions libpam-tmpdir -y
```
 
<div align="center">
<table>
  <tr>
    <th align="center">Pacote</th>
    <th align="center">Função</th>
  </tr>
  <tr>
    <td align="left"><code>needrestart</code></td>
    <td align="left">Avisa quais serviços precisam ser reiniciados após atualizações</td>
  </tr>
  <tr>
    <td align="left"><code>debsums</code></td>
    <td align="left">Verifica integridade dos arquivos de pacotes instalados</td>
  </tr>
  <tr>
    <td align="left"><code>apt-show-versions</code></td>
    <td align="left">Exibe quais pacotes têm atualizações disponíveis</td>
  </tr>
  <tr>
    <td align="left"><code>libpam-tmpdir</code></td>
    <td align="left">Isola o <code>/tmp</code> por sessão de usuário, impedindo leitura cruzada entre processos</td>
  </tr>
</table>
</div>
 
#### Endurecimento do SSH (SSH-7408)
 
```bash
sudo nano /etc/ssh/sshd_config
```
 
Localize e altere com `Ctrl+W`:
 
<div align="center">
<table>
  <tr>
    <th align="center">Parâmetro</th>
    <th align="center">De</th>
    <th align="center">Para</th>
  </tr>
  <tr>
    <td align="left"><code>AllowTcpForwarding</code></td>
    <td align="left"><code>yes</code></td>
    <td align="left"><code>no</code></td>
  </tr>
  <tr>
    <td align="left"><code>ClientAliveCountMax</code></td>
    <td align="left"><code>3</code></td>
    <td align="left"><code>2</code></td>
  </tr>
  <tr>
    <td align="left"><code>LogLevel</code></td>
    <td align="left"><code>INFO</code></td>
    <td align="left"><code>VERBOSE</code></td>
  </tr>
  <tr>
    <td align="left"><code>MaxAuthTries</code></td>
    <td align="left"><code>6</code></td>
    <td align="left"><code>3</code></td>
  </tr>
  <tr>
    <td align="left"><code>MaxSessions</code></td>
    <td align="left"><code>10</code></td>
    <td align="left"><code>2</code></td>
  </tr>
  <tr>
    <td align="left"><code>TCPKeepAlive</code></td>
    <td align="left"><code>yes</code></td>
    <td align="left"><code>no</code></td>
  </tr>
  <tr>
    <td align="left"><code>X11Forwarding</code></td>
    <td align="left"><code>yes</code></td>
    <td align="left"><code>no</code></td>
  </tr>
  <tr>
    <td align="left"><code>AllowAgentForwarding</code></td>
    <td align="left"><code>yes</code></td>
    <td align="left"><code>no</code></td>
  </tr>
  </table>
</div>
 
Salve e reinicie:
 
```bash
sudo systemctl restart ssh
```
 
> ⚠️ Teste a conexão SSH em um segundo terminal antes de fechar o terminal atual.
 
---
 
**Passo 7 — Sugestões do Lynis ignoradas intencionalmente**
 
<div align="center">
<table>
  <tr>
    <th align="center">Código</th>
    <th align="center">Sugestão</th>
    <th align="center">Motivo para ignorar</th>
  </tr>
  <tr>
    <td align="left"><code>BOOT-5122</code></td>
    <td align="left">Senha no GRUB</td>
    <td align="left">Só relevante com acesso físico malicioso ao servidor</td>
  </tr>
  <tr>
    <td align="left"><code>FILE-6310</code></td>
    <td align="left">/home e /var em partições separadas</td>
    <td align="left">Exige reparticionar o disco — risco alto, ganho baixo</td>
  </tr>
  <tr>
    <td align="left"><code>USB-1000</code></td>
    <td align="left">Desativar USB</td>
    <td align="left">O SSD do sistema usa USB 3.0 — desativar quebraria o boot</td>
  </tr>
  <tr>
    <td align="left"><code>AUTH-9262</code></td>
    <td align="left">Política de força de senha</td>
    <td align="left">Irrelevante — acesso é feito exclusivamente via chave SSH</td>
  </tr>
  <tr>
    <td align="left"><code>LOGG-2154</code></td>
    <td align="left">Logging para host externo</td>
    <td align="left">Válido no futuro com mais serviços, desnecessário agora</td>
  </tr>
  <tr>
    <td align="left"><code>ACCT-9622/9626/9628</code></td>
    <td align="left">auditd / sysstat</td>
    <td align="left">Overhead desnecessário no Celeron N2840</td>
  </tr>
</table>
</div>
 
---

</details>

### Resumo de Segurança — O que está protegido
 
<div align="center">
<table>
  <tr>
    <th align="center">Camada</th>
    <th align="center">Ferramenta</th>
    <th align="center">Função</th>
  </tr>
  <tr>
    <td align="left">DNS</td>
    <td align="left">AdGuard Home</td>
    <td align="left">Bloqueia anúncios, malware e phishing na rede inteira</td>
  </tr>
  <tr>
    <td align="left">Firewall de borda</td>
    <td align="left">UFW</td>
    <td align="left">Nega todo tráfego de entrada não autorizado</td>
  </tr>
  <tr>
    <td align="left">Proxy reverso</td>
    <td align="left">Nginx Proxy Manager</td>
    <td align="left">Único ponto de entrada público, com SSL</td>
  </tr>
  <tr>
    <td align="left">Detecção de intrusos</td>
    <td align="left">CrowdSec (agente)</td>
    <td align="left">Analisa logs do SSH e Nginx em tempo real</td>
  </tr>
  <tr>
    <td align="left">Bloqueio automático</td>
    <td align="left">CrowdSec (bouncer)</td>
    <td align="left">Injeta IPs maliciosos no iptables automaticamente</td>
  </tr>
  <tr>
    <td align="left">Acesso remoto seguro</td>
    <td align="left">Tailscale</td>
    <td align="left">SSH e painel acessíveis de qualquer lugar sem expor portas</td>
  </tr>
  <tr>
    <td align="left">Antivírus</td>
    <td align="left">ClamAV</td>
    <td align="left">Varredura diária agendada na pasta de mídia e downloads</td>
  </tr>
  <tr>
    <td align="left">Auditoria</td>
    <td align="left">Lynis</td>
    <td align="left">Verifica falhas de configuração e permissões do sistema</td>
  </tr>
</table>
</div>

</details>


---

<details>
  <summary>📌 EP 03 — Mídia e Downloads</summary>

### EP 03 — Mídia e Downloads

**Pré-requisitos:**

> - Episódio 1 e 2 concluídos — CasaOS, Conexão SSH e Firewall UFW configurados

---

**Visão Geral**

<div align="center">
<table>
  <tr>
    <th align="center">Etapa</th>
    <th align="center">Ferramenta</th>
    <th align="center">Função</th>
  </tr>
  <tr>
    <td align="left"><a href="#ep03-etapa1">Estrutura de Pastas</a></td>
    <td align="left">Terminal</td>
    <td align="left">Estrutura dos diretórios dos arquivos, ajustado com permissões</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep03-etapa2">Jellyfin</a></td>
    <td align="left">CasaOS App Store</td>
    <td align="left">Servidor de mídia — filmes, séries, livros</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep03-etapa3">qBittorrent</a></td>
    <td align="left">CasaOS App Store</td>
    <td align="left">Cliente de torrent com WebUI</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep03-etapa4">Rede Docker (arrstack)</a></td>
    <td align="left">Terminal</td>
    <td align="left">Rede Docker dedicada comunicação interna entre os serviços</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep03-etapa5">Radarr</a></td>
    <td align="left">CasaOS App Store</td>
    <td align="left">Gerenciador automático de filmes</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep03-etapa6">Sonarr</a></td>
    <td align="left">CasaOS App Store</td>
    <td align="left">Gerenciador automático de séries</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep03-etapa7">Bazarr</a></td>
    <td align="left">CasaOS App Store</td>
    <td align="left">Download automático de legendas</td>  
  </tr>
  <tr>
    <td align="left"><a href="#ep03-etapa8">Samba</a></td>
    <td align="left">Terminal (apt)</td>
    <td align="left">Compartilhamento de arquivos na rede</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep03-etapa9">Stirling-PDF</a></td>
    <td align="left">CasaOS App Store</td>
    <td align="left">Processamento de PDFs — OCR, juntar, dividir</td></code></td> 
  </tr>
</table>
</div>

---

**Convenções Utilizadas Neste Documento**

<div align="justify">
Este guia utiliza variáveis de template representadas pelo formato >NOME_DA_VARIAVEL<. Sempre que encontrar uma delas em comandos, arquivos de configuração ou exemplos, substitua pelo valor correspondente ao seu ambiente antes de prosseguir.
</div>

> ⚠️ Quando uma etapa exigir atenção especial a essa substituição, um aviso como este será exibido.

<div align="center">
<table>
  <tr>
    <th align="center">Variável</th>
    <th align="center">Descrição</th>
  </tr>
  <tr>
    <td align="left"><code>>IP_TAILSCALE<</code></td>
    <td align="left">IP virtual atribuído ao servidor pelo Tailscale (formato 100.x.x.x).</td>
  </tr>
  <tr>
    <td align="left"><code>>IP_DO_SERVIDOR<</code></td>
    <td align="left">Endereço IP local fixo atribuído ao servidor na rede interna.</td>
  </tr>
</table>
</div>

---

### Etapas Documentadas

<details id="ep03-etapa1">
  <summary>🪨 Etapa 1 — Estrutura de Pastas</summary>

**Por que Downloads dentro de Media?**

<div align="justify">
O Radarr e o Sonarr fazem hardlink dos arquivos baixados para as pastas de destino. O hardlink só funciona se origem e destino estiverem na mesma partição. Mantendo Downloads dentro de Media, o arquivo de 10GB continua ocupando 10GB — não 20GB como ocorreria com uma cópia convencional.
</div>

**Passo 1 — Criar estrutura de diretórios**

```bash
mkdir -p /DATA/Storage/Media/{Filmes,Series,Livros,Mangas,Downloads/{completos,incompletos}}
mkdir -p /DATA/Storage/Media/Pessoal-Anderson
mkdir -p /DATA/Storage/Media/Pessoal-Samira
```

**Passo 2 — Ajustar permissões**

```bash
chmod -R 775 /DATA/Storage/Media
chown -R root:root /DATA/Storage/Media
```

**Estrutura final**

```
/DATA/Storage/
└── Media/
    ├── Filmes/
    ├── Series/
    ├── Livros/
    ├── Mangas/
    ├── Pessoal-Anderson/
    ├── Pessoal-Samira/
    └── Downloads/
        ├── completos/
        └── incompletos/
```

**Validação**

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>ls -R /DATA/Storage/Media</code></td>
    <td align="left">Todas as pastas listadas corretamente</td>
  </tr>
</table>
</div>

</details>

<details id="ep03-etapa2">
  <summary>🪨 Etapa 2 — Jellyfin</summary>

**Passo 1 — Instalar via CasaOS**

<div align="justify">
No CasaOS, acesse a App Store, busque por Jellyfin e clique em instalação personalizada e configure os volumes antes de instalar:
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Host</th>
    <th align="center">Container</th>
  </tr>
  <tr>
    <td align="left"><code>/DATA/Storage/Media</code></td>
    <td align="left"><code>/media</code></td>
  </tr>
  <tr>
    <td align="left"><code>/DATA/AppData/Jellyfin/config</code></td>
    <td align="left"><code>/config</code></td>
  </tr>
  <tr>
    <td align="left"><code>/DATA/AppData/Jellyfin/cache</code></td>
    <td align="left"><code>/cache</code></td>
  </tr>
</table>
</div>

> ⚠️ Se aparecer o volume `/opt/vc/lib` pré-configurado, remova — é exclusivo para Raspberry Pi.

> 💡 O CasaOS atribuiu a porta `8097` pois a `8096` já estava em uso. Acesse em `>IP_DO_SERVIDOR<:8097`.

**Passo 2 — Setup inicial e bibliotecas**

<div align="justify">
No assistente de configuração, crie o usuário admin e adicione as bibliotecas abaixo. Deixe todas as outras opções no padrão — o Radarr e Sonarr gerenciam metadados e organização.
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Biblioteca</th>
    <th align="center">Tipo</th>
    <th align="center">Caminho no container</th>
  </tr>
  <tr>
    <td align="left">Filmes</td>
    <td align="left">Filmes</td>
    <td align="left"><code>/media/Filmes</code></td>
  </tr>
  <tr>
    <td align="left">Séries</td>
    <td align="left">Séries</td>
    <td align="left"><code>/media/Series</code></td>
  </tr>
  <tr>
    <td align="left">Livros</td>
    <td align="left">Livros</td>
    <td align="left"><code>/media/Livros</code></td>
  </tr>
  <tr>
    <td align="left">Mangás</td>
    <td align="left">Livros</td>
    <td align="left"><code>/media/Mangas</code></td>
  </tr>
</table>
</div>

**Passo 3 — Forçar Direct Play (Painel → Reprodução → Transcodificação)**

<div align="justify">
O Celeron N2840 não possui capacidade para transcodificação em tempo real. Configurar threads para 2 limita o uso da CPU ao número real de núcleos físicos. O objetivo principal é garantir que todos os arquivos sejam reproduzidos via Direct Play, nunca via transcodificação.
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Opção</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Aceleração de hardware</td>
    <td align="left"><code>Nenhum</code></td>
  </tr>
  <tr>
    <td align="left">Permitir codificação HEVC</td>
    <td align="left">❌ Desativado</td>
  </tr>
  <tr>
    <td align="left">Permitir codificação AV1</td>
    <td align="left">❌ Desativado</td>
  </tr>
  <tr>
    <td align="left">Contagem de threads da transcodificação</td>
    <td align="left"><code>2</code></td>
  </tr>
</table>
</div>

> 💡 O codec ideal para Direct Play é **H.264 + AAC** — compatível nativamente com praticamente todos os clientes modernos.

> ⚠️ Não ative VA-API ou QSV no N2840 — o suporte é instável nessa geração de hardware e pode causar mais problemas do que ganhos.

**Passo 4 — Desativar Trickplay (Painel → Reprodução → Trickplay)**

<div align="justify">
O Trickplay gera miniaturas de prévia ao passar o mouse na barra de progresso. No Celeron, esse processo consome CPU e disco de forma desnecessária.
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Opção</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Comportamento do Escaneamento</td>
    <td align="left"><code>Desativado</code></td>
  </tr>
  <tr>
    <td align="left">Tarefas de processamento FFmpeg</td>
    <td align="left"><code>1</code></td>
  </tr>
</table>
</div>

**Passo 5 — Criar usuário externo (Painel → Usuários → Adicionar Usuário)**

<div align="center">
<table>
  <tr>
    <th align="center">Campo</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Nome</td>
    <td align="left"><code>Samira</code></td>
  </tr>
  <tr>
    <td align="left">Senha</td>
    <td align="left"><code>[SENHA_SAMIRA_JELLYFIN]</code></td>
  </tr>
  <tr>
    <td align="left">Acesso às bibliotecas</td>
    <td align="left">Filmes, Séries (conforme desejado)</td>
  </tr>
</table>
</div>

> 💡 Acesso via Tailscale: `http://>IP_TAILSCALE_DO_SERVIDOR<:8097` — funciona pelo navegador ou pelo app Jellyfin.

**Validação**

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left">Acessar <code>http://192.168.15.5:8097</code></td>
    <td align="left">Tela de login do Jellyfin</td>
  </tr>
  <tr>
    <td align="left">Reproduzir um arquivo de vídeo</td>
    <td align="left">Reprodução via Direct Play sem transcodificação</td>
  </tr>
  <tr>
    <td align="left">Acessar via IP Tailscale</td>
    <td align="left">Login e reprodução funcionando remotamente</td>
  </tr>
</table>
</div>

</details>

<details id="ep03-etapa3">
  <summary>🪨 Etapa 3 — qBittorrent</summary>

**Passo 1 — Instalar qBittorrent via CasaOS**

<div align="justify">
No CasaOS, acesse a App Store, busque por qBittorrente e clique em instalação personalizada e configure os volumes da seguinte maneira antes de instalar:
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Host</th>
    <th align="center">Container</th>
  </tr>
  <tr>
    <td align="left"><code>/DATA/AppData/qBittorrent/config</code></td>
    <td align="left"><code>/config</code></td>
  </tr>
  <tr>
    <td align="left"><code>/DATA/Storage/Media/Downloads</code></td>
    <td align="left"><code>/downloads</code></td>
  </tr>
</table>
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Porta Host</th>
    <th align="center">Porta Container</th>
  </tr>
  <tr>
    <td align="left"><code>8181</code></td>
    <td align="left"><code>8080</code></td>
  </tr>
</table>
</div>

> 💡 A senha inicial está nos logs do container no CasaOS. Após o primeiro login, troque imediatamente.

**Passo 2 — Aba Downloads (Ferramentas → Opções → Downloads)**

<div align="center">
<table>
  <tr>
    <th align="center">Opção</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Caminho de salvamento padrão</td>
    <td align="left"><code>/downloads/completos</code></td>
  </tr>
  <tr>
    <td align="left">Manter torrents incompletos em</td>
    <td align="left"><code>/downloads/incompletos</code></td>
  </tr>
  <tr>
    <td align="left">Manter torrents incompletos (checkbox)</td>
    <td align="left">✅ Ativado</td>
  </tr>
  <tr>
    <td align="left">Condição para parada do torrent</td>
    <td align="left"><code>Nenhum</code></td>
  </tr>
  <tr>
    <td align="left">Pré-alocar espaço em disco</td>
    <td align="left">✅ Ativado</td>
  </tr>
  <tr>
    <td align="left">Adicionar extensão .!qB aos arquivos incompletos</td>
    <td align="left">✅ Ativado</td>
  </tr>
  <tr>
    <td align="left">Apagar arquivos .torrent posteriormente</td>
    <td align="left">❌ Desativado</td>
  </tr>
</table>
</div>

**Passo 3 — Aba BitTorrent**

<div align="center">
<table>
  <tr>
    <th align="center">Opção</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">DHT</td>
    <td align="left">✅ Ativado</td>
  </tr>
  <tr>
    <td align="left">Troca de peers</td>
    <td align="left">✅ Ativado</td>
  </tr>
  <tr>
    <td align="left">Quando a proporção alcançar</td>
    <td align="left">✅ Ativado → <code>1</code></td>
  </tr>
  <tr>
    <td align="left">Quando o tempo total de semeadura for atingido</td>
    <td align="left">✅ Ativado → <code>60</code> minutos</td>
  </tr>
  <tr>
    <td align="left">Então</td>
    <td align="left"><code>Parar torrent</code></td>
  </tr>
</table>
</div>

> ⚠️ Use `Parar torrent` e não `Remover` — o Radarr/Sonarr precisam gerenciar a remoção após importarem o arquivo.

**Passo 4 — Aba Interface Web**

<div align="center">
<table>
  <tr>
    <th align="center">Opção</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Ignorar autenticação para clientes no localhost</td>
    <td align="left">✅ Ativado</td>
  </tr>
  <tr>
    <td align="left">Ignorar autenticação para clientes na sub-rede</td>
    <td align="left">✅ Ativado → <code>192.168.15.0/24</code></td>
  </tr>
  <tr>
    <td align="left">Habilitar HTTPS</td>
    <td align="left">❌ Desativado</td>
  </tr>
</table>
</div>

**Passo 5 — Aba Avançado (cache e modo E/S)**

<div align="justify">
Fixar o cache de disco evita estouro de memória e uso agressivo de swap no Celeron. Desativar o cache do sistema em leitura e escrita impede duplicação de cache entre o qBittorrent e o kernel Linux — o qBittorrent gerencia o cache ele mesmo dentro do limite fixado.
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Opção</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Cache de disco (MB)</td>
    <td align="left"><code>256</code></td>
  </tr>
  <tr>
    <td align="left">Modo de leitura de E/S do disco</td>
    <td align="left"><code>Desativar cache do sistema</code></td>
  </tr>
  <tr>
    <td align="left">Modo de escrita de E/S do disco</td>
    <td align="left"><code>Desativar cache do sistema</code></td>
  </tr>
  <tr>
    <td align="left">Threads de E/S assíncronos</td>
    <td align="left"><code>4</code></td>
  </tr>
</table>
</div>

> 💡 O N2840 tem 2 núcleos físicos. Reduzir threads de 10 para 4 evita competição com o sistema operacional e outros containers.

**Passo 6 — Aba Velocidade (agendamento de banda)**

<div align="justify">
O agendamento libera 100% da velocidade na madrugada (02:00–06:00) e aplica limites durante o dia para preservar o chip Wi-Fi e o Celeron. Os valores de limite serão definidos após medição da velocidade real da conexão.
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Opção</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Programar o uso de limites de velocidade alternativos</td>
    <td align="left">✅ Ativado</td>
  </tr>
  <tr>
    <td align="left">De</td>
    <td align="left"><code>06:00</code></td>
  </tr>
  <tr>
    <td align="left">Até</td>
    <td align="left"><code>02:00</code></td>
  </tr>
  <tr>
    <td align="left">Dias</td>
    <td align="left"><code>Todos os dias</code></td>
  </tr>
  <tr>
    <td align="left">Download alternativo</td>
    <td align="left"><code>[LIMITE_DOWNLOAD_KB]</code> — a definir</td>
  </tr>
  <tr>
    <td align="left">Upload alternativo</td>
    <td align="left"><code>[LIMITE_UPLOAD_KB]</code> — a definir</td>
  </tr>
</table>
</div>

**Validação**

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left">Acessar <code>http://>IP_DO_SERVIDOR<:8181</code></td>
    <td align="left">Interface do qBittorrent carrega</td>
  </tr>
  <tr>
    <td align="left">Adicionar um torrent de teste</td>
    <td align="left">Download inicia em <code>/downloads/incompletos</code></td>
  </tr>
  <tr>
    <td align="left">Download concluído</td>
    <td align="left">Arquivo move para <code>/downloads/completos</code></td>
  </tr>
</table>
</div>

</details>

<details id="ep03-etapa4">
  <summary>🪨 Etapa 4 — Rede Docker (arrstack)</summary>

**Por que criar uma rede dedicada?**

<div align="justify">
Containers Docker não conseguem se comunicar entre si usando o IP da rede local (ex: 192.168.15.5). É necessário criar uma rede Docker dedicada para que cada container receba um IP interno fixo e se comunique diretamente com os demais containers da mesma rede.
</div>

**Passo 1 — Criar a rede**

```bash
docker network create arrstack
```

**Passo 2 — Conectar todos os containers**

```bash
docker network connect arrstack qbittorrent
docker network connect arrstack radarr
docker network connect arrstack sonarr
docker network connect arrstack bazarr
```

> ⚠️ Novos containers que precisem se comunicar com os existentes devem ser conectados da mesma forma após a instalação.

**Passo 3 — Verificar IPs atribuídos**

```bash
docker network inspect arrstack
```

<div align="center">
<table>
  <tr>
    <th align="center">Container</th>
    <th align="center">IP interno</th>
    <th align="center">Porta interna</th>
  </tr>
  <tr>
    <td align="left">qBittorrent</td>
    <td align="left"><code>172.19.0.2</code></td>
    <td align="left"><code>8080</code></td>
  </tr>
  <tr>
    <td align="left">Radarr</td>
    <td align="left"><code>172.19.0.3</code></td>
    <td align="left"><code>7878</code></td>
  </tr>
  <tr>
    <td align="left">Sonarr</td>
    <td align="left"><code>172.19.0.4</code></td>
    <td align="left"><code>8989</code></td>
  </tr>
  <tr>
    <td align="left">Bazarr</td>
    <td align="left"><code>172.19.0.5</code></td>
    <td align="left"><code>6767</code></td>
  </tr>
</table>
</div>

> 💡 Dentro da rede `arrstack`, sempre use a porta interna do container. Por exemplo, para o qBittorrent use `172.19.0.2:8080` e não `192.168.15.5:8181`.

**Validação**

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>docker network inspect arrstack</code></td>
    <td align="left">Todos os containers listados com seus IPs</td>
  </tr>
  <tr>
    <td align="left"><code>docker exec -it radarr curl -v http://172.19.0.2:8080</code></td>
    <td align="left">Resposta HTTP 200 OK da interface do qBittorrent</td>
  </tr>
</table>
</div>

</details>

<details id="ep03-etapa5">
  <summary>🪨 Etapa 5 — Radarr</summary>

**Passo 1 — Instalar via CasaOS** 

<div align="justify">
No CasaOS, acesse a App Store, busque por Radarr e clique em instalação personalizada e configure os volumes da seguinte maneira antes de instalar:
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Host</th>
    <th align="center">Container</th>
  </tr>
  <tr>
    <td align="left"><code>/DATA/AppData/Radarr/config</code></td>
    <td align="left"><code>/config</code></td>
  </tr>
  <tr>
    <td align="left"><code>/DATA/Storage/Media</code></td>
    <td align="left"><code>/media</code></td>
  </tr>
</table>
</div>

> ⚠️ Mapeie `/Media` inteiro (não só `/Filmes`) — o Radarr precisa acessar tanto `/Filmes` quanto `/Downloads` para fazer o hardlink.

**Passo 2 — Conectar à rede arrstack**

```bash
docker network connect arrstack radarr
```

**Passo 3 — Configurar autenticação (Settings → General)**

<div align="center">
<table>
  <tr>
    <th align="center">Opção</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Authentication</td>
    <td align="left"><code>Forms (Login Page)</code></td>
  </tr>
  <tr>
    <td align="left">Username</td>
    <td align="left"><code>[USUARIO_RADARR]</code></td>
  </tr>
  <tr>
    <td align="left">Password</td>
    <td align="left"><code>[SENHA_RADARR]</code></td>
  </tr>
</table>
</div>

**Passo 4 — Configurar pasta raiz (Settings → Media Management → Root Folders)**

```
/media/Filmes
```

**Passo 5 — Configurar cliente de download (Settings → Download Clients → Add)**

<div align="center">
<table>
  <tr>
    <th align="center">Opção</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Nome</td>
    <td align="left"><code>qBittorrent</code></td>
  </tr>
  <tr>
    <td align="left">Host</td>
    <td align="left"><code>172.19.0.2</code></td>
  </tr>
  <tr>
    <td align="left">Port</td>
    <td align="left"><code>8080</code></td>
  </tr>
  <tr>
    <td align="left">Username</td>
    <td align="left"><code>admin</code></td>
  </tr>
  <tr>
    <td align="left">Password</td>
    <td align="left"><code>[SENHA_QBITTORRENT]</code></td>
  </tr>
  <tr>
    <td align="left">Category</td>
    <td align="left"><code>radarr</code></td>
  </tr>
</table>
</div>

> 💡 Clique em `Test` — deve aparecer ✅ verde — depois em `Save`.

**Validação**

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left">Settings → Download Clients → Test</td>
    <td align="left">✅ verde — conexão com qBittorrent OK</td>
  </tr>
  <tr>
    <td align="left">Settings → Media Management → Root Folders</td>
    <td align="left"><code>/media/Filmes</code> listado</td>
  </tr>
</table>
</div>

</details>

<details id="ep03-etapa6">
  <summary>🪨 Etapa 6 — Sonarr</summary>

**Passo 1 — Instalar via CasaOS**

<div align="justify">
No CasaOS, acesse a App Store, busque por Sonarr e clique em instalação personalizada e configure os volumes da seguinte maneira antes de instalar:
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Host</th>
    <th align="center">Container</th>
  </tr>
  <tr>
    <td align="left"><code>/DATA/AppData/Sonarr/config</code></td>
    <td align="left"><code>/config</code></td>
  </tr>
  <tr>
    <td align="left"><code>/DATA/Storage/Media</code></td>
    <td align="left"><code>/media</code></td>
  </tr>
</table>
</div>

**Passo 2 — Conectar à rede arrstack**

```bash
docker network connect arrstack sonarr
```

**Passo 3 — Configurar autenticação, pasta raiz e cliente de download**

<div align="justify">
Repita exatamente o mesmo processo do Radarr (Passos 3, 4 e 5), com as seguintes diferenças:
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Opção</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Root Folder</td>
    <td align="left"><code>/media/Series</code></td>
  </tr>
  <tr>
    <td align="left">Category (qBittorrent)</td>
    <td align="left"><code>sonarr</code></td>
  </tr>
</table>
</div>

**Passo 4 — Adicionar séries existentes (Series → Add New → Add Existing)**

<div align="justify">
Para séries que já estão nas pastas mas não foram baixadas pelo Sonarr, use a opção de adicionar séries existentes. O Sonarr reconhece automaticamente os arquivos já presentes na pasta.
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Opção</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Root Folder</td>
    <td align="left"><code>/media/Series</code></td>
  </tr>
  <tr>
    <td align="left">Quality Profile</td>
    <td align="left"><code>HD-1080p</code></td>
  </tr>
  <tr>
    <td align="left">Monitor</td>
    <td align="left"><code>All Episodes</code></td>
  </tr>
  <tr>
    <td align="left">Search for missing episodes</td>
    <td align="left">❌ Desativado</td>
  </tr>
</table>
</div>

> 💡 O Bazarr reconhece automaticamente as séries adicionadas ao Sonarr e inicia a busca por legendas.

</details>

<details id="ep03-etapa7">
  <summary>🪨 Etapa 7 — Bazarr</summary>

**Passo 1 — Instalar via CasaOS**

<div align="justify">
No CasaOS, acesse a App Store, busque por Bazarr e clique em instalação personalizada e configure os volumes da seguinte maneira antes de instalar:
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Host</th>
    <th align="center">Container</th>
  </tr>
  <tr>
    <td align="left"><code>/DATA/AppData/Bazarr/config</code></td>
    <td align="left"><code>/config</code></td>
  </tr>
  <tr>
    <td align="left"><code>/DATA/Storage/Media</code></td>
    <td align="left"><code>/media</code></td>
  </tr>
</table>
</div>

**Passo 2 — Conectar à rede arrstack**

```bash
docker network connect arrstack bazarr
```

**Passo 3 — Conectar ao Radarr (Settings → Radarr)**

<div align="center">
<table>
  <tr>
    <th align="center">Opção</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Enabled</td>
    <td align="left">✅ Ativado</td>
  </tr>
  <tr>
    <td align="left">Host</td>
    <td align="left"><code>172.19.0.3</code></td>
  </tr>
  <tr>
    <td align="left">Port</td>
    <td align="left"><code>7878</code></td>
  </tr>
  <tr>
    <td align="left">Base URL</td>
    <td align="left">deixar em branco</td>
  </tr>
  <tr>
    <td align="left">API Key</td>
    <td align="left"><code>[API_KEY_RADARR]</code></td>
  </tr>
</table>
</div>

> 💡 API Key do Radarr: `Settings → General → API Key`.

**Passo 4 — Conectar ao Sonarr (Settings → Sonarr)**

<div align="center">
<table>
  <tr>
    <th align="center">Opção</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Enabled</td>
    <td align="left">✅ Ativado</td>
  </tr>
  <tr>
    <td align="left">Host</td>
    <td align="left"><code>172.19.0.4</code></td>
  </tr>
  <tr>
    <td align="left">Port</td>
    <td align="left"><code>8989</code></td>
  </tr>
  <tr>
    <td align="left">Base URL</td>
    <td align="left">deixar em branco</td>
  </tr>
  <tr>
    <td align="left">API Key</td>
    <td align="left"><code>[API_KEY_SONARR]</code></td>
  </tr>
</table>
</div>

**Passo 5 — Adicionar provedores de legenda (Settings → Providers)**

<div align="center">
<table>
  <tr>
    <th align="center">Provedor</th>
    <th align="center">Para quê</th>
  </tr>
  <tr>
    <td align="left">OpenSubtitles.com</td>
    <td align="left">Legendas internacionais e PT-BR</td>
  </tr>
  <tr>
    <td align="left">Legendasdivx</td>
    <td align="left">Legendas PT-BR</td>
  </tr>
</table>
</div>

**Passo 6 — Configurar idioma (Settings → Languages → Add New Profile)**

<div align="center">
<table>
  <tr>
    <th align="center">Campo</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Name</td>
    <td align="left"><code>Português BR</code></td>
  </tr>
  <tr>
    <td align="left">Language</td>
    <td align="left"><code>Portuguese (Brazil)</code></td>
  </tr>
  <tr>
    <td align="left">Subtitles Type</td>
    <td align="left"><code>Normal or hearing-impaired</code></td>
  </tr>
  <tr>
    <td align="left">Search only when...</td>
    <td align="left"><code>Always</code></td>
  </tr>
</table>
</div>

<div align="justify">
Na seção Default Language Profiles For Newly Added Shows, ative o perfil Português BR para Series e Movies.
</div>

**Buscar legendas manualmente**

<div align="justify">
Para séries já existentes, acesse `Series` no menu lateral, clique na série e depois em `Search → Search All Episodes`. Se as legendas estiverem fora de sincronia, clique no ícone de pessoa (👤) no episódio para buscar uma versão diferente.
</div>

**Validação**

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left">Settings → Radarr → Test</td>
    <td align="left">✅ verde</td>
  </tr>
  <tr>
    <td align="left">Settings → Sonarr → Test</td>
    <td align="left">✅ verde</td>
  </tr>
  <tr>
    <td align="left">Series → [Série] → episódios</td>
    <td align="left">Ícone PB (Português BR) nos episódios</td>
  </tr>
</table>
</div>

</details>

<details id="ep03-etapa8">
  <summary>🪨 Etapa 8 — Samba</summary>

**Passo 1 — Instalar o Samba via terminal**

```bash
apt update && apt install samba smbclient -y
```

**Passo 2 — Backup da configuração original**

```bash
cp /etc/samba/smb.conf /etc/samba/smb.conf.bak
```

**Passo 3 — Configurar smb.conf**

```bash
nano /etc/samba/smb.conf
```

Substitua todo o conteúdo por:

```ini
[global]
   workgroup = WORKGROUP
   server string = Legacy NAS
   netbios name = legacy-server
   server role = standalone server
   security = user
   map to guest = bad user
   dns proxy = no
   log file = /var/log/samba/log.%m
   max log size = 1000
   logging = file
   panic action = /usr/share/samba/panic-action %d
   obey pam restrictions = yes
   unix password sync = yes
   passwd program = /usr/bin/passwd %u
   passwd chat = *Enter\snew\s*\spassword:* %n\n *Retype\snew\s*\spassword:* %n\n *password\supdated\ssuccessfully* .
   pam password change = yes
   min protocol = SMB2
   max protocol = SMB3
   socket options = TCP_NODELAY IPTOS_LOWDELAY
   ea support = yes
   vfs objects = catia fruit streams_xattr
   fruit:metadata = stream
   fruit:model = MacSamba
   fruit:posix_rename = yes
   fruit:zero_file_id = yes

[Media]
   path = /DATA/Storage/Media
   browseable = yes
   writable = yes
   guest ok = no
   valid users = anderson samira
   create mask = 0775
   directory mask = 0775
   force group = users
```

> 💡 As opções `vfs objects = catia fruit streams_xattr` e as diretivas `fruit:` são necessárias para compatibilidade de escrita com iOS via app Arquivos.

**Passo 4 — Criar usuários**

```bash
# Criar usuário samira no sistema (sem acesso ao shell)
useradd -M -s /sbin/nologin samira

# Criar senhas Samba
smbpasswd -a anderson
smbpasswd -a samira
```

**Passo 5 — Testar e iniciar**

```bash
# Testar configuração
testparm

# Iniciar e habilitar na inicialização
systemctl enable smbd nmbd
systemctl start smbd nmbd
```

**Passo 6 — Acesso pelo Windows/Mac**

```
\\[IP_TAILSCALE_DO_SERVIDOR]
```

**Passo 7 — Acesso pelo iOS (app Arquivos)**

<div align="justify">
Com o Tailscale ativo no iPhone, abra o app Arquivos, toque em ··· (canto superior direito) → Conectar ao Servidor.
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Campo</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Endereço</td>
    <td align="left"><code>smb://[IP_TAILSCALE_DO_SERVIDOR]</code></td>
  </tr>
  <tr>
    <td align="left">Usuário</td>
    <td align="left"><code>anderson</code> ou <code>samira</code></td>
  </tr>
  <tr>
    <td align="left">Senha</td>
    <td align="left">senha definida no <code>smbpasswd</code></td>
  </tr>
</table>
</div>

**Passo 8 — Acesso externo para a Samira via Tailscale**

<div align="justify">
A Samira instala o Tailscale no dispositivo dela em tailscale.com/download. Você a adiciona à rede pelo painel em login.tailscale.com. Após a conexão, ela acessa o NAS exatamente como se estivesse na rede local, usando o IP Tailscale do servidor.
</div>

**Validação**

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>testparm</code></td>
    <td align="left"><code>Loaded services file OK</code> sem erros</td>
  </tr>
  <tr>
    <td align="left"><code>smbclient -L localhost -U anderson</code></td>
    <td align="left">Compartilhamento <code>Media</code> listado</td>
  </tr>
  <tr>
    <td align="left">Acessar via Windows Explorer</td>
    <td align="left">Pasta Media visível e acessível</td>
  </tr>
  <tr>
    <td align="left">Acessar via app Arquivos no iOS</td>
    <td align="left">Pasta Media visível com suporte a escrita</td>
  </tr>
</table>
</div>

</details>

<details id="ep03-etapa9">
  <summary>🪨 Etapa 9 — Stirling-PDF</summary>

**Sobre o Stirling-PDF**

<div align="justify">
O Stirling-PDF é uma suíte completa de processamento de arquivos PDF — permite juntar, dividir, aplicar OCR, proteger com senha e muito mais, tudo via interface web. Futuramente será integrado ao LibreOffice Headless para conversão de arquivos .docx e .xlsx diretamente para PDF, formando uma suíte completa de processamento de documentos sob demanda.
</div>

**Passo 1 — Instalar via CasaOS App Store**

<div align="justify">
No CasaOS, acesse a App Store, busque por Stirling-PDF e clique em instalação personalizada e configure os volumes da seguinte maneira antes de instalar:
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Host</th>
    <th align="center">Container</th>
  </tr>
  <tr>
    <td align="left"><code>/opt/AppData/StirlingPDF/config</code></td>
    <td align="left"><code>/configs</code></td>
  </tr>
  <tr>
    <td align="left"><code>/opt/AppData/StirlingPDF/logs</code></td>
    <td align="left"><code>/logs</code></td>
  </tr>
  <tr>
    <td align="left"><code>/opt/AppData/StirlingPDF/training</code></td>
    <td align="left"><code>/usr/share/tessdata</code></td>
  </tr>
</table>
</div>

> ⁉️ A integração completa com LibreOffice Headless e a configuração de OCR em português serão documentadas em episódio futuro.

</details>
</details>

---

<details>
  <summary>📌 EP 04 — A Área de Lazer</summary>

### EP 04 — A Área de Lazer

**Pré-requisitos:**

> - EP 01, 02 e 03 concluídos
> - Nginx Proxy Manager operacional com domínio configurado
> - Sistema de Arquivos montado e acessível

---

**Visão Geral:**

<div align="center">
<table>
  <tr>
    <th align="center">Etapa</th>
    <th align="center">Ferramenta</th>
    <th align="center">Função</th>
  </tr>
  <tr>
    <td align="left"><a href="#ep04-etapa1">Biblioteca de Mangás</a></td>
    <td align="left">Suwayomi-Server + Byparr</td>
    <td align="left">Servidor de mangás com suporte a extensões, acessível via Paperback e Aidoku no iOS.</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep04-etapa2">Servidores Minecraft</a></td>
    <td align="left">Crafty Controller</td>
    <td align="left">Painel de gerenciamento para servidores Minecraft Java e Bedrock simultâneos.</td>
  </tr>
</table>
</div>

---

**Convenções Utilizadas Neste Documento**

<div align="justify">
Este guia utiliza variáveis de template representadas pelo formato >NOME_DA_VARIAVEL<. Sempre que encontrar uma delas em comandos, arquivos de configuração ou exemplos, substitua pelo valor correspondente ao seu ambiente antes de prosseguir.
</div>

> ⚠️ Quando uma etapa exigir atenção especial a essa substituição, um aviso como este será exibido.

<div align="center">
<table>
  <tr>
    <th align="center">Variável</th>
    <th align="center">Descrição</th>
  </tr>
  <tr>
    <td align="left"><code>>IP_DO_SERVIDOR<</code></td>
    <td align="left">Endereço IP local fixo atribuído ao servidor na rede interna.</td>
  </tr>
  <tr>
    <td align="left"><code>>IP_PUBLICO<</code></td>
    <td align="left">Endereço IP público fornecido pelo provedor de internet.</td>
  </tr>
  <tr>
    <td align="left"><code>>SEU_USUARIO<</code></td>
    <td align="left">Nome do usuário comum utilizado para administração do sistema.</td>
  </tr>
  <tr>
    <td align="left"><code>>NICK_DO_JOGADOR<</code></td>
    <td align="left">Nome de usuário utilizado dentro do Minecraft.</td>
  </tr>
  <tr>
    <td align="left"><code>>SEU_SUBDOMINIO_SUWAYOMI<</code></td>
    <td align="left">Subdomínio configurado no Nginx Proxy Manager para acesso ao Suwayomi.</td>
  </tr>
  <tr>
    <td align="left"><code>>CAMINHO_STORAGE<</code></td>
    <td align="left">Diretório onde seu armazenamento principal está montado.</td>
  </tr>
</table>
</div>

---

### Etapas Documentadas

<details id="ep04-etapa1">
  <summary>🪨 Etapa 1 — Suwayomi-Server</summary>

<div align="justify">
O Suwayomi-Server é um servidor de mangás que roda localmente. Ele funciona como o backend do Tachiyomi/Mihon, mas hospedado no seu próprio servidor: em vez de acessar sites cheios de anúncios, o Paperback ou Aidoku no iPhone consultam diretamente o seu servidor, que faz o acesso e entrega o conteúdo de forma limpa. É possível também adicionar mangás manualmente à biblioteca.
</div>

> ⁉️ O Suwayomi-Server não está disponível na App Store do CasaOS. Todo o deploy é feito por linha de comando.

**Passo 1 — Criar a estrutura de pastas**

<div align="justify">
Conecte ao servidor via SSH e eleve para root antes de prosseguir.
</div>

> ⚠️ A variável `>CAMINHO_STORAGE<` deve ser substituída pelo diretório raiz do armazenamento montado no seu servidor.

```bash
su -
mkdir -p /DATA/AppData/suwayomi/data
mkdir -p >CAMINHO_STORAGE</Media/Mangas
```

> 💡 O parâmetro `-p` cria todos os diretórios intermediários de uma vez e não retorna erro caso os diretórios já existam.

---

**Passo 2 — Criar o docker-compose.yml**

> ⚠️ A variável `>CAMINHO_STORAGE<` deve ser substituída pelo diretório raiz do armazenamento. Os mangás baixados serão armazenados nesse caminho.

```bash
cat > /DATA/AppData/suwayomi/docker-compose.yml << 'EOF'
name: suwayomi
services:
    suwayomi:
        command: []
        container_name: suwayomi
        environment:
            EXTENSION_REPOS: '["https://raw.githubusercontent.com/keiyoushi/extensions/repo/index.min.json"]'
            PGID: "1000"
            PUID: "1000"
            TZ: America/Sao_Paulo
        hostname: suwayomi
        image: ghcr.io/suwayomi/tachidesk:latest
        labels:
            icon: https://github.com/Suwayomi/Tachidesk/raw/master/server/src/main/resources/icon/faviconlogo.png
        networks:
            default: null
        ports:
            - mode: ingress
              target: 4567
              published: "4567"
              protocol: tcp
        restart: unless-stopped
        volumes:
            - type: bind
              source: /DATA/AppData/suwayomi/data
              target: /home/suwayomi/.local/share/Tachidesk
              bind:
                create_host_path: true
            - type: bind
              source: >CAMINHO_STORAGE</Media/Mangas
              target: /home/suwayomi/.local/share/Tachidesk/downloads
              bind:
                create_host_path: true
    byparr:
        container_name: byparr
        image: ghcr.io/thephaseless/byparr:latest
        environment:
            - TZ=America/Sao_Paulo
            - LOG_LEVEL=info
        networks:
            default: null
        restart: unless-stopped
networks:
    default:
        name: suwayomi_default
EOF
```

> 💡 O Byparr foi incluído no mesmo compose para garantir que ambos os containers estejam na mesma rede Docker (`suwayomi_default`), permitindo comunicação interna pelo nome do container sem expor a porta 8191 externamente. O repositório Keiyoushi é o único com schema compatível com o Suwayomi — outros repositórios como o Ubeca usam um formato diferente que o Suwayomi não reconhece.

---

**Passo 3 — Corrigir permissões**

<div align="justify">
As pastas foram criadas como root, mas o container roda como o usuário de UID 1000. Sem essa correção, o container não consegue escrever e entra em loop de reinicialização.
</div>

> ⚠️ A variável `>CAMINHO_STORAGE<` deve ser substituída pelo diretório raiz do armazenamento utilizado no seu servidor.

```bash
chown -R 1000:1000 /DATA/AppData/suwayomi/data
chown -R 1000:1000 >CAMINHO_STORAGE</Media/Mangas
```

---

**Passo 4 — Subir os containers**

```bash
cd /DATA/AppData/suwayomi
docker compose up -d
docker ps | grep -E "suwayomi|byparr"
```

> ⁉️ O Byparr pode aparecer com status `health: starting` por até 2 minutos enquanto o Chromium interno inicializa. Aguarde antes de concluir que há erro.

---

**Passo 5 — Configurar o Byparr no server.conf**

<div align="justify">
O Byparr resolve desafios Cloudflare usando um Chromium headless real. Sem ele, sites com proteção Cloudflare retornam erro ao carregar capítulos.
</div>

```bash
nano /DATA/AppData/suwayomi/data/server.conf
```

Localize o bloco `# Cloudflare` e ajuste os valores diretamente nas linhas existentes:

```
# Cloudflare
server.flareSolverrEnabled = true
server.flareSolverrUrl = "http://byparr:8191/v1"
server.flareSolverrTimeout = 60
server.flareSolverrSessionName = "suwayomi"
server.flareSolverrSessionTtl = 15
server.flareSolverrAsResponseFallback = false
```

> ⚠️ Não adicione linhas novas ao final do arquivo. O `server.conf` já contém esse bloco com valores padrão, edite diretamente as linhas existentes. Duplicatas fazem o Suwayomi ignorar as alterações.

Salve com `Ctrl+O`, `Enter`, `Ctrl+X` e reinicie:

```bash
cd /DATA/AppData/suwayomi
docker compose restart suwayomi
```

---

**Passo 6 — Acessar o painel e instalar extensões**

> ⚠️ A variável `>IP_DO_SERVIDOR<` deve ser substituída pelo IP do servidor na rede local.

```
http://>IP_DO_SERVIDOR<:4567
```

No painel, vá em `Extensions → All` e instale as extensões desejadas.

---

**Passo 7 — Configurar Proxy Host no NPM**

<div align="justify">
No painel do Nginx Proxy Manager, vá em <code>Hosts → Proxy Hosts → Add Proxy Host</code> e preencha:
</div>

> ⚠️ A variável `>SEU_SUBDOMINIO_SUWAYOMI<` deve ser substituída pelo subdomínio que você deseja usar (ex: `mangas.seudominio.com`). A variável `>IP_DO_SERVIDOR<` deve ser substituída pelo IP do servidor.

<div align="center">
<table>
  <tr>
    <th align="center">Campo</th>
    <th align="center">Valor</th>
  </tr>
  <tr>
    <td align="left">Domain Names</td>
    <td align="left"><code>>SEU_SUBDOMINIO_SUWAYOMI<</code></td>
  </tr>
  <tr>
    <td align="left">Scheme</td>
    <td align="left"><code>http</code></td>
  </tr>
  <tr>
    <td align="left">Forward Hostname/IP</td>
    <td align="left"><code>>IP_DO_SERVIDOR<</code></td>
  </tr>
  <tr>
    <td align="left">Forward Port</td>
    <td align="left"><code>4567</code></td>
  </tr>
</table>
</div>

Na aba `SSL`, selecione o certificado Let's Encrypt e marque `Force SSL`. Clique em `Save`.

---

**Passo 8 — Conectar o leitor iOS**

**No Paperback:**
1. Abra o app → `Settings` → `Servers`
2. Toque em `+` e insira: `https://>SEU_SUBDOMINIO_SUWAYOMI<`

**No Aidoku:**
1. Abra o app → `Browse` → ícone de engrenagem
2. Adicione a URL: `https://>SEU_SUBDOMINIO_SUWAYOMI<`

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>docker ps</code></td>
    <td align="left">Containers <code>suwayomi</code> e <code>byparr</code> com status <strong>Up</strong></td>
  </tr>
  <tr>
    <td align="left">Acesso ao painel</td>
    <td align="left"><code>http://>IP_DO_SERVIDOR<:4567</code> abre normalmente</td>
  </tr>
  <tr>
    <td align="left">Extensões visíveis</td>
    <td align="left">Lista de fontes disponível em <code>Extensions → All</code></td>
  </tr>
  <tr>
    <td align="left">Logs do Byparr</td>
    <td align="left"><code>docker logs byparr --tail 20</code> exibe <code>Uvicorn running on http://0.0.0.0:8191</code></td>
  </tr>
</table>
</div>

---
</details>

<details id="ep04-etapa2">
  <summary>🪨 Etapa 2 — Servidores de Minecraft</summary>

<div align="justify">
Dois servidores rodando simultaneamente, gerenciados pelo Crafty Controller. As portas são expostas diretamente na internet pública via Port Forwarding, por isso a whitelist está ativada nos dois servidores.
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Servidor</th>
    <th align="center">Porta</th>
    <th align="center">Protocolo</th>
    <th align="center">Para quem</th>
  </tr>
  <tr>
    <td align="left">Minecraft Bedrock (última versão)</td>
    <td align="left"><code>19132</code></td>
    <td align="left">UDP</td>
    <td align="left">Celular, console, Windows 10/11</td>
  </tr>
  <tr>
    <td align="left">Minecraft Java Paper 1.20.1</td>
    <td align="left"><code>25565</code></td>
    <td align="left">TCP</td>
    <td align="left">PC — Java Edition</td>
  </tr>
</table>
</div>

---

**Passo 1 — Instalar o Crafty Controller pelo CasaOS**

> ⚠️ A variável `>IP_DO_SERVIDOR<` deve ser substituída pelo IP do servidor na rede local.

1. No CasaOS, abra a `App Store`
2. Pesquise por `Crafty` e clique em `Install`

Após a instalação, acesse: `http://>IP_DO_SERVIDOR<:8443`

---

**Passo 2 — Criar a estrutura de pastas no Storage**

```bash
mkdir -p /DATA/Storage/Minecraft/Bedrock
mkdir -p /DATA/Storage/Minecraft/Java
```

> 💡 Mundos, plugins e arquivos de jogo ficam no Storage. As configurações de runtime do Crafty ficam no SSD em `/DATA/AppData/crafty/`.

---

**Passo 3 — Criar o servidor Bedrock no Crafty**

1. Acesse `http://>IP_DO_SERVIDOR<:8443` e faça login
2. Clique em `New Server` → `Minecraft Bedrock`
3. Configure:
   - **Server Version:** `Latest`
   - **Server Directory:** `/DATA/Storage/Minecraft/Bedrock`
   - **Max Players:** `8`
4. Clique em `Create Server` e aguarde o download

---

**Passo 4 — Criar o servidor Java no Crafty**

1. Clique em `New Server` → `Minecraft Java`
2. Configure:
   - **Server Type:** `Paper`
   - **Server Version:** `1.20.1`
   - **Server Directory:** `/DATA/Storage/Minecraft/Java`
   - **Max RAM:** `2048` MB
   - **Max Players:** `8`
3. Clique em `Create Server` e aguarde

> 💡 Com 8 GB de RAM total e vários outros serviços ativos, 2 GB para o servidor Java é um valor seguro e ajustável conforme necessidade.

---

**Passo 5 — Ativar whitelist nos dois servidores**

**No servidor Java**, pelo console do Crafty:

```
whitelist on
whitelist add >NICK_DO_JOGADOR<
```

**No servidor Bedrock**, edite o `server.properties`:

```bash
nano /DATA/Storage/Minecraft/Bedrock/server.properties
```

Localize e ajuste:

```
white-list=true
```

Em seguida, adicione o jogador ao arquivo de whitelist:

```bash
nano /DATA/Storage/Minecraft/Bedrock/whitelist.json
```

```json
[
  {
    "ignoresPlayerLimit": false,
    "name": ">NICK_DO_JOGADOR<",
    "xuid": ""
  }
]
```

> 💡 O campo `xuid` pode ficar vazio, o Bedrock preenche automaticamente quando o jogador se conectar pela primeira vez. Se a whitelist não funcionar via IP local, desative temporariamente o `online-mode` no `server.properties` para capturar o xuid na primeira conexão, depois reative.

---

**Passo 6 — Configurar Port Forwarding no roteador**

> ⚠️ A variável `>IP_DO_SERVIDOR<` deve ser substituída pelo IP local do servidor.

<div align="center">
<table>
  <tr>
    <th align="center">Nome da Regra</th>
    <th align="center">Protocolo</th>
    <th align="center">Porta Externa</th>
    <th align="center">Porta Interna</th>
    <th align="center">IP Interno</th>
  </tr>
  <tr>
    <td align="left">Minecraft Java</td>
    <td align="left">TCP</td>
    <td align="left"><code>25565</code></td>
    <td align="left"><code>25565</code></td>
    <td align="left"><code>>IP_DO_SERVIDOR<</code></td>
  </tr>
  <tr>
    <td align="left">Minecraft Bedrock</td>
    <td align="left">UDP</td>
    <td align="left"><code>19132</code></td>
    <td align="left"><code>19132</code></td>
    <td align="left"><code>>IP_DO_SERVIDOR<</code></td>
  </tr>
</table>
</div>

> ⚠️ O Bedrock usa protocolo UDP, não TCP. Confirme o dropdown correto antes de salvar a regra no roteador.

---

**Passo 7 — Descobrir o IP público**

```bash
curl -4 ifconfig.me
```

<div align="justify">
O endereço retornado é o IP público do servidor. Repasse para seus amigos conforme o servidor:
</div>

<div align="center">
<table>
  <tr>
    <th align="center">Servidor</th>
    <th align="center">Endereço de conexão</th>
  </tr>
  <tr>
    <td align="left">Java</td>
    <td align="left"><code>>IP_PUBLICO<:25565</code></td>
  </tr>
  <tr>
    <td align="left">Bedrock</td>
    <td align="left"><code>>IP_PUBLICO<:19132</code></td>
  </tr>
</table>
</div>

> ⚠️ A maioria dos provedores residenciais muda o IP público periodicamente. Se os amigos não conseguirem conectar, execute `curl -4 ifconfig.me` novamente e verifique se o IP mudou. Mas isso não deve ser um problema se você tiver fixado o IP do servidor no episódio 1.

</details>
</details>

---

<details>
  <summary>📌 EP 05 — Otimização</summary>

### EP 05 — Otimização

**Pré-requisitos:**

> - Concluído toda configuração inicial do Debian e CasaOS
> - Ter concluído o passo de segurança, baixando corretamente o ClamAV e Lynis

---

**Visão Geral:**

<div align="center">
<table>
  <tr>
    <th align="center">Etapa</th>
    <th align="center">Ferramenta</th>
    <th align="center">Função</th>
  </tr>
  <tr>
    <td align="left"><a href="#ep05-etapa1">Debloat Crítico</a></td>
    <td align="left">systemd (disable/mask)</td>
    <td align="left">Remove serviços desnecessários e ajusta energia e desligamento.</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep05-etapa2">Tunagem de RAM e Kernel</a></td>
    <td align="left">tmpfs + sysctl + journald</td>
    <td align="left">Otimiza memória, rede e limita o tamanho dos logs.</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep05-etapa3">Manutenção Automatizada</a></td>
    <td align="left">fstrim + cron + Docker</td>
    <td align="left">Agenda TRIM do SSD, limpeza do Docker e demais rotinas.</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep05-etapa4">Central de Alertas Push</a></td>
    <td align="left">ntfy</td>
    <td align="left">Envia notificações de boot, login SSH, disco e temperatura.</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep05-etapa5">Varredura de Segurança</a></td>
    <td align="left">ClamAV + Lynis</td>
    <td align="left">Realiza varredura de malware e auditoria semanal de segurança.</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep05-etapa6">Backup Offsite Criptografado</a></td>
    <td align="left">Rclone + Google Drive</td>
    <td align="left">Envia backup mensal criptografado do AppData para a nuvem.</td>
  </tr>
  <tr>
    <td align="left"><a href="#ep05-etapa7">Atualizações Automáticas</a></td>
    <td align="left">Unattended-Upgrades</td>
    <td align="left">Aplica patches de segurança e reinicia o sistema quando necessário.</td>
  </tr>
</table>
</div>

---

**Convenções Utilizadas Neste Documento**

<div align="justify">
Este guia utiliza variáveis de template representadas pelo formato >NOME_DA_VARIAVEL<. Sempre que encontrar uma delas em comandos, arquivos de configuração ou exemplos, substitua pelo valor correspondente ao seu ambiente antes de prosseguir.
</div>

> ⚠️ Quando uma etapa exigir atenção especial a essa substituição, um aviso como este será exibido.

<div align="center">
<table>
  <tr>
    <th align="center">Variável</th>
    <th align="center">Descrição</th>
  </tr>
  <tr>
    <td align="left"><code>>SEU_TOPICO_NTFY<</code></td>
    <td align="left">Nome do tópico criado no ntfy.sh. Deve ser uma string única e difícil de adivinhar, ex: <code>legacyserver-anderson-x7k2m</code>.</td>
  </tr>
  <tr>
    <td align="left"><code>>IP_NTFY<</code></td>
    <td align="left">IP do servidor ntfy.sh resolvido via DNS. Obtido com <code>nslookup ntfy.sh 8.8.8.8</code>. Necessário pois o DNS local (Tailscale) pode bloquear a resolução direta do hostname.</td>
  </tr>
  <tr>
    <td align="left"><code>>SEU_USUARIO<</code></td>
    <td align="left">Nome do usuário do sistema Linux, ex: <code>anderson</code>.</td>
  </tr>
</table>
</div>

---

### Etapas Documentadas

<details id="ep05-etapa1">
  <summary>🪨 Etapa 1 — Debloat Crítico do Debian 13</summary>

**Passo 1 — Desativar e mascarar o ModemManager**

<div align="justify">
O ModemManager é um serviço responsável por gerenciar modems 3G/4G. Em um servidor fixo conectado por cabo ou Wi-Fi, ele é completamente inútil e consome recursos desnecessários. Além de desativá-lo, ele é mascarado — vinculado ao <code>/dev/null</code> — para que nenhuma dependência futura possa reativá-lo acidentalmente.
</div>

```bash
systemctl disable --now ModemManager.service
systemctl mask ModemManager.service
```

**Passo 2 — Desativar e mascarar o exim4**

<div align="justify">
O exim4 é um servidor de e-mail local. Em um servidor doméstico sem necessidade de envio de e-mails pelo sistema, ele é dispensável. Caso o serviço não esteja instalado, o comando de disable retornará um erro, mas o mask será aplicado normalmente — ambos os comportamentos são corretos.
</div>

```bash
systemctl disable --now exim4.service
systemctl mask exim4.service
```

**Passo 3 — Desativar e mascarar o samba-ad-dc**

<div align="justify">
O samba-ad-dc é o controlador de domínio corporativo do Samba, utilizado em ambientes empresariais com Active Directory. O servidor usa apenas o compartilhamento de arquivos simples do Samba — este serviço é desnecessário e deve ser removido do boot.
</div>

```bash
systemctl disable --now samba-ad-dc.service
systemctl mask samba-ad-dc.service
```

**Passo 4 — Prevenir suspensão e hibernação**

<div align="justify">
Por padrão, o Linux pode suspender ou hibernar a máquina em determinadas condições. Em um servidor que deve estar disponível 24/7, todos os alvos de energia devem ser mascarados permanentemente.
</div>

```bash
systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

**Passo 5 — Configurar comportamento do botão de power e da tampa**

<div align="justify">
O arquivo <code>/etc/systemd/logind.conf</code> controla o comportamento do sistema ao pressionar o botão físico de power e ao fechar a tampa do notebook. Pressionar o botão deve executar um desligamento limpo (desmontando o Storage com segurança), e fechar a tampa não deve suspender o sistema.
</div>

```bash
nano /etc/systemd/logind.conf
```

Localize e ajuste as seguintes linhas:

```ini
HandlePowerKey=poweroff
HandleLidSwitch=ignore
```

Aplique as alterações sem reiniciar:

```bash
systemctl restart systemd-logind
```

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>grep -E "HandlePowerKey|HandleLidSwitch" /etc/systemd/logind.conf</code></td>
    <td align="left">Exibir as duas linhas sem comentário: <code>HandlePowerKey=poweroff</code> e <code>HandleLidSwitch=ignore</code></td>
  </tr>
  <tr>
    <td align="left"><code>systemctl is-masked sleep.target</code></td>
    <td align="left"><code>masked</code></td>
  </tr>
</table>
</div>

</details>

---

<details id="ep05-etapa2">
  <summary>🪨 Etapa 2 — Tunagem de RAM, Kernel e Logs</summary>

**Passo 1 — Montar /tmp na RAM (tmpfs)**

<div align="justify">
Por padrão, o diretório <code>/tmp</code> é criado no disco. Montá-lo na RAM via tmpfs elimina escritas desnecessárias no SSD e acelera operações temporárias. O arquivo de unit do systemd não existe por padrão no Debian 13 Trixie e deve ser criado manualmente.
</div>

```bash
cat > /etc/systemd/system/tmp.mount << 'EOF'
[Unit]
Description=Temporary Directory /tmp
Documentation=man:hier(7)
Before=local-fs.target

[Mount]
What=tmpfs
Where=/tmp
Type=tmpfs
Options=mode=1777,strictatime,nosuid,nodev,size=512M

[Install]
WantedBy=local-fs.target
EOF

systemctl daemon-reload
systemctl enable --now tmp.mount
```

**Passo 2 — Ajustar swappiness e parâmetros de rede do kernel**

<div align="justify">
O valor padrão de <code>vm.swappiness</code> é 60, o que faz o kernel jogar dados para o disco (swap) cedo demais. Com 8 GB de RAM disponíveis, o valor 10 força o uso de swap apenas em situações críticas, preservando a memória física para os containers. Os parâmetros de rede aumentam a capacidade de conexões simultâneas e reduzem o tempo de timeout de conexões encerradas. O parâmetro <code>kernel.panic=10</code> faz o sistema reiniciar automaticamente 10 segundos após um kernel panic, em vez de travar indefinidamente.
</div>

```bash
nano /etc/sysctl.conf
```

Adicione ao final do arquivo:

```ini
vm.swappiness=10
net.core.somaxconn = 1024
net.core.netdev_max_backlog = 5000
net.ipv4.tcp_fin_timeout = 15
kernel.panic = 10
```

Aplique sem reiniciar:

```bash
sysctl -p
```

**Passo 3 — Limitar o tamanho dos logs do systemd**

<div align="justify">
Por padrão, o journald pode crescer indefinidamente e consumir gigabytes do SSD ao longo do tempo. Limitar o tamanho máximo total e o tamanho máximo por arquivo garante que os logs sejam rotacionados automaticamente.
</div>

```bash
nano /etc/systemd/journald.conf
```

Localize e ajuste (ou adicione) na seção `[Journal]`:

```ini
SystemMaxUse=200M
SystemMaxFileSize=20M
```

Aplique:

```bash
systemctl restart systemd-journald
```

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>systemctl status tmp.mount --no-pager</code></td>
    <td align="left"><code>Active: active (mounted)</code> com <code>What: tmpfs</code></td>
  </tr>
  <tr>
    <td align="left"><code>sysctl vm.swappiness</code></td>
    <td align="left"><code>vm.swappiness = 10</code></td>
  </tr>
  <tr>
    <td align="left"><code>grep SystemMaxUse /etc/systemd/journald.conf</code></td>
    <td align="left"><code>SystemMaxUse=200M</code></td>
  </tr>
</table>
</div>

</details>

---
<details id="ep05-etapa3">
  <summary>🪨 Etapa 3 — Rotinas de Manutenção Automatizadas</summary>

**Passo 1 — Ativar o TRIM semanal do SSD**

<div align="justify">
O TRIM notifica o SSD sobre quais blocos de dados não estão mais em uso, permitindo que o controlador do disco os apague antecipadamente. Isso mantém a velocidade de escrita e estende a vida útil do dispositivo. O timer já existe no systemd e precisa apenas ser ativado.
</div>

```bash
systemctl enable --now fstrim.timer
```

**Passo 2 — Criar o script de limpeza do Docker**

<div align="justify">
O Docker acumula imagens antigas, containers parados e volumes órfãos ao longo das semanas. O script abaixo executa a limpeza completa e envia uma notificação push informando quanto espaço foi liberado.
</div>

> ⚠️ Substitua `>SEU_TOPICO_NTFY<` e `>IP_NTFY<` pelos seus valores antes de executar.

```bash
cat > /usr/local/bin/docker-cleanup.sh << 'EOF'
#!/bin/bash

TOPICO=">SEU_TOPICO_NTFY<"
NTFY_IP=">IP_NTFY<"

OUTPUT=$(docker system prune -a --volumes -f 2>&1)
LIBERADO=$(echo "$OUTPUT" | grep "Total reclaimed space" | awk '{print $NF}')

curl -s \
    -H "Title: 🐳 Docker Cleanup OK" \
    -H "Priority: low" \
    -H "Tags: whale" \
    -d "Limpeza semanal concluída. Espaço liberado: ${LIBERADO:-0B}. $(date +%d/%m/%Y)" \
    https://$NTFY_IP/$TOPICO -H "Host: ntfy.sh" -k
EOF

chmod +x /usr/local/bin/docker-cleanup.sh
```

**Passo 3 — Configurar o crontab completo**

<div align="justify">
Todas as rotinas automatizadas são registradas no crontab do root. Os horários foram definidos para evitar sobreposição, respeitando uma janela de 00:00 às 06:00, com o Unattended-Upgrades sempre como última tarefa da noite.
</div>

```bash
crontab -e
```

Configure o crontab com o seguinte conteúdo:

```
# ClamAV + Lynis (domingo 00:00)
0 0 * * 0 /usr/local/bin/clamav-scan.sh

# Docker Cleanup - remove imagens, containers e volumes órfãos (domingo 01:00)
0 1 * * 0 /usr/local/bin/docker-cleanup.sh

# Backup mensal AppData criptografado no Google Drive (dia 1 01:00)
0 1 1 * * /usr/local/bin/backup-rclone.sh

# Alerta quando SSD ou Storage passar de 85% de uso (a cada 1 hora)
0 * * * * /usr/local/bin/monitor-disco.sh

# Alerta quando CPU ultrapassar 75°C (a cada 1 hora)
0 * * * * /usr/local/bin/monitor-temp.sh
```

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>systemctl status fstrim.timer --no-pager</code></td>
    <td align="left"><code>Active: active (waiting)</code> com próximo trigger exibido</td>
  </tr>
  <tr>
    <td align="left"><code>crontab -l | grep -v "^#" | grep -v "^$"</code></td>
    <td align="left">Listar os 5 crons configurados sem linhas em branco</td>
  </tr>
</table>
</div>

</details>

---
<details id="ep05-etapa4">
  <summary>🪨 Etapa 4 — Central de Alertas Push (ntfy)</summary>

**Passo 1 — Instalar o app ntfy no iPhone**

<div align="justify">
O ntfy é um sistema de notificações pub/sub baseado em HTTP puro. Não requer app proprietário pesado. Instale o app <strong>ntfy</strong> (de Philipp Heckel) na App Store e crie uma inscrição com o nome do seu tópico.
</div>

> ⚠️ O tópico funciona como um canal público — qualquer pessoa que souber o nome consegue ler as mensagens. Use um nome longo e aleatório, como `legacyserver-anderson-x7k2m`.

> ⁉️ Após instalar o app, vá em **Configurações → ntfy → Notificações → Permitir Notificações** no iOS para que os alertas apareçam na tela de bloqueio.

**Passo 2 — Adicionar o hostname do ntfy ao /etc/hosts**

<div align="justify">
O DNS local gerenciado pelo Tailscale pode bloquear a resolução do hostname <code>ntfy.sh</code> para conexões HTTPS externas. A solução é fixar o IP diretamente no arquivo <code>/etc/hosts</code>, garantindo que todos os scripts encontrem o servidor sem depender do DNS.
</div>

> ⚠️ O IP abaixo é o IP do servidor ntfy.sh em vigor no momento da configuração. Se os scripts pararem de funcionar no futuro, execute <code>nslookup ntfy.sh 8.8.8.8</code> para obter o IP atualizado e corrija esta linha.

```bash
echo ">IP_NTFY< ntfy.sh" >> /etc/hosts
```

**Passo 3 — Configurar notificação de boot do servidor**

<div align="justify">
Um serviço do systemd dispara uma notificação push toda vez que o servidor é iniciado. Isso permite identificar reinicializações inesperadas causadas por queda de energia, kernel panic ou atualizações automáticas.
</div>

> ⚠️ Substitua `>SEU_TOPICO_NTFY<` e `>IP_NTFY<` pelos seus valores antes de executar.

```bash
cat > /etc/systemd/system/ntfy-boot.service << 'EOF'
[Unit]
Description=Notificação ntfy no boot
After=network-online.target
Wants=network-online.target

[Service]
Type=oneshot
ExecStart=/bin/bash -c 'curl -s -H "Title: 🔄 Servidor Reiniciado" -H "Priority: default" -H "Tags: arrows_counterclockwise" -d "Legacy Server reiniciado em $(date +\"%d/%m/%Y %H:%M\")" https://>IP_NTFY</>SEU_TOPICO_NTFY< -H "Host: ntfy.sh" -k'
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
EOF

systemctl daemon-reload
systemctl enable ntfy-boot.service
systemctl start ntfy-boot.service
```

**Passo 4 — Configurar notificação de login SSH**

<div align="justify">
Toda vez que um usuário autentica com sucesso via SSH, o sistema envia uma notificação push informando o nome do usuário, o IP de origem e o horário do acesso. A integração é feita via PAM, sem necessidade de modificar o sshd.
</div>

> ⚠️ Substitua `>SEU_TOPICO_NTFY<` e `>IP_NTFY<` pelos seus valores antes de executar.

```bash
cat > /usr/local/bin/ntfy-login.sh << 'EOF'
#!/bin/bash

TOPICO=">SEU_TOPICO_NTFY<"
NTFY_IP=">IP_NTFY<"

if [ "$PAM_TYPE" = "open_session" ]; then
    curl -s \
        -H "Title: 🔐 Login SSH: $PAM_USER" \
        -H "Priority: urgent" \
        -H "Tags: key" \
        -d "Usuário $PAM_USER logou no Legacy Server via $PAM_RHOST em $(date +\"%d/%m/%Y %H:%M\")" \
        https://$NTFY_IP/$TOPICO -H "Host: ntfy.sh" -k
fi
EOF

chmod +x /usr/local/bin/ntfy-login.sh
echo "session optional pam_exec.so /usr/local/bin/ntfy-login.sh" >> /etc/pam.d/sshd
```

**Passo 5 — Criar script de monitoramento de disco**

<div align="justify">
O script verifica o uso de todos os discos físicos a cada hora. Quando qualquer ponto de montagem ultrapassar 85% de uso, uma notificação de alta prioridade é enviada ao iPhone. O filtro <code>^/dev/sd|^/dev/md</code> garante que apenas discos reais sejam monitorados, ignorando overlays do Docker, tmpfs e efivarfs.
</div>

> ⚠️ Substitua `>SEU_TOPICO_NTFY<` e `>IP_NTFY<` pelos seus valores antes de executar.

```bash
cat > /usr/local/bin/monitor-disco.sh << 'EOF'
#!/bin/bash

TOPICO=">SEU_TOPICO_NTFY<"
NTFY_IP=">IP_NTFY<"
LIMITE=85

LC_ALL=C df -h | grep -E "^/dev/sd|^/dev/md" | while read -r linha; do
    USO=$(echo "$linha" | awk '{print $5}' | tr -d '%')
    PONTO=$(echo "$linha" | awk '{print $6}')
    DISPONIVEL=$(echo "$linha" | awk '{print $4}')

    if [ "$USO" -ge "$LIMITE" ] 2>/dev/null; then
        curl -s \
            -H "Title: 💾 Disco Crítico: $PONTO" \
            -H "Priority: high" \
            -H "Tags: warning" \
            -d "Uso em $PONTO está em $USO%. Disponível: $DISPONIVEL" \
            https://$NTFY_IP/$TOPICO -H "Host: ntfy.sh" -k
    fi
done
EOF

chmod +x /usr/local/bin/monitor-disco.sh
```

**Passo 6 — Criar script de monitoramento de temperatura**

<div align="justify">
O script lê a temperatura do Core 0 via lm-sensors a cada hora. O Celeron N2840 possui TDP de 7.5W e throttle a 90°C — o limite de alerta é definido em 75°C, garantindo margem suficiente para intervenção antes de degradação de performance.
</div>

> ⚠️ Substitua `>SEU_TOPICO_NTFY<` e `>IP_NTFY<` pelos seus valores antes de executar.

```bash
apt install -y lm-sensors
sensors-detect --auto

cat > /usr/local/bin/monitor-temp.sh << 'EOF'
#!/bin/bash

TOPICO=">SEU_TOPICO_NTFY<"
NTFY_IP=">IP_NTFY<"
LIMITE=75

TEMP=$(sensors | grep "Core 0" | awk '{print $3}' | tr -d '+°C')
TEMP_INT=${TEMP%.*}

if [ "$TEMP_INT" -ge "$LIMITE" ] 2>/dev/null; then
    curl -s \
        -H "Title: 🌡️ CPU Crítica: ${TEMP}°C" \
        -H "Priority: urgent" \
        -H "Tags: thermometer" \
        -d "Temperatura do Core 0 em ${TEMP}°C. Limite: ${LIMITE}°C. Verifique a refrigeração!" \
        https://$NTFY_IP/$TOPICO -H "Host: ntfy.sh" -k
fi
EOF

chmod +x /usr/local/bin/monitor-temp.sh
```

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left">Fazer login SSH a partir de outro dispositivo</td>
    <td align="left">Notificação push urgente chegando no iPhone com usuário e IP</td>
  </tr>
  <tr>
    <td align="left">Reiniciar o servidor (<code>reboot</code>)</td>
    <td align="left">Notificação "🔄 Servidor Reiniciado" chegando ao conectar novamente</td>
  </tr>
  <tr>
    <td align="left"><code>bash -x /usr/local/bin/monitor-temp.sh</code></td>
    <td align="left">Script executando, lendo temperatura e comparando ao limite sem erros</td>
  </tr>
</table>
</div>

</details>

---

<details id="ep05-etapa5">
  <summary>🪨 Etapa 5 — Varredura de Segurança (ClamAV e Lynis)</summary>

**Passo 1 — Criar o script unificado de varredura**

<div align="justify">
O ClamAV não roda em modo daemon contínuo para preservar memória RAM. Em vez disso, o <code>freshclam</code> atualiza as definições de vírus e o <code>clamscan</code> varre o diretório Storage completo uma vez por semana, sempre seguido pela auditoria do Lynis. Se malware for detectado ou o Lynis encontrar warnings críticos, uma notificação urgente é enviada ao iPhone. Caso tudo esteja limpo, uma notificação de baixa prioridade confirma a execução.
</div>

> ⚠️ Substitua `>SEU_TOPICO_NTFY<` e `>IP_NTFY<` pelos seus valores antes de executar.

```bash
cat > /usr/local/bin/clamav-scan.sh << 'EOF'
#!/bin/bash

TOPICO=">SEU_TOPICO_NTFY<"
NTFY_IP=">IP_NTFY<"
LOG="/var/log/clamav/scan-$(date +%Y-%m-%d).log"
PASTAS="/DATA/Storage"
LYNIS_LOG="/var/log/lynis-$(date +%Y-%m-%d).log"

echo "=== Varredura ClamAV - $(date) ===" >> "$LOG"

# Atualizar definições de vírus
freshclam >> "$LOG" 2>&1

# Executar varredura
clamscan --recursive --infected --log="$LOG" $PASTAS
RESULTADO=$?

echo "=== Fim da varredura ClamAV ===" >> "$LOG"

# Notificar resultado do ClamAV
if [ "$RESULTADO" -eq 1 ]; then
    curl -s \
        -H "Title: 🚨 ALERTA: Malware Detectado!" \
        -H "Priority: urgent" \
        -H "Tags: warning" \
        -d "ClamAV encontrou arquivos infectados. Verifique: $LOG" \
        https://$NTFY_IP/$TOPICO -H "Host: ntfy.sh" -k
else
    curl -s \
        -H "Title: 🦠 ClamAV Scan OK" \
        -H "Priority: low" \
        -H "Tags: white_check_mark" \
        -d "Varredura concluída sem ameaças. $(date +%d/%m/%Y)" \
        https://$NTFY_IP/$TOPICO -H "Host: ntfy.sh" -k
fi

# Executar auditoria Lynis
echo "=== Auditoria Lynis - $(date) ===" > "$LYNIS_LOG"
lynis audit system --no-colors >> "$LYNIS_LOG" 2>&1

# Verificar warnings críticos
WARNINGS=$(grep -c "^Warning" "$LYNIS_LOG" 2>/dev/null); WARNINGS=${WARNINGS:-0}

if [ "$WARNINGS" -gt 0 ]; then
    curl -s \
        -H "Title: 🚨 ALERTA: Lynis - $WARNINGS Warning(s)!" \
        -H "Priority: urgent" \
        -H "Tags: warning" \
        -d "Lynis encontrou $WARNINGS avisos críticos. Verifique: $LYNIS_LOG" \
        https://$NTFY_IP/$TOPICO -H "Host: ntfy.sh" -k
else
    curl -s \
        -H "Title: 🔍 Lynis Audit OK" \
        -H "Priority: low" \
        -H "Tags: white_check_mark" \
        -d "Auditoria Lynis concluída. ${WARNINGS} warnings. $(date +%d/%m/%Y)" \
        https://$NTFY_IP/$TOPICO -H "Host: ntfy.sh" -k
fi
EOF

chmod +x /usr/local/bin/clamav-scan.sh
```

> 💡 Para testar a detecção de malware sem risco, crie um arquivo EICAR (padrão da indústria, inofensivo) e rode o script manualmente: `echo 'X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*' > /tmp/eicar_test.txt && clamscan /tmp/eicar_test.txt`

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>bash /usr/local/bin/clamav-scan.sh</code></td>
    <td align="left">Script executa, notificações "🦠 ClamAV Scan OK" e "🔍 Lynis Audit OK" chegam no iPhone</td>
  </tr>
  <tr>
    <td align="left">Criar arquivo EICAR e rodar o script</td>
    <td align="left">Notificação "🚨 ALERTA: Malware Detectado!" com prioridade urgente no iPhone</td>
  </tr>
</table>
</div>

</details>

---

<details id="ep05-etapa6">
  <summary>🪨 Etapa 6 — Backup Offsite Criptografado (Rclone + Google Drive)</summary>

**Passo 1 — Instalar o Rclone**

<div align="justify">
O Rclone é uma ferramenta de linha de comando para sincronização com serviços de armazenamento em nuvem. Ele suporta criptografia nativa dos arquivos antes do envio, garantindo que nem o Google consiga ler o conteúdo dos backups.
</div>

```bash
curl https://rclone.org/install.sh | bash
rclone version
```

> 💡 Se o Rclone já estiver instalado, o script de instalação apenas confirma a versão existente.

**Passo 2 — Configurar o remote do Google Drive**

<div align="justify">
O Rclone utiliza OAuth para autenticação com o Google Drive. Como o servidor não possui navegador, a autenticação é feita em dois passos: o servidor gera um link de autorização, e o usuário autentica em um PC com navegador e cola o token resultante de volta no servidor.
</div>

```bash
rclone config
```

Siga a sequência no menu interativo:

- `n` → New remote
- Nome: `gdrive`
- Storage type: `drive`
- Client ID: deixe em branco (Enter)
- Client Secret: deixe em branco (Enter)
- Scope: `1` (acesso completo)
- Root folder ID: deixe em branco (Enter)
- Service account: deixe em branco (Enter)
- Edit advanced config: `n`
- Use auto config: `n`

> ⁉️ Um link de autorização será exibido. No PC Windows com navegador, baixe o Rclone em https://rclone.org/downloads/ e execute o comando exibido no terminal do servidor: `rclone.exe authorize "drive" "TOKEN_EXIBIDO"`. Após autenticar no navegador, cole o token gerado de volta no terminal do servidor.

- Shared Drive: `n`
- Keep remote: `y`
- Quit: `q`

**Passo 3 — Configurar a camada de criptografia (Rclone Crypt)**

<div align="justify">
O remote <code>gdrive-crypt</code> é uma camada de criptografia sobre o <code>gdrive</code>. Todos os arquivos enviados por este remote são criptografados antes de sair do servidor — o Google Drive armazena apenas dados ilegíveis sem as senhas do Rclone.
</div>

```bash
rclone config
```

Siga a sequência:

- `n` → New remote
- Nome: `gdrive-crypt`
- Storage type: `crypt`
- Remote: `gdrive:LegacyServer-Backup`
- Filename encryption: `1` (standard)
- Directory name encryption: `1` (true)
- Password: `g` (gerar automaticamente) → `128` bits → `y` (usar)
- Salt password: `g` (gerar automaticamente) → `128` bits → `y` (usar)
- Keep remote: `y`
- Quit: `q`

> ⚠️ As senhas geradas são exibidas apenas uma vez. Anote-as imediatamente em um gerenciador de senhas ou local seguro. Sem elas, é impossível recuperar qualquer backup armazenado no Google Drive.

Crie a pasta remota:

```bash
rclone mkdir gdrive-crypt:
```

**Passo 4 — Criar o script de backup mensal**

<div align="justify">
O script compacta o diretório <code>/DATA/AppData</code> em um arquivo <code>.tar.gz</code> nomeado com o mês atual, envia ao Google Drive criptografado e apaga automaticamente a versão com mais de 3 meses, mantendo sempre as 3 últimas cópias. Ao final, uma notificação informa o resultado e o tamanho do arquivo gerado.
</div>

> ⚠️ Substitua `>SEU_TOPICO_NTFY<` e `>IP_NTFY<` pelos seus valores antes de executar.

```bash
cat > /usr/local/bin/backup-rclone.sh << 'EOF'
#!/bin/bash

TOPICO=">SEU_TOPICO_NTFY<"
NTFY_IP=">IP_NTFY<"
ORIGEM="/DATA/AppData"
DESTINO="gdrive-crypt:"
MES_ATUAL=$(date +%Y-%m)
MES_1=$(date -d "1 month ago" +%Y-%m)
MES_2=$(date -d "2 months ago" +%Y-%m)
MES_3=$(date -d "3 months ago" +%Y-%m)
ARQUIVO_TAR="/tmp/backup-appdata-$MES_ATUAL.tar.gz"
LOG="/var/log/backup-rclone-$MES_ATUAL.log"

echo "=== Backup iniciado - $(date) ===" > "$LOG"

# Compactar AppData
tar -czf "$ARQUIVO_TAR" "$ORIGEM" >> "$LOG" 2>&1
TAMANHO=$(du -sh "$ARQUIVO_TAR" | cut -f1)

# Enviar para Google Drive criptografado
rclone sync "$ARQUIVO_TAR" "$DESTINO" --log-file="$LOG"
RESULTADO=$?

# Remover arquivo temporário local
rm -f "$ARQUIVO_TAR"

# Apagar backup com mais de 3 meses
rclone deletefile "$DESTINO/backup-appdata-$MES_3.tar.gz" 2>/dev/null

if [ "$RESULTADO" -eq 0 ]; then
    curl -s \
        -H "Title: ☁️ Backup Concluído" \
        -H "Priority: low" \
        -H "Tags: white_check_mark" \
        -d "Backup $MES_ATUAL concluído. Tamanho: $TAMANHO. Versões mantidas: $MES_ATUAL, $MES_1, $MES_2" \
        https://$NTFY_IP/$TOPICO -H "Host: ntfy.sh" -k
else
    curl -s \
        -H "Title: 🚨 ALERTA: Backup Falhou!" \
        -H "Priority: urgent" \
        -H "Tags: warning" \
        -d "Erro no backup $MES_ATUAL. Verifique: $LOG" \
        https://$NTFY_IP/$TOPICO -H "Host: ntfy.sh" -k
fi

echo "=== Backup finalizado - $(date) ===" >> "$LOG"
EOF

chmod +x /usr/local/bin/backup-rclone.sh
```

> 💡 Para restaurar um backup: instale o Rclone em outra máquina, copie o arquivo `/root/.config/rclone/rclone.conf` do servidor original, execute `rclone sync gdrive-crypt: /tmp/restore/` e depois `tar -xzf /tmp/restore/backup-appdata-YYYY-MM.tar.gz -C /`.

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>bash /usr/local/bin/backup-rclone.sh</code></td>
    <td align="left">Notificação "☁️ Backup Concluído" com tamanho do arquivo no iPhone</td>
  </tr>
  <tr>
    <td align="left">Google Drive → pasta LegacyServer-Backup</td>
    <td align="left">Arquivo com nome criptografado (ilegível) presente na pasta</td>
  </tr>
  <tr>
    <td align="left"><code>rclone lsd gdrive:LegacyServer-Backup</code></td>
    <td align="left">Listar a pasta com o arquivo de backup</td>
  </tr>
</table>
</div>

</details>

---

<details id="ep05-etapa7">
  <summary>🪨 Etapa 7 — Atualizações Automáticas de Segurança (Unattended-Upgrades)</summary>

**Passo 1 — Instalar e ativar o Unattended-Upgrades**

<div align="justify">
O Unattended-Upgrades aplica automaticamente apenas atualizações de segurança do Debian, sem intervenção manual. Patches de segurança são aplicados diariamente às 05:00. Se uma atualização de kernel exigir reinicialização, o sistema reinicia automaticamente às 06:00 — fora da janela de todos os outros crons.
</div>

```bash
apt install -y unattended-upgrades apt-listchanges
dpkg-reconfigure -plow unattended-upgrades
```

> ⁉️ Quando perguntar se deseja ativar as atualizações automáticas, selecione **Sim**.

**Passo 2 — Configurar reinicialização automática**

<div align="justify">
Por padrão, o Unattended-Upgrades não reinicia o sistema mesmo quando necessário. As linhas abaixo ativam a reinicialização automática e definem o horário para as 06:00, garantindo que ocorra sempre após todos os outros crons terem concluído.
</div>

```bash
nano /etc/apt/apt.conf.d/50unattended-upgrades
```

Localize e descomente (ou adicione) as seguintes linhas:

```
Unattended-Upgrade::Automatic-Reboot "true";
Unattended-Upgrade::Automatic-Reboot-Time "06:00";
```

Confirme o arquivo de periodicidade:

```bash
cat /etc/apt/apt.conf.d/20auto-upgrades
```

O conteúdo deve ser:

```
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Unattended-Upgrade "1";
```

<div align="center">
<table>
  <tr>
    <th align="center">Verificação</th>
    <th align="center">Resultado esperado</th>
  </tr>
  <tr>
    <td align="left"><code>systemctl status unattended-upgrades --no-pager</code></td>
    <td align="left"><code>Active: active (running)</code></td>
  </tr>
  <tr>
    <td align="left"><code>grep -E "Automatic-Reboot" /etc/apt/apt.conf.d/50unattended-upgrades</code></td>
    <td align="left">Duas linhas sem comentário: <code>"true"</code> e <code>"06:00"</code></td>
  </tr>
</table>
</div>

</details>

---

## Resumo Final — Scripts e Crontab

<div align="justify">
Todos os scripts de automação criados neste episódio estão listados abaixo com seus caminhos e funções.
</div>
&nbsp;

<div align="center">
<table>
  <tr>
    <th align="center">Script</th>
    <th align="center">Caminho</th>
    <th align="center">Função</th>
  </tr>
  <tr>
    <td align="left"><strong>clamav-scan.sh</strong></td>
    <td align="left"><code>/usr/local/bin/clamav-scan.sh</code></td>
    <td align="left">Atualiza definições, varre o Storage, executa Lynis e notifica via ntfy</td>
  </tr>
  <tr>
    <td align="left"><strong>docker-cleanup.sh</strong></td>
    <td align="left"><code>/usr/local/bin/docker-cleanup.sh</code></td>
    <td align="left">Remove imagens, containers e volumes órfãos do Docker e notifica espaço liberado</td>
  </tr>
  <tr>
    <td align="left"><strong>backup-rclone.sh</strong></td>
    <td align="left"><code>/usr/local/bin/backup-rclone.sh</code></td>
    <td align="left">Compacta /DATA/AppData, envia ao Google Drive criptografado e mantém 3 versões</td>
  </tr>
  <tr>
    <td align="left"><strong>monitor-disco.sh</strong></td>
    <td align="left"><code>/usr/local/bin/monitor-disco.sh</code></td>
    <td align="left">Alerta quando qualquer disco físico ultrapassar 85% de uso</td>
  </tr>
  <tr>
    <td align="left"><strong>monitor-temp.sh</strong></td>
    <td align="left"><code>/usr/local/bin/monitor-temp.sh</code></td>
    <td align="left">Alerta quando a temperatura do Core 0 ultrapassar 75°C</td>
  </tr>
  <tr>
    <td align="left"><strong>ntfy-login.sh</strong></td>
    <td align="left"><code>/usr/local/bin/ntfy-login.sh</code></td>
    <td align="left">Notifica logins SSH bem-sucedidos com usuário, IP e horário</td>
  </tr>
</table>
</div>

<div align="justify">
E aqui está a tabela final das rotinas configuradas
</div>
&nbsp;

<div align="center">
<table>
  <tr>
    <th align="center">Horário</th>
    <th align="center">Frequência</th>
    <th align="center">Tarefa</th>
  </tr>
  <tr>
    <td align="left"><code>00:00</code></td>
    <td align="left">Semanal (domingo)</td>
    <td align="left">ClamAV + Lynis</td>
  </tr>
  <tr>
    <td align="left"><code>01:00</code></td>
    <td align="left">Semanal (domingo)</td>
    <td align="left">Docker Cleanup</td>
  </tr>
  <tr>
    <td align="left"><code>01:00</code></td>
    <td align="left">Mensal (dia 1)</td>
    <td align="left">Backup Rclone → Google Drive</td>
  </tr>
  <tr>
    <td align="left"><code>*/1h</code></td>
    <td align="left">A cada hora</td>
    <td align="left">Monitor de disco (>85%)</td>
  </tr>
  <tr>
    <td align="left"><code>*/1h</code></td>
    <td align="left">A cada hora</td>
    <td align="left">Monitor de temperatura (>75°C)</td>
  </tr>
  <tr>
    <td align="left"><code>06:00</code></td>
    <td align="left">Diário</td>
    <td align="left">Unattended-Upgrades + reboot se necessário</td>
  </tr>
</table>
</div>


</details>

---

## Ajustes e melhorias

<div align="justify">
A infraestrutura atual está funcional, porém precisa de ajustes finos em alguns serviços. O projeto continua em evolução técnica para garantir maior estabilidade a longo prazo.

### Infraestrutura Física e Energia
- [ ] Integração com No-Break (UPS) via *Network UPS Tools* (NUT) para automação de *graceful shutdown* em quedas de energia

### Automação e Novos Recursos (Software)
- [x] Implementação de rotina automatizada de backup off-site para dados críticos (configurações e documentos)
- [ ] Implementação de Proxy Reverso com SSL para portfólio pessoal
- [ ] Automação da pipeline de mídia: integrar o cliente de downloads a ferramentas de indexação automática para automação de buscas e download de legendas embutidas
- [ ] Implementar Grafana + InfluxDB para visualização de dashboards, gerar relatórios e alertas para dispositivos sensores IoT

### Ajustes Finos e Correções (Troubleshooting)
- [ ] Otimização de rotas de rede/DNS no container do Suwayomi-Server para corrigir a falha de carregamento de extensões externa

</div>

---

## Episódios

<div align="center">
<table>
  <tr>
    <th align="center">Episódio</th>
    <th align="center">Título</th>
    <th align="center">Link</th>
  </tr>
  <tr>
    <td align="left">EP 01</td>
    <td align="left">Do Zero ao Servidor de Pé</td>
    <td align="left">em breve</td>
  </tr>
  <tr>
    <td align="left">EP 02</td>
    <td align="left">Segurança</td>
    <td align="left">em breve</td>
  </tr>
  <tr>
    <td align="left">EP 03</td>
    <td align="left">Mídia e Downloads</td>
    <td align="left">em breve</td>
  </tr>
  <tr>
    <td align="left">EP 04</td>
    <td align="left">A Área de Lazer</td>
    <td align="left">em breve</td>
  </tr>
  <tr>
    <td align="left">EP 05</td>
    <td align="left">Otimização</td>
    <td align="left">em breve</td>
  </tr>
</table>
</div>

---

## Licença

MIT — veja [LICENSE](./LICENSE) para detalhes.

---
<div align="center">
  <p>Desenvolvido com rigor técnico por <strong>> Ansi Labs_</strong></p>
</div>
