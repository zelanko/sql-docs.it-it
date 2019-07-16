---
title: Chiama una Stored Procedure | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- calling stored procedures
- ODBC, stored procedures
- stored procedures [ODBC], calling
- SQL Server Native Client ODBC driver, stored procedures
- ODBC CALL escape sequence
- escape sequences [SQL Server]
- CALL statement
ms.assetid: d13737f4-f641-45bf-b56c-523e2ffc080f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7b1441f06a5825467431a7c11ee9a8e3e46df6fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910268"
---
# <a name="calling-a-stored-procedure"></a>Chiamata di una stored procedure
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta sia la sequenza di escape ODBC CALL e la [!INCLUDE[tsql](../../includes/tsql-md.md)] [EXECUTE](../../t-sql/language-elements/execute-transact-sql.md) istruzione per l'esecuzione di stored procedure, la sequenza di escape ODBC CALL è il metodo preferito. L'utilizzo di sintassi ODBC consente a un'applicazione di recuperare i codici restituiti delle stored procedure e il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client è anch'esso ottimizzato per l'utilizzo di un protocollo sviluppato in origine per l'invio di chiamate a procedure remote (RPC, Remote Procedure Call) tra computer che eseguono [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo protocollo RPC migliora le prestazioni riducendo l'elaborazione dei parametri e l'analisi delle istruzioni eseguite sul server.  
  
> [!NOTE]  
>  Quando si chiama [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stored procedure utilizzando parametri denominati con ODBC (per altre informazioni, vedere [Binding Parameters by Name (Named Parameters)](https://go.microsoft.com/fwlink/?LinkID=209721)), i nomi dei parametri devono iniziare con il '\@' caratteri. Si tratta di una restrizione specifica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client applica questa limitazione in modo più restrittivo rispetto a MDAC (Microsoft Data Access Components).  
  
 La sequenza di escape ODBC CALL per la chiamata a una procedura è la seguente:  
  
 {[ **? =** ]**chiamare**_procedure_name_[([*parametro*] [ **,** [*parametro*]] ...)]}  
  
 in cui *procedure_name* specifica il nome di una stored procedure e *parametro* specifica un parametro di routine. I parametri denominati sono supportati solo nelle istruzioni che utilizzano la sequenza di escape ODBC CALL.  
  
 Una procedura può avere zero o più parametri. Una procedura può inoltre restituire un valore, come indicato dall'indicatore di parametro facoltativo ?= all'inizio della sintassi. Se un parametro è un parametro di input/output, può essere un valore letterale o un marcatore di parametro. Se il parametro è un parametro di output, deve essere un marcatore di parametro, in quanto l'output non è noto. Marcatori di parametro devono essere associati con [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) prima della chiamata di procedura viene eseguita l'istruzione.  
  
 I parametri di input e di input/output possono essere omessi dalle chiamate alle procedure. Se una procedura viene chiamata con parentesi ma senza alcun parametro, il driver indica all'origine dati di utilizzare il valore predefinito per il primo parametro. Ad esempio:  
  
 {**chiamare** _procedure_name_ **()** }  
  
 Se la procedura non include alcun parametro, può non essere eseguita. Se una procedura viene chiamata senza parentesi, il driver non invia alcun valore di parametro. Ad esempio:  
  
 {**chiamare** _procedure_name_}  
  
 È possibile specificare valori letterali per parametri di input e di input/output nelle chiamate alle procedure. La procedura InsertOrder, ad esempio, include cinque parametri di input. La chiamata seguente a InsertOrder omette il primo parametro, fornisce un valore letterale per il secondo parametro e utilizza un marcatore di parametro per i parametri terzo, quarto e quinto. I parametri sono numerati in sequenza, a partire dal valore 1.  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}  
```  
  
 Si noti che se si omette un parametro, la virgola che lo delimita rispetto ad altri parametri deve comunque essere presente. Se si omette un parametro di input o di input/output, la procedura utilizza il valore predefinito del parametro. Altri modi di specificare il valore predefinito di un parametro di input o di input/output consistono nell'impostare il valore del buffer di lunghezza/indicatore associato al parametro su SQL_DEFAULT_PARAM oppure nell'utilizzare la parola chiave DEFAULT.  
  
 Se si omette un parametro di input/output o se si fornisce un valore letterale per il parametro, il driver ignora il valore di output. Analogamente, se il marcatore di parametro per il valore restituito di una procedura viene omesso, il driver ignora il valore restituito. Se, infine, un'applicazione specifica un parametro di valore restituito per una procedura che non restituisce alcun valore, il driver imposta il valore per il buffer di lunghezza/indicatore associato al parametro su SQL_NULL_DATA.  
  
## <a name="delimiters-in-call-statements"></a>Delimitatori nelle istruzioni CALL  
 Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client supporta inoltre per impostazione predefinita un'opzione di compatibilità specifica della sequenza di escape ODBC {CALL}. Il driver accetta istruzioni CALL con un singolo set di virgolette doppie che delimitano l'intero nome di stored procedure:  
  
```  
{ CALL "master.dbo.sp_who" }  
```  
  
 Per impostazione predefinita, il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client accetta inoltre istruzioni CALL che seguono le regole ISO e racchiudono ogni identificatore tra virgolette doppie:  
  
```  
{ CALL "master"."dbo"."sp_who" }  
```  
  
 Se eseguito con le impostazioni predefinite, tuttavia, il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client non supporta l'utilizzo di alcuna forma di identificatore tra virgolette con identificatori che contengono caratteri non specificati come validi negli identificatori dallo standard ISO. Ad esempio, il driver non è possibile accedere a una stored procedure denominata **"My. proc"** utilizzando un'istruzione CALL con identificatori tra virgolette:  
  
```  
{ CALL "MyDB"."MyOwner"."My.Proc" }  
```  
  
 Questa istruzione viene interpretata dal driver nel modo seguente:  
  
```  
{ CALL MyDB.MyOwner.My.Proc }  
```  
  
 Il server genera un errore che un server collegato denominato **MyDB** non esiste.  
  
 Il problema non si verifica quando si utilizzano identificatori tra parentesi. In questo caso, l'istruzione viene interpretata correttamente:  
  
```  
{ CALL [MyDB].[MyOwner].[My.Table] }  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione delle stored procedure](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
