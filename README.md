
# Kali Linux Remote Access Lab

## Objetivo

Implementar e documentar um ambiente de acesso remoto ao Kali Linux executando em uma máquina virtual VMware Workstation, permitindo administração remota via SSH, Visual Studio Code Remote SSH e Área de Trabalho Remota (XRDP).

---

# Ambiente Utilizado

## Hardware

### Host

* Windows 11
* VMware Workstation

### Cliente

* Notebook Windows 11

### Máquina Virtual

* Kali Linux
* XFCE Desktop

---

# Topologia

```text
Notebook
│
├── SSH
├── VS Code Remote SSH
└── RDP (XRDP)
        │
        ▼
Kali Linux VM
        │
        ▼
VMware Workstation
        │
        ▼
Windows 11 Host
        │
        ▼
Rede Local
```

---

# Objetivos do Laboratório

* Configurar acesso remoto ao Kali Linux
* Utilizar SSH para administração remota
* Utilizar VS Code Remote SSH para desenvolvimento e documentação
* Utilizar XRDP para acesso gráfico remoto
* Compreender configuração de rede Bridge no VMware
* Praticar troubleshooting de Linux e serviços

---

# Configuração de Rede

## VMware

Modo de Rede:

```text
Bridge
```

Objetivo:

Permitir que a máquina virtual receba um endereço IP diretamente da rede local.

---

## Verificação do Endereço IP

```bash
ip a
```

ou

```bash
hostname -I
```

Resultado:

```text
192.168.0.125
```

---

# Configuração do SSH

## Instalação

```bash
sudo apt update
sudo apt install openssh-server -y
```

## Inicialização

```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

## Verificação

```bash
sudo systemctl status ssh
```

---

# Testes de Conectividade

## Ping

No cliente:

```bash
ping 192.168.0.125
```

## Porta SSH

PowerShell:

```powershell
Test-NetConnection 192.168.0.125 -Port 22
```

Resultado esperado:

```text
TcpTestSucceeded : True
```

---

# Conexão SSH

```bash
ssh kali@192.168.0.125
```

---

# Configuração do XRDP

## Instalação

```bash
sudo apt install xrdp -y
```

## Dependências

```bash
sudo apt install xorgxrdp dbus-x11 -y
```

## Inicialização

```bash
sudo systemctl enable xrdp
sudo systemctl restart xrdp
```

---

# Configuração do XFCE

Arquivo:

```bash
~/.xsession
```

Conteúdo:

```text
xfce4-session
```

Configuração:

```bash
echo xfce4-session > ~/.xsession
```

---

# Configuração do x-session-manager

Verificação:

```bash
sudo update-alternatives --config x-session-manager
```

Configuração final:

```text
/usr/bin/xfce4-session
```

Verificação:

```bash
readlink -f /usr/bin/x-session-manager
```

Resultado:

```text
/usr/bin/xfce4-session
```

---

# VS Code Remote SSH

## Extensão

Remote - SSH (Microsoft)

## Host Configurado

```text
ssh kali@192.168.0.125
```

## Benefícios

* Administração remota
* Terminal integrado
* Edição remota de arquivos
* Integração com Git e GitHub

---

# Troubleshooting

## Problema

XRDP retornava para a tela de login após autenticação.

## Diagnóstico

Análise dos logs:

```bash
~/.xsession-errors
/var/log/xrdp-sesman.log
```

## Solução

* Configuração correta do arquivo `.xsession`
* Ajuste do `x-session-manager`
* Reinicialização dos serviços XRDP e LightDM

---

# Snapshot VMware

Snapshot criado:

```text
Kali-Remoto-Completo-v1
```

Objetivo:

Permitir rápida restauração do ambiente funcional.

---

# Conhecimentos Aplicados

* Linux Administration
* VMware Workstation
* Redes TCP/IP
* SSH
* XRDP
* XFCE
* Troubleshooting
* VS Code Remote SSH
* Administração Remota

---

# Próximos Laboratórios

* Git e GitHub
* Linux Administration
* Wireshark
* TCP/IP
* CrowdSec
* Suricata
* Nmap
* VLANs
* Active Directory
* Azure

```
```
