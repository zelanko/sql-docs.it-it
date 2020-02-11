---
title: Utilità Profiler | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server], profiler90 utility
- profiler90 utility
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
ms.assetid: e91c30a9-0d29-4f84-bcb8-e8fb62afadda
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 572644cf673c70000cee7de77f2bca9199f19675
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211091"
---
# <a name="profiler-utility"></a>Utilità profiler
  L'utilità **Profiler** avvia lo [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] strumento. Gli argomenti facoltativi elencati di seguito in questo argomento consentono di controllare la modalità di avvio dell'applicazione.  
  
> [!NOTE]  
>  L'utilità **profiler** non viene usata per lo scripting delle tracce. Per altre informazioni, vedere [SQL Server Profiler](sql-server-profiler/sql-server-profiler.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
      profiler  
          [ /? ] |  
[  
{  
{ /U login_id [ /P password ] }  
| /E  
}  
{[ /S sql_server_name ] | [ /A analysis_services_server_name ] }  
[ /D database ]  
[ /T "template_name" ]  
[ /B { "trace_table_name" } ]  
{ [/F "filename" ] | [ /O "filename" ] }  
[ /L locale_ID ]  
[ /M "MM-DD-YY hh:mm:ss" ]  
[ /R ]  
[ /Z file_size ]  
]  
```  
  
## <a name="arguments"></a>Argomenti  
 **/?**  
 Visualizza il riepilogo della sintassi degli argomenti di **profiler** .  
  
 **/U** *login_ID*  
 ID di accesso utente per l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Per gli ID di accesso la distinzione tra maiuscole e minuscole è rilevante.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)].  
  
 **/P** *password*  
 Specifica una password definita dall'utente per l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **/E**  
 Specifica la connessione tramite l'autenticazione di Windows e le credenziali dell'utente corrente.  
  
 **/S**  *SQL_server_name*  
 Specifica un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Profiler viene automaticamente connesso al server specificato usando le informazioni di autenticazione definite nelle opzioni **/U** e **/P** o **/E** . Usare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]/S**sql_server_name** **\\instance_name* per connettersi a un'istanza denominata di *.  
  
 **/A**  *analysis_services_server_name*  
 Consente di specificare un'istanza di Analysis Services. Profiler viene automaticamente connesso al server specificato usando le informazioni di autenticazione definite nelle opzioni **/U** e **/P** o **/E** . Usare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]/A**analysis_services_server_name\instance_name** * per connettersi a un'istanza denominata di *.  
  
 **/D** *database*  
 Specifica il nome del database da utilizzare con la connessione. Se non si specifica alcun database, questa opzione selezionerà il database predefinito per l'utente specificato.  
  
 **/B "** *trace_table_name* **"**  
 Specifica una tabella di traccia da caricare all'avvio di SQL Profiler. Assieme alla tabella è necessario specificare il database, l'utente oppure lo schema.  
  
 **/T "** *template_name* **"**  
 Specifica il modello che verrà caricato per configurare la traccia. È necessario racchiudere il nome del modello tra virgolette. Il nome del modello deve trovarsi nella directory dei modelli di sistema oppure in quella dei modelli utente. Se in entrambe le directory esistono due modelli con lo stesso nome, verrà caricato il modello incluso nella directory di sistema. Se non esiste alcun modello con il nome specificato, verrà caricato il modello standard. Si noti che l'estensione di file tdf del modello non dovrà essere specificata come parte del *template_name*. Ad esempio:  
  
```  
/T "standard"  
```  
  
 **/F "** *nomefile* **"**  
 Specifica il percorso e il nome file di un file di traccia da caricare all'avvio di SQL Profiler. È necessario racchiudere l'intero percorso e il nome file tra virgolette. Questa opzione non può essere usata in combinazione con **/O**.  
  
 **/O "** *nomefile*  **"**  
 Specifica il percorso e il nome file di un file nel quale verranno scritti i risultati della traccia. È necessario racchiudere l'intero percorso e il nome file tra virgolette. Questa opzione non può essere usata in combinazione con **/F**.  
  
 **/L** *locale_ID*  
 Non disponibile.  
  
 **/M "** *mm-dd-yy hh: mm: SS* **"**  
 Specifica la data e l'ora in cui verrà arrestata la traccia. È necessario racchiudere l'ora di arresto tra virgolette. Specificare l'ora di arresto in base ai parametri descritti nella tabella seguente.  
  
|Parametro|Definizione|  
|---------------|----------------|  
|MM|Mese nel formato a 2 cifre|  
|GG|Giorno nel formato a 2 cifre|  
|YY|Anno nel formato a 2 cifre|  
|hh|Ora a 2 cifre nel formato a 24 ore|  
|MM|Minuti nel formato a 2 cifre|  
|ss|Secondi nel formato a 2 cifre|  
  
> [!NOTE]  
>  Il formato "MM-DD-YY hh:mm:ss" può essere utilizzato solo se l'opzione **Visualizza valori di data e ora in base alle impostazioni internazionali** è abilitata in [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]. Se questa opzione non è abilitata, è necessario utilizzare il formato di data e ora "YYYY-MM-DD hh:mm:ss".  
  
 **/R**  
 Abilita il rollover del file di traccia.  
  
 *****File_size* /Z    
 Specifica le dimensioni del file di traccia espresse in megabyte (MB). Le dimensioni predefinite sono pari a 5 MB. Se si abilita il rollover, a tutti i file di rollover verrà applicato il valore limite specificato in questo argomento.  
  
## <a name="remarks"></a>Osservazioni  
 Per avviare la traccia con un modello specifico, usare contemporaneamente le opzioni **/S** e **/T** . Per avviare una traccia utilizzando il modello Standard in MyServer\MyInstance, ad esempio, al prompt dei comandi digitare quanto segue:  
  
```  
profiler /S MyServer\MyInstance /T "Standard"  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'utilità del prompt dei comandi &#40;motore di database&#41;](command-prompt-utility-reference-database-engine.md)  
  
  
