# 🛡️ To-Do: Laboratório de Cybersecurity com Wazuh

> Checklist de progresso do lab. Marque `[x]` conforme for concluindo e adicione novos itens/seções livremente. O laboratório foi desenvolvido no Windows 11, utilizando o VirtualBox como ferramenta de virtualização.

## 🐳 Infraestrutura — Wazuh

- [ ] Baixar o arquivo OVA do Wazuh por meio da documentação oficial.
- [ ] Importar a máquina para o VirtualBox.
- [ ] Iniciar a máquina e testar o acesso ao Wazuh.
## 🐧 VM Ubuntu

- [ ] Baixar a ISO e criar a VM Ubuntu.
- [ ] Instalar o serviço openssh-server:
    - [ ] Executar: `sudo apt update && sudo apt install openssh-server -y`.
    - [ ] Executar: `sudo systemctl enable --now ssh`.
    - [ ] Executar: `sudo systemctl status ssh`.
- [ ] Configurar um port-forwarding para acessá-la via SSH.
- [ ] Configurá-la corretamente com o Wazuh Agent.
- [ ] Tirar snapshot da máquina.
## 🎯 VM Metasploitable

- [ ] Baixar os arquivos do site da Rapid7 e importar o Virtual Disk.
- [ ] Configurar um port-forwarding para acessá-la via SSH.
- [ ] Configurá-la corretamente com o Wazuh Agent.
- [ ] Tirar snapshot da máquina.
## 🐋 Docker

- [ ] Baixar e instalar o Docker Desktop.
## 🔎 GLPI + N8N

- [ ] Configurar os containers a partir do repositório ([https://github.com/MatheSiq/-Cybersecurity-Lab-GLPI-N8N](https://www.google.com/search?q=https://github.com/MatheSiq/-Cybersecurity-Lab-GLPI-N8N&utm_source=gemini)):
    - [ ] Baixar o arquivo `docker-compose.yml` e o `env.txt`.
    - [ ] Alterar as credenciais dentro do `env.txt`.
    - [ ] Renomear o arquivo `env.txt` para `.env` (removendo a extensão .txt e adicionando o ponto no início).
    - [ ] Executar o comando `docker compose up -d` para subir o container.
    - [ ] Acessar o GLPI a partir de http://localhost:8080.
    - [ ] Acessar o N8N a partir de http://localhost:5678.
    - [ ] _(Nota)_ Para derrubar o container, utilize o comando `docker compose down`.
- [ ] Configurar o GLPI para atuar como Incident Management:
    - [ ] Acessar **Setup** > **Dropdowns** > **ITIL Categories**.
    - [ ] Criar uma categoria de incidentes (ex: `Security Incident`).
    - [ ] Criar subcategorias mapeando técnicas do MITRE ATT&CK (ex: `TA0043 - Reconnaissance`).
    - [ ] Acessar **Setup** > **Dropdowns** > **Ticket templates**.
    - [ ] Criar um template para incidentes de segurança (ex: `Alerta de Segurança - Wazuh`).
    - [ ] Na aba **Predefined fields**, forçar o preenchimento automático: definir **Type** como `Incident`, **Status** como `New`, e **Urgency** como `High` ou `Very High`.
    - [ ] Ocultar os campos que são irrelevantes para a equipe de analistas de segurança.
- [ ] Configurar a API REST no GLPI:
    - [ ] Acessar **Setup** > **General** > **API** e marcar a opção **Enable REST API** para permitir a comunicação com o N8N.
    - [ ] Na seção **API clients**, adicionar um novo cliente chamado `Integracao_N8N`.
    - [ ] Após salvar, marcar a caixa **Regenerate** no campo **App-Token** e salvar novamente para gerar a chave.
    - [ ] Copiar o **App-Token** e armazená-lo em um bloco de notas.
    - [ ] Validar se a URL da API (geralmente `http://<seu-ip>/glpi/apirest.php`) está ativa.
- [ ] Configurar o acesso do N8N via Token de Usuário:
    - [ ] Acessar **Administration** > **Users**.
    - [ ] Criar um usuário de serviço exclusivo para a integração (ex: `api_n8n`), evitando o uso de conta pessoal.
    - [ ] Atribuir a este usuário um perfil com permissão de criação e atualização de chamados (perfis `Admin` ou `Super-Admin` são recomendados para o lab).
    - [ ] Acessar as preferências do usuário recém-criado e gerar um **Personal API Token**.
    - [ ] Armazenar o **User-Token** junto com o **App-Token**, pois ambas as chaves serão obrigatórias para a autenticação no N8N.
## 🚀 Próximos passos

- [ ] _(a definir)_