---
title: SQL Server risultati del messaggio | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3383dcd08ed5910d949608e521b3cd23f37aace8
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73790157"
---
# <a name="sql-server-message-results"></a>Risultati dei messaggi di SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Le seguenti istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] non generano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] set di righe del provider di OLE DB Native client o un conteggio delle righe interessate quando vengono eseguite:  
  
-   PRINT  
  
-   RAISERROR con gravità minore o uguale a 10  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Queste istruzioni restituiscono uno o più messaggi informativi o determinano la restituzione da parte di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di messaggi informativi in sostituzione dei risultati del conteggio o del set di righe. Al completamento dell'esecuzione, il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client restituisce S_OK e i messaggi sono disponibili per il consumer del provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client restituisce S_OK e dispone di uno o più messaggi informativi disponibili dopo l'esecuzione di molte istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] o dell'esecuzione del consumer di una funzione membro del provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB.  
  
 Il consumer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB provider che consente di specificare dinamicamente il testo della query deve controllare le interfacce di errore dopo l'esecuzione di ogni funzione membro indipendentemente dal valore del codice restituito, dalla presenza o dall'assenza di un oggetto **IRowset restituito** o riferimento all'interfaccia **IMultipleResults** o conteggio delle righe interessate.  
  
## <a name="see-also"></a>Vedere anche  
 [errori](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
