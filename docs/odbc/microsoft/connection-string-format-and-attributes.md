---
title: Formato e attributi della stringa di connessione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connection strings
ms.assetid: 0c360112-8720-4e54-a1a6-b9b18d943557
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d95866976d2e83c058f83b3a0ae5e9a4e8888ed1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281151"
---
# <a name="connection-string-format-and-attributes"></a>Formato e attributi della stringa di connessione
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Anziché utilizzare una finestra di dialogo, è possibile che alcune applicazioni richiedano una stringa di connessione che specifichi le informazioni di connessione all'origine dati. La stringa di connessione è costituita da una serie di attributi che specificano il modo in cui un driver si connette a un'origine dati. Un attributo identifica una parte specifica di informazioni che il driver deve essere a conoscenza prima di poter eseguire la connessione all'origine dati appropriata. Ogni driver potrebbe avere un set di attributi diverso, ma il formato della stringa di connessione è sempre lo stesso. Una stringa di connessione ha il formato seguente:  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Microsoft ODBC driver for Oracle supporta il formato della stringa di connessione della prima versione del driver, che ha utilizzato `CONNECTSTRING`= anziché `SERVER=`.  
  
 Se ci si connette a un provider dell'origine dati che supporta l'autenticazione di Windows, `Trusted_Connection=yes` è necessario specificare al posto delle informazioni sull'ID utente e sulla password nella stringa di connessione.  
  
 Se non si specificano gli attributi UID, PWD, SERVER (o CONNECTSTRING) e DRIVER, è necessario specificare il nome dell'origine dati. Tutti gli altri attributi, tuttavia, sono facoltativi. Se non si specifica un attributo, per impostazione predefinita l'attributo viene impostato su quello specificato nella scheda DSN pertinente della finestra di dialogo **Amministrazione origine dati ODBC** . Il valore dell'attributo può fare distinzione tra maiuscole e minuscole.  
  
 Gli attributi per la stringa di connessione sono i seguenti:  
  
|Attributo|Descrizione|Valore predefinito|  
|---------------|-----------------|-------------------|  
|DSN|Nome dell'origine dati elencato nella scheda driver della finestra di dialogo **Amministrazione origine dati ODBC** .|""|  
|PWD|Password per il server Oracle a cui si vuole accedere. Questo driver supporta le limitazioni che Oracle inserisce sulle password.|""|  
|SERVER|Stringa di connessione per il server Oracle a cui si vuole accedere.|""|  
|UID|Nome utente del server Oracle. A seconda del sistema, questo attributo potrebbe non essere facoltativo, ovvero alcuni database e tabelle potrebbero richiedere questo attributo per motivi di sicurezza.<br /><br /> Usare "/" per usare l'autenticazione del sistema operativo di Oracle.|""|  
|BUFFERSIZE|Dimensione del buffer ottimale utilizzata durante il recupero delle colonne.<br /><br /> Il driver ottimizza il recupero in modo che un recupero dal server Oracle restituisca un numero di righe sufficiente per riempire un buffer di queste dimensioni. I valori più grandi tendono ad aumentare le prestazioni in caso di recupero di una grande quantità di dati.|65535|  
|SYNONYMCOLUMNS|Quando questo valore è true (1), una chiamata API sqlcolumn () restituisce informazioni sulla colonna. In caso contrario, sqlcolumn () restituisce solo le colonne per le tabelle e le viste. Il driver ODBC per Oracle consente un accesso più rapido quando questo valore non è impostato.|1|  
|REMARKS|Quando questo valore è true (1), il driver restituisce le colonne di commento per il set di risultati [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) . Il driver ODBC per Oracle consente un accesso più rapido quando questo valore non è impostato.|0|  
|StdDayOfWeek|Applica lo standard ODBC per lo scalare DAYOFWEEK. Per impostazione predefinita, questa opzione è attivata, ma gli utenti che necessitano della versione localizzata possono modificare il comportamento per usare qualsiasi valore restituito da Oracle.|1|  
|GuessTheColDef|Specifica se il driver deve restituire un valore diverso da zero per l'argomento *cbColDef* di **SQLDescribeCol**. Si applica solo alle colonne in cui non esiste alcuna scala definita da Oracle, ad esempio colonne numeriche calcolate e colonne definite come numeri senza precisione o scala. Una chiamata **SQLDescribeCol** restituisce 130 per la precisione quando Oracle non fornisce tali informazioni.|0|  
  
 Ad esempio, una stringa di connessione che si connette all'origine dati DataSource utilizzando il server MyOracleServerOracle e l'utente Oracle ID utente sarà:  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 Una stringa di connessione che si connette all'origine dati MyOtherDataSource usando l'autenticazione del sistema operativo e il server MyOtherOracleServerOracle sarà:  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
