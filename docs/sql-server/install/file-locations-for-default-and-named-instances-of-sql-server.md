---
title: Percorsi dei file per le istanze predefinite e denominate di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 463c570e-9f75-4653-b3b8-4d61753b0013
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3ed7b8afd15e4c78eb10476504d21db8c42caffb
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028884"
---
# <a name="file-locations-for-default-and-named-instances-of-sql-server"></a>Percorsi dei file per le istanze predefinite e denominate di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Un'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è costituita da una o più istanze separate. Un'istanza, predefinita o denominata, contiene un proprio set di file di programma e di dati, oltre a un set di file comuni condivisi tra tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presenti nel computer.  
  
 Per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che include [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], ogni componente ha un set completo di file di dati, file eseguibili e file comuni condivisi da tutti i componenti.  
  
 Per isolare i percorsi di installazione di ogni componente, vengono generati ID istanza univoci per ogni componente all'interno di una determinata istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Non è possibile installare i file di programma e i file di dati in un'unità disco rimovibile, in un file system che utilizza la compressione, in una directory in cui sono presenti file di sistema o in unità condivise in un'istanza del cluster di failover.  
>  
>  Potrebbe essere necessario configurare software di scansione, ad esempio applicazioni antivirus e antispyware, per escludere le cartelle e i tipi di file di SQL Server. Per altre informazioni, vedere questo articolo del supporto: [Come scegliere il software antivirus in esecuzione su computer che eseguono SQL Server](https://support.microsoft.com/kb/309422)
> 
>  I database di sistema (master, model, MSDB e tempdb) e i database utente del [!INCLUDE[ssDE](../../includes/ssde-md.md)] possono essere installati con il file server SMB (Server Message Block) come opzione di archiviazione. Questa condizione è valida per le installazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autonome e per le installazioni del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Installazione di SQL Server con l'opzione di archiviazione su condivisione file SMB](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
>   
>  Non eliminare nessuna delle directory seguenti o il relativo contenuto: Binn, Data, Ftdata, HTML o 1033. Se necessario, è possibile eliminare altre directory; potrebbe non essere tuttavia possibile recuperare funzionalità o dati non più disponibili se prima non si disinstalla e quindi si reinstalla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non eliminare o modificare nessuno dei file htm disponibile nella directory HTML. Questi file sono necessari per il corretto funzionamento degli strumenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="shared-files-for-all-instances-of-includessnoversionincludesssnoversion-mdmd"></a>File condivisi per tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 I file comuni usati da tutte le istanze in un singolo computer sono installati nella cartella [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]. \<*unità*> è la lettera corrispondente all'unità in cui sono installati i componenti. Il valore predefinito è in genere l'unità C. \<*nnn*> indica la versione. La tabella seguente indica le versioni per i percorsi. 

|\<*nnn*>|Versione
|-----|-----
|140|[!INCLUDE[ssqlv14](../../includes/sssqlv14-md.md)]
|130|[!INCLUDE[ssqlv13](../../includes/sssql15-md.md)]
|120|SQL Server 2014
|110|[!INCLUDE[sssql11](../../includes/sssql11-md.md)] 
  
## <a name="file-locations-and-registry-mapping"></a>Percorsi dei file e mapping del Registro di sistema  
 Durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , viene generato un ID istanza per ogni componente. I componenti server di questa versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono il [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 L'ID dell'istanza predefinita viene creato utilizzando il formato seguente:  
  
-   MSSQL per [!INCLUDE[ssDE](../../includes/ssde-md.md)], seguito dal numero di versione principale, da un carattere di sottolineatura e, se possibile, dalla versione secondaria e quindi da un punto, seguiti dal nome di istanza.  
  
-   MSAS per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], seguito dal numero di versione principale, da un carattere di sottolineatura e, se possibile, dalla versione secondaria e quindi da un punto, seguiti dal nome di istanza.  
  
-   MSRS per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], seguito dal numero di versione principale, da un carattere di sottolineatura e, se possibile, dalla versione secondaria e quindi da un punto, seguiti dal nome di istanza.  
  
 Di seguito vengono indicati alcuni esempi di ID delle istanze predefinite utilizzati in questa versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   MSSQL14.MSSQLSERVER per un'istanza predefinita di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   MSAS14.MSSQLSERVER per un'istanza predefinita di [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)].  
  
-   MSSQL14.MyInstance per un'istanza denominata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] il cui nome è "MyInstance".  
  
    >[!NOTE]
    >Il numero a due cifre nel percorso dell'ID istanza indica il numero di versione. Negli esempi precedenti il numero di versione 14 è [!INCLUDE[ssqlv14](../../includes/sssqlv14-md.md)]. 

 Di seguito viene indicata la struttura di directory per un'istanza denominata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] che include [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], denominata "Istanza" e installata nelle directory predefinite:  
  
-   C:\Programmi\Microsoft SQL Server\MSSQL14.MyInstance\  
  
-   C:\Programmi\Microsoft SQL Server\MSAS14.MyInstance\  
  
 È possibile specificare qualsiasi valore per l'ID istanza, evitando tuttavia caratteri speciali e parole chiave riservate.  
  
 È possibile specificare l'ID di un'istanza non predefinita durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se l'utente sceglie di modificare la directory di installazione predefinita, invece di \<Programmi>\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], viene usato un \<percorso predefinito>\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si noti che gli ID delle istanze che iniziano con un carattere di sottolineatura (_) o che contengono il simbolo cancelletto (#) o il segno di dollaro ($) non sono supportati.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e i componenti client non sono specifici dell'istanza e non dispongono pertanto di un ID istanza assegnato. Per impostazione predefinita, i componenti non specifici dell'istanza vengono installati in un'unica directory: [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]. Se si modifica il percorso di installazione di un componente condiviso, la modifica sarà valida anche per tutti gli altri componenti condivisi. Nelle successive installazioni i componenti non specifici dell'istanza verranno installati nella stessa directory dell'installazione originale.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è l'unico componente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che supporta la ridenominazione delle istanze in seguito all'installazione. Se un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene rinominata, l'ID istanza non cambierà di conseguenza. Al termine della ridenominazione dell'istanza, le directory e le chiavi del Registro di sistema continueranno a utilizzare l'ID istanza creato durante l'installazione.  
  
 L'hive del Registro di sistema viene creato in HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<*ID_Istanza*> per i componenti specifici dell'istanza. Ad esempio,  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.MyInstance  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS14.MyInstance  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS14.MyInstance  
  
 Nel Registro di sistema viene inoltre gestito un mapping degli ID istanza ai nomi delle istanze. Il mapping degli ID istanza in base ai nomi delle istanze è gestito nel modo seguente:  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\SQL] "InstanceName"="MSSQL14"  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\OLAP] "InstanceName"="MSAS14"  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\RS] "InstanceName"="MSRS14"  
  
## <a name="specifying-file-paths"></a>Specifica dei percorsi dei file  
 Durante l'installazione è possibile modificare il percorso di installazione delle funzionalità seguenti:  
  
 Durante la procedura di installazione viene visualizzato il percorso di installazione delle caratteristiche con una cartella di destinazione configurabile dall'utente:  
  
|Componente|Percorso predefinito|Percorso configurabile o fisso|  
|---------------|------------------|--------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] componenti server|\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.\<IDIstanza>\ |Configurabile|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] file di dati|\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.\<IDIstanza>\ |Configurabile|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] server|\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS14.\<IDIstanza>\ |Configurabile|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] file di dati|\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS14.\<IDIstanza>\ |Configurabile|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] server di report|\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS14.\<IDIstanza>\Reporting Services\ReportServer\Bin\ |Configurabile|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Gestione report|\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS14.\<IDIstanza>\Reporting Services\ReportManager\ |Percorso fisso|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|\<Directory di installazione>\140\DTS\\ <sup>1</sup> |Configurabile |  
|Componenti client (ad eccezione di bcp.exe e sqlcmd.exe)|\<Directory di installazione>\140\Tools\\ <sup>1</sup> |Configurabile |  
|Componenti client (bcp.exe e sqlcmd.exe)|\<Directory di installazione>\Client SDK\ODBC\110\Tools\Binn|Percorso fisso|  
|Oggetti di replica e oggetti COM sul lato server|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]COM\\ <sup>2</sup> |Percorso fisso|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] DLL del componente per il motore di run-time e il motore della pipeline Data Transformation Services e l'utilità della riga di comando **dtexec**|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|Percorso fisso|  
|DLL che forniscono supporto per connessioni gestite di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Connections|Percorso fisso|  
|DLL per ogni tipo di enumeratore supportato da [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\ForEachEnumerators|Percorso fisso|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser, provider WMI|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Shared\\ |Percorso fisso|  
|Componenti condivisi tra tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Shared\\ |Percorso fisso|  
  
> [!WARNING]
> Assicurarsi che la cartella \Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ sia protetta con autorizzazioni limitate.  
  
L'unità predefinita per i percorsi dei file è *systemdrive*, che in genere corrisponde a C. I percorsi di installazione per le funzionalità figlio sono determinati dal percorso di installazione della funzionalità padre.  
  
<sup>1</sup> Un singolo percorso di installazione viene condiviso tra [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e i componenti client. La modifica del percorso di installazione per un componente si applica quindi a tutti i componenti. Nel caso di installazioni successive i componenti vengono installati nello stesso percorso dell'installazione iniziale.  
  
<sup>2</sup> Questa directory viene usata da tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presenti in un computer. Se si applica un aggiornamento a una delle istanze nel computer, le modifiche apportate ai file inclusi in questa cartella interesseranno tutte le istanze presenti nel computer. Quando si aggiungono funzionalità a un'installazione esistente, non è possibile modificare il percorso di una caratteristica installata in precedenza, né specificare il percorso di una nuova caratteristica. È necessario installare le caratteristiche aggiuntive nelle directory già stabilite durante l'installazione iniziale oppure disinstallare e reinstallare il prodotto.  
  
> [!NOTE]  
>  Per le configurazioni cluster, è necessario selezionare un'unità locale che sia disponibile per ogni nodo del cluster.  
  
 Se durante l'installazione si specifica un percorso di installazione per i componenti server o i file di dati, oltre al percorso specificato per i file di dati e di programma, verrà utilizzato l'ID istanza. L'ID istanza non viene utilizzato per gli strumenti e altri file condivisi, né per i file di dati e di programma di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , ma solo per il repository di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Se si imposta un percorso di installazione per la caratteristica [!INCLUDE[ssDE](../../includes/ssde-md.md)] , nell'istallazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tale percorso verrà utilizzato come directory radice di tutte le cartelle specifiche dell'istanza per l'installazione, inclusi i file di dati SQL. In questo caso, se si imposta la radice su "C:\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.\<NomeIstanza>\MSSQL\\", le directory specifiche dell'istanza vengono aggiunte alla fine del percorso.  
  
 Se si utilizza la funzionalità di aggiornamento USESYSDB nell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (modalità interfaccia utente del programma di installazione), è probabile che si verifichino le condizioni per un'installazione del prodotto in una struttura di cartelle ricorsiva, Ad esempio, \<*SQLProgramFiles*>\MSSQL14\MSSQL\MSSQL10_50\MSSQL\Data\\. Per utilizzare la funzionalità USESYSDB, impostare invece un percorso di installazione per la funzionalità dei file di dati SQL anziché per la funzionalità [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
> [!NOTE]
>  I file di dati si trovano in genere in una directory figlio denominata Data. Specificare ad esempio C:\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.\<NomeIstanza>\ per indicare il percorso radice della directory dei dati dei database di sistema durante l'aggiornamento quando i file di dati si trovano in C:\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.\<NomeIstanza>\MSSQL\Data.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione Motore di database - Directory dati](https://msdn.microsoft.com/library/9b1fa0fc-623b-479a-afc3-4f13bd850487)   
 [Configurazione di Analysis Services - Directory dati](https://msdn.microsoft.com/library/ef732855-b7af-4f40-a619-5573c1c354bb)  
  
  
