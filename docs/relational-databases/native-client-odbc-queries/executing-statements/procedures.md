---
title: Procedure | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC]
- stored procedures [ODBC], about ODBC stored procedures
- ODBC applications, statements
- statements [ODBC], stored procedures
- ODBC applications, stored procedures
ms.assetid: c64d5f3a-376b-48ef-84f3-b6148ac8600a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 59d971f4d835470924874b0a08a648d36d98c0f9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81297912"
---
# <a name="procedures"></a>Procedure
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Una stored procedure è un oggetto eseguibile precompilato che contiene una o più istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Le stored procedure possono includere parametri di input e di output e possono restituire anche codice di tipo integer. Un'applicazione può enumerare le stored procedure disponibili utilizzando funzioni di catalogo.  
  
 Le applicazioni ODBC destinate a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devono utilizzare solo l'esecuzione diretta per chiamare una stored procedure. Quando si è connessi a versioni [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , il driver ODBC di Native Client implementa la [funzione SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360) creando una stored procedure temporanea, che viene quindi chiamata in **SQLExecute**. Viene aggiunto un sovraccarico per fare in modo che **SQLPrepare** crei una stored procedure temporanea che chiama solo il stored procedure di destinazione anziché eseguire direttamente il stored procedure di destinazione. Anche in caso di connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la preparazione di una chiamata richiede round trip aggiuntivo in rete e la compilazione di un piano di esecuzione che chiami solo il piano di esecuzione della stored procedure.  
  
 Le applicazioni ODBC devono utilizzare la sintassi ODBC CALL in caso di esecuzione di una stored procedure. Il driver è ottimizzato per l'utilizzo di un meccanismo di chiamata a procedure remote per chiamare la procedura quando si utilizza la sintassi ODBC CALL. Si tratta di un meccanismo molto più efficiente di quello utilizzato per inviare un'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE al server.  
  
 Per ulteriori informazioni, vedere [esecuzione di stored procedure](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di istruzioni &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
