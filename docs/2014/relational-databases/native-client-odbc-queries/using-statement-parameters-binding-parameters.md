---
title: Parametri di binding | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 9dfe88f11cc26d4a9711b7f21caf4c4475ec954b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68206743"
---
# <a name="binding-parameters"></a>Associazione di parametri
  Ogni marcatore di parametro in un'istruzione SQL deve essere associato a una variabile nell'applicazione prima di eseguire l'istruzione. Questa operazione viene eseguita chiamando la funzione [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) . **SQLBindParameter** descrive la variabile di programma (indirizzo, tipo di dati C e così via) al driver. La funzione identifica inoltre il marcatore di parametro specificandone il valore ordinale e quindi descrive le caratteristiche dell'oggetto SQL rappresentato (tipo di dati SQL, precisione e così via).  
  
 I marcatori di parametro possono essere associati o riassociati in qualunque momento prima di eseguire un'istruzione. Un'associazione di parametri rimane effettiva fino a quando non si verifica uno dei casi seguenti:  
  
-   Una chiamata a [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) con il parametro *Option* impostato su SQL_RESET_PARAMS libera tutti i parametri associati all'handle di istruzione.  
  
-   Una chiamata a **SQLBindParameter** con *ParameterNumber* impostato sull'ordinale di un marcatore di parametro associato rilascia automaticamente l'associazione precedente.  
  
 Un'applicazione può inoltre associare parametri a matrici di variabili di programma per elaborare un'istruzione SQL in batch. Sono disponibili due tipi diversi di associazione di matrici:  
  
-   L'associazione per colonna viene eseguita quando ogni singolo parametro viene associato alla relativa matrice di variabili.  
  
     L'associazione per colonna viene specificata chiamando [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) con *Attribute* impostato su SQL_ATTR_PARAM_BIND_TYPE e *ValuePtr* impostato su SQL_PARAM_BIND_BY_COLUMN.  
  
-   L'associazione per riga viene eseguita quando tutti i parametri nell'istruzione SQL vengono associati come unità a una matrice di strutture contenente le singole variabili per i parametri.  
  
     L'associazione per riga viene specificata chiamando **SQLSetStmtAttr** con *Attribute* impostato su SQL_ATTR_PARAM_BIND_TYPE e *ValuePtr* impostato sulle dimensioni della struttura che contiene le variabili di programma.  
  
 Quando il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client invia parametri di stringa di tipo carattere o binario al server, i valori vengono ripresi alla lunghezza specificata nel parametro **SQLBindParameter** *ColumnSize* . Se un'applicazione ODBC 2. x specifica 0 per *ColumnSize*, il driver riempie il valore del parametro con la precisione del tipo di dati. La precisione è 8000 in caso di connessione a server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 255 in caso di connessione a versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *ColumnSize* è in byte per le colonne variant.  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta la definizione di nomi per parametri delle stored procedure. Anche in ODBC 3.5 è stato introdotto il supporto per parametri denominati utilizzati per chiamare stored procedure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo supporto può essere utilizzato per effettuare le operazioni seguenti:  
  
-   Chiamare una stored procedure e fornire valori per un subset dei parametri definiti per la stored procedure.  
  
-   Specificare i parametri in un ordine diverso nell'applicazione rispetto all'ordine specificato alla creazione della stored procedure.  
  
 I parametri denominati sono supportati solo [!INCLUDE[tsql](../../includes/tsql-md.md)] `EXECUTE` quando si utilizza l'istruzione o la sequenza di escape ODBC CALL per eseguire un stored procedure.  
  
 Se per un parametro della stored procedure è impostato `SQL_DESC_NAME`, sarà necessario impostare `SQL_DESC_NAME` anche per tutti gli altri parametri della stored procedure nella query.  Se vengono usati valori letterali nelle chiamate di stored procedure, in `SQL_DESC_NAME` cui sono impostati i parametri, i valori letterali devono usare il formato *' nome*=*valore*', dove *nome* è il nome del @p1parametro di stored procedure (ad esempio,). Per ulteriori informazioni, vedere [associazione di parametri in base al nome (parametri denominati)](https://go.microsoft.com/fwlink/?LinkId=167215).  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo dei parametri delle istruzioni](using-statement-parameters.md)  
  
  
