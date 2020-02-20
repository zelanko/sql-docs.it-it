---
title: Risultati dei messaggi di SQL Server | Microsoft Docs
description: risultati dei messaggi di SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 05d731f418bad21f9e8ec32c620b352c5663994a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67994915"
---
# <a name="sql-server-message-results"></a>Risultati dei messaggi di SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Le istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] seguenti non generano set di righe del driver OLE DB per SQL Server o un conteggio delle righe interessate durante l'esecuzione:  
  
-   PRINT  
  
-   RAISERROR con gravità minore o uguale a 10  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Queste istruzioni restituiscono uno o più messaggi informativi o determinano la restituzione da parte di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di messaggi informativi in sostituzione dei risultati del conteggio o del set di righe. Al completamento dell'esecuzione, OLE DB Driver per SQL Server restituisce S_OK e i messaggi sono disponibili per il consumer di OLE DB Driver per SQL Server.  
  
 OLE DB Driver per SQL Server restituisce S_OK e include uno o più messaggi informativi disponibili in seguito all'esecuzione di più istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] o all'esecuzione da parte del consumer di una funzione membro di OLE DB Driver per SQL Server.  
  
 Il consumer del driver OLE DB per SQL Server che consente la specifica dinamica del testo della query deve controllare le interfacce di errore dopo l'esecuzione di ogni funzione membro, indipendentemente dal valore del codice restituito, dalla presenza o dall'assenza di un riferimento all'interfaccia **IRowset** o **IMultipleResults** restituito o di un conteggio delle righe interessate.  
  
## <a name="see-also"></a>Vedere anche  
 [Errori](../../oledb/ole-db-errors/errors.md)  
  
  
