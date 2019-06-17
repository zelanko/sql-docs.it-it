---
title: MSSQLSERVER_2512 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2512 (Database Engine error)
ms.assetid: 989b527f-5b02-403c-9b7f-51580f4e7688
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4b964e1a3958ed57251b2b5cccc8ec4dfc13f9eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62869211"
---
# <a name="mssqlserver2512"></a>MSSQLSERVER_2512
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|2512|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC_DUPLICATE_KEYS|  
|Testo del messaggio|Errore di tabella: ID di oggetto O_ID, indice con ID I_ID, partizione con ID PN_ID, unità allocazione con ID A_ID (tipo TYPE). Chiavi duplicate alla pagina ID1_P, slot SLOT1, e alla pagina ID2_P, slot SLOT2.|  
  
## <a name="explanation"></a>Spiegazione  
 I due slot specificati dispongono di chiavi identiche, inclusi gli `uniqueifiers`.  
  
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
 Se il record è un record fantasma o se l'indice non è univoco, DBCC è in grado di risolvere questo problema ricompilando l'indice. Altrimenti, se necessario, REPAIR eliminerà lo slot *SLOT2* nella pagina *P_ID2* o contrassegnerà lo slot come ghost.  
  
  
