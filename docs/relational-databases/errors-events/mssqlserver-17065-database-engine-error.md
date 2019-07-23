---
title: MSSQLSERVER_17065 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17065 (Database Engine error)
ms.assetid: 63c2ba5a-be34-461e-bee1-03c25b396cd2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 67ad5d8ffb2f6ba2c0f70898e37081a889da9830
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100367"
---
# <a name="mssqlserver17065"></a>MSSQLSERVER_17065
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|17065|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SQLASSERT_BOTH|  
|Testo del messaggio|Asserzione SQL Server: file: \<%s>, riga = %d Asserzione non riuscita = '%s' %s. L'errore può essere correlato agli intervalli di tempo. Se dopo aver rieseguito l'istruzione l'errore persiste, utilizzare DBCC CHECKDB per verificare l'integrità strutturale del database oppure riavviare il server per verificare che le strutture di dati in memoria non siano danneggiate.|  
  
## <a name="explanation"></a>Spiegazione  
Questo errore può essere causato da errori temporanei, correlati agli intervalli di tempo o da un danno dei dati in memoria o su disco.  
  
## <a name="user-action"></a>Azione dell'utente  
Eseguire nuovamente l'istruzione che ha causato l'attivazione dell'eccezione. Se l'errore è causato da un evento correlato agli intervalli di tempo, è possibile che non si ripeta. Se il problema persiste, eseguire DBCC CHECKDB per verificare il danno su disco. Riavviare il server per assicurarsi che le strutture di dati in memoria non siano danneggiate.  
  
## <a name="see-also"></a>Vedere anche  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
