---
title: MSSQLSERVER_17066 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17066 (Database Engine error)
ms.assetid: 7d650bbf-c583-4af8-9e22-993ee2880d95
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8c2bc421fb969e4f24e49871ff97047be9040ae0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967911"
---
# <a name="mssqlserver_17066"></a>MSSQLSERVER_17066
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|17066|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SQLASSERT_ONLY|  
|Testo del messaggio|Asserzione SQL Server: file: \<%s> , riga =% d asserzione non riuscita = '% s'. L'errore può essere correlato agli intervalli di tempo. Se dopo aver rieseguito l'istruzione l'errore persiste, utilizzare DBCC CHECKDB per verificare l'integrità strutturale del database oppure riavviare il server per verificare che le strutture di dati in memoria non siano danneggiate.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo errore può essere causato da errori temporanei, correlati agli intervalli di tempo o da un danno dei dati in memoria o su disco.  
  
## <a name="user-action"></a>Azione dell'utente  
 Eseguire nuovamente l'istruzione che ha causato l'attivazione dell'eccezione. Se l'errore è causato da un evento correlato agli intervalli di tempo, è possibile che non si ripeta. Se il problema persiste, eseguire DBCC CHECKDB per verificare il danno su disco. Riavviare il server per assicurarsi che le strutture di dati in memoria non siano danneggiate.  
  
## <a name="see-also"></a>Vedere anche  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
  
