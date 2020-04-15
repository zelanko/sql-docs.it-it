---
title: Esecuzione Diretta . Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, statements
- direct execution [ODBC]
- SQLExecDirect function
- statements [ODBC], direct execution
ms.assetid: fa36e1af-ed98-4abc-97c1-c4cc5d227b29
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a89888ac055e83ab38588646f2f9b38ecd6444d0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297990"
---
# <a name="direct-execution"></a>Esecuzione diretta
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  L'esecuzione diretta rappresenta la modalità più semplice di esecuzione di un'istruzione. Un'applicazione compila una stringa [!INCLUDE[tsql](../../../includes/tsql-md.md)] di caratteri contenente un'istruzione e la invia per l'esecuzione utilizzando la funzione **SQLExecDirect.** Dopo avere raggiunto il server, l'istruzione viene compilata da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in un piano di esecuzione, che viene quindi immediatamente eseguito.  
  
 L'esecuzione diretta viene in genere utilizzata dalle applicazioni che compilano ed eseguono istruzioni in fase di esecuzione e rappresenta il metodo più efficiente per le istruzioni eseguite una sola volta. Lo svantaggio con molti database consiste nel fatto che l'istruzione SQL deve essere analizzata e compilata ogni volta che viene eseguita determinando un aumento dell'overhead se l'istruzione viene eseguita più volte.  
  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono notevolmente migliorate le prestazioni dell'esecuzione diretta delle istruzioni utilizzate più di frequente negli ambienti multiutente e l'utilizzo di SQLExecDirect con gi marcatori di parametro per le istruzioni SQL utilizzate più di frequente si avvicina all'efficienza dell'esecuzione preparata.  
  
 Quando si è [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]connessi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un'istanza di , il driver ODBC Native Client [utilizza sp_executesql](../../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md) per trasmettere l'istruzione SQL o il batch specificato in **SQLExecDirect**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]dispone di logica per determinare rapidamente se un'istruzione SQL o un batch eseguito con **sp_executesql** corrisponde all'istruzione o al batch che ha generato un piano di esecuzione già esistente in memoria. Se esiste una corrispondenza, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] riutilizza semplicemente il piano esistente anziché compilarne uno nuovo. Ciò significa che le istruzioni SQL comunemente eseguite eseguite con **SQLExecDirect** in un sistema con molti utenti trarranno vantaggio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]da molti dei vantaggi del riutilizzo del piano che erano disponibili solo per le stored procedure nelle versioni precedenti di .  
  
 Il vantaggio di riutilizzare i piani di esecuzione è valido solo quando più utenti eseguono lo stesso batch o la stessa istruzione SQL. Rispettare le seguenti convenzioni di scrittura del codice per aumentare la probabilità che le istruzioni SQL eseguite da client diversi siano simili abbastanza per potere riutilizzare i piani di esecuzione:  
  
-   Non includere costanti di dati nelle istruzioni SQL; utilizzare invece i marcatori di parametro associati alle variabili di programma. Per ulteriori informazioni, vedere [Utilizzo dei parametri dell'istruzione](../../../relational-databases/native-client-odbc-queries/using-statement-parameters.md).  
  
-   Utilizzare nomi di oggetto completi. I piani di esecuzione non vengono riutilizzati se i nomi di oggetto non sono completi.  
  
-   Se possibile, utilizzare per le connessioni dell'applicazione un set comune di opzioni dell'istruzione e di connessione. I piani di esecuzione generati per una connessione con un set di opzioni, ad esempio ANSI_NULLS, non vengono riutilizzati per una connessione con un altro set di opzioni. Il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e il provider ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client hanno le stesse impostazioni predefinite per queste opzioni.  
  
 Se tutte le istruzioni eseguite con **SQLExecDirect** vengono [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] codificate utilizzando queste convenzioni, è possibile riutilizzare i piani di esecuzione quando si verifica l'opportunità.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di istruzioni &#40;&#41;ODBCExecuting Statements &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
