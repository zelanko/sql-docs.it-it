---
title: Associazione dei parametri | Documenti di Microsoft
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 03903eedf9d1434ae7b1c20c2e6ddd57836b33cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942789"
---
# <a name="using-statement-parameters---binding-parameters"></a>Uso dei parametri dell'istruzione - Associazione di parametri
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Ogni marcatore di parametro in un'istruzione SQL deve essere associato a una variabile nell'applicazione prima di eseguire l'istruzione. Questa operazione viene eseguita chiamando il [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) funzione. **La funzione SQLBindParameter** descrive la variabile di programma (indirizzo, tipo di dati C e così via) al driver. La funzione identifica inoltre il marcatore di parametro specificandone il valore ordinale e quindi descrive le caratteristiche dell'oggetto SQL rappresentato (tipo di dati SQL, precisione e così via).  
  
 I marcatori di parametro possono essere associati o riassociati in qualunque momento prima di eseguire un'istruzione. Un'associazione di parametri rimane effettiva fino a quando non si verifica uno dei casi seguenti:  
  
-   Una chiamata a [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con il *opzione* parametro impostato su SQL_RESET_PARAMS rilascia tutti i parametri associati all'handle di istruzione.  
  
-   Una chiamata a **SQLBindParameter** con *ParameterNumber* è il numero ordinale di un indicatore di parametro associato viene rilasciata automaticamente l'associazione precedente.  
  
 Un'applicazione può inoltre associare parametri a matrici di variabili di programma per elaborare un'istruzione SQL in batch. Sono disponibili due tipi diversi di associazione di matrici:  
  
-   L'associazione per colonna viene eseguita quando ogni singolo parametro viene associato alla relativa matrice di variabili.  
  
     L'associazione per colonna viene specificata chiamando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) con *attributo* impostato su SQL_ATTR_PARAM_BIND_TYPE e *ValuePtr* impostato su SQL_PARAM_BIND_BY_COLUMN.  
  
-   L'associazione per riga viene eseguita quando tutti i parametri nell'istruzione SQL vengono associati come unità a una matrice di strutture contenente le singole variabili per i parametri.  
  
     L'associazione per riga viene specificata chiamando **SQLSetStmtAttr** con *attributo* impostato su SQL_ATTR_PARAM_BIND_TYPE e *ValuePtr* impostata sulle dimensioni dell'azienda struttura il variabili di programma.  
  
 Quando il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client invia i parametri di stringa binaria o di carattere al server, aggiungere spazi o i valori per la lunghezza specificata **SQLBindParameter** *ColumnSize* parametro. Se un'applicazione di ODBC 2. x specifica 0 per *ColumnSize*, il driver aggiunge riempimenti alla precisione del tipo di dati il valore del parametro. La precisione è 8000 in caso di connessione a server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 255 in caso di connessione a versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *ColumnSize* è espresso in byte per le colonne variant.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta la definizione di nomi per parametri delle stored procedure. Anche in ODBC 3.5 è stato introdotto il supporto per parametri denominati utilizzati per chiamare stored procedure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo supporto può essere utilizzato per effettuare le operazioni seguenti:  
  
-   Chiamare una stored procedure e fornire valori per un subset dei parametri definiti per la stored procedure.  
  
-   Specificare i parametri in un ordine diverso nell'applicazione rispetto all'ordine specificato alla creazione della stored procedure.  
  
 Parametri denominati sono supportati solo quando si utilizza il [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXECUTE** istruzione o la sequenza di escape ODBC CALL per eseguire una stored procedure.  
  
 Se **SQL_DESC_NAME** è impostata per un parametro di stored procedure, è necessario impostare anche tutti i parametri di stored procedure nella query **SQL_DESC_NAME**.  Se i valori letterali vengono usati nelle chiamate a stored procedure, in cui i parametri hanno **SQL_DESC_NAME** impostato, i valori letterali devono utilizzare il formato *' nome*=*valore*', in cui *name* è il nome di parametro della stored procedure (ad esempio, @p1). Per ulteriori informazioni, vedere [associazione di parametri (parametri) di nome](https://go.microsoft.com/fwlink/?LinkId=167215).  
  
## <a name="see-also"></a>Vedere anche  
 [Uso dei parametri di un'istruzione](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
  
