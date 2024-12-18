# SeminarioRedes-4p
Repositório do seminário final da matéria de Redes 4º P


## Índice

1. [Descrição do Projeto](#descrição-do-projeto)
2. [Topologia da Rede](#topologia-da-rede)
3. [Segmentação de Sub-redes](#segmentação-de-sub-redes)
4. [Requisitos dos Serviços](#requisitos-dos-serviços)
5. [Configuração dos Serviços](#configuração-dos-serviços)
6. [Testes Realizados](#testes-realizados)


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

## Configuração dos Serviços

**DHCP**

1. Instale o DHCP
   
![{E701F5ED-3E83-4485-83DF-2F8BAEA15A22}](https://github.com/user-attachments/assets/3d5adb47-22c3-4efa-8851-9e5087872cf4)

3. Edite a configuração do DHCP

Comando:
   
![{4057C698-EA3B-4CA3-A093-B1E7499897B4}](https://github.com/user-attachments/assets/8577bc58-bbb1-4eee-bdbf-3b00a70a2ade)

Adicione:
  
![{F9D2F804-9655-492A-B773-499D5AAE3165}](https://github.com/user-attachments/assets/71a58b8d-cd36-44c0-b039-d3612f4cddd5)

4. Reinicie o DHCP:

![{A7B96FF9-00A9-42C5-9EB4-CF88EF0B6232}](https://github.com/user-attachments/assets/8ade45a5-e02d-4577-810d-cd3ad06740c3)

**DNS**
1. Instale o Bind9

Comando:

![{687B651D-AA62-460A-88DE-BDC84D3240FD}](https://github.com/user-attachments/assets/eb269361-ab12-47e6-a729-37b16694d4b4)

2. Configure o Bind9

Comando: 

![{BBB11DB6-02C2-4608-90D7-755C6CB912D3}](https://github.com/user-attachments/assets/42971205-f859-4852-b9e3-fc8702bff9c9)

Adicione:

![{652EA8D0-4F64-4EB5-B012-736A88435D28}](https://github.com/user-attachments/assets/aac0d57e-6aba-4209-b213-1dbb8a66928d)

3. Reinicie o Serviço:

![{85D26F8E-0F99-4A20-9064-76991412C4DE}](https://github.com/user-attachments/assets/6545b67f-95b0-4998-b1e6-be1d707146ef)

**WEB**
1. Instale o APACHE

Comando:

![{3AEC95DD-038E-443A-822F-A51618CAFB9A}](https://github.com/user-attachments/assets/c9d17ee3-fed0-4a67-8324-eab64c27959b)

2. Inicie e Habilite o serviço:

![{42448CB7-715F-4FE0-8B9A-D564F139A9FF}](https://github.com/user-attachments/assets/b1c7d636-a4a6-4963-96fd-293a270c38c0)

3. Teste o Servidor: Acesse o endereço IP da VM no navegador: http://192.168.1.X

**4. FTP**

1. Instale o FTP

![{A0911DB6-5517-4C30-B437-1B04284DF148}](https://github.com/user-attachments/assets/840e54cc-35a6-4782-bed0-f7fddb04104a)

2. Faça backup da configuração padrão:

![{8AFF17EC-5EB3-44CB-B8A1-5CD962D4F623}](https://github.com/user-attachments/assets/f04a7491-78c7-4c93-80a9-45f23720ed37)

3. Edite o arquivo de configuração:

![{609EE8A9-394B-4814-A1EB-F1667880F3FD}](https://github.com/user-attachments/assets/8df259c6-87b1-4b11-89dc-c97f4db6919d)

Configure as seguintes opções: 

![{2626CED8-1BE9-40C4-A271-DBDF927E5159}](https://github.com/user-attachments/assets/b5c9729e-ce65-4705-b7a4-af5d0ff90c2e)

4. Crie um diretório FTP para um usuário:

![{4AFD4963-1D13-4A32-A3AD-33A99A7B8041}](https://github.com/user-attachments/assets/a1b1fbe1-de23-441d-a125-ef4313f9cd1b)

5. Crie um usuário

![{96C572F6-77E6-4E20-B8B6-471B9B7FAB6B}](https://github.com/user-attachments/assets/3f6cb1b7-5709-408e-93fa-6b4a41428aa0)

6. Reinicie o serviço vsftpd:

![{5EA5AD63-DE7F-429F-9959-8FF9A3FC4454}](https://github.com/user-attachments/assets/19ba0e69-2703-49bd-8a83-ca7f7af1e761)

7. Teste a conexão FTP:

Use um cliente FTP como FileZilla ou o comando ftp:

![{D6B3B739-B59D-451E-8820-34E7CA5C0E5D}](https://github.com/user-attachments/assets/8565a092-1427-4fce-ad85-f7703038985b)

Entre com usuario e senha Configurados.

**NFS**

1. Instale o Servidor NFS:

![{C3557A73-84EA-445C-9EE9-083C35F18CCA}](https://github.com/user-attachments/assets/c66f8073-2e6e-413a-aa7a-62bf65450eaf)

2.Crie o diretório compartilhado:

![{D995B03B-C685-4B71-9C07-851BFDB6F799}](https://github.com/user-attachments/assets/e0497a23-9425-4a15-996e-311445a6d6e2)

3.Configure o NFS:

![{8873A44C-0F0B-47E5-BF48-D281BB7E63A6}](https://github.com/user-attachments/assets/e621591f-e03f-457e-ab6f-b21f02a66d1a)

Adicione:

![{DBC85B7D-1A7C-4B67-861D-33A634643461}](https://github.com/user-attachments/assets/fa6692fe-f00d-4cc1-b235-f85a8134b275)

4. Reinicie o serviço:
  
![{D5A31766-AF71-437C-9115-E779EC8F997A}](https://github.com/user-attachments/assets/d02ba397-15f6-43b0-b436-30a2897351f7)

5. Acesse do cliente:

![{EE021F38-BF0E-4A35-BC48-443CCFF6BA2A}](https://github.com/user-attachments/assets/a42d5efc-b9c0-4672-87bb-864923194862)

**VAGRANT** #Meu pior inimigo  

1.Instale o Vagrant:

![{7A91A949-042F-4726-AD96-3F4487039BF3}](https://github.com/user-attachments/assets/a8c58168-8c58-4aa5-bd23-3af01cf4dc1d)

2. Baixe e inicialize uma máquina Vagrant:

![{B7393BCE-5718-47B2-88E8-CE4C1395353E}](https://github.com/user-attachments/assets/1a4d9c53-56cf-4015-824a-6e937094c6ae)

3. Acesse a VM criada:

![{59E95B3D-0568-47FF-8B9D-171CC6115670}](https://github.com/user-attachments/assets/513541c4-d7ae-4c76-a81d-5ce694381b0f)

## Testes Realizados
**DHCP**
![WhatsApp Image 2024-12-18 at 18 21 47_598f2cb1](https://github.com/user-attachments/assets/8f311a17-3438-4486-b0db-ba10b854c91c)

![WhatsApp Image 2024-12-18 at 18 21 47_64ce20be](https://github.com/user-attachments/assets/80175bc5-db51-458a-883f-343989508b05)

**BIND69**

![WhatsApp Image 2024-12-18 at 18 21 47_0c3ebfc9](https://github.com/user-attachments/assets/eb7b2688-8a25-429f-b864-26a1a653882a)

**APACHE**

![WhatsApp Image 2024-12-18 at 18 21 47_5ffc313b](https://github.com/user-attachments/assets/5589de50-eaf4-4226-91b7-1590c077ecb0)

**FTP**

![WhatsApp Image 2024-12-18 at 18 21 47_60fd7dfb](https://github.com/user-attachments/assets/f91982f7-6446-4306-b9e2-f54f66a385e9)


**Computador HOST acessando o arquivo padrão do Apache que se encontra dentro da Virtual Box por meio de IP**

![WhatsApp Image 2024-12-18 at 18 22 00_72212b0e](https://github.com/user-attachments/assets/1a92a4bd-8ae6-46c5-94ab-788fc655cf86)












