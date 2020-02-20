---
title: Usare più versioni e istanze
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- concurrent installations [SQL Server]
- versions [SQL Server], multiple
- side-by-side installations [SQL Server]
- multiple SQL Server component versions
- installing SQL Server, side-by-side installations
- Setup [SQL Server], side-by-side installations
- 64-bit edition [SQL Server]
- 32-bit edition [SQL Server]
- editions [SQL Server], side-by-side installations
ms.assetid: 93acefa8-bb41-4ccc-b763-7801f51134e0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0ff71430707e210daf970e969d854e408d777e4e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75258974"
---
# <a name="work-with-multiple-versions-and-instances-of-sql-server"></a>Usare più versioni e istanze di SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

È possibile installare più istanze di SQL Server o installare SQL Server in un computer in cui sono già installate versioni precedenti di SQL Server.

Gli elementi seguenti correlati a SQL Server sono compatibili con l'installazione di più istanze nello stesso computer:

- Motore di database

- Analysis Services

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
- Reporting Services
::: moniker-end

È possibile aggiornare le versioni precedenti di SQL Server in un computer in cui sono già installate altre versioni di SQL Server. Per gli scenari di aggiornamento supportati, vedere [Aggiornamenti di versione ed edizione supportati](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).
  
## <a name="version-components-and-numbering"></a>Numerazione e componenti della versione

 I concetti seguenti sono utili per comprendere il comportamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le istanze side-by-side di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
 Il formato della versione del prodotto standard per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è MM.nn.bbbb.rr dove ogni segmento è definito come indicato di seguito:
  
 MM: versione principale  
  
 nn: versione secondaria  
  
 bbbb: numero di build  
  
 rr - numero revisione build  
  
 In ogni versione principale o secondaria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il numero di versione viene aumentato per differenziarlo dalle versioni precedenti. Questa modifica alla versione viene utilizzata per diversi scopi. Ciò include la visualizzazione delle informazioni sulla versione nell'interfaccia utente, il controllo della modalità di sostituzione dei file durante l'aggiornamento, l'applicazione di Service Pack e un meccanismo per una differenziazione funzionale tra le versioni successive.
  
### <a name="components-shared-by-all-versions-of-ssnoversion"></a>Componenti condivisi da tutte le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

 Alcuni componenti sono condivisi da tutte le istanze di tutte le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installate. Quando si esegue l'installazione affiancata di versioni diverse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nello stesso computer, questi componenti vengono aggiornati automaticamente alla versione più recente. Tali componenti in genere vengono disinstallati automaticamente quando viene disinstallata l'ultima istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
 Esempi: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser e Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer.
  
### <a name="components-shared-across-all-instances-of-the-same-major-version-of-ssnoversion"></a>Componenti condivisi da tutte le istanze della stessa versione principale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Le versioni con la stessa versione principale condividono alcuni componenti in tutte le istanze. Se i componenti condivisi vengono selezionati durante l'aggiornamento, i componenti esistenti vengono aggiornati alla versione più recente.
  
Esempi: documentazione online di: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
### <a name="components-shared-across-minor-versions"></a>Componenti condivisi nelle versioni secondarie

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Le versioni con componenti che condividono la stessa versione principale e secondaria.
  
Esempio: File di supporto per l'installazione.
  
### <a name="components-specific-to-an-instance-of-ssnoversion"></a>Componenti specifici di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Alcuni componenti o servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono specifici di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essi sono anche noti come specifici dell'istanza. Condividono la stessa versione dell'istanza che li ospita e vengono utilizzati esclusivamente per quell'istanza.
  
Esempi: [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
### <a name="components-that-are-independent-of-the-ssnoversion-versions"></a>Componenti indipendenti dalle versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Alcuni componenti vengono installati durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ma sono indipendenti dalle versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essi possono essere condivisi dalle versioni principali o da tutte le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

Esempi: Microsoft Sync Framework, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
Per altre informazioni sull'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, vedere [Installare SQL Server 2016 dall'Installazione guidata &#40;programma di installazione&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md). Per altre informazioni su come disinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, vedere [Disinstallare un'istanza esistente di SQL Server &#40;programma di installazione&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md).  
  
## <a name="using-ssnoversion-side-by-side-with-previous-versions-of-ssnoversion"></a>Utilizzo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] insieme a versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

È possibile installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un computer in cui sono già in esecuzione istanze di una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se nel computer è già presente un'istanza predefinita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere installato come istanza denominata.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep non supporta l'installazione side-by-side di istanze predisposte di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nello stesso computer. Ad esempio, non è possibile preparare un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] side-by-side a un'istanza predisposta di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Tuttavia, nello stesso computer, è possibile installare side-by-side più istanze predisposte della stessa versione principale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Considerazioni sull'installazione di SQL Server tramite SysPrep](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
>
> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] non può essere installato side-by-side con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un computer in cui è in esecuzione Windows Server 2008 R2 Server Core SP1. Per altre informazioni sulle installazioni di Server Core, vedere [Installare SQL Server 2016 in Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md).  
  
Nella tabella seguente viene descritto il supporto per installazioni side-by-side di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:
  
|Istanza esistente di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|Supporto installazione side-by-side|  
|--------------------------------------------------|----------------------------|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (64 bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (32 bit)<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (64 bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (32 bit)<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (64 bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (32 bit)<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (64 bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (32 bit)<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (64 bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (32 bit)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (64 bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)] <br /><br /> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|  

Nella tabella seguente viene descritto il supporto per installazioni side-by-side di [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] con le versioni precedenti:

|Istanza esistente di [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Supporto side-by-side per le versioni precedenti|  
|--------------------------------------------------|----------------------------|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (32 bit)<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (64 bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (32 bit)<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (64 bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (32 bit)<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (64 bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (32 bit)<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (64 bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (32 bit)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (64 bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|  

## <a name="preventing-ip-address-conflicts"></a>Metodi per evitare conflitti di indirizzi IP

Quando si esegue un'installazione side-by-side di un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con un'istanza autonoma del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], prestare attenzione per evitare conflitti del numero di porta TCP negli indirizzi IP. Di solito i conflitti si verificano quando due istanze del [!INCLUDE[ssDE](../../includes/ssde-md.md)] sono entrambe configurate per utilizzare la porta TCP predefinita (1433). Per evitare conflitti, configurare un'istanza in modo che venga utilizzata una porta fissa non predefinita. La configurazione di una porta fissa è di solito più facile nell'istanza autonoma. Configurare il [!INCLUDE[ssDE](../../includes/ssde-md.md)] in modo che vengano utilizzate porte diverse per evitare un conflitto di indirizzo IP o di porta TCP non previsto che blocca l'avvio di un'istanza quando si verifica un errore dell'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel nodo di standby.
  
## <a name="see-also"></a>Vedere anche

* [Requisiti hardware e software per l'installazione di SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
* [Installare SQL Server dall'Installazione guidata &#40;Installazione&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
* [Aggiornamenti di versione ed edizione supportati](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)
* [Eseguire l'aggiornamento di SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
* [Edizioni e le funzionalità supportate di SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)
* [Edizioni e le funzionalità supportate di SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)
* [Backward Compatibility_deleted](https://msdn.microsoft.com/library/15d9117e-e2fa-4985-99ea-66a117c1e9fd)