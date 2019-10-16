---
title: Requisiti hardware e software per l'installazione di SQL Server | Microsoft Docs
ms.custom: sqlfreshmay19
ms.date: 07/24/2019
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
ms.openlocfilehash: 79818fa5cb41b27a15d531f22a21b86c10cb018a
ms.sourcegitcommit: 84e6922a57845a629391067ca4803e8d03e0ab90
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2019
ms.locfileid: "72008465"
---
# <a name="hardware-and-software-requirements-for-installing-sql-server"></a>Hardware and Software Requirements for Installing SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo elenca i requisiti hardware e software minimi per l'installazione e l'esecuzione di [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] nel sistema operativo Windows. 

In [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] è stato introdotto il supporto per [!INCLUDE[sscurrent](../../includes/sssqlv14-md.md)] in Linux. Per altre informazioni, vedere [Requisiti hardware e software per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] su Linux](../../linux/sql-server-linux-setup.md#system). 

  
**Per provarlo:**  
  
-   Eseguire il download di SQL Server da [**Evaluation Center**.](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) 
  
-   Accedere a una macchina virtuale con [**SQL Server 2017**](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) già installato.  
  
**Le considerazioni seguenti sono valide per tutte le edizioni:**  
  
-   È consigliabile eseguire [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] nei computer con il formato file NTFS o ReFS. L'installazione di [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] in un computer con file system FAT32 è supportata ma non consigliata, perché questo file system è meno sicuro di NTFS o ReFS.  
  
-   Le installazioni su unità di sola lettura, di cui è stato eseguito il mapping o sono state compresse verranno bloccate dal programma di installazione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   L'installazione ha esito negativo se viene avviata tramite connessione Desktop remoto con il supporto su una risorsa locale del client connessione Desktop remoto. Per installare il supporto in remoto, questo deve essere in una condivisione di rete o in una macchina virtuale o fisica locale. Il supporto di installazione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può trovarsi in una condivisione di rete, un'unità mappata, un'unità locale o presentato come un file ISO per una macchina virtuale.  
  
-   L'installazione di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] richiede .NET 4.6.1 come prerequisito. .NET 4.6.1 verrà installato automaticamente quando si seleziona [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] durante l'installazione.  
  
-   Tramite il programma di installazione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono installati i seguenti componenti software necessari per il funzionamento del prodotto:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] File di supporto per l'installazione  
  
-   Per i requisiti minimi di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[win8srv](../../includes/win8srv-md.md)] o [!INCLUDE[win8](../../includes/win8-md.md)], vedere [Installazione di SQL Server in Windows Server 2012 o Windows 8](https://support.microsoft.com/kb/2681562).  
  
##  <a name="hwswr"></a> Requisiti hardware e software  
I requisiti seguenti si applicano a tutte le installazioni:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|.NET Framework|[!INCLUDE[sql2016](../../includes/sssql15-md.md)] RC1 e versioni successive richiedono [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6 per il motore di database, Master Data Services o la replica. Il programma di installazione di SQL Server installa automaticamente [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. È anche possibile installare manualmente [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] da [Microsoft .NET Framework 4.6 (programma di installazione Web) per Windows](https://support.microsoft.com/kb/3045560).<br/><br/>[!INCLUDE[sql2019](../../includes/sssqlv15-md.md)] richiede .NET Framework 4.6.2. Disponibile dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53344)<br/><br/> Per altre informazioni, suggerimenti e indicazioni su [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6 vedere [Guida alla distribuzione di .NET Framework per sviluppatori](https://msdn.microsoft.com/library/ee942965\(v=vs.110\).aspx).<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]e [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)] richiedono [KB2919355](https://support.microsoft.com/kb/2919355) prima di installare [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6.|  
|Software di rete|I sistemi operativi supportati per [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] includono software di rete integrato. Le istanze denominate e predefinite di un'installazione autonoma supportano i protocolli di rete seguenti: Memoria condivisa, named pipe, TCP/IP e VIA.<br/><br/> **Nota:** il protocollo VIA non è supportato nei cluster di failover. I client o le applicazioni in esecuzione sullo stesso nodo del cluster di failover dell'istanza di SQL Server, possono usare il protocollo Shared Memory per la connessione a SQL Server tramite il relativo indirizzo pipe locale. Tuttavia questo tipo di connessione non è in grado di riconoscere il cluster e avrà esito negativo dopo un failover dell'istanza. Pertanto non è consigliata e deve essere usata solo in scenari molto specifici.<br/><br/> **Importante:** Il protocollo VIA è deprecato. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br/><br/> Per ulteriori informazioni su protocolli e librerie di rete, vedere [Network Protocols and Network Libraries](../../sql-server/install/network-protocols-and-network-libraries.md).|  
|Disco rigido|Per[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] sono necessari almeno 6 GB di spazio libero su disco rigido.<br/><br/> I requisiti di spazio su disco variano a seconda dei componenti di [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] installati. Per altre informazioni, vedere [Requisiti di spazio su disco rigido](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace) più avanti in questo articolo. Per informazioni sui tipi di archiviazione supportati per i file di dati, vedere [Storage Types for Data Files](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes).|  
|Unità|Per l'installazione da disco è necessaria un'unità DVD.|  
|Monitoraggio|Per[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] è necessario un monitor con risoluzione Super-VGA (800 x 600) o superiore.|  
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
  
 **Supporto WOW64:**  
  
 WOW64 (Windows 32-bit on Windows 64-bit) è una funzionalità delle edizioni a 64 bit di Windows che consente l'esecuzione a livello nativo in modalità a 32 bit delle applicazioni a 32 bit. Le applicazioni verranno eseguite in modalità a 32 bit anche se il sistema operativo sottostante viene eseguito a 64 bit. La funzionalità WOW64 non è supportata per le installazioni di [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] . Tuttavia, gli strumenti di gestione sono supportati in WOW64.  


**Supporto di Server Core:**

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions" 

L'installazione di SQL Server 2019 nella modalità Server Core è supportata dalle edizioni di Windows Server seguenti:

|                              |                                |
| :------------------------    | :------------------------------|
| Windows Server 2019 Standard | Windows Server 2019 Datacenter |
| Windows Server 2016 Standard | Windows Server 2016 Datacenter |
   | &nbsp; | &nbsp; |

::: moniker-end

::: moniker range=">=sql-server-2016 <=sql-server-2017||=sqlallproducts-allversions"

L'installazione di SQL Server 2016 e 2017 nella modalità Server Core è supportata dalle edizioni di Windows Server seguenti:

|                              |                                |
| :------------------------    | :------------------------------|
| Windows Server 2019 Standard | Windows Server 2019 Datacenter |
| Windows Server 2016 Standard | Windows Server 2016 Datacenter |
| Windows Server 2012 R2 Standard | Windows Server 2012 R2  Datacenter|
| Windows Server 2012 Standard | Windows Server 2012 Datacenter |
| Windows Server 2008 R2 SP1 Standard | Windows Server 2008 R2 SP1 Datacenter |
| Windows Server 2008 R2 SP1 Enterprise | Windows Server 2008 R2 SP1 Web|
   | &nbsp; | &nbsp; |
::: moniker-end

Per altre informazioni sull'installazione di SQL Server in Server Core, vedere [Installare SQL Server in Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md).  

  
### <a name="features-supported-on-32-bit-client-operating-systems"></a>Funzionalità supportate nei sistemi operativi client a 32 bit  
 I sistemi operativi client Windows, ad esempio Windows 10 e Windows 8.1, sono disponibili come architetture a 32 o a 64 bit.   Tutte le funzionalità di SQL Server sono supportate in sistemi operativi client a 64 bit. Nei sistemi operativi client a 32 bit Microsoft supporta le funzionalità seguenti:  
  
-   Client Data Quality
-   Connettività strumenti client
-   Integration Services
-   Compatibilità con le versioni precedenti di strumenti client
-   SDK di strumenti client
-   Componenti della documentazione
-   Componenti di Riesecuzione distribuita
-   Controller di Riesecuzione distribuita
-   Client Riesecuzione distribuita
-   SDK di Connettività SQL Client
  
 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] e sistemi operativi del server successivi non sono disponibili come architetture a 32 bit. Tutti i sistemi operativi server supportati sono disponibili solo a 64 bit. Tutte le funzionalità sono supportate in sistemi operativi server a 64 bit.  
  
###  <a name="TOP_Principal"></a> Compatibilità del sistema operativo   

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions" 
Nella tabella seguente sono indicate le edizioni di SQL Server 2019 compatibili con le varie versioni di Windows:  
  

| Edizione di SQL Server:               | Enterprise | Developer | Standard | Web | Express |  
| :------------------------         | :--------- | :-------- | :------- | :-- | :------ | 
| Windows Server 2019 Datacenter    |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2019 Standard      |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2019 Essentials    |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2016 Datacenter    |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2016 Standard      |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2016 Essentials    |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| &nbsp; | &nbsp; |
::: moniker-end

::: moniker range=">=sql-server-2016 <=sql-server-2017||=sqlallproducts-allversions"

Nella tabella seguente sono indicate le edizioni di SQL Server 2016 e 2017 compatibili con le varie versioni di Windows:  
  
| Edizione di SQL Server:               | Enterprise | Developer | Standard | Web | Express |  
| :------------------------         | :--------- | :-------- | :------- | :-- | :------ | 
| Windows Server 2019 Datacenter    |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2019 Standard      |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2019 Essentials    |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2016 Datacenter    |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2016 Standard      |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2016 Essentials    |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2012 R2 Datacenter |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2012 R2 Standard   |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2012 R2 Essentials |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2012 R2 Foundation |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2012 Datacenter    |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2012 Standard      |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2012 Essentials    |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows Server 2012 Foundation    |    Sì     |    Sì    |    Sì   | Sì |   Sì   |
| Windows 10 IoT Enterprise         |    no      |    Sì    |    Sì   | no  |   Sì   |
| Windows 10 Enterprise             |    no      |    Sì    |    Sì   | no  |   Sì   |
| Windows 10 Professional           |    no      |    Sì    |    Sì   | no  |   Sì   |
| Windows 10 Home                   |    no      |    Sì    |    Sì   | no  |   Sì   |
| Windows 8.1 Enterprise            |    no      |    Sì    |    Sì   | no  |   Sì   |
| Windows 8.1 Pro                   |    no      |    Sì    |    Sì   | no  |   Sì   |
| Windows 8.1 Enterprise            |    no      |    Sì    |    Sì   | no  |   Sì   |
| Windows 8 Pro                     |    no      |    Sì    |    Sì   | no  |   Sì   |
| Windows 8                         |    no      |    Sì    |    Sì   | no  |   Sì   | 

> [!NOTE]  
> Le seguenti funzionalità di [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e versioni precedenti costituiscono un'eccezione rispetto ai sistemi operativi supportati elencati in questa sezione in quanto possono essere installate in Windows Server 2008 R2 SP1 o versioni successive:  
>  
>-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint  
>-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - Componente aggiuntivo per prodotti SharePoint  
::: moniker-end


  
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
  
-   Disco locale 
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attualmente supporta unità disco con dimensioni del settore native standard di 512 byte e 4 KB.  I dischi rigidi con dimensioni del settore superiori a 4KB possono causare errori durante il tentativo di archiviazione dei file di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sui dischi.  Vedere [Limiti di dimensioni del settore supportati da unità disco rigido in SQL Server](https://support.microsoft.com/kb/926930) per altre informazioni sulle dimensioni del settore dei dischi rigidi supportate in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 
    - Il disco locale è supportato nell'installazione del cluster di failover di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo per l'installazione dei file tempdb. Assicurarsi che il percorso specificato per i file di dati tempdb e di log sia valido su tutti i nodi del cluster. Durante il failover, se le directory tempdb non sono disponibili nel nodo di destinazione del failover, la risorsa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non verrà riportata online.
-   Archiviazione condivisa  
-   [Spazi di archiviazione diretta \(S2D\)](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)  
-   Condivisione file SMB  
    - L'archiviazione SMB non è supportata per i file di dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per le installazioni autonome o cluster. Usare invece l'archiviazione collegata direttamente, una rete SAN o S2D. 
    - L'archiviazione SMB può essere ospitata da un file server di Windows o da un dispositivo di archiviazione SMB di terze parti. Nel primo caso, la versione del file server di Windows deve essere la versione 2008 o successiva. Per ulteriori informazioni sull'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una condivisione file SMB come opzione di archiviazione, vedere [Installazione di SQL Server con l'opzione di archiviazione su condivisione file SMB](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
  
  
  
##  <a name="DC_support"></a> L'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un controller di dominio  
 Per motivi di sicurezza, è consigliabile non installare [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] in un controller di dominio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ma verranno applicate le limitazioni seguenti:  
  
-   Non è possibile eseguire servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un controller di dominio utilizzando un account Servizio locale.    
-   Al termine dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un computer, non è possibile modificare il computer da membro di dominio a controller di dominio. Prima di modificare il computer host in controller di dominio, è necessario disinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .    
-   Al termine dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un computer, non è possibile modificare il computer da controller di dominio a membro di dominio. Prima di modificare il computer host in membro di dominio, è necessario disinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .   
-   Le istanze del cluster di failover di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non sono supportate quando i nodi del cluster sono controller di dominio.   
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è supportato in un controller di dominio di sola lettura. Tramite il programma di installazione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non sarà possibile creare gruppi di sicurezza o fornire account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un controller di dominio di sola lettura. In questo scenario il programma di installazione non verrà completato. 

  > [!NOTE]
  > Questa restrizione si applica anche alle installazioni nei nodi membro del dominio.

- Un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è supportata in un ambiente in cui si può accedere solo a un controller di dominio di sola lettura. 

  > [!NOTE]
  > Questa restrizione si applica anche alle installazioni nei nodi membro del dominio.
  
## <a name="see-also"></a>Vedere anche  
 [Pianificazione di un'installazione di SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Considerazioni sulla sicurezza per un'installazione di SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   

