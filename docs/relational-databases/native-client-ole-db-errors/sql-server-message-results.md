---
title: Risultati dei messaggi di SQL Server | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 577b609fd2f878e6c97010cac004e0b10b3a4e4e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300973"
---
# <a name="sql-server-message-results"></a>Risultati dei messaggi di SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] seguenti non generano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] set di righe del provider OLE DB Native client o un conteggio delle righe interessate quando vengono eseguite:  
  
-   PRINT  
  
-   RAISERROR con gravità minore o uguale a 10  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Queste istruzioni restituiscono uno o più messaggi informativi o determinano la restituzione da parte di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di messaggi informativi in sostituzione dei risultati del conteggio o del set di righe. Al completamento dell'esecuzione, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il provider di OLE DB di Native client restituisce S_OK e i messaggi sono disponibili [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il consumer del provider OLE DB di Native Client.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client restituisce S_OK e include uno o più messaggi informativi disponibili dopo l' [!INCLUDE[tsql](../../includes/tsql-md.md)] esecuzione di molte istruzioni o l'esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del consumer di una funzione membro del provider di OLE DB di Native Client.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer del provider OLE DB di Native client che consente di specificare dinamicamente il testo della query deve controllare le interfacce di errore dopo l'esecuzione di ogni funzione membro, indipendentemente dal valore del codice restituito, dalla presenza o dall'assenza di un riferimento all'interfaccia **IRowset** o **IMultipleResults** restituito o da un conteggio delle righe interessate.  
  
## <a name="see-also"></a>Vedere anche  
 [Errors](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
