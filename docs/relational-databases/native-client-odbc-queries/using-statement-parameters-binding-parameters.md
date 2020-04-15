---
title: Parametri di binding . Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, parameters
- parameters [SQL Server Native Client], ODBC
- statements [ODBC], parameters
- binding parameters [SQL Server Native Client]
- parameter markers [ODBC]
- unbound parameter markers
- SQLBindParameter function
- ODBC applications, parameters
- bound parameter markers [SQL Server Native Client]
ms.assetid: d6c69739-8f89-475f-a60a-b2f6c06576e2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 01e179d2abc6ef786f94b6d7938f0e21938c5a59
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304630"
---
# <a name="using-statement-parameters---binding-parameters"></a>Uso dei parametri dell'istruzione - Associazione di parametri
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Ogni marcatore di parametro in un'istruzione SQL deve essere associato a una variabile nell'applicazione prima di eseguire l'istruzione. Questa operazione viene eseguita chiamando il [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) funzione. **SQLBindParameter** descrive la variabile di programma (indirizzo, tipo di dati C e così via) al driver. La funzione identifica inoltre il marcatore di parametro specificandone il valore ordinale e quindi descrive le caratteristiche dell'oggetto SQL rappresentato (tipo di dati SQL, precisione e così via).  
  
 I marcatori di parametro possono essere associati o riassociati in qualunque momento prima di eseguire un'istruzione. Un'associazione di parametri rimane effettiva fino a quando non si verifica uno dei casi seguenti:  
  
-   Una chiamata a [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con il parametro *Option* impostato su SQL_RESET_PARAMS libera tutti i parametri associati all'handle dell'istruzione.  
  
-   Una chiamata a **SQLBindParameter** con *ParameterNumber* impostato sull'ordinale di un marcatore di parametro associato rilascia automaticamente l'associazione precedente.  
  
 Un'applicazione può inoltre associare parametri a matrici di variabili di programma per elaborare un'istruzione SQL in batch. Sono disponibili due tipi diversi di associazione di matrici:  
  
-   L'associazione per colonna viene eseguita quando ogni singolo parametro viene associato alla relativa matrice di variabili.  
  
     L'associazione per colonna viene specificata chiamando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) con *Attribute* impostato su SQL_ATTR_PARAM_BIND_TYPE e *ValuePtr* impostato su SQL_PARAM_BIND_BY_COLUMN.  
  
-   L'associazione per riga viene eseguita quando tutti i parametri nell'istruzione SQL vengono associati come unità a una matrice di strutture contenente le singole variabili per i parametri.  
  
     L'associazione per riga viene specificata chiamando **SQLSetStmtAttr** con *Attribute* impostato su SQL_ATTR_PARAM_BIND_TYPE e *ValuePtr* impostato sulla dimensione della struttura contenente le variabili di programma.  
  
 Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il driver ODBC Native Client invia parametri di tipo carattere o stringa binaria al server, riempie i valori alla lunghezza specificata nel parametro *ColumnSize* **SQLBindParameter.** Se un'applicazione ODBC 2.x specifica 0 per *ColumnSize*, il driver memorizza il valore del parametro alla precisione del tipo di dati. La precisione è 8000 in caso di connessione a server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 255 in caso di connessione a versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *ColumnSize* è in byte per le colonne variante.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta la definizione di nomi per parametri delle stored procedure. Anche in ODBC 3.5 è stato introdotto il supporto per parametri denominati utilizzati per chiamare stored procedure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo supporto può essere utilizzato per effettuare le operazioni seguenti:  
  
-   Chiamare una stored procedure e fornire valori per un subset dei parametri definiti per la stored procedure.  
  
-   Specificare i parametri in un ordine diverso nell'applicazione rispetto all'ordine specificato alla creazione della stored procedure.  
  
 I parametri denominati sono [!INCLUDE[tsql](../../includes/tsql-md.md)] supportati solo quando si utilizza l'istruzione **EXECUTE** o la sequenza di escape ODBC CALL per eseguire una stored procedure.  
  
 Se **SQL_DESC_NAME** è impostato per un parametro di stored procedure, tutti i parametri della stored procedure nella query devono anche impostare **SQL_DESC_NAME**.  Se i valori letterali vengono utilizzati nelle chiamate di stored procedure, in cui i parametri **sono** SQL_DESC_NAME impostati, @p1i valori letterali devono utilizzare il formato *'valore* *nome*=', dove *nome* è il nome del parametro della stored procedure (ad esempio, ). Per ulteriori informazioni, vedere [Associazione di parametri in base al nome (parametri denominati)](https://go.microsoft.com/fwlink/?LinkId=167215).  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo dei parametri delle istruzioni](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
  
