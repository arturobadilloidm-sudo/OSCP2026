# 6. Information Gathering


El information Gatering es la fase en la que se recopila información para realizar el mapeo de la superficie de ataque de una compañia, es decir , se identifican IPś , puertos, dominios, servicios etc.. que estan expuestos en la superficie de ataque.
## 6.1. The Penetration Testing Lifecycle

A typical penetration test comprises the following stages:

- Defining the Scope
- Information Gathering
- Vulnerability Detection
- Initial Foothold
- Privilege Escalation
- Lateral Movement
- Reporting/Analysis
- Lessons Learned/Remediation


	En la fase inicial obtendremos los elementos basicos que haran posible el hambiente de ataque.

ACTIVE RECON:  Se tiene interacción directamente con la infraestructura.
PASIVE RECON: Se recopila información del target de manera indirecta (shodan, osit, ingenieria social).

## 6.2. Passive Information Gathering

This Learning Unit covers the following Learning Objectives:

- Understand the Two Different Passive Information Gathering Approaches
- Learn About Open-Source Intelligence (OSINT)
- Understand Web Server and DNS Passive Information Gathering


Fase en la que se adquiere de manera indirecta los primeros indicios de acceso hacia el Target.
Tirar ansuelos o ver previamente el campo.


## 6.2.1. Whois Enumeration

Whois es un protocolo que utiliza el puerto 43 del TCP para comunicarse  bases de datos público. La herramienta whois consulta las bases de datos para recuperar dominio Registros de registro.


- [_Nombre Servidor_](https://www.forbes.com/advisor/business/software/what-is-a-name-server/) : Estos servidores son parte del [_Nombre_](https://www.internetsociety.org/resources/doc/2023/fact-sheet-encrypted-dns) de [](https://www.internetsociety.org/resources/doc/2023/fact-sheet-encrypted-dns)(DNS) y ayudar a traducir los nombres de dominio en direcciones IP, dirigiendo tráfico al servidor web apropiado.
    
- [_Secretario de la_](https://www.cloudflare.com/learning/dns/glossary/what-is-a-domain-name-registrar/) La empresa a través de la cual se registró el nombre de dominio. 
    
- _Registante Contacto:_ La persona o organización que legalmente es dueño del dominio. Esto puede incluir un nombre, organización, correo electrónico, y número de teléfono.
    
- _Contacto Administrativo_ : La persona responsable de la gestión del dominio propiedad y acceso. A menudo el principal punto de contacto para dominio cambios.
    
- _Contacto técnico:_ El individuo o equipo que gestiona el Configuración técnica de dominio, como registros DNS o integración de servidores.
    
- _Fechas de creación y Expiración:_ Cuando el dominio fue primero registrada y cuando expira. Esto ayuda a evaluar cuánto tiempo un el dominio ha estado activo.
    
- _Estado de dominio_ : Elementos que indican si el dominio está bloqueado, activo, o en transferencia


Con el comando  whois megacorpone.com -h 192.168.50.251 podemos recopliar información relevante de una empresa

```

kali@kali:~$ whois megacorpone.com -h 192.168.50.251
   Domain Name: MEGACORPONE.COM
   Registry Domain ID: 1775445745_DOMAIN_COM-VRSN
   Registrar WHOIS Server: whois.gandi.net
   Registrar URL: http://www.gandi.net
   Updated Date: 2019-01-01T09:45:03Z
   Creation Date: 2013-01-22T23:01:00Z
   Registry Expiry Date: 2023-01-22T23:01:00Z
...
Registry Registrant ID: 
Registrant Name: Alan Grofield
Registrant Organization: MegaCorpOne
Registrant Street: 2 Old Mill St
Registrant City: Rachel
Registrant State/Province: Nevada
Registrant Postal Code: 89001
Registrant Country: US
Registrant Phone: +1.9038836342
...
Registry Admin ID: 
Admin Name: Alan Grofield
Admin Organization: MegaCorpOne
Admin Street: 2 Old Mill St
Admin City: Rachel
Admin State/Province: Nevada
Admin Postal Code: 89001
Admin Country: US
Admin Phone: +1.9038836342
...
Registry Tech ID: 
Tech Name: Alan Grofield
Tech Organization: MegaCorpOne
Tech Street: 2 Old Mill St
Tech City: Rachel
Tech State/Province: Nevada
Tech Postal Code: 89001
Tech Country: US
Tech Phone: +1.9038836342
...
Name Server: NS1.MEGACORPONE.COM
Name Server: NS2.MEGACORPONE.COM
Name Server: NS3.MEGACORPONE.COM
...
```



LAb

Hacer una consulta WHOIS al dominio megacorpone.com utilizando la dirección IP de la máquina virtual como servidor WHOIS. ¿Cuál es el nombre de host del tercer servidor de nombres de Megacorp One?

1. NS3.MEGACORPONE.COM


ver si el puerto tcp 43 esta abierto
```
telnet  192.168.59.251 43
```


```
$ whois megacorpone.com -h 192.168.59.251
% IANA WHOIS server
% for more information on IANA, visit http://www.iana.org
% This query returned 1 object

refer:        whois.verisign-grs.com

domain:       COM

organisation: VeriSign Global Registry Services
address:      12061 Bluemont Way
address:      Reston Virginia 20190
address:      United States

contact:      administrative
name:         Registry Customer Service
organisation: VeriSign Global Registry Services
address:      12061 Bluemont Way
address:      Reston Virginia 20190
address:      United States
phone:        +1 703 925-6999
fax-no:       +1 703 948 3978
e-mail:       info@verisign-grs.com

contact:      technical
name:         Registry Customer Service
organisation: VeriSign Global Registry Services
address:      12061 Bluemont Way
address:      Reston Virginia 20190
address:      United States
phone:        +1 703 925-6999
fax-no:       +1 703 948 3978
e-mail:       info@verisign-grs.com

nserver:      A.GTLD-SERVERS.NET 192.5.6.30 2001:503:a83e:0:0:0:2:30
nserver:      B.GTLD-SERVERS.NET 192.33.14.30 2001:503:231d:0:0:0:2:30
nserver:      C.GTLD-SERVERS.NET 192.26.92.30 2001:503:83eb:0:0:0:0:30
nserver:      D.GTLD-SERVERS.NET 192.31.80.30 2001:500:856e:0:0:0:0:30
nserver:      E.GTLD-SERVERS.NET 192.12.94.30 2001:502:1ca1:0:0:0:0:30
nserver:      F.GTLD-SERVERS.NET 192.35.51.30 2001:503:d414:0:0:0:0:30
nserver:      G.GTLD-SERVERS.NET 192.42.93.30 2001:503:eea3:0:0:0:0:30
nserver:      H.GTLD-SERVERS.NET 192.54.112.30 2001:502:8cc:0:0:0:0:30
nserver:      I.GTLD-SERVERS.NET 192.43.172.30 2001:503:39c1:0:0:0:0:30
nserver:      J.GTLD-SERVERS.NET 192.48.79.30 2001:502:7094:0:0:0:0:30
nserver:      K.GTLD-SERVERS.NET 192.52.178.30 2001:503:d2d:0:0:0:0:30
nserver:      L.GTLD-SERVERS.NET 192.41.162.30 2001:500:d937:0:0:0:0:30
nserver:      M.GTLD-SERVERS.NET 192.55.83.30 2001:501:b1f9:0:0:0:0:30
ds-rdata:     30909 8 2 E2D3C916F6DEEAC73294E8268FB5885044A833FC5459588F4A9184CFC41A5766

whois:        whois.verisign-grs.com

status:       ACTIVE
remarks:      Registration information: http://www.verisigninc.com

created:      1985-01-01
changed:      2017-10-05
source:       IANA

# whois.verisign-grs.com

   Domain Name: MEGACORPONE.COM
   Registry Domain ID: 1775445745_DOMAIN_COM-VRSN
   Registrar WHOIS Server: whois.gandi.net
   Registrar URL: http://www.gandi.net
   Updated Date: 2021-06-15T17:59:57Z
   Creation Date: 2013-01-22T23:01:00Z
   Registry Expiry Date: 2024-01-22T23:01:00Z
   Registrar: Gandi SAS
   Registrar IANA ID: 81
   Registrar Abuse Contact Email: abuse@support.gandi.net
   Registrar Abuse Contact Phone: +33.170377661
   Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
   Name Server: NS1.MEGACORPONE.COM
   Name Server: NS2.MEGACORPONE.COM
   Name Server: NS3.MEGACORPONE.COM
   DNSSEC: unsigned
   URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/
>>> Last update of whois database: 2022-02-28T08:34:51Z <<<






```


Basándonos en la respuesta de la pregunta anterior, ¿cuál es el servidor WHOIS del Registrador?

La respuesta es  whois.gandi.net y se encuentra buscando el dato a lo largo del comando.

```
# whois.verisign-grs.com

   Domain Name: OFFENSIVE-SECURITY.COM
   Registry Domain ID: 606288052_DOMAIN_COM-VRSN
   Registrar WHOIS Server: whois.gandi.net
   Registrar URL: http://www.gandi.net
   Updated Date: 2021-08-24T17:36:03Z
   Creation Date: 2006-09-24T20:27:59Z
   Registry Expiry Date: 2022-09-24T20:27:59Z
   Registrar: Gandi SAS
   Registrar IANA ID: 81
   Registrar Abuse Contact Email: abuse@support.gandi.net
   Registrar Abuse Contact Phone: +33.170377661
   Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
   Name Server: NS-182-B.GANDI.NET
   Name Server: OS{1234}
   Name Server: NS-34-A.GANDI.NET
   DNSSEC: unsigned
   URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/
>>> Last update of whois database: 2022-02-28T10:40:03Z <<<

```

Realizar una consulta WHOIS en el dominio offensive-security.com contra la IP del equipo. El indicador se encuentra en la sección DNS del registro WHOIS.

con el comando:

whois offensive-security.com -h 192.168.62.251

la respuesta es  =     Name Server: OS{fe366b5cf4206b2c54e40fd1b07e49b5}

```
Registrant Phone: REDACTED FOR PRIVACY
Registrant Phone Ext:
Registrant Fax: REDACTED FOR PRIVACY
Registrant Fax Ext:
Registrant Email: OS{1234}
Registry Admin ID: REDACTED FOR PRIVACY
Admin Name: REDACTED FOR PRIVACY
Admin Organization: REDACTED FOR PRIVACY
Admin Street: REDACTED FOR PRIVACY
Admin City: REDACTED FOR PRIVACY
Admin State/Province: REDACTED FOR PRIVACY
Admin Postal Code: REDACTED FOR PRIVACY
Admin Country: REDACTED FOR PRIVACY
Admin Phone: REDACTED FOR PRIVACY
Admin Phone Ext:
Admin Fax: REDACTED FOR PRIVACY
Admin Fax Ext:
Admin Email: OS{1234}
Registry Tech ID: REDACTED FOR PRIVACY
Tech Name: REDACTED FOR PRIVACY
Tech Organization: REDACTED FOR PRIVACY
Tech Street: REDACTED FOR PRIVACY
Tech City: REDACTED FOR PRIVACY
Tech State/Province: REDACTED FOR PRIVACY
Tech Postal Code: REDACTED FOR PRIVACY
Tech Country: REDACTED FOR PRIVACY
Tech Phone: REDACTED FOR PRIVACY
Tech Phone Ext:
Tech Fax: REDACTED FOR PRIVACY
Tech Fax Ext:
Tech Email: 1224861dbf76da04cb0faff2ddb47834-14869841@contact.gandi.net
Name Server: NS-34-A.GANDI.NET
Name Server: NS-182-B.GANDI.NET
Name Server: OS{fe366b5cf4206b2c54e40fd1b07e49b5}
Name Server: 
Name Server:

```


Realiza una consulta WHOIS en el dominio kali.org contra la IP de la máquina. ¿Cuál es la dirección de correo electrónico del técnico?

se aplica el comando:

whois kali.org -h 192.168.62.251

la respuesta  =   Tech Email: OS{8d77e83ae92157e6809ba05d26a43af5}


Se busca en la salida del siguiente comando.

```
Admin State/Province: REDACTED FOR PRIVACY
Admin Postal Code: REDACTED FOR PRIVACY
Admin Country: REDACTED FOR PRIVACY
Admin Phone: REDACTED FOR PRIVACY
Admin Phone Ext:
Admin Fax: REDACTED FOR PRIVACY
Admin Fax Ext:
Admin Email: OS{1234}
Registry Tech ID: REDACTED FOR PRIVACY
Tech Name: REDACTED FOR PRIVACY
Tech Organization: REDACTED FOR PRIVACY
Tech Street: REDACTED FOR PRIVACY
Tech City: REDACTED FOR PRIVACY
Tech State/Province: REDACTED FOR PRIVACY
Tech Postal Code: REDACTED FOR PRIVACY
Tech Country: REDACTED FOR PRIVACY
Tech Phone: REDACTED FOR PRIVACY
Tech Phone Ext:
Tech Fax: REDACTED FOR PRIVACY
Tech Fax Ext:
Tech Email: OS{8d77e83ae92157e6809ba05d26a43af5}
Name Server: NS-34-A.GANDI.NET
Name Server: NS-182-B.GANDI.NET
Name Server: NS-185-C.GANDI.NET
Name Server: 
Name Server:
Name Server:
Name Server:
Name Server:
Name Server:
Name Server:
```







