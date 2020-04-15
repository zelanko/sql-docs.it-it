---
title: Formato e attributi della stringa di connessione Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281151"
---
# <a name="connection-string-format-and-attributes"></a>Formato e attributi della stringa di connessione
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Anziché utilizzare una finestra di dialogo, alcune applicazioni potrebbero richiedere una stringa di connessione che specifica le informazioni di connessione all'origine dati. La stringa di connessione è costituita da un numero di attributi che specificano la modalità di connessione di un driver a un'origine dati. Un attributo identifica un'informazione specifica che il driver deve conoscere prima di poter effettuare la connessione all'origine dati appropriata. Ogni driver potrebbe avere un set di attributi diverso, ma il formato della stringa di connessione è sempre lo stesso. Una stringa di connessione ha il formato seguente:A connection string has the following format:  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Il driver Microsoft ODBC per Oracle supporta il formato della stringa `CONNECTSTRING`di connessione `SERVER=`della prima versione del driver, che ha utilizzato , anziché .  
  
 Se ci si connette a un provider di origini `Trusted_Connection=yes` dati che supporta l'autenticazione di Windows, è necessario specificare al posto delle informazioni relative all'ID utente e alla password nella stringa di connessione.  
  
 È necessario specificare il nome dell'origine dati se non si specificano gli attributi UID, PWD, SERVER (o CONNECTSTRING) e DRIVER. Tuttavia, tutti gli altri attributi sono facoltativi. Se non si specifica un attributo, per impostazione predefinita tale attributo sarà quello specificato nella scheda DSN pertinente della finestra di dialogo **Amministratore origine dati ODBC.** Il valore dell'attributo potrebbe fare distinzione tra maiuscole e minuscole.  
  
 Gli attributi per la stringa di connessione sono i seguenti:The attributes for the connection string are as follows:  
  
|Attributo|Descrizione|Valore predefinito|  
|---------------|-----------------|-------------------|  
|DSN|Nome dell'origine dati elencato nella scheda Driver della finestra di dialogo **Amministratore origine dati ODBC.**|""|  
|PWD|Password per il server Oracle a cui si desidera accedere. Questo driver supporta le limitazioni che Oracle impone alle password.|""|  
|SERVER|Stringa di connessione per il server Oracle a cui si desidera accedere.|""|  
|UID|Nome utente di Oracle Server. A seconda del sistema, questo attributo potrebbe non essere facoltativo, ovvero alcuni database e tabelle potrebbero richiedere questo attributo per motivi di sicurezza.<br /><br /> Utilizzare "/" per utilizzare l'autenticazione del sistema operativo Oracle.|""|  
|Buffersize|Dimensione ottimale del buffer utilizzata durante il recupero delle colonne.<br /><br /> Il driver ottimizza il recupero in modo che un recupero da Oracle Server restituisce un numero sufficiente di righe per riempire un buffer di queste dimensioni. Valori più grandi tendono ad aumentare le prestazioni se si recuperano molti dati.|65535|  
|COLONNE SYNONYM|Quando questo valore è true (1), una chiamata API SQLColumn( ) restituisce informazioni sulla colonna. In caso contrario, SQLColumn( ) restituisce solo le colonne per tabelle e viste. Il driver ODBC per Oracle fornisce un accesso più rapido quando questo valore non è impostato.|1|  
|REMARKS|Quando questo valore è true (1), il driver restituisce le colonne Remarks per il set di risultati [SQLColumns.](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) Il driver ODBC per Oracle fornisce un accesso più rapido quando questo valore non è impostato.|0|  
|StdDayOfWeek|Applica lo standard ODBC per lo scalare DAYOFWEEK. Per impostazione predefinita, questa opzione è attivata, ma gli utenti che necessitano della versione localizzata possono modificare il comportamento in modo da utilizzare qualsiasi operazione restituita da Oracle.By default this is turned on, but users who need the localized version can change the behavior to use whatever Oracle returns.|1|  
|GuessTheColDef|Specifica se il driver deve restituire un valore diverso da zero per l'argomento *cbColDef* di **SQLDescribeCol**. Si applica solo alle colonne in cui non è presente una scala definita da Oracle, ad esempio le colonne numeriche calcolate e le colonne definite come NUMBER senza precisione o scala. Una chiamata **SQLDescribeCol** restituisce 130 per la precisione quando Oracle non fornisce tali informazioni.|0|  
  
 Ad esempio, una stringa di connessione che si connette all'origine dati MyDataSource utilizzando il server MyOracleServerOracle e l'utente Oracle MyUserID sarebbe:For example, a connection string that connects to the MyDataSource data source using the MyOracleServerOracle Server and the Oracle User MyUserID would be:  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 Una stringa di connessione che si connette all'origine dati MyOtherDataSource utilizzando l'autenticazione del sistema operativo e il server MyOtherOracleServerOracle sarebbe:  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
