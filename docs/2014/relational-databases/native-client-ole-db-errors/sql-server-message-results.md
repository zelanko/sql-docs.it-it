---
title: Risultati di SQL Server messaggi | Documenti di Microsoft
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206716"
---
# <a name="sql-server-message-results"></a>Risultati dei messaggi di SQL Server
  Nell'esempio [!INCLUDE[tsql](../../includes/tsql-md.md)] non generano istruzioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client rowset OLE DB provider o un conteggio di righe quando viene eseguito è influenzato:  
  
-   PRINT  
  
-   RAISERROR con gravità minore o uguale a 10  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Queste istruzioni restituiscono uno o più messaggi informativi o determinano la restituzione da parte di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di messaggi informativi in sostituzione dei risultati del conteggio o del set di righe. In caso di esecuzione, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce S_OK e i messaggi sono disponibili per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer del provider OLE DB Native Client.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce S_OK e include uno o più messaggi informativi disponibili in seguito all'esecuzione di molte [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzioni o l'esecuzione del consumer di un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] membro del provider OLE DB Native Client funzione.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client consumer OLE DB provider consentendo dinamico specifica del testo della query è necessario controllare interfacce degli errori dopo ogni esecuzione della funzione membro indipendentemente dal valore del codice restituito, la presenza o assenza di un restituito**IRowset** o **IMultipleResults** riferimenti all'interfaccia o un numero di righe modificate.  
  
## <a name="see-also"></a>Vedere anche  
 [errori](errors.md)  
  
  
