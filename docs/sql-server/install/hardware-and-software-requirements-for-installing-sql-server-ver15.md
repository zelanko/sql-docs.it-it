---
title: Requisiti hardware e software per l'installazione di SQL Server | Microsoft Docs
ms.custom: sqlfreshmay19
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Setup [SQL Server], software
- software [SQL Server]
- installing SQL Server, software
- operating systems [SQL Server], SQL Server requirements
- Setup [SQL Server], cross-language support
- operating systems [SQL Server], cross-language support
- network connections [SQL Server], requirements
- disk space [SQL Server], SQL Server installations
- WOW [SQL Server]
- Setup [SQL Server], hardware
- dependencies [SQL Server], SQL Server installations
- cluster hardware requirements [SQL Server]
- endpoints [SQL Server], SQL Server installations
- Internet [SQL Server], SQL Server installations
- hardware [SQL Server]
- Windows on Windows [SQL Server]
- installing SQL Server, hardware
- Setup Configuration Checker
- SCC [SQL Server]
- operating systems [SQL Server]
- space [SQL Server], SQL Server installations
- system configuration checker
- installing SQL Server, cross-language support
- Internet [SQL Server]
- space [SQL Server]
- extended system support [SQL Server]
- 64-bit edition [SQL Server]
- failover clustering [SQL Server]
- failover clustering [SQL Server], hardware requirements
- 32-bit edition [SQL Server]
- locales [SQL Server], SQL Server installations
- cross-language support
- disk space [SQL Server]
- localized SQL Server versions
ms.assetid: 09bcf20b-0a40-4131-907f-b61479d5e4d8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: aca31d10c030c360dcd82d6c4851df700bc3c4fe
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "74319046"
---
# <a name="hardware-and-software-requirements-for-installing-sql-server"></a>Requisiti hardware e software per l'installazione di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo elenca i requisiti hardware e software minimi per l'installazione e l'esecuzione di [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] nel sistema operativo Windows.

In [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] è stato introdotto il supporto per [!INCLUDE[sscurrent](../../includes/sssqlv14-md.md)] in Linux. Per altre informazioni, vedere [Requisiti hardware e software per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] su Linux](../../linux/sql-server-linux-setup.md#system). 

**Per provarlo:**  
  
- Eseguire il download di SQL Server da [**Evaluation Center**.](https://www.microsoft.com/evalcenter/evaluate-sql-server-2019-rc) 
  
<!-- 
- Spin up a Virtual Machine with [**SQL Server 2017**](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) already installed.  
-->
  
**Le considerazioni seguenti sono valide per tutte le edizioni:**  
  
- Le installazioni su unità di sola lettura, di cui è stato eseguito il mapping o sono state compresse verranno bloccate dal programma di installazione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
- L'installazione ha esito negativo se viene avviata tramite connessione Desktop remoto con il supporto su una risorsa locale del client connessione Desktop remoto. Per installare il supporto in remoto, questo deve essere in una condivisione di rete o in una macchina virtuale o fisica locale. Il supporto di installazione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può trovarsi in una condivisione di rete, un'unità mappata, un'unità locale o presentato come un file ISO per una macchina virtuale.
- Tramite il programma di installazione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono installati i seguenti componenti software necessari per il funzionamento del prodotto:  
  
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] File di supporto per l'installazione  

##  <a name="hwswr"></a> Requisiti hardware e software  
I requisiti seguenti si applicano a tutte le installazioni:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|Sistema operativo|Windows 10 TH1 1507 o versione successiva<br/><br>Windows Server 2016 o versione successiva<br/><br/>
|.NET Framework|I sistemi operativi minimi devono includere almeno .NET Framework.|  
|Software di rete|I sistemi operativi supportati per [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] includono software di rete integrato. Le istanze denominate e predefinite di un'installazione autonoma supportano i protocolli di rete seguenti: Memoria condivisa, named pipe e TCP/IP.<br/><br/> |  
|Disco rigido|Per[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] sono necessari almeno 6 GB di spazio libero su disco rigido.<br/><br/> I requisiti di spazio su disco variano a seconda dei componenti di [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] installati. Per altre informazioni, vedere [Requisiti di spazio su disco rigido](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace) più avanti in questo articolo. Per informazioni sui tipi di archiviazione supportati per i file di dati, vedere [Storage Types for Data Files](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes).|  
|Monitorare|Per[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] è necessario un monitor con risoluzione Super-VGA (800 x 600) o superiore.|  
|Internet|Per la funzionalità Internet è necessario l'accesso a Internet (potrebbero essere applicati costi aggiuntivi).|  

> [!NOTE]
> L'esecuzione di [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] su una macchina virtuale risulterà più lenta rispetto all'esecuzione in modalità nativa a causa dell'overhead della virtualizzazione.  

> [!IMPORTANT]
> Vi sono altri requisiti hardware e software per la funzionalità PolyBase. Per altre informazioni, vedere [Get started with PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)(Introduzione a PolyBase).  
  
##  <a name="pmosr"></a> Requisiti del processore, della memoria e del sistema operativo  
 I seguenti requisiti di memoria e processore si applicano a tutte le edizioni di [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|Memoria \*|**Minimo:**<br/><br/> Edizioni Express: 512 MB<br/><br/> Tutte le altre edizioni: 1 GB<br/><br/> **Consigliato:**<br/><br/> Edizioni Express: 1 GB<br/><br/> Tutte le altre edizioni: almeno 4 GB, che devono essere incrementati con l'aumentare delle dimensioni del database per garantire prestazioni ottimali.|  
|Velocità del processore|**Minima**: processore x64: 1,4 GHz<br/><br/> **Consigliato:** almeno 2 GHz|  
|Tipo di processore|Processore x64: AMD Opteron, AMD Athlon 64, Intel Xeon con supporto Intel EM64T, Intel Pentium IV con supporto EM64T|  
  
> [!NOTE]  
> L'installazione di [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] è supportata solo su processori x64, non è più supportata su processori x86.  
  
 \* La quantità di memoria minima richiesta per l'installazione del componente [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] in [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) è 2 GB di RAM, diversa dal requisito minimo di memoria di [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]. Per informazioni sull'installazione di DQS, vedere [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  

**Supporto di Server Core:**

L'installazione di SQL Server 2019 nella modalità Server Core è supportata dalle edizioni di Windows Server seguenti:

|                              |
| :------------------------  |
| Windows Server 2019 Core | 
| Windows Server 2016 Core |
| &nbsp; | 

Per altre informazioni sull'installazione di SQL Server in Server Core, vedere [Installare SQL Server in Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md).  

###  <a name="TOP_Principal"></a> Compatibilità del sistema operativo   

Nella tabella seguente sono indicate le edizioni di SQL Server 2019 compatibili con le varie versioni di Windows:  
  

| Edizione di SQL Server:               | Enterprise | Developer | Standard | Web | Express |  
| :------------------------         | :--------- | :-------- | :------- | :-- | :------ | 
| Windows Server 2019 Datacenter    |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2019 Standard      |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2019 Essentials    |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2016 Datacenter    |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2016 Standard      |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2016 Essentials    |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows 10 Enterprise             |    No      |    Sì    |    Sì   | No  |   Sì   |
| Windows 10 Professional           |    No      |    Sì    |    Sì   | No  |   Sì   |
| Windows 10 Home                   |    No      |    Sì    |    Sì   | No  |   Sì   |
| &nbsp; | &nbsp; |


##  <a name="CrossLanguageSupport"></a> Supporto di lingue diverse  
 Per altre informazioni sul supporto di lingue diverse e per considerazioni relative all'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nelle lingue localizzate, vedere [Versioni in lingua locale di SQL Server](../../sql-server/install/local-language-versions-in-sql-server.md).  
  
##  <a name="HardDiskSpace"></a> Requisiti di spazio su disco rigido  
 Durante l'installazione di [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]vengono creati alcuni file temporanei nell'unità di sistema. Prima di eseguire il programma di installazione per installare o aggiornare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verificare che nell'unità di sistema siano disponibili almeno 6,0 GB di spazio su disco per tali file. Tale requisito deve essere soddisfatto anche se tutti i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono installati in un'unità di sistema non predefinita.  
  
 I requisiti effettivi di spazio su disco rigido possono variare in base alla configurazione del sistema e alle funzionalità selezionate per l'installazione. Nella tabella seguente vengono indicati i requisiti di spazio su disco dei componenti di [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] .  
  
|**Funzionalità**|**Requisito di spazio su disco**|  
|-----------------|--------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] e file di dati, replica, ricerca full-text e Data Quality Services|1480 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (come sopra) con R Services (In-Database)|2744 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] come sopra con Servizio Query PolyBase per i dati esterni|4194 MB|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e file di dati|698 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|967 MB|  
|[!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] (Standalone)|280 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint|1203 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - Componente aggiuntivo per prodotti SharePoint|325 MB|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|121 MB|  
|Connettività strumenti client|328 MB|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|306 MB|  
|Componenti client, diversi dai componenti della documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e dagli strumenti di Integration Services|445 MB|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|280 MB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Componenti della documentazione online per visualizzare e gestire il contenuto della Guida*|27 MB|  
|Tutte le funzionalità|8030 MB|  
  
 *Il requisito di spazio su disco per il contenuto della documentazione online scaricato è pari a 200 MB.  
  
##  <a name="StorageTypes"></a> Tipi di archiviazione per i file di dati  
 I tipi di archiviazione supportati per i file di dati sono:  
  
- Disco locale 
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attualmente supporta unità disco con dimensioni del settore native standard di 512 byte e 4 KB.  I dischi rigidi con dimensioni del settore superiori a 4KB possono causare errori durante il tentativo di archiviazione dei file di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sui dischi.  Vedere [Limiti di dimensioni del settore supportati da unità disco rigido in SQL Server](https://support.microsoft.com/kb/926930) per altre informazioni sulle dimensioni del settore dei dischi rigidi supportate in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 
    - Il disco locale è supportato nell'installazione del cluster di failover di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo per l'installazione dei file tempdb. Assicurarsi che il percorso specificato per i file di dati tempdb e di log sia valido su tutti i nodi del cluster. Durante il failover, se le directory tempdb non sono disponibili nel nodo di destinazione del failover, la risorsa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non verrà riportata online.
- Archiviazione condivisa  
- [Spazi di archiviazione diretta \(S2D\)](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)  
- Condivisione file SMB  
    - L'archiviazione SMB non è supportata per i file di dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per le installazioni autonome o cluster. Usare invece l'archiviazione collegata direttamente, una rete SAN o S2D. 
    - L'archiviazione SMB può essere ospitata da un file server di Windows o da un dispositivo di archiviazione SMB di terze parti. Nel primo caso, la versione del file server di Windows deve essere la versione 2008 o successiva. Per ulteriori informazioni sull'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una condivisione file SMB come opzione di archiviazione, vedere [Installazione di SQL Server con l'opzione di archiviazione su condivisione file SMB](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
  
  
  
##  <a name="DC_support"></a> Installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un controller di dominio  
 Per motivi di sicurezza, è consigliabile non installare [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] in un controller di dominio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ma verranno applicate le limitazioni seguenti:  
  
- Non è possibile eseguire servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un controller di dominio utilizzando un account Servizio locale.    
- Al termine dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un computer, non è possibile modificare il computer da membro di dominio a controller di dominio. Prima di modificare il computer host in controller di dominio, è necessario disinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .    
- Al termine dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un computer, non è possibile modificare il computer da controller di dominio a membro di dominio. Prima di modificare il computer host in membro di dominio, è necessario disinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .   
- Le istanze del cluster di failover di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non sono supportate quando i nodi del cluster sono controller di dominio.   
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è supportato in un controller di dominio di sola lettura. Tramite il programma di installazione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non sarà possibile creare gruppi di sicurezza o fornire account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un controller di dominio di sola lettura. In questo scenario il programma di installazione non verrà completato. 
- Un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è supportata in un ambiente in cui si può accedere solo a un controller di dominio di sola lettura. 
  
## <a name="see-also"></a>Vedere anche  
 [Pianificazione di un'installazione di SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Considerazioni sulla sicurezza per un'installazione di SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   

