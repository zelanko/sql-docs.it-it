---
title: MSSQLSERVER_2515 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2515 (Database Engine error)
ms.assetid: af93aa29-70c9-4923-90af-aafadb20c1c6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7e531a2d916cfc464c18aab931c268197fbf5982
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62915028"
---
# <a name="mssqlserver2515"></a>MSSQLSERVER_2515
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|2515|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC_DIFF_MAP_OUT_OF_SYNC|  
|Testo del messaggio|La pagina ID_P, con ID di oggetto ID_O, ID di indice ID_I, ID di partizione ID_PN e ID di unità di allocazione ID_A (tipo TIPO) è stata modificata ma non è contrassegnata come modificata nella mappa di bit del backup differenziale.|  
  
## <a name="explanation"></a>Spiegazione  
 La pagina specificata ha un numero di sequenza del file di log (LSN) superiore all'LSN di riferimento del backup differenziale nella gestione dei backup del database oppure all'LSN di base differenziale nel blocco di controllo file, a seconda di quello più recente. La pagina non viene tuttavia contrassegnata come modificata nella mappa di bit del backup differenziale.  
  
 Dato che questo controllo viene eseguito solo quando è noto che la mappa di bit differenziale è priva di errori, verrà segnalata solo una pagina per database.  
  
## <a name="user-action"></a>Azione dell'utente  
  
### <a name="look-for-hardware-failure"></a>Individuare errori hardware  
 Eseguire gli strumenti di diagnostica hardware e risolvere eventuali problemi. Esaminare inoltre il registro di sistema di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e il registro delle applicazioni, nonché il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per stabilire se l'errore è dovuto a un problema hardware. Risolvere tutti i problemi relativi all'hardware indicati nei log.  
  
 In caso di problemi persistenti che provocano il danneggiamento dei dati, provare a sostituire i vari componenti hardware per isolare il problema. Verificare che nel sistema non sia abilitata la memorizzazione nella cache in scrittura sul controller del disco. Se si ritiene che il problema sia dovuto alla memorizzazione nella cache in scrittura, rivolgersi al fornitore dell'hardware.  
  
 Infine, potrebbe essere conveniente passare a un nuovo sistema hardware. A tale scopo può essere necessario riformattare le unità disco e reinstallare il sistema operativo.  
  
### <a name="restore-from-backup"></a>Eseguire un ripristino da backup  
 Se il problema non è correlato all'hardware ed è disponibile un backup valido noto, ripristinare il database dal backup.  
  
### <a name="run-dbcc-checkdb"></a>Eseguire DBCC CHECKDB  
 Se non è disponibile un backup valido, eseguire DBCC CHECKDB senza la clausola REPAIR per determinare l'entità del danno. Verrà automaticamente suggerita la clausola REPAIR da usare. Eseguire quindi DBCC CHECKDB con la clausola REPAIR appropriata per correggere il database.  
  
> [!CAUTION]  
>  Se non si è certi dell'effetto prodotto sui dati dall'esecuzione di DBCC CHECKDB con la clausola REPAIR, contattare il personale del supporto tecnico prima di eseguire l'istruzione.  
  
 Se l'esecuzione di DBCC CHECKDB con una clausola REPAIR non consente di risolvere il problema, contattare il personale del supporto tecnico.  
  
### <a name="results-of-running-repair-options"></a>Risultati dell'esecuzione delle opzioni REPAIR  
 L'esecuzione di REPAIR invalida la mappa di bit differenziale. Non è possibile eseguire un backup differenziale fino a che viene eseguito un backup completo del database. Il backup completo del database offre un riferimento per la ricompilazione della mappa di bit differenziale.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un backup completo del database &#40;SQL Server&#41;](../backup-restore/create-a-full-database-backup-sql-server.md)   
 [MSSQLSERVER_2516](mssqlserver-2516-database-engine-error.md)  
  
  
