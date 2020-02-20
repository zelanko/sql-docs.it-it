---
title: Utilità SSMS
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], opening
- command prompt utilities [SQL Server], sqlwb
- sqlwb utility
- Management Studio command line
- opening SQL Server Management Studio
ms.assetid: aafda520-9e2a-4e1e-b936-1b165f1684e8
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 08/07/2019
ms.openlocfilehash: 5a31fb94fad2e063fe9846bd820957abb4ce9b32
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75243902"
---
# <a name="ssms-utility"></a>Utilità SSMS

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

L'utilità **Ssms** consente di aprire [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Se specificato, **Ssms** anche una connessione a un server e apre query, script, file, progetti e soluzioni.

È possibile specificare file che includono query, progetti o soluzioni. I file contenenti query vengono automaticamente connessi a un server se si specificano le informazioni di connessione e il tipo di file è associato al tipo corrispondente di server. Ad esempio, i file SQL aprono una finestra dell'Editor di query SQL in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], mentre i file MDX aprono una finestra dell'Editor di query MDX in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. L'apertura di **Soluzioni e progetti di SQL Server** avviene in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. 

> [!NOTE]
> L'utilità **Ssms** non esegue query. Per eseguire query dalla riga di comando, usare l'utilità **sqlcmd** . 
 
## <a name="syntax"></a>Sintassi
 
 ```
 Ssms 
 [scriptfile] [projectfile] [solutionfile] 
 [-S servername] [-d databasename] [-G] [-U username] [-E] [-nosplash] [-log [filename]?] [-?] 
 ``` 
 
## <a name="arguments"></a>Argomenti

 *scriptfile* Specifica uno o più file di script da aprire. Il parametro deve includere il percorso completo dei file. 
 
 *projectfile* Specifica un progetto di script da aprire. Il parametro deve includere il percorso completo del file del progetto script. 
 
 *solutionfile* Specifica una soluzione da aprire. Il parametro deve includere il percorso completo del file di soluzione. 
 
[ **-S** _servername_] Nome del server
 
[ **-d** _databasename_] Nome del database

[ **-G**] Connessione con l'autenticazione di Azure Active Directory. Il tipo di connessione dipende dalla presenza di **-U**.

> [!Note]
> L'opzione **Active Directory - Universale con supporto MFA** non è attualmente supportata.
 
[ **-U** _username_] Nome utente per la connessione con l'autenticazione SQL
 
[ **-E**] Viene stabilita la connessione con l'autenticazione di Windows
 
[ **-nosplash**] Impedisce a [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] di visualizzare la grafica della schermata iniziale durante l'apertura. Utilizzare questa opzione in caso di connessione al computer che esegue [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per mezzo di Servizi terminal tramite una connessione a larghezza di banda limitata. Questo argomento non supporta la distinzione tra maiuscole e minuscole e può trovarsi prima o dopo altri argomenti.
 
[ **-log** _[filename]?_ ] Registra l'attività di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] nel file specificato per la risoluzione dei problemi
 
[ **-?** ] Visualizza la guida relativa alla riga di comando

## <a name="remarks"></a>Osservazioni

Tutte le opzioni sono facoltative e separate da uno spazio, ad eccezione dei file che devono essere separati da virgole. Se non viene specificata alcuna opzione, **Ssms** apre [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] in base alle impostazioni definite in **Opzioni** nel menu **Strumenti** . Se ad esempio l'opzione **All'avvio** della pagina **Ambiente/Generale** specifica **Apri nuova finestra Query**, **Ssms** si apre con un editor di query vuoto.
 
L'opzione **-log** deve trovarsi alla fine della riga di comando, dopo tutte le altre opzioni. L'argomento del nome del file è facoltativo. Se il nome del file è specificato e il file non esiste, il file viene creato. Se non è possibile creare il file, ad esempio a causa dell'accesso in scrittura insufficiente, il log viene invece scritto nella posizione APPDATA non localizzata (vedere di seguito). Se l'argomento del nome del file non viene specificato, i file vengono scritti nella cartella di dati dell'applicazione non localizzata dell'utente corrente. La cartella di dati dell'applicazione non localizzata per SQL Server può essere individuata tramite la variabile di ambiente APPDATA. Ad esempio, per SQL Server 2012, la cartella è \<unità di sistema>:\Users\\<nomeutente\>\AppData\Roaming\Microsoft\AppEnv\10.0\\. Per impostazione predefinita, i due file sono denominati ActivityLog.xml e ActivityLog.xsl. Il primo contiene i dati del log attività, mentre il secondo è un foglio di stile XML che fornisce un modo più comodo per visualizzare il file XML. Usare i passaggi seguenti per visualizzare il file di log nel visualizzatore XML predefinito, ad esempio Internet Explorer: fare clic su Start, scegliere Esegui..., quindi digitare "\<unità di sistema>:\Users\\<nomeutente\>\AppData\Roaming\Microsoft\AppEnv\10.0\ActivityLog.xml" nel campo visualizzato e quindi premere Invio.
 
I file che contengono query richiedono la connessione a un server se si specificano le informazioni di connessione e il tipo di file è associato al tipo corrispondente di server. Ad esempio, i file SQL aprono una finestra dell'Editor di query SQL in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], mentre i file MDX aprono una finestra dell'Editor di query MDX in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. L'apertura di **Soluzioni e progetti di SQL Server** avviene in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].

Nella tabella seguente viene eseguito il mapping dei tipi di server alle estensioni di file.
 
|Tipo di server|Estensione| 
|-----------------|---------------| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|sql|
|SQL Server Analysis Services|mdx<br /><br /> xmla|

## <a name="examples"></a>Esempi

Lo script seguente apre [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] da un prompt dei comandi in base alle impostazioni predefinite.
 
 ```
 Ssms
 ```

Il codice seguente apre [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] da un prompt dei comandi usando *Active Directory - Integrata*:
 
 ```
 Ssms.exe -S servername.database.windows.net -G
 ```

Lo script seguente apre [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] da un prompt dei comandi utilizzando l'autenticazione di Windows, con l'editor del codice impostato sul server `ACCTG and the database AdventureWorks2012,` senza visualizzare la schermata iniziale.
 
 ```
 Ssms -E -S ACCTG -d AdventureWorks2012 -nosplash
 ```

 Lo script seguente apre [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] da un prompt dei comandi e quindi apre lo script MonthEndQuery.
 
 ```
 Ssms "C:\Documents and Settings\username\My Documents\SQL Server Management Studio Projects\FinanceScripts\FinanceScripts\MonthEndQuery.sql"
 ```
 
 Lo script seguente apre [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] da un prompt dei comandi e quindi apre il progetto NewReportsProject nel computer denominato `developer`.
 
 ```
 Ssms "\\developer\fin\ReportProj\ReportProj\NewReportProj.ssmssqlproj"
 ```
 
 Lo script seguente apre [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] da un prompt dei comandi e quindi apre la soluzione MonthlyReports. 

 ```
Ssms "C:\solutionsfolder\ReportProj\MonthlyReports.ssmssln"
 ```

## <a name="see-also"></a>Vedere anche

[Utilizzo di SQL Server Management Studio](https://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)