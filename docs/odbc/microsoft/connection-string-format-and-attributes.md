---
title: Formato stringa di connessione e gli attributi | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a007f4c7c92bf4254e4d36638cf2d92ba0764be5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082018"
---
# <a name="connection-string-format-and-attributes"></a>Formato e attributi della stringa di connessione
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Invece di usare una finestra di dialogo, alcune applicazioni potrebbero richiedere una stringa di connessione che specifica le informazioni di connessione origine dati. La stringa di connessione è costituita da un numero di attributi che specificano il modo in cui un driver si connette a un'origine dati. Un attributo identifica un'informazione specifica che il driver deve sapere per poter effettuare la connessione all'origine dati appropriata. Ogni driver potrebbe essere un diverso set di attributi, ma il formato di stringa di connessione è sempre lo stesso. Una stringa di connessione ha il formato seguente:  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Il Driver ODBC di Microsoft per Oracle supporta il formato di stringa di connessione della prima versione del driver, che usati `CONNECTSTRING`= anziché `SERVER=`.  
  
 Se ci si connette a un provider dell'origine dati che supporta l'autenticazione di Windows, è necessario specificare `Trusted_Connection=yes` anziché le informazioni utente di ID e la password nella stringa di connessione.  
  
 È necessario specificare l'origine dati se non si specifica l'UID, PWD, SERVER o CONNECTSTRING, assegnare un nome e gli attributi DRIVER. Tuttavia, tutti gli altri attributi sono facoltativi. Se non si specifica un attributo, tale attributo predefinito a quello specificato nella relativa scheda DSN del **Amministrazione origine dati ODBC** nella finestra di dialogo. Il valore dell'attributo potrebbe essere distinzione maiuscole/minuscole.  
  
 Gli attributi per la stringa di connessione sono i seguenti:  
  
|attribute|Descrizione|Valore predefinito|  
|---------------|-----------------|-------------------|  
|DSN|Nome dell'origine dati elencati nella scheda driver del **Amministrazione origine dati ODBC** nella finestra di dialogo.|""|  
|PWD|La password per il Server Oracle che si desidera accedere. Il driver supporta le limitazioni che Oracle posiziona su password.|""|  
|SERVER|La stringa di connessione per il Server Oracle che si desidera accedere.|""|  
|UID|Nome utente del Server Oracle. A seconda del sistema, questo attributo non sia facoltativo, vale a dire, alcune tabelle e database potrebbero richiedere questo attributo per motivi di sicurezza.<br /><br /> Usare "/" per l'uso di Oracle operativo dell'autenticazione del sistema.|""|  
|BUFFERSIZE|Le dimensioni del buffer ottimale utilizzata durante il recupero di colonne.<br /><br /> Il driver consente di ottimizzare il recupero in modo che un'operazione di recupero da Server Oracle restituisce un numero di righe sufficiente per riempire un buffer di queste dimensioni. I valori maggiori tendono ad aumentare le prestazioni se si recupera una grande quantità di dati.|65535|  
|SYNONYMCOLUMNS|Quando questo valore è true (1), una chiamata di API () SQLColumn restituisce informazioni sulle colonne. In caso contrario, SQLColumn () restituisce solo le colonne per le tabelle e viste. Il Driver ODBC per Oracle fornisce un accesso più veloce quando questo valore non è impostato.|1|  
|REMARKS|Quando questo valore è true (1), il driver restituisce le colonne di osservazioni per il [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) set di risultati. Il Driver ODBC per Oracle fornisce un accesso più veloce quando questo valore non è impostato.|0|  
|StdDayOfWeek|Applica lo standard ODBC per la funzione scalare DAYOFWEEK. Per impostazione predefinita questo è attivato, ma gli utenti che necessitano della versione localizzata possono modificare il comportamento per usare qualsiasi restituisce Oracle.|1|  
|GuessTheColDef|Specifica se il driver deve restituire un valore diverso da zero per il *cbColDef* argomenti del **SQLDescribeCol**. Si applica solo alle colonne in cui non sono presente alcuna scalabilità definito Oracle, ad esempio calcolata numeriche colonne e le colonne definite come numero senza una precisione o scala. Oggetto **SQLDescribeCol** chiamata restituisce 130 per la precisione quando Oracle non fornisce tali informazioni.|0|  
  
 Ad esempio, potrebbe essere una stringa di connessione che si connette all'origine dati MyDataSource usando il MyOracleServerOracle Server e MyUserID l'utente Oracle:  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 Una stringa di connessione che si connette all'origine dati MyOtherDataSource tramite l'autenticazione del sistema operativo e il MyOtherOracleServerOracle Server sarebbe:  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
