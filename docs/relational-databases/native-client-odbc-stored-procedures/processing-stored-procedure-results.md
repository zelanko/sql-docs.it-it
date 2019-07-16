---
title: Elaborazione dei risultati delle Stored Procedure | Documenti di Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], results
ms.assetid: 788ef2a4-17de-4526-960b-46bf29aafc9f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4051a18aeec513a19781df7f4a98006b7f0ccd54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910276"
---
# <a name="processing-stored-procedure-results"></a>Risultati dell'elaborazione delle stored procedure
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Per le stored procedure di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono disponibili quattro meccanismi di restituzione dei dati:  
  
-   Ogni istruzione SELECT di una stored procedure genera un set di risultati.  
  
-   La procedura può restituire dati tramite parametri di output.  
  
-   Un parametro di output del cursore può passare nuovamente un cursore del server [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   La procedura può avere un codice restituito di tipo integer.  
  
 Le applicazioni devono essere in grado di gestire tutti questi output dalle stored procedure. L'istruzione CALL o EXECUTE deve includere marcatori di parametro per il codice restituito e i parametri di output. Usa [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) per associarli tutti come parametri di output e di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client verranno trasferiti i valori di output in variabili associate. I parametri di output e i codici restituiti sono gli ultimi elementi restituiti al client da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; non vengono restituiti all'applicazione solo [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) restituisce SQL_NO_DATA.  
  
 ODBC non supporta i parametri di cursore [!INCLUDE[tsql](../../includes/tsql-md.md)] di associazione. Dal momento che tutti i parametri di output devono essere associati prima di eseguire una stored procedure, le stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] che contengono un parametro di cursore di output non possono essere chiamate dalle applicazioni ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione delle stored procedure](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
