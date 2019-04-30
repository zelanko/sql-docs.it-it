---
title: Utilità SqlLocalDB | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- SqlLocalDB utility [SQL Server]
- local database runtime utility
- LocalDB, SqlLocalDB Utility
ms.assetid: d785cdb7-1ea0-4871-bde9-1ae7881190f5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f13a16e7c8f507914abe8529e02b76161072c5bc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63035400"
---
# <a name="sqllocaldb-utility"></a>Utilità SqlLocalDB
  Usare la `SqlLocalDB` utilità per creare un'istanza di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssExpCurrent](../includes/ssexpcurrent-md.md)] **LocalDB**. Il `SqlLocalDB` utilità (SqlLocalDB.exe) è uno strumento semplice riga di comando per abilitare gli utenti e sviluppatori di creare e gestire un'istanza di [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] **LocalDB**. Per informazioni su come usare **LocalDB**, vedere [SQL Server 2014 Express LocalDB](../database-engine/configure-windows/sql-server-2016-express-localdb.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
SqlLocalDB.exe   
{  
      [ create   | c ] <instance-name><instance-version> [-s ]  
    | [ delete   | d ] <instance-name>  
    | [ start    | s ] <instance-name>  
    | [ stop     | p ] <instance-name>  [ -i ] [ -k ]  
    | [ share    | h ] ["<user_SID>" | "<user_account>" ] "<private-name>""<shared-name>"  
    | [ unshare  | u ] "<shared-name>"  
    | [ info     | i ] <instance-name>  
    | [ versions | v ]  
    | [ trace    | t ] [ on | off ]  
    | [ help     | -? ]  
}  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **create** | **c** ] *\<instance-name>* *\<instance-version>* [**-s** ]  
 Crea una nuova istanza di **LocalDB** di [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]. `SqlLocalDB` Usa la versione di [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] specificati da file binari  *\<istanza-version >* argomento. Il numero di versione viene specificato in formato numerico con almeno un numero decimale. I numeri di versione secondari (Service Pack) sono facoltativi. Ad esempio i numeri di versione due seguenti sono entrambi accettabili: 11.0 o 11.0.1186. La versione specificata deve essere installata nel computer. Se non specificato, il numero di versione predefinito per la versione del `SqlLocalDB` utilità. Aggiungere **-s** per avviare la nuova istanza di **LocalDB**.  
  
 [ **share** | **h** ]  
 Condivide l'istanza privata specificata di **LocalDB** tramite il nome condiviso indicato. Se viene omesso il SID dell'utente o il nome dell'account, il valore predefinito è l'utente corrente.  
  
 [ **unshared** | **u** ]  
 Arresta la condivisione dell'istanza condivisa specificata di **LocalDB**.  
  
 [ **delete** | **d** ] *\<instance-name>*  
 Elimina l'istanza specificata di **LocalDB** di [!INCLUDE[ssExpress](../includes/ssexpress-md.md)].  
  
 [ **start** | **s** ] "*\<instance-name>*"  
 Avvia l'istanza specificata di **LocalDB** di [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]. Quando ha esito positivo, l'istruzione restituisce l'indirizzo della named pipe del **database locale**.  
  
 [ **stop** | **p** ] *\<instance-name>* [**-i** ] [**-k** ]  
 Arresta l'istanza specificata di **LocalDB** di [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]. Aggiunta **-i** richiede l'arresto dell'istanza con il `NOWAIT` opzione. Aggiungere **-k** per terminare il processo dell'istanza senza contattarlo.  
  
 [ **info** | **i** ] [ *\<instance-name>* ]  
 Elenca tutte le istanze di [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** di proprietà dell'utente corrente.  
  
 *\<<instance-name>* restituisce il nome, la versione, lo stato (In esecuzione o Arrestato), l'ultima ora di inizio per l'istanza specificata di [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** e il nome della pipe locale di **LocalDB**.  
  
 [ **trace** | **t** ] **on** | **off**  
 **traccia sul** abilita la traccia per il `SqlLocalDB` chiamate API per l'utente corrente. **trace off** disabilita la traccia.  
  
 **-?**  
 Restituisce brevi descrizioni della ognuno `SqlLocalDB` opzione.  
  
## <a name="remarks"></a>Note  
 L'argomento *instance name* deve seguire le regole per gli identificatori di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] oppure deve essere incluso tra virgolette.  
  
 L'esecuzione di SqlLocalDB senza argomenti restituisce il testo della Guida.  
  
 Le operazioni diverse dall'avvio possono essere eseguite solo su un'istanza che appartiene all'utente attualmente connesso.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-creating-an-instance-of-localdb"></a>A. Creazione di un'istanza di LocalDB.  
 L'esempio seguente crea e avvia un'istanza di [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**di** denominata `DEPARTMENT` usando i file binari di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] .  
  
```  
SqlLocalDB.exe create "DEPARTMENT" 12.0 -s  
```  
  
### <a name="b-working-with-a-shared-instance-of-localdb"></a>B. Utilizzo di un'istanza condivisa di LocalDB  
 Aprire un prompt dei comandi con privilegi di amministratore.  
  
```  
SqlLocalDB.exe create "DeptLocalDB"  
SqlLocalDB.exe share "DeptLocalDB" "DeptSharedLocalDB"  
SqlLocalDB.exe start "DeptLocalDB"  
SqlLocalDB.exe info "DeptLocalDB"  
REM The previous statement outputs the Instance pipe name for the next step  
sqlcmd -S np:\\.\pipe\LOCALDB#<use your pipe name>\tsql\query  
CREATE LOGIN NewLogin WITH PASSWORD = 'Passw0rd!!@52';   
GO  
CREATE USER NewLogin;  
GO  
EXIT  
```  
  
 Eseguire il codice riportato di seguito per connettersi all'istanza condivisa di **LocalDB** utilizzando l'account di accesso `NewLogin` .  
  
```  
sqlcmd -S (localdb)\.\DeptSharedLocalDB -U NewLogin -P Passw0rd!!@52  
```  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server 2014 Express Local DB](../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
  
