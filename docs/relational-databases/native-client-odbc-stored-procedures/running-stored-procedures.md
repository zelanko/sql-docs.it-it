---
title: Esecuzione di Stored procedure | Documenti di Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- stored procedures [ODBC], running
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], executing
ms.assetid: 866b6dd3-2acd-4dfb-aeca-a0352b2d4c6a
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b44a9b4a863de7d3c7b37ec3b8b53837e6acf953
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740545"
---
# <a name="running-stored-procedures"></a>Esecuzione delle stored procedure
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Una stored procedure è un oggetto eseguibile archiviato in un database. Supporti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Stored procedure:  
  
     Una o più istruzioni SQL precompilate in una sola stored procedure eseguibile.  
  
-   Stored procedure estese:  
  
     DLL C o C++ scritte nell'API ODS di SQL Server per le stored procedure estese. L'API ODS amplia le funzionalità delle stored procedure per includere il codice C o C++.  
  
 Durante l'esecuzione delle istruzioni, la chiamata a una stored procedure sull'origine dati, in alternativa all'esecuzione o alla preparazione diretta di un'istruzione nell'applicazione client, può offrire:  
  
-   Prestazioni più elevate  
  
     Le istruzioni SQL vengono analizzate e compilate durante la creazione delle stored procedure. Questo overhead viene quindi salvato durante l'esecuzione delle stored procedure.  
  
-   Overhead di rete ridotto  
  
     L'esecuzione di una stored procedure in alternativa all'invio di query complesse in rete può ridurre il traffico di rete. Se un'applicazione ODBC utilizza la sintassi ODBC {CALL} per eseguire una stored procedure, il driver ODBC esegue ulteriori ottimizzazioni che eliminano la necessità di convertire i dati dei parametri.  
  
-   Maggiore coerenza  
  
     Se le regole di un'organizzazione vengono implementate in una risorsa centrale, ad esempio una stored procedure, possono essere codificate, testate e sottoposte a debug una volta. I singoli programmatori possono quindi utilizzare le stored procedure testate anziché sviluppare implementazioni personalizzate.  
  
-   Maggiore precisione  
  
     Poiché le stored procedure vengono in genere sviluppate da programmatori esperti, sono più efficienti e contengono un numero di errori inferiore rispetto al codice sviluppato più volte da programmatori meno competenti.  
  
-   Maggior numero di funzionalità  
  
     Le stored procedure estese possono utilizzare le caratteristiche C e C++ non disponibili nelle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
     Per un esempio di come chiamare una stored procedure, vedere [processo codici e i parametri di Output &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/running-stored-procedures-process-return-codes-and-output-parameters.md).  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Chiamata di una stored procedure](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
  
-   [Invio in batch di chiamate di stored procedure](../../relational-databases/native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)  
  
-   [Elaborazione dei risultati delle stored procedure](../../relational-databases/native-client-odbc-stored-procedures/processing-stored-procedure-results.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [Esecuzione di procedure per la Stored procedure &#40;ODBC&#41;](https://msdn.microsoft.com/library/c2220182-a23d-4475-b353-77a77ab613d6)  
  
  
