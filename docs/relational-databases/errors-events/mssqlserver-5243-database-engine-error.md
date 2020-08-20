---
description: MSSQLSERVER_5243
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
ms.openlocfilehash: 2575d81f09ccb3ac4aceb2396f5db0f8d9bee451
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470995"
---
# <a name="mssqlserver_5243"></a>MSSQLSERVER_5243
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
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
  
