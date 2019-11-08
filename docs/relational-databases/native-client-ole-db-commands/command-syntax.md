---
title: Sintassi del comando | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, commands
- commands [OLE DB]
- SQL Server Native Client OLE DB provider, stored procedures
- stored procedures [OLE DB], command syntax
ms.assetid: d463d3d7-e5cb-426d-8e92-aa29980356b6
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 88ba95d4664d4ec3247fbd37c4eb33c37410cd6b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73790671"
---
# <a name="command-syntax"></a>Sintassi dei comandi
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client riconosce la sintassi del comando specificata dalla DBGUID_SQL macro. Per il provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB, l'identificatore indica che un'amalgama di ODBC SQL, ISO e [!INCLUDE[tsql](../../includes/tsql-md.md)] è una sintassi valida. L'istruzione SQL seguente, ad esempio, utilizza una sequenza di escape ODBC SQL per specificare la funzione per i valori stringa LCASE:  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE restituisce una stringa di caratteri, convertendo tutti i caratteri maiuscoli nei rispettivi equivalenti minuscoli. Poiché la funzione per i valori stringa ISO LOWER esegue la stessa operazione, l'istruzione SQL seguente è un equivalente ISO dell'istruzione ODBC presentata nell'esempio precedente:  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client elabora correttamente una delle forme dell'istruzione quando viene specificato come testo per un comando.  
  
## <a name="stored-procedures"></a>Stored procedure  
 Quando si esegue un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stored procedure utilizzando un comando del provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client, utilizzare la sequenza di escape ODBC CALL nel testo del comando. Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client usa quindi il meccanismo di chiamata a procedura remota di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ottimizzare l'elaborazione del comando. L'istruzione ODBC SQL seguente, ad esempio, rappresenta il testo del comando preferito rispetto alla forma [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Comandi](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
