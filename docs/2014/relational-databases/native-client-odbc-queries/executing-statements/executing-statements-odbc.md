---
title: Esecuzione di istruzioni (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a367d5ee7def19ffdfd40e24860ebf95f642fae9
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82700425"
---
# <a name="executing-statements-odbc"></a>Esecuzione di istruzioni (ODBC)
  Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native Client offre diversi modi per eseguire istruzioni SQL in un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] database:  
  
-   Esecuzione diretta  
  
-   Esecuzione preparata  
  
 L'esecuzione diretta implica la compilazione di una stringa di caratteri contenente un' [!INCLUDE[tsql](../../../includes/tsql-md.md)] istruzione e l'invio per l'esecuzione tramite la funzione **SQLExecDirect** . L'esecuzione preparata implica la compilazione di una stringa di caratteri contenente un'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] e la successiva esecuzione di questa in due fasi. Nella prima fase viene utilizzata la funzione [SQLPrepare function](https://go.microsoft.com/fwlink/?LinkId=59360) per analizzare e compilare il piano di esecuzione per l'istruzione in [!INCLUDE[ssDE](../../../includes/ssde-md.md)] . Nella seconda fase viene utilizzata la funzione **SQLExecute** per eseguire il piano di esecuzione preparato in precedenza. con conseguente risparmio dell'overhead correlato all'analisi e alla compilazione in ogni esecuzione. L'esecuzione preparata viene generalmente utilizzata dalle applicazioni per eseguire ripetutamente la stessa istruzione SQL con parametri.  
  
 Sia nel caso dell'esecuzione diretta che in quello dell'esecuzione preparata è possibile eseguire una singola istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] o un batch di istruzioni SQL oppure è possibile chiamare una stored procedure.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Esecuzione diretta](direct-execution.md)  
  
-   [Esecuzione preparata](prepared-execution.md)  
  
-   [Procedure](procedures.md)  
  
-   [Batch di istruzioni](batches-of-statements.md)  
  
-   [Effetti delle opzioni ISO](effects-of-iso-options.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di query &#40;ODBC&#41;](../executing-queries-odbc.md)  
  
  
