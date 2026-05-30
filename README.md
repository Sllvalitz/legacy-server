<div align="center">
  <img src="https://img.shields.io/badge/Status-Ativo-success?style=for-the-badge" alt="Status Ativo">
  <img src="https://img.shields.io/badge/Licença-MIT-blue?style=for-the-badge" alt="Licença MIT">
</div>

# Legacy Server

<div align="center">
  <img src="imagem.png" alt="Servidor Legacy NAS em funcionamento" width="600">
  <br>
  <em>Servidor operando 24/7 no gabinete customizado impresso em 3D.</em>
</div>
<br>

Um servidor doméstico construído a partir de uma placa-mãe de notebook descartada (Acer ES1-511), rodando 24/7 com consumo ínfimo de ~10W. O projeto prova que hardware legado possui vida útil real e escalável para hospedar mídia, serviços locais e um portfólio web próprio, dispensando infraestruturas externas de nuvem.

> 📺 Este projeto é documentado em série no YouTube — links dos episódios abaixo.

---

## Hardware

O hardware foi escolhido com o objetivo estrito de reaproveitamento de sucata tecnológica. O Celeron N2840 é fraco para transcodificação de vídeo, mas é exatamente o que se precisa para um servidor NAS: baixíssimo consumo, poder computacional suficiente para servir arquivos, filtrar DNS e gerenciar containers leves. O RAID 1 garante que uma falha de disco não signifique perda de dados.

<div align="center">

| Componente | Especificação |
| :--- | :--- |
| **Processador** | Intel Celeron N2840 |
| **RAM** | 8 GB — HyperX Impact DDR3L 1600 MHz |
| **Sistema** | Rise Mode Gamer Line 120 GB (SSD via USB 3.0) |
| **Dados** | RAID 1 — 2× HGST 500 GB 7200 RPM 2.5" SATA |
| **Rede** | Intel 7260HMW (Wi-Fi Dual Band AC + Bluetooth) |
| **Gabinete** | Case customizado impresso em 3D (modelos na pasta `/modelos-3d`) |

</div>

---

## Demonstração da aplicação

<div align="center">
  <img src="demo-dashboard.gif" alt="Demonstração do CasaOS" width="400">
  <img src="demo-jellyfin.gif" alt="Acesso ao Jellyfin" width="400">
  <br>
  <em>Dashboard de gerenciamento e streaming local operando em Direct Play.</em>
</div>

---

## Stack

A infraestrutura base é o **Debian 12 Bookworm** puro, escolhido por sua estabilidade, uso mínimo de RAM e suporte de longo prazo. Sobre ele, o **CasaOS** atua como uma camada de abstração visual para a engine do **Docker**, agilizando o monitoramento e o deploy de containers sem restringir o acesso nativo ao terminal.

A topologia de rede é gerenciada por dois componentes críticos: o **Tailscale** cria uma malha VPN criptografada via WireGuard, provendo acesso remoto seguro à gerência sem expor portas na WAN. Em paralelo, o **Nginx Proxy Manager (NPM)** orquestra as requisições HTTP/HTTPS, roteando o tráfego interno e sendo a peça-chave para expor e hospedar meu **site portfólio pessoal** diretamente neste hardware, com renovação automatizada de certificados SSL via Let's Encrypt.

- **OS:** Debian 12 Bookworm
- **Engine de Containers:** CasaOS + Docker
- **Túnel & VPN:** Tailscale
- **Proxy Reverso & Web Server:** Nginx Proxy Manager
- **Resolução Local:** AdGuard Home

---

## Serviços ativos

Cada serviço foi escolhido pelas minhas necessidades e interesses de estudo, somado a compatibilidade com restrições de CPU e consumo de memória ram mínimo. Nenhum container realiza transcodificação sob demanda — o Jellyfin opera de forma estrita em *Direct Play*.

<div align="center">

| Serviço | Função |
| :--- | :--- |
| **AdGuard Home** | DNS filtering e bloqueio de anúncios para toda a rede |
| **Nginx Proxy Manager** | Reverse proxy com HTTPS e SSL automático via Let's Encrypt |
| **Jellyfin** | Servidor de mídia (Direct Play — H.264 + AAC) |
| **Samba** | Compartilhamento de arquivos na rede local e via Tailscale |
| **qBittorrent** | Cliente de downloads com agendamento de banda |
| **Stirling PDF** | Ferramentas PDF — juntar, dividir, OCR, converter |
| **LibreOffice headless** | Conversão de arquivos de escritório (PDF ↔ Word e similares) |
| **ntfy** | Notificações push para iPhone via ntfy.sh |
| **Kavita** | Leitor de livros e quadrinhos (epub, pdf, cbz) |
| **Suwayomi-Server** | Servidor de mangás — fonte para Tachiyomi e Mihon |
| **Minecraft Bedrock** | Servidor de jogo via Docker (itzg/bedrock-server) |
| **Site estático** | Portfólio pessoal em HTML/CSS/JS servido pelo Nginx |
| **Tailscale** | VPN gerenciada — acesso remoto seguro a todos os serviços privados |
| **CrowdSec** | Detecção de intrusão e bloqueio de IPs maliciosos |

</div>

---

## Ajustes e melhorias

A infraestrutura atual está funcional, mas o projeto continua em evolução técnica para garantir maior resiliência e estabilidade a longo prazo. As próximas atualizações focarão nas seguintes tarefas:

- [x] Migração de hardware de rede para padrão AC (Intel 7260HMW)
- [x] Implementação de Proxy Reverso com SSL para portfólio pessoal
- [ ] Implementação de rotina automatizada de backup off-site para dados críticos (configurações e documentos)
- [ ] Integração com No-Break (UPS) via *Network UPS Tools* (NUT) para automação de *graceful shutdown* em quedas de energia

---

## Documentação

Cada arquivo em `/docs` corresponde a um episódio da série e contém todos os comandos utilizados, com explicação do que cada um faz e por quê foi escolhido. Os arquivos de configuração prontos estão em `/configs`.

- [`01-instalacao.md`](./docs/01-instalacao.md) — Hardware, BIOS, Debian 12, CasaOS, SSH, AdGuard
- [`02-seguranca.md`](./docs/02-seguranca.md) — UFW, Nginx Proxy Manager, Tailscale
- [`03-midia-downloads.md`](./docs/03-midia-downloads.md) — Jellyfin, qBittorrent, Samba, Stirling, ntfy
- [`04-biblioteca.md`](./docs/04-biblioteca.md) — Kavita, Suwayomi, Minecraft Bedrock
- [`05-otimizacao.md`](./docs/05-otimizacao.md) — Debloat, kernel, RAM, automações

---

## Episódios

<div align="center">

| Episódio | Título | Link |
| :--- | :--- | :--- |
| EP 01 | Do Zero ao Servidor de Pé | em breve |
| EP 02 | Segurança | em breve |
| EP 03 | Mídia e Downloads | em breve |
| EP 04 | A Biblioteca | em breve |
| EP 05 | Otimização | em breve |

</div>

---

## Licença

MIT — veja [LICENSE](./LICENSE) para detalhes.
