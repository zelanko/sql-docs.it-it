---
title: Requisiti hardware e software per l'installazione di SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 07/10/2018
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: ce6cef69abe7c2461552229363c8334ca56555b4
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245660"
---
# <a name="hardware-and-software-requirements-for-installing-sql-server-2014"></a>Requisiti hardware e software per l'installazione di SQL Server 2014

 > - Provare SQL Server 2016 installando la ** [versione gratuita Developer Edition](https://my.visualstudio.com/Downloads?q=SQL%20Server%20Developer).**  
  
## <a name="considerations"></a>Considerazioni 
  
-   È consigliabile eseguire [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] in computer con il formato di file NTFS. Il file system FAT32 è supportato ma non consigliato perché è meno sicuro rispetto al file system NTFS.  
  
-   Non è possibile installare in unità di sola lettura, con mapping o compresse.  
  
-   Per consentire l'installazione corretta del componente di Visual Studio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario installare un aggiornamento. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Il programma di installazione verifica la presenza di questo aggiornamento, quindi richiede di scaricare e installare l'aggiornamento prima di poter continuare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'installazione. Per evitare l'interruzione durante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'installazione, scaricare e installare l'aggiornamento **prima di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eseguire l'installazione** , come descritto di seguito (o installare tutti gli aggiornamenti per .NET 3,5 SP1 disponibili in Windows Update):  
  
    -   Per [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2, ottenere l'aggiornamento necessario [qui](https://go.microsoft.com/fwlink/?LinkId=198093).  
  
    -   Per tutti gli altri sistemi operativi supportati, questo aggiornamento è incluso.  
  
-   L'avvio del programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite il client di Servizi terminal non è supportato. L'installazione non riesce se si avvia il programma di installazione tramite il client di Servizi terminal.   
  
-   Tramite il programma di installazione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono installati i seguenti componenti software necessari per il funzionamento del prodotto:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client  
  
    -   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] File di supporto per l'installazione  
  
-   Per i requisiti di versione minimi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per [!INCLUDE[win8srv](../../includes/win8srv-md.md)] l' [!INCLUDE[win8](../../includes/win8-md.md)]installazione di in o, vedere [installazione di SQL Server in Windows Server 2012 o Windows 8](https://support.microsoft.com/kb/2681562) (https://support.microsoft.com/kb/2681562).  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
-   [Requisiti hardware e software](hardware-and-software-requirements-for-installing-sql-server.md#hwswr)  
  
-   [Requisiti del processore, della memoria e del sistema operativo](hardware-and-software-requirements-for-installing-sql-server.md#pmosr)  
  
-   [Supporto tra linguaggi diversi](hardware-and-software-requirements-for-installing-sql-server.md#CrossLanguageSupport)  
  
-   [Supporto per sistemi estesi](hardware-and-software-requirements-for-installing-sql-server.md#ess)  
  
-   [Requisiti di spazio su disco rigido (32 bit e 64 bit)](hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace)  
  
-   [Tipi di archiviazione per i file di dati](hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)  
  
-   [Installazione di SQL Server in un controller di dominio](hardware-and-software-requirements-for-installing-sql-server.md#DC_support)  
  
##  <a name="hwswr"></a>Requisiti hardware e software  
 I requisiti seguenti si applicano a tutte le installazioni di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] :  
  
|Componente|Requisito|  
|---------------|-----------------|  
|.NET Framework|.NET 3.5 SP1 è un requisito necessario per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] se si seleziona [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)], Replica o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e non viene più installato tramite il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . <br />-Se si esegue il programma di installazione di e non si dispone di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .NET 3,5 SP1, il programma di installazione di richiede di scaricare e installare .NET 3,5 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SP1 prima di poter continuare l'installazione. Installare .NET 3,5 SP1 da [Microsoft .NET Framework 3,5 Service Pack 1](https://www.microsoft.com/download/details.aspx?id=22). Il messaggio di errore include un collegamento all'area download. in alternativa, è possibile scaricare .NET 3,5 SP1 da Windows Update. Prima di installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è necessario scaricare e installare .NET 3.5 SP1 per evitare l'interruzione dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br />-Se si esegue il programma di installazione in [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] un computer [!INCLUDE[win8](../../includes/win8-md.md)]con SP1 o, è necessario abilitare .NET Framework 3,5 SP1 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]prima di installare.<br />-Se non è disponibile l'accesso a Internet, è necessario scaricare e installare .NET Framework 3,5 SP1 prima di eseguire il programma di installazione per installare uno dei componenti menzionati in precedenza. Per ulteriori informazioni sui suggerimenti e indicazioni su come acquisire e abilitare .NET Framework 3,5 [!INCLUDE[win8](../../includes/win8-md.md)] in e [!INCLUDE[win8srv](../../includes/win8srv-md.md)], vedere considerazioni sulla [distribuzione di Microsoft .NET Framework 3,5](https://msdn.microsoft.com/library/windows/hardware/hh975396) (https://msdn.microsoft.com/library/windows/hardware/hh975396).<br /><br /> .NET 4.0 è un requisito necessario per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è prevista l'installazione di .NET 4.0 durante il passaggio di installazione delle funzionalità.<br />-Se si installano le [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] edizioni, verificare che nel computer sia disponibile una connessione Internet. Tramite il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene scaricato e installato il componente .NET Framework 4, poiché non è incluso nei supporti di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].<br />-[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]non installa .NET 4,0 nella modalità Server Core di [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 o. [!INCLUDE[win8srv](../../includes/win8srv-md.md)] È necessario installare .NET 4.0 prima di installare [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] in un'installazione Server Core di [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 o [!INCLUDE[win8srv](../../includes/win8srv-md.md)].|  
|Windows PowerShell|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]non installa o Abilita Windows PowerShell 2,0; Tuttavia, Windows PowerShell 2,0 è un prerequisito [!INCLUDE[ssDE](../../includes/ssde-md.md)] di installazione [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]per i componenti e. Se durante l'installazione viene segnalato che Windows PowerShell 2.0 non è presente, è possibile installarlo o abilitarlo seguendo le istruzioni disponibili nella pagina relativa a [Windows Management Framework](https://go.microsoft.com/fwlink/?LinkId=186214) .|  
|Software di rete|I sistemi operativi supportati per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] includono software di rete integrato. Le istanze denominate e predefinite di un'installazione autonoma supportano i protocolli di rete seguenti: Shared Memory, TCP/IP, Named Pipes e VIA.<br /><br /> Nota: il protocollo VIA non è supportato nei cluster di failover. I client o le applicazioni in esecuzione sullo stesso nodo del cluster di failover dell'istanza di SQL Server, possono usare il protocollo Shared Memory per la connessione a SQL Server tramite il relativo indirizzo pipe locale. Tuttavia questo tipo di connessione non è in grado di riconoscere il cluster e avrà esito negativo dopo un failover dell'istanza. Pertanto non è consigliata e deve essere usata solo in scenari molto specifici. Il protocollo VIA è deprecato. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br /><br /> Per ulteriori informazioni su protocolli e librerie di rete, vedere [Network Protocols and Network Libraries](network-protocols-and-network-libraries.md).|  
|Virtualizzazione|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] è supportato in ambienti di macchina virtuale in esecuzione con il ruolo Hyper-V nelle edizioni seguenti:<br />-<br />                    
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard, Enterprise e Datacenter<br />-[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard, Enterprise e Datacenter Edition.<br />-<br />                    [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Datacenter e Standard Edition.<br /><br /> Oltre alle risorse richieste dalla partizione padre, ogni macchina virtuale (partizione figlio) deve essere provvista di risorse del processore, memoria e risorse del disco sufficienti per la relativa istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . I requisiti sono elencati più avanti in questo argomento.\*<br /><br /> Nel ruolo Hyper-V in [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 o [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 possono essere allocati un massimo di 4 (quattro) processori virtuali alle macchine virtuali in cui vengono eseguite le edizioni di [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 a 32 o 64 bit o [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 a 64 bit o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] a 64 bit.<br /><br /> Nel ruolo Hyper-V in [!INCLUDE[win8srv](../../includes/win8srv-md.md)]:<br />è possibile allocare un massimo di 8 (otto) processori virtuali alle macchine virtuali in cui sono in esecuzione edizioni di [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 a 32 o 64 bit.<br />È possibile allocare un massimo di 64 (sessantaquattro) processori virtuali alle macchine virtuali in cui sono in esecuzione edizioni a 64 bit di [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] .<br /><br /> Per ulteriori informazioni sui limiti della capacità di calcolo per diverse edizioni di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e sulle differenze in ambienti fisici e virtualizzati con i processori con Hyper-Threading, vedere [Compute Capacity Limits by Edition of SQL Server](../compute-capacity-limits-by-edition-of-sql-server.md). Per ulteriori informazioni sul ruolo Hyper-V, visitare il [sito Web di Windows Server 2008](https://go.microsoft.com/fwlink/?LinkId=182820).<br /><br /> ** \* Importante \* \* ** Il clustering di failover guest è [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]supportato in. Per ulteriori informazioni sulle versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e i sistemi operativi che supportano il clustering di failover guest, nonché sul supporto per la virtualizzazione, vedere [Criteri di supporto per i prodotti Microsoft SQL Server eseguiti in un ambiente hardware virtuale](https://go.microsoft.com/fwlink/?LinkId=151676).|  
|Disco rigido|Per[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] sono necessari almeno 6 GB di spazio libero su disco rigido.<br /><br /> I requisiti di spazio su disco variano a seconda dei componenti di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] installati. Per ulteriori informazioni, vedere [Hard Disk Space Requirements (32-Bit and 64 Bit)](hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace) più avanti in questo argomento. Per informazioni sui tipi di archiviazione supportati per i file di dati, vedere [Storage Types for Data Files](hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes).|  
|Unità|Per l'installazione da disco è necessaria un'unità DVD.|  
|Monitorare|Per[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] è necessario un monitor con risoluzione Super-VGA (800 x 600) o superiore.|  
|Internet|Per la funzionalità Internet è necessario l'accesso a Internet (potrebbero essere applicati costi aggiuntivi).|  
  
 * L' [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] esecuzione in una macchina virtuale risulterà più lenta rispetto all'esecuzione a livello nativo a causa dell'overhead della virtualizzazione.  
  
##  <a name="pmosr"></a>Requisiti del processore, della memoria e del sistema operativo  
 I seguenti requisiti di memoria e processore si applicano a tutte le edizioni di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|Memoria<sup>[1]</sup>|**Minimo**<br /><br /> Edizioni Express: 512 MB<br /><br /> Tutte le altre edizioni: 1 GB<br /><br /> **Consigliabile**<br /><br /> Edizioni Express: 1 GB<br /><br /> Tutte le altre edizioni: almeno 4 GB che devono essere incrementati all'aumentare delle dimensioni del database per garantire prestazioni ottimali.|  
|Velocità del processore|**Minimo**<br /><br /> Processore x86: 1,0 GHz<br /><br /> Processore x64: 1,4 GHz<br /><br /> **Consigliato:** 2,0 GHz o superiore|  
|Tipo di processore|Processore x64: AMD Opteron, AMD Athlon 64, Intel Xeon con supporto Intel EM64T, Intel Pentium IV con supporto EM64T<br /><br /> Processore x86: Pentium III o superiore|  
  
 <sup>[1]</sup> La quantità di memoria minima richiesta per [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] l'installazione [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] del componente in (DQS) è 2 GB di RAM, diversa dal [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] requisito minimo di memoria. Per informazioni sull'installazione di DQS, vedere [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
  
 **Supporto di WOW64:**  
  
 WOW64 (Windows 32-bit on Windows 64-bit) è una funzionalità delle edizioni a 64 bit di Windows che consente l'esecuzione a livello nativo in modalità a 32 bit delle applicazioni a 32 bit. Le applicazioni verranno eseguite in modalità a 32 bit anche se il sistema operativo sottostante viene eseguito a 64 bit.  
  
-   In un sistema operativo a 64 bit supportato, è possibile installare edizioni a 32 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel sottosistema a 32 bit WOW64 di un server a 64 bit. La funzionalità WOW64 è supportata solo per le istanze autonome di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non è supportata per le installazioni di cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Per le installazioni di edizioni a 64 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in sistemi operativi a 64 bit supportati, gli strumenti di gestione sono supportati in WOW64. Per ulteriori informazioni sui sistemi operativi supportati, selezionare un'edizione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dalle sezioni riportate di seguito.  
  
 **Supporto di Server Core:**  

 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  è ora supportato in un'installazione Server Core di Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 e Windows Server 2019. 

L'installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nella modalità Server Core è supportata dalle edizioni di Windows Server seguenti:

|                              |                                |
| :------------------------    | :------------------------------|
| Windows Server 2019 Standard | Windows Server 2019 Datacenter |
| Windows Server 2016 Standard | Windows Server 2016 Datacenter |
| Windows Server 2012 R2 Standard | Windows Server 2012 R2  Datacenter|
| Windows Server 2012 Standard | Windows Server 2012 Datacenter |
| Windows Server 2008 R2 SP1 Standard | Windows Server 2008 R2 SP1 Datacenter |
| Windows Server 2008 R2 SP1 Enterprise | Windows Server 2008 R2 SP1 Web|
   | &nbsp; | &nbsp; |
  
 Per altre informazioni sull'installazione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di in Server Core, vedere [installare SQL Server 2014 in Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md).  
  
   >[!NOTE]
   > Le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportate in [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] a 64 bit x64 Standard Edition sono supportate anche in [!INCLUDE[sbs_2](../../includes/sbs-2-md.md)] a 64 bit x64.  
  
 **Supporto del sistema operativo:**  
  
 Le edizioni [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] vengono classificate come segue:  
  
-   [Edizioni principali di SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md#TOP_Principal)  
  
-   [Edizioni specializzate di SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md#TOP_SP)  
  
-   [Edizioni Breadth di SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md#TOP_Breadth)  
  
###  <a name="TOP_Principal"></a>Requisiti dei sistemi operativi delle edizioni principali  
 Nella tabella seguente vengono indicati i requisiti del sistema operativo per le edizioni principali di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Edizione|32 bit|64 bit|  
|---------------------------------------|-------------|-------------|  
|[!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)]|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Data Center (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (32 bit)<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (32 bit)|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard (64 bit)<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Data Center (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (64 bit)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Business Intelligence|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard (64 bit)<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Data Center (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (32 bit)<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (32 bit)|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard (64 bit)<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Data Center (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (64 bit)|  
|[!INCLUDE[ssStandard](../../includes/ssstandard-md.md)]|Windows 10 Home (64 bit)<br /><br /> Windows 10 Professional (64 bit)<br /><br /> Windows 10 Enterprise (64 bit)<br /><br /> Windows 10 Home (32 bit)<br /><br /> Windows 10 Professional (32 bit)<br /><br /> Windows 10 Enterprise (32 bit)<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard (64 bit)<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Data Center (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web (64 bit)<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]32 bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]32 bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]32 bit<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64 bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64 bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64 bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]32 bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]32 bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]32 bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64 bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64 bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate (32 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise (32 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional (32 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (32 bit)<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (32 bit)|Windows 10 Home (64 bit)<br /><br /> Windows 10 Professional (64 bit)<br /><br /> Windows 10 Enterprise (64 bit)<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard (64 bit)<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Data Center (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web (64 bit)<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64 bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64 bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64 bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64 bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64 bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional a 64 bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (64 bit)| 
  
###  <a name="TOP_SP"></a>Requisiti del sistema operativo per le edizioni specializzate  
 Nella tabella seguente vengono indicati i requisiti del sistema operativo per le edizioni specializzate di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Edizione|32 bit|64 bit|  
|---------------------------------------|-------------|-------------|  
|[!INCLUDE[ssWeb](../../includes/ssweb-md.md)]|Windows 10 Home (64 bit)<br /><br /> Windows 10 Professional (64 bit)<br /><br /> Windows 10 Enterprise (64 bit)<br /><br /> Windows 10 Home (32 bit)<br /><br /> Windows 10 Professional (32 bit)<br /><br /> Windows 10 Enterprise (32 bit)<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard (64 bit)<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Data Center (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (32 bit)<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (32 bit)|Windows 10 Home (64 bit)<br /><br /> Windows 10 Professional (64 bit)<br /><br /> Windows 10 Enterprise (64 bit)<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter (64 bit)<br /><br />
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard (64 bit)<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Data Center (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (64 bit)| 
  
###  <a name="TOP_Breadth"></a>Requisiti del sistema operativo per le edizioni di ampiezza
 Nella tabella seguente vengono indicati i requisiti del sistema operativo per le edizioni breadth di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Edizione|32 bit|64 bit|  
|---------------------------------------|-------------|-------------|  
|[!INCLUDE[ssDeveloper](../../includes/ssdeveloper-md.md)]|Windows 10 Home (64 bit)<br /><br /> Windows 10 Professional (64 bit)<br /><br /> Windows 10 Enterprise (64 bit)<br /><br /> Windows 10 Home (32 bit)<br /><br /> Windows 10 Professional (32 bit)<br /><br /> Windows 10 Enterprise (32 bit)<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter (64 bit)<br /><br />
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard (64 bit)<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Data Center (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web (64 bit)<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]32 bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]32 bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]32 bit<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64 bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64 bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64 bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]32 bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]32 bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]32 bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64 bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64 bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate (32 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise (32 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional (32 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium (32 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic (32 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (32 bit)<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (32 bit)|Windows 10 Home (64 bit)<br /><br /> Windows 10 Professional (64 bit)<br /><br /> Windows 10 Enterprise (64 bit)<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter (64 bit)<br /><br />
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard (64 bit)<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Data Center (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web (64 bit)<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64 bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64 bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64 bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64 bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64 bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic a 64 bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (64 bit)|  
|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]|Windows 10 Home (64 bit)<br /><br /> Windows 10 Professional (64 bit)<br /><br /> Windows 10 Enterprise (64 bit)<br /><br /> Windows 10 Home (32 bit)<br /><br /> Windows 10 Professional (32 bit)<br /><br /> Windows 10 Enterprise (32 bit)<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard (64 bit)<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Data Center (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web (64 bit)<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]32 bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]32 bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]32 bit<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64 bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64 bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64 bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]32 bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]32 bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]32 bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64 bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64 bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate (32 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise (32 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional (32 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium (32 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic (32 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (32 bit)<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (32 bit)|Windows 10 Home (64 bit)<br /><br /> Windows 10 Professional (64 bit)<br /><br /> Windows 10 Enterprise (64 bit)<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard (64 bit)<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Data Center (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials (64 bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web (64 bit)<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64 bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64 bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64 bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64 bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64 bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium a 64 bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic a 64 bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation (64 bit)<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web (64 bit)|  
  
## <a name="minimum-sql-server-version-requirements-for-windows-10"></a>Requisiti minimi della versione di SQL Server per Windows 10  
 Prima di installare SQL Server in un computer che esegue Windows 10, è necessario assicurarsi che i requisiti minimi seguenti siano soddisfatti:  
  
-   Per SQL Server 2014, è necessario applicare SQL Server 2014 Service Pack 1 o un aggiornamento successivo. Per altre informazioni, vedere [Come ottenere il service pack più recente per SQL Server 2014](https://support.microsoft.com/kb/2958069).  
  
-   Per SQL Server 2012, è necessario applicare SQL Server 2012 Service Pack 2 o un aggiornamento successivo. Per altre informazioni, vedere [Come ottenere il service pack più recente per SQL Server 2012](https://support.microsoft.com/kb/2755533).  
  
-   SQL Server 2008 R2  
    e SQL Server 2008 non sono supportati in Windows 10.  
  
##  <a name="CrossLanguageSupport"></a>Supporto tra linguaggi diversi  
 Per altre informazioni sul supporto di lingue diverse e per considerazioni relative all'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nelle lingue localizzate, vedere [Versioni in lingua locale di SQL Server](local-language-versions-in-sql-server.md).  
  
##  <a name="ess"></a>Supporto per sistemi estesi  
 Nelle versioni a 64 bit di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] è incluso il supporto per sistemi estesi, noti anche come sistemi WOW64 (Windows 32-bit on Windows 64-bit). WOW64 è una funzionalità delle edizioni a 64 bit di Windows che consente l'esecuzione a livello nativo in modalità a 32 bit delle applicazioni a 32 bit. Le applicazioni verranno eseguite in modalità a 32 bit anche se il sistema operativo sottostante viene eseguito a 64 bit.  
  
##  <a name="HardDiskSpace"></a>Requisiti di spazio su disco rigido (bit 32 e 64)  
 Durante l'installazione Windows Installer crea file temporanei nell'unità di sistema. Prima di eseguire il programma di installazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installare o aggiornare, verificare di disporre di almeno **6,0 GB** di spazio su disco disponibile nell'unità di sistema per questi file. Questo requisito si applica anche se si installano componenti in un'unità non predefinita.  
  
 I requisiti effettivi di spazio su disco rigido possono variare in base alla configurazione del sistema e alle funzionalità selezionate per l'installazione. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Nella tabella seguente vengono indicati i requisiti di spazio su disco dei componenti di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
|**Funzionalità**|**Requisito di spazio su disco**|  
|-----------------|--------------------------------|  
|
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] e file di dati, replica, ricerca full-text e Data Quality Services|811 MB|  
|
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e file di dati|345 MB|  
|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e Gestione report|304 MB|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|591 MB|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|243 MB|  
|Componenti client, diversi dai componenti della documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e dagli strumenti di Integration Services|1823 MB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Componenti della documentazione online per visualizzare e gestire il contenuto della Guida<sup>1</sup>|375 KB|  
  
 <sup>1</sup> Il requisito di spazio su disco per il contenuto della documentazione online scaricato è 200 MB.  
  
##  <a name="StorageTypes"></a>Tipi di archiviazione per i file di dati  
 I tipi di archiviazione supportati per i file di dati sono:  
  
-   Disco locale  
  
-   Archiviazione condivisa  
  
-   Condivisione file SMB  
  
    > **Nota:**  L'archiviazione SMB non è supportata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per i file di dati per le installazioni autonome o in cluster. Utilizzare l'archiviazione associata diretta o, in alternativa, una rete di archiviazione.  
  
    > **IMPORTANTE!** L'archiviazione SMB può essere ospitata da un file server di Windows o da un dispositivo di archiviazione SMB di terze parti. Nel primo caso, la versione del file server di Windows deve essere la versione 2008 o successiva. Per ulteriori informazioni sull'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una condivisione file SMB come opzione di archiviazione, vedere [Installazione di SQL Server con l'opzione di archiviazione su condivisione file SMB](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
  
    > **AVVISO!!!!**  Il disco locale è supportato nell'installazione del cluster di failover di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo per l'installazione dei file tempdb. Verificare che il percorso specificato per i file di dati e di log di tempdb sia valido in **tutti** i nodi del cluster. Durante il failover, se le directory tempdb non sono disponibili nel nodo di destinazione del failover, la risorsa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non verrà riportata online.  
  
##  <a name="DC_support"></a>Installazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un controller di dominio-limitazioni  
 Per motivi di sicurezza, è consigliabile non installare [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] in un controller di dominio. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ma verranno applicate le limitazioni seguenti:  
  
-   Non è possibile eseguire servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un controller di dominio utilizzando un account Servizio locale.  
  
-   Al termine dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un computer, non è possibile modificare il computer da membro di dominio a controller di dominio. Prima di modificare il computer host in controller di dominio, è necessario disinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Al termine dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un computer, non è possibile modificare il computer da controller di dominio a membro di dominio. Prima di modificare il computer host in membro di dominio, è necessario disinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Le istanze del cluster di failover di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non sono supportate quando i nodi del cluster sono controller di dominio.  
  
-   Tramite il programma di installazione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non sarà possibile creare gruppi di sicurezza o fornire account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un controller di dominio di sola lettura. In questo scenario il programma di installazione non verrà completato.  
  
## <a name="see-also"></a>Vedere anche  
 [Pianificazione di un'installazione di SQL Server](planning-a-sql-server-installation.md)   
 [Considerazioni sulla sicurezza per un'installazione di SQL Server](security-considerations-for-a-sql-server-installation.md)   
 [Specifiche di prodotto per SQL Server 2014](../../getting-started/sql-server-2014-product-specifications.md)  
