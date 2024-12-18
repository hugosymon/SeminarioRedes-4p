# SeminarioRedes-4p
Repositório do seminário final da matéria de Redes 4º P


## Índice

1. [Descrição do Projeto](#descrição-do-projeto)
2. [Topologia da Rede](#topologia-da-rede)
3. [Segmentação de Sub-redes](#segmentação-de-sub-redes)
4. [Requisitos dos Serviços](#requisitos-dos-serviços)
5. [Implantação com Vagrant](#implantação-com-vagrant)
6. [Configuração dos Serviços](#configuração-dos-serviços)
7. [Testes Realizados](#testes-realizados)
8. [Resultados](#resultados)
9. [Anexos e Scripts](#anexos-e-scripts)



## Descrição do Projeto

O objetivo deste projeto é projetar, implantar e gerenciar uma rede empresarial usando tecnologia Linux. A rede inclui os seguintes serviços principais:

- **DHCP**: Distribuição automática de endereços IP.
- **DNS**: Resolução de nomes e gerenciamento de domínios.
- **Web**: Servidor Web Apache configurado para hospedar uma página HTML.
- **FTP**: Servidor de transferência de arquivos usando FTP.
- **NFS**: Compartilhamento de arquivos na rede usando NFS.
- **Virtualização**: Uso do **Vagrant** e VirtualBox para provisionar máquinas virtuais.

Todo o projeto foi documentado neste repositório e inclui os scripts de configuração e resultados dos testes.



## Topologia da Rede

Diagrama:
                        
                        +-------------------+
                        |      Router       |
                        |  192.168.1.1/24   |
                        +-------------------+
                                  |
                    -------------------------------
                    |             |             |
            DHCP Server      DNS Server     Web/FTP/NFS Server
         192.168.1.10/24   192.168.1.20/24    192.168.1.30/24
                    |             |             |
                Clients         Clients       Clients


- Servidor DHCP: Fornece IPs para os clientes.
- Servidor DNS: Resolução de nomes.
- Servidor Web/FTP/NFS: Hospeda os serviços Web, FTP e compartilhamento NFS.
- Clientes: Máquinas que utilizam os serviços configurados.



## Segmentação de Sub-redes

| **Sub-rede**         | **Endereço de Rede** | **Faixa de IPs**              | **Máscara**       | **Serviço**              |
|----------------------|----------------------|-------------------------------|-------------------|--------------------------|
| Sub-rede Principal   | 192.168.1.0          | 192.168.1.10 - 192.168.1.254  | 255.255.255.0     | DHCP, DNS, Web, FTP, NFS |
| Gerenciamento        | 10.0.0.0             | 10.0.0.10 - 10.0.0.100        | 255.255.255.0     | Administração            |

## Requisitos dos Serviços

**1. DHCP:**
- Configuração para fornecer IPs automaticamente (192.168.1.10 - 192.168.1.200).
- Gateway padrão: 192.168.1.1.
- Servidor DNS: 192.168.1.20.

**2. DNS:**
- Domínio: empresa.local.
- Configuração de zonas direta e reversa.

 **3. Servidor Web:**
- Apache configurado para hospedar uma página HTML básica.
  
 **4. Servidor FTP:**

- Servidor FTP configurado para permitir acesso anônimo.
**4. NFS: **

- Compartilhamento de diretórios para clientes.
  
** 6. Virtualização:**

- Uso de Vagrant para provisionar máquinas virtuais.

  ##Implantação com Vagrant

** VagrantFile


![{D1B714FC-2919-488B-B6B6-B6013804547F}](https://github.com/user-attachments/assets/00faac12-2586-4785-b327-3b420ee1baf7)

##Configuração dos Serviços

**1. DHCP**
**2. DNS**
**3. WEB**
**4. FTP**
**5. NFS**

  

  
  








