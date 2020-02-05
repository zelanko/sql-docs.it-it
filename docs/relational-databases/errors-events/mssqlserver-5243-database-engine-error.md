---
title: MSSQLSERVER_5243 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5243 (Database Engine error)
ms.assetid: e04a1934-e57d-420e-ac79-97071745824e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 19fd1351963a578d83e8cf67a48c6f97dcd96afe
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68078863"
---
# <a name="mssqlserver_5243"></a>MSSQLSERVER_5243
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|5243|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico||  
|Testo del messaggio|Rilevata inconsistenza durante un'operazione interna. Contattare il supporto tecnico. Numero di riferimento %ld.|  
  
## <a name="explanation"></a>Spiegazione  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha rilevato un'inconsistenza strutturale in una struttura del motore di archiviazione in memoria.  
  
## <a name="user-action"></a>Azione dell'utente  
Trovare gli errori hardware. Eseguire gli strumenti di diagnostica hardware e risolvere eventuali problemi. Esaminare inoltre i registri applicazioni e il Registro di sistema di Windows, nonché il log degli errori di SQL Server per stabilire se l'errore è dovuto a un problema hardware. Risolvere tutti i problemi relativi all'hardware indicati nei log.

In caso di problemi persistenti che provocano il danneggiamento dei dati, provare a sostituire i vari componenti hardware per isolare il problema. Verificare che nel sistema non sia abilitata la memorizzazione nella cache in scrittura sul controller del disco. Se si ritiene che il problema sia dovuto alla memorizzazione nella cache in scrittura, rivolgersi al fornitore dell'hardware.

Infine, potrebbe essere conveniente passare a un nuovo sistema hardware. A tale scopo può essere necessario riformattare le unità disco e reinstallare il sistema operativo.

Ripristino da un backup. Se il problema non è correlato all'hardware ed è disponibile un backup valido noto, ripristinare il database dal backup.

Eseguire DBCC CHECKDB. Se non è disponibile un backup valido, eseguire DBCC CHECKDB senza la clausola REPAIR per determinare l'entità del danno. Verrà automaticamente suggerita la clausola REPAIR da usare. Eseguire quindi DBCC CHECKDB con la clausola REPAIR appropriata per correggere il database.

> **alert tag is not supported!!!!** 
> **tr tag is not supported!!!!** 
> **tr tag is not supported!!!!**

Se l'esecuzione di DBCC CHECKDB con una clausola REPAIR non consente di risolvere il problema, contattare il personale del supporto tecnico.
  
## <a name="see-also"></a>Vedere anche  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[Filegroup e file di database](~/relational-databases/databases/database-files-and-filegroups.md)  
  
