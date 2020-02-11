---
title: Sintassi del comando | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 00ab769ee2051edc499d586ab7d5ee1fa47dd854
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62468218"
---
# <a name="command-syntax"></a>Sintassi dei comandi
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client riconosce la sintassi del comando specificata dalla macro DBGUID_SQL. Per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client, l'identificatore indica che un'amalgama di ODBC SQL, ISO [!INCLUDE[tsql](../../includes/tsql-md.md)] ed è una sintassi valida. L'istruzione SQL seguente, ad esempio, utilizza una sequenza di escape ODBC SQL per specificare la funzione per i valori stringa LCASE:  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE restituisce una stringa di caratteri, convertendo tutti i caratteri maiuscoli nei rispettivi equivalenti minuscoli. Poiché la funzione per i valori stringa ISO LOWER esegue la stessa operazione, l'istruzione SQL seguente è un equivalente ISO dell'istruzione ODBC presentata nell'esempio precedente:  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client elabora una forma dell'istruzione correttamente quando viene specificato come testo per un comando.  
  
## <a name="stored-procedures"></a>Stored procedure  
 Quando si esegue un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stored procedure utilizzando un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comando del provider OLE DB di Native client, utilizzare la sequenza di escape ODBC Call nel testo del comando. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client usa quindi il meccanismo RPC ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Remote Procedure Call) di per ottimizzare l'elaborazione dei comandi. L'istruzione ODBC SQL seguente, ad esempio, rappresenta il testo del comando preferito rispetto alla forma [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Comandi](commands.md)  
  
  
