---
title: Note sulla versione di SQL Server 2008 R2 SP2 | Microsoft Docs
ms.prod: sql
ms.technology: install
ms.custom: ''
ms.date: 01/31/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server 2008 R2 SP2
- Release Notes, SQL Server 2008 R2 SP2
ms.assetid: e2bd3de7-674c-4ea7-8d53-bb40bba86fae
author: craigg-msft
ms.author: craigg
manager: jhubbard
monikerRange: = sql-server-2014 || = sqlallproducts-allversions
ms.openlocfilehash: 1a45ddf4920f693db928dddd30256c20f36ebe4a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63037259"
---
# <a name="sql-server-2008-r2-sp2-release-notes"></a>SQL Server 2008 R2 SP2 Release Notes
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
Nel presente documento sono descritti i problemi noti di cui è necessario essere a conoscenza prima di installare o risolvere i problemi relativi a Microsoft SQL Server 2008 R2 Service Pack 2. Il documento Note sulla versione è valido per tutte le edizioni di SQL Server 2008 R2 SP2 ed è disponibile solo online. Questo documento viene aggiornato periodicamente.  
  
## <a name="10-whats-new-in-service-pack-2"></a>1.0 Novità del Service Pack 2  
È stata aggiunta la vista a gestione dinamica (DMV) **sys.dm_db_stats_properties**. È possibile utilizzare questa DMV per restituire le proprietà delle statistiche di una tabella o una vista indicizzata specificata nel database corrente. Questa DMV restituisce, ad esempio, il numero di righe campionate e il numero di intervalli nell'istogramma.  
  
## <a name="20-before-you-install"></a>2.0 Prima di installare  
Per informazioni sull'installazione degli aggiornamenti di [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] , vedere [SQL Server 2008 R2 Servicing Documentation](https://msdn.microsoft.com/library/dd638062(SQL.105).aspx)(Documentazione sui servizi SQL Server 2008 R2).  
  
Per informazioni generali su come avviare e installare SQL Server 2008 R2, vedere il File Leggimi di SQL Server 2008 R2. Il file Leggimi è incluso nei supporti di installazione. Ulteriori informazioni sono disponibili nella [documentazione online di SQL Server](sql-server-technical-documentation.md) e nel [forum su SQL Server](https://social.msdn.microsoft.com/Forums/category/sqlserver/).  
  
### <a name="21-choose-the-correct-file-to-download-and-install"></a>2.1 Scegliere il file corretto da scaricare e installare  
Fare riferimento alla tabella seguente per determinare il file da scaricare e installare. Verificare di disporre dei requisiti di sistema corretti prima di installare il Service Pack. I requisiti di sistema sono indicati nelle pagine di download di cui viene fornito il collegamento all'interno della tabella.  
  
|Versione attualmente installata|Operazione da eseguire|File da scaricare e installare|  
|-------------------------------------------|----------------------|---------------------------|  
|Versione a 32 bit di qualsiasi edizione di SQL Server 2008 R2 o SQL Server 2008 R2 SP1|Aggiornare alla versione a 32 bit di SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU in [questa pagina](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Versione a 32 bit di SQL Server 2008 R2 RTM Express o SQL Server 2008 R2 SP1 Express|Aggiornare alla versione a 32 bit di SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU.exe in [questa pagina](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Versione a 32 bit solo degli strumenti client e di gestibilità per SQL Server 2008 R2 o SQL Server 2008 R2 SP1 (incluso SQL Server 2008 R2 Management Studio)|Aggiornare gli strumenti client e di gestibilità alla versione a 32 bit di SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU.exe in [questa pagina](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Versione a 32 bit di SQL Server 2008 R2 Management Studio Express o SQL Server 2008 R2 SP1 Management Studio Express|Aggiornare alla versione a 32 bit di SQL Server 2008 R2 SP2 Management Studio Express|SQLManagementStudio_x86_ENU.exe in [questa pagina](https://go.microsoft.com/fwlink/p/?LinkId=251791)|  
|Versione a 32 bit di qualsiasi edizione di SQL Server 2008 R2 o SQL Server 2008 R2 SP1 **e** versione a 32 bit degli strumenti client e di gestibilità (incluso SQL Server 2008 R2 RTM Management Studio)|Aggiornare tutti i prodotti alla versione a 32 bit di SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU.exe in [questa pagina](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Versione a 32 bit di uno o più strumenti di [Microsoft SQL Server 2008 R2 RTM Feature Pack](https://www.microsoft.com/download/en/details.aspx?id=16978)|Aggiornare gli strumenti alla versione a 32 bit di Microsoft SQL Server 2008 R2 SP2 Feature Pack|Uno o più file di [Microsoft SQL Server 2008 R2 SP2 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=251792)|  
|Nessuna installazione a 32 bit di SQL Server 2008 R2|Installare Server 2008 R2 con SP2|Andare alla pagina [SQL Server 2008 R2 SP2 - Express Edition](https://go.microsoft.com/fwlink/?LinkId=251791) e seguire le istruzioni.|  
|Nessuna installazione a 32 bit di SQL Server 2008 R2 Management Studio|Installare SQL Server 2008 R2 Management Studio con SP2|SQLManagementStudio_x86_ENU.exe in [questa pagina](https://go.microsoft.com/fwlink/p/?LinkId=251791) per installare la versione gratuita di SQL Server 2008 R2 SP2 Management Studio Express Edition.|  
|Versione a 64 bit di qualsiasi edizione di SQL Server 2008 R2 o SQL Server 2008 R2 SP1|Aggiornare alla versione a 64 bit di SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU or SQLServer2008R2SP2-KB2630455-IA64-ENU.exe in [questa pagina](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Versione a 64 bit di SQL Server 2008 R2 RTM Express o SQL Server 2008 R2 SP1 Express|Aggiornare alla versione a 64 bit di SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU.exe or SQLServer2008R2SP2-KB2630455-IA64-ENU.exe in [questa pagina](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Versione a 64 bit solo degli strumenti client e di gestibilità per SQL Server 2008 R2 o SQL Server 2008 R2 SP1 (incluso SQL Server 2008 R2 Management Studio)|Aggiornare gli strumenti client e di gestibilità alla versione a 64 bit di SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU.exe or SQLServer2008R2SP2-KB2630455-IA64-ENU.exe in [questa pagina](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Versione a 64 bit di SQL Server 2008 R2 Management Studio Express o SQL Server 2008 R2 SP1 Management Studio Express|Aggiornare alla versione a 64 bit di SQL Server 2008 R2 SP2 Management Studio Express|SQLManagementStudio_x64_ENU.exe in [questa pagina](https://go.microsoft.com/fwlink/p/?LinkId=251791)|  
|Versione a 64 bit di qualsiasi edizione di SQL Server 2008 R2 o SQL Server 2008 R2 SP1 **e** versione a 64 bit degli strumenti client e di gestibilità (incluso SQL Server 2008 R2 RTM Management Studio)|Aggiornare tutti i prodotti alla versione a 64 bit di SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU.exe in [questa pagina](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Versione a 64 bit di uno o più strumenti di [Microsoft SQL Server 2008 R2 RTM Feature Pack](https://www.microsoft.com/download/en/details.aspx?id=16978)|Aggiornare gli strumenti alla versione a 64 bit di Microsoft SQL Server 2008 R2 SP2 Feature Pack|Uno o più file di [Microsoft SQL Server 2008 R2 SP2 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=251792)|  
|Nessuna installazione a 64 bit di SQL Server 2008 R2|Installare Server 2008 R2 con SP2|Andare alla pagina [SQL Server 2008 R2 SP2 - Express Edition](https://go.microsoft.com/fwlink/?LinkId=251791) e seguire le istruzioni.|  
|Nessuna installazione a 64 bit di SQL Server 2008 R2 Management Studio|Installare SQL Server 2008 R2 Management Studio con SP2|SQLManagementStudio_x64_ENU.exe in [questa pagina](https://go.microsoft.com/fwlink/p/?LinkId=251791) per installare la versione gratuita di SQL Server 2008 R2 SP2 Management Studio Express Edition.|  
  
### <a name="22-setup-might-fail-if-sqagtresdll-is-locked-by-another-process"></a>2.2 Possibile errore di installazione se il file SQAGTRES.dll è bloccato da un altro processo  
**Problema**: un'operazione dell'installazione di SQL Server potrebbe non riuscire con l'errore: `Upgrading of cluster resource C:\Program Files\Microsoft SQL Server\MSSQL10_50.<Instance name>\MSSQL\Binn\SQAGTRES.DLL on machine <Computer name> failed with Win32Exception. Please look at inner exception for details.` La causa principale consiste nel fatto che il file C:\Windows\system32\SQAGTRES.DLL è bloccato da un altro processo e pertanto non può essere aggiornato dall'installazione.  
  
**Soluzione alternativa**: rinominare C:\Windows\system32\SQAGTRES.DLL con un nome temporaneo, ad esempio C:\Windows\system32\SQAGTRES_old.DLL, e selezionare l'opzione Riprova nel messaggio di errore dell'installazione. In questo modo, sarà possibile continuare l'installazione. Dopo il riavvio, è possibile eliminare il file temporaneo C:\Windows\system32\SQAGTRES_old.DLL.  
  
## <a name="30-known-issues-fixed-in-this-service-pack"></a>3.0 Problemi noti risolti in questo Service Pack  
Per un elenco completo dei bug e dei problemi noti risolti in questo Service Pack, vedere questo [articolo riepilogativo della Knowledge Base](https://support.microsoft.com/kb/2630455).  
  
## <a name="see-also"></a>Vedere anche  
[Identificazione della versione e dell'edizione di SQL Server](https://support.microsoft.com/kb/321185)  
  
