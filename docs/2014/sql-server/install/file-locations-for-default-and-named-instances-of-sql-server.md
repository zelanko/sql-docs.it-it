---
title: Percorsi dei file per le istanze predefinite e denominate di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 463c570e-9f75-4653-b3b8-4d61753b0013
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ca9df655e00b1f2fd1919f30bb1bb166e2556b91
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53208770"
---
# <a name="file-locations-for-default-and-named-instances-of-sql-server"></a>Percorsi dei file per le istanze predefinite e denominate di SQL Server
  Un'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è costituita da una o più istanze separate. Un'istanza, predefinita o denominata, contiene un proprio set di file di programma e di dati, oltre a un set di file comuni condivisi tra tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presenti nel computer.  
  
 Per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che include [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], ogni componente ha un set completo di file di dati, file eseguibili e file comuni condivisi da tutti i componenti.  
  
 Per isolare i percorsi di installazione di ogni componente, vengono generati ID istanza univoci per ogni componente all'interno di una determinata istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Non è possibile installare i file di programma e i file di dati in un'unità disco rimovibile, in un file system che utilizza la compressione, in una directory in cui sono presenti file di sistema o in unità condivise in un'istanza del cluster di failover.  
>   
>  I database di sistema (master, model, MSDB e tempdb) e i database utente del [!INCLUDE[ssDE](../../includes/ssde-md.md)] possono essere installati con il file server SMB (Server Message Block) come opzione di archiviazione. Questa condizione è valida per le installazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autonome e per le installazioni del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Installazione di SQL Server con l'opzione di archiviazione su condivisione file SMB](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
>   
>  Non eliminare alcuna delle directory seguenti o il relativo contenuto: Binn, Data, Ftdata, HTML o 1033. Binn, Data, Ftdata, HTML o 1033. Se necessario, è possibile eliminare altre directory; potrebbe non essere tuttavia possibile recuperare funzionalità o dati non più disponibili se prima non si disinstalla e quindi si reinstalla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non eliminare o modificare nessuno dei file htm disponibile nella directory HTML. Questi file sono necessari per il corretto funzionamento degli strumenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="shared-files-for-all-instances-of-includessnoversionincludesssnoversion-mdmd"></a>File condivisi per tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 I file comuni usati da tutte le istanze presenti in un singolo computer vengono installati nella cartella [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)], dove \<*unità*> è la lettera dell'unità in cui vengono installati i componenti. L'unità C è in genere quella predefinita.  
  
## <a name="file-locations-and-registry-mapping"></a>Percorsi dei file e mapping del Registro di sistema  
 Durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , viene generato un ID istanza per ogni componente. I componenti server di questa versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono il [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 L'ID dell'istanza predefinita viene creato utilizzando il formato seguente:  
  
-   MSSQL per [!INCLUDE[ssDE](../../includes/ssde-md.md)], seguito dal numero di versione principale, da un carattere di sottolineatura e, se possibile, dalla versione secondaria e quindi da un punto, seguiti dal nome di istanza.  
  
-   MSAS per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], seguito dal numero di versione principale, da un carattere di sottolineatura e, se possibile, dalla versione secondaria e quindi da un punto, seguiti dal nome di istanza.  
  
-   MSRS per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], seguito dal numero di versione principale, da un carattere di sottolineatura e, se possibile, dalla versione secondaria e quindi da un punto, seguiti dal nome di istanza.  
  
 Di seguito vengono indicati alcuni esempi di ID delle istanze predefinite utilizzati in questa versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   MSSQL12.MSSQLSERVER per un'istanza predefinita di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   MSAS12.MSSQLSERVER per un'istanza predefinita di [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)].  
  
-   MSSQL12.Istanza per un'istanza denominata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] il cui nome è "Istanza".  
  
 Di seguito viene indicata la struttura di directory per un'istanza denominata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] che include [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], denominata "Istanza" e installata nelle directory predefinite:  
  
-   C:\Programmi\Microsoft SQL Server\MSSQL12.Istanza\  
  
-   C:\Programmi\Microsoft SQL Server\MSAS12.Istanza\  
  
 È possibile specificare qualsiasi valore per l'ID istanza, evitando tuttavia caratteri speciali e parole chiave riservate.  
  
 È possibile specificare l'ID di un'istanza non predefinita durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se l'utente sceglie di modificare la directory di installazione predefinita, invece di \<Programmi>\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], viene usato un \<percorso predefinito>\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si noti che gli ID delle istanze che iniziano con un carattere di sottolineatura (_) o che contengono il simbolo cancelletto (#) o il segno di dollaro ($) non sono supportati.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e i componenti client non sono specifici dell'istanza e non dispongono pertanto di un ID istanza assegnato. Per impostazione predefinita, i componenti non specifici dell'istanza vengono installati in un'unica directory: [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]. Se si modifica il percorso di installazione di un componente condiviso, la modifica sarà valida anche per tutti gli altri componenti condivisi. Nelle successive installazioni i componenti non specifici dell'istanza verranno installati nella stessa directory dell'installazione originale.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è l'unico componente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che supporta la ridenominazione delle istanze in seguito all'installazione. Se un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene rinominata, l'ID istanza non cambierà di conseguenza. Al termine della ridenominazione dell'istanza, le directory e le chiavi del Registro di sistema continueranno a utilizzare l'ID istanza creato durante l'installazione.  
  
 L'hive del Registro di sistema viene creato in HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<*ID_Istanza*> per i componenti specifici dell'istanza. Ad esempio,  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12. MyInstance  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12. MyInstance  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS12. MyInstance  
  
 Nel Registro di sistema viene inoltre gestito un mapping degli ID istanza ai nomi delle istanze. Il mapping degli ID istanza in base ai nomi delle istanze è gestito nel modo seguente:  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\SQL] "InstanceName"="MSSQL12"  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\OLAP] "InstanceName"="MSAS12"  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\RS] "InstanceName"="MSRS12"  
  
## <a name="specifying-file-paths"></a>Specifica dei percorsi dei file  
 Durante l'installazione è possibile modificare il percorso di installazione delle funzionalità seguenti:  
  
 Durante la procedura di installazione viene visualizzato il percorso di installazione delle caratteristiche con una cartella di destinazione configurabile dall'utente:  
  
|Componente|Percorso predefinito<sup>1, 2</sup>|Configurabile<sup>3</sup> o percorso corretto|  
|---------------|---------------------------------|--------------------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] componenti server|File \Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\< ID istanza >\|configurabile|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] file di dati|File \Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\< ID istanza >\|configurabile|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] server|File \Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12.\< ID istanza >\|configurabile|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] file di dati|File \Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12.\< ID istanza >\|configurabile|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] server di report|File \Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS12.\< ID istanza > \Reporting\|configurabile|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Gestione report|File \Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS12.\< ID istanza > Services\ReportManager.\|fissa del percorso|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|\<Directory di installazione > \120\DTS\|configurabile<sup>4</sup>|  
|Componenti client (ad eccezione di bcp.exe e sqlcmd.exe)|\<Directory di installazione > \120\Tools\|configurabile<sup>4</sup>|  
|Componenti client (bcp.exe e sqlcmd.exe)|\<Directory di installazione>\Client SDK\ODBC\110\Tools\Binn|Percorso fisso|  
|Oggetti di replica e oggetti COM sul lato server|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]COM\\<sup>5</sup>|Percorso fisso|  
|DLL del componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per il motore di runtime Data Transformation Services, motore della pipeline di trasformazione dati e utilità della riga di comando `dtexec`|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|Percorso fisso|  
|DLL che forniscono supporto per connessioni gestite di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Connections|Percorso fisso|  
|DLL per ogni tipo di enumeratore supportato da [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\ForEachEnumerators|Percorso fisso|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser, provider WMI|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Condiviso\|fissa del percorso|  
|Componenti condivisi tra tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Condiviso\|fissa del percorso|  
  
 <sup>1</sup>assicurarsi che il \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ cartella sia protetta con autorizzazioni limitate.  
  
 <sup>2</sup>è l'unità predefinita di queste posizioni *systemdrive*, in genere unità C.  
  
 <sup>3</sup>i percorsi di installazione per le funzionalità figlio sono determinati dal percorso di installazione della funzionalità padre.  
  
 <sup>4</sup>un singolo percorso di installazione viene condiviso tra [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e i componenti client. La modifica del percorso di installazione per un componente si applica quindi a tutti i componenti. Nel caso di installazioni successive i componenti vengono installati nello stesso percorso dell'installazione iniziale.  
  
 <sup>5</sup>questa directory viene usata da tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un computer. Se si applica un aggiornamento a una delle istanze nel computer, le modifiche apportate ai file inclusi in questa cartella interesseranno tutte le istanze presenti nel computer. Quando si aggiungono funzionalità a un'installazione esistente, non è possibile modificare il percorso di una caratteristica installata in precedenza, né specificare il percorso di una nuova caratteristica. È necessario installare le caratteristiche aggiuntive nelle directory già stabilite durante l'installazione iniziale oppure disinstallare e reinstallare il prodotto.  
  
> [!NOTE]  
>  Per le configurazioni cluster, è necessario selezionare un'unità locale che sia disponibile per ogni nodo del cluster.  
  
 Se durante l'installazione si specifica un percorso di installazione per i componenti server o i file di dati, oltre al percorso specificato per i file di dati e di programma, verrà utilizzato l'ID istanza. L'ID istanza non viene utilizzato per gli strumenti e altri file condivisi, né per i file di dati e di programma di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , ma solo per il repository di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Se si imposta un percorso di installazione per la caratteristica [!INCLUDE[ssDE](../../includes/ssde-md.md)] , nell'istallazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tale percorso verrà utilizzato come directory radice di tutte le cartelle specifiche dell'istanza per l'installazione, inclusi i file di dati SQL. In questo caso, se si imposta la radice su "C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\< NomeIstanza > \MSSQL\\", le directory specifiche dell'istanza verranno aggiunte alla fine del percorso.  
  
 Se si utilizza la funzionalità di aggiornamento USESYSDB nell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (modalità interfaccia utente del programma di installazione), è probabile che si verifichino le condizioni per un'installazione del prodotto in una struttura di cartelle ricorsiva, Ad esempio, \< *Programmisql*> \MSSQL12\MSSQL\MSSQL10_50\MSSQL\Data\\. Per utilizzare la funzionalità USESYSDB, impostare invece un percorso di installazione per la funzionalità dei file di dati SQL anziché per la funzionalità [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
> [!NOTE]
>  I file di dati si trovano in genere in una directory figlio denominata Data. Ad esempio, specificare il file c:\Programmi\Microsoft\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\< NomeIstanza > \ per indicare il percorso radice della directory dei dati dei database di sistema durante l'aggiornamento se i file di dati si trovano in C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\< NomeIstanza > \MSSQL\Data.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione Motore di database - Directory dati](../../../2014/sql-server/install/database-engine-configuration-data-directories.md)   
 [Configurazione di Analysis Services - Directory dati](../../../2014/sql-server/install/analysis-services-configuration-data-directories.md)  
  
  
