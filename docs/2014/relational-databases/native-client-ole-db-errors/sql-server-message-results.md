---
title: Risultati dei messaggi di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: ff604f4c5d66a5742868e25ba05ca6b4528ddb1a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "68206716"
---
# <a name="sql-server-message-results"></a>Risultati dei messaggi di SQL Server
  Le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] seguenti non generano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] set di righe del provider OLE DB Native client o un conteggio delle righe interessate quando vengono eseguite:  
  
-   PRINT  
  
-   RAISERROR con gravità minore o uguale a 10  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Queste istruzioni restituiscono uno o più messaggi informativi o determinano la restituzione da parte di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di messaggi informativi in sostituzione dei risultati del conteggio o del set di righe. Al completamento dell'esecuzione, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il provider di OLE DB di Native client restituisce S_OK e i messaggi sono disponibili [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il consumer del provider OLE DB di Native Client.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client restituisce S_OK e include uno o più messaggi informativi disponibili dopo l' [!INCLUDE[tsql](../../includes/tsql-md.md)] esecuzione di molte istruzioni o l'esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del consumer di una funzione membro del provider di OLE DB di Native Client.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer del provider OLE DB di Native client che consente di specificare dinamicamente il testo della query deve controllare le interfacce di errore dopo l'esecuzione di ogni funzione membro, indipendentemente dal valore del codice restituito, dalla presenza o dall'assenza di un riferimento all'interfaccia **IRowset** o **IMultipleResults** restituito o da un conteggio delle righe interessate.  
  
## <a name="see-also"></a>Vedi anche  
 [Errors](errors.md)  
  
  
