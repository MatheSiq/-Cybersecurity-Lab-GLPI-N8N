# 🛡️ To-Do: Laboratório de Cybersecurity com Wazuh

> Checklist de progresso do lab. Marque `[x]` conforme for concluindo e adicione novos itens/seções livremente.
> O laboratório foi desenvolvido no Windows 11, utilizando o VirtualBox como ferramenta de virtualização.

---

## 🐳 Infraestrutura — Wazuh
- [ ] Baixar o arquivo OVA do Wazuh por meio da documentação oficial
- [ ] Importar a máquina para o VirtualBox
- [ ] Iniciar a máquina e testar o acesso ao Wazuh
## 🐧 VM Ubuntu
- [ ] Baixar a ISO e criar a VM Ubuntu
- [ ] Instalar o serviço openssh-server
	- [ ] `sudo apt update && sudo apt install openssh-server -y`
	- [ ] `sudo systemctl enable --now ssh`
	- [ ] `sudo systemctl status ssh`
- [ ] Configurar um port-fowarding para acessá-la via SSH
- [ ] Configurá-la corretamente com o Wazuh Agent
- [ ] Tirar snapshot
## 🎯 VM Metasploitable
- [ ] Baixar os arquivos do site da Rapid7 e importar o Virtual Disk
- [ ] Configurar um port-fowarding para acessá-la via SSH
- [ ] Configurá-la corretamente com o Wazuh Agent
- [ ] Tirar snapshot
## 🐋 Docker
- [ ] Baixar o Docker Desktop
## 🔎 GLPI + N8N
- [ ] https://github.com/MatheSiq/-Cybersecurity-Lab-GLPI-N8N
	- [ ] Baixar o docker-compose.yml e o env.txt
	- [ ] Alterar o conteúdo do env.txt e alterar sua extensão, removendo o .txt e adicionando um ponto "." antes do env.
	- [ ] Alterar as credenciais do .env
	- [ ] Executar o comando `docker compose up -d` para subir o container
	- [ ] Acessar o GLPI a partir do http://localhost:8080
	- [ ] Acessar o N8N a partir do http://localhost:5678
	- [ ] Para derrubar o container, executar o `docker compose down`
- [ ] Configurar o GLPI para Incident Management.
	- [ ] Acessar Setup - Dropdowns - ITIL Categories
	- [ ] Criar uma categoria de inicentes(Security Incident)
	- [ ] Criar subcategorias com técnicas do MITRE ATT&CK (TA0043 - Reconnaissance)
	- [ ] Acessar Setup - Dropdowns - Ticket templates
	- [ ] Criar um template para incidentes de segurança(Alerta de Segurança - Wazuh, por exemplo)
	- [ ] Na aba "Predefined fields", force o preenchimento automático de campos cruciais para o SOC: defina **Type** como `Incident`, **Status** como `New`, e **Urgency** como `High` ou `Very High`. Oculte campos irrelevantes para os analistas de segurança.
- [ ] Agora é necessário acessar Setup - General - API O N8N vai precisar se comunicar com a API do GLPI. Marque a opção Enable REST API.
	- [ ] Na seção "API clients", adicione um novo cliente chamado "Integracao_N8N". Após salvar, marque a caixa "Regenerate" no campo App-Token e salve novamente para gerar a chave. Copie esse valor.
	- [ ] A URL da API (geralmente `http://<seu-ip>/glpi/apirest.php`) deve estar ativa, e você deve ter o App-Token salvo em um bloco de notas
- [ ] Acessar Administration - Users
	- [ ] Agora é necessário gerar um token de usuário para o N8N
	- [ ] Evite usar sua conta pessoal para a integração. Crie um usuário de serviço (ex: `api_n8n`) e atribua a ele um perfil com permissão para criar e atualizar chamados (o perfil `Admin` ou `Super-Admin` atende bem ao lab).
	- [ ] Acesse as preferências desse usuário recém-criado e gere um **Personal API Token**.
	- [ ] Você agora possui as duas chaves obrigatórias para a autenticação no N8N: o **App-Token** e o **User-Token**.

## 🚀 Próximos passos
- [ ] _(a definir)_

---

**Legenda:** `[x]` concluído · `[ ]` pendente