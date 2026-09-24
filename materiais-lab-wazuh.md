# Materiais Necessários — Laboratório Wazuh

Lista de ISOs, softwares, ferramentas e recursos para montar o ambiente completo.

> **Nota:** o Wazuh (Manager + Indexer + Dashboard) será deployado via **Docker no host Windows**, e não numa VM Ubuntu dedicada. Isso simplifica bastante o deploy, já que o foco do lab são as atividades de detecção/resposta, não o processo de instalação.

---

## 1. Docker (para o Wazuh)

- [ ] **Docker Desktop for Windows** — necessário para rodar o Wazuh via containers direto no host (docker.com/products/docker-desktop)
- [ ] **WSL2 habilitado** — pré-requisito do Docker Desktop no Windows, geralmente configurado automaticamente na instalação (`wsl --install` caso não esteja ativo)
- [ ] **Repositório `wazuh-docker`** — contém o `docker-compose.yml` oficial com Manager, Indexer e Dashboard prontos (github.com/wazuh/wazuh-docker)
- [ ] **Wazuh Agent** — pacote de instalação para cada SO monitorado (deb/rpm/msi), baixado do site oficial e configurado para apontar para o IP do host Windows

## 2. Virtualização (para as VMs vítima e atacante — escolher uma)

- [ ] **VirtualBox** — gratuito, mais simples para começar. (virtualbox.org)
- [ ] **VMware Workstation Pro** — agora gratuito para uso pessoal. (vmware.com)
- [ ] *(Proxmox não se aplica aqui, já que o Wazuh roda direto no host Windows via Docker — use-o só se preferir virtualizar tudo, incluindo o host)*

## 3. Sistemas Operacionais (ISOs) — apenas para as VMs vítima e atacante

- [ ] **Ubuntu Desktop ou CentOS/Rocky Linux** — para a VM "vítima" Linux
- [ ] **Windows 10 ISO** — para a VM "vítima" Windows (Microsoft disponibiliza ISO de avaliação gratuita via Media Creation Tool ou site oficial)
- [ ] **Windows Server 2019/2022 (Evaluation)** — se for montar o Active Directory (180 dias grátis via Microsoft Evaluation Center)
- [ ] **Kali Linux** — VM atacante, já vem com as ferramentas de pentest instaladas (kali.org/get-kali)
- [ ] *(Opcional)* **Parrot OS** — alternativa ao Kali (parrotsec.org)

## 4. Ferramentas do "atacante" (já vêm no Kali, mas liste para conferir)

- [ ] **Nmap** — scanner de portas/serviços
- [ ] **Hydra** ou **Medusa** — brute force (SSH, RDP, etc.)
- [ ] **Metasploit Framework** — exploração e geração de payloads
- [ ] **Sliver** ou **Cobalt Strike (trial)** — simulação de C2, se for testar cenários mais avançados
- [ ] **Mimikatz** — se for simular ataques em ambiente Windows/AD (pass-the-hash, dump de credenciais)
- [ ] **Impacket** (scripts Python) — para ataques em AD como Kerberoasting

## 5. Wordlists

- [ ] **rockyou.txt** — já vem no Kali (`/usr/share/wordlists/rockyou.txt.gz`), usado para brute force
- [ ] **SecLists** — repositório com várias wordlists úteis (github.com/danielmiessler/SecLists)

## 6. Coleta de logs adicional (para enriquecer os dados no Wazuh)

- [ ] **Sysmon** (Sysinternals) — para Windows, captura eventos detalhados de processo/rede/registro (learn.microsoft.com/sysinternals)
- [ ] **Configuração do Sysmon (SwiftOnSecurity)** — arquivo XML pronto e comentado, ótimo ponto de partida (github.com/SwiftOnSecurity/sysmon-config)
- [ ] **auditd** — para Linux, geralmente já vem no repositório da distro (`apt install auditd`)
- [ ] *(Opcional)* **Suricata** — IDS/IPS de rede, complementa a visibilidade que o Wazuh sozinho não tem (ex: para port scans)

## 7. Threat Intelligence / Enriquecimento (opcional)

- [ ] **Conta/API Key do VirusTotal** — para consultar reputação de hashes/arquivos (virustotal.com)
- [ ] **Conta/API Key do AbuseIPDB** — para reputação de IPs (abuseipdb.com)

## 8. Integrações SOAR / Notificações (opcional, para o lab avançado)

- [ ] **TheHive** — plataforma de gestão de casos/incidentes (thehive-project.org)
- [ ] **Shuffle** — SOAR open-source, para criar workflows de automação (shuffler.io)
- [ ] **Webhook do Slack ou bot do Telegram** — para receber alertas em tempo real

## 9. Documentação e referência

- [ ] **Documentação oficial do Wazuh** — documentation.wazuh.com
- [ ] **MITRE ATT&CK Navigator** — attack.mitre.org (para mapear técnicas dos ataques simulados)
- [ ] **CIS Benchmarks** — cisecurity.org (referência usada pelo módulo SCA do Wazuh)

## 10. Requisitos de hardware (recomendado)

- [ ] **CPU**: mínimo 4 núcleos livres (Docker + VMs rodando ao mesmo tempo consome bastante)
- [ ] **RAM**: mínimo 16GB no host (o stack do Wazuh via Docker já recomenda ~8GB só para si; some as VMs vítima/atacante)
- [ ] **Disco**: pelo menos 100-150GB livres (SSD recomendado para performance do Indexer)
- [ ] **Rede**: adaptador de rede virtual das VMs configurado em modo host-only/interno, mas que consiga rotear até o host Windows (onde o Docker publica as portas do Wazuh). Não usar bridge exposta à rede real para não vazar tráfego malicioso.
- [ ] **Virtualização aninhada habilitada na BIOS/UEFI** (VT-x/AMD-V) — necessária tanto para o VirtualBox/VMware quanto para o WSL2 do Docker rodarem ao mesmo tempo

---

### Observação
Os itens das seções 6 a 8 são opcionais e servem para quando você quiser expandir o lab além do cenário básico (Fases 8, 9 e 10 do To-Do). Para começar, o essencial é: Docker Desktop (Wazuh) + um virtualizador + uma VM vítima (Linux ou Windows) + Kali Linux.
