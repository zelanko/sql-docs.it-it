---
title: Utilità Ssms | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], opening
- command prompt utilities [SQL Server], sqlwb
- sqlwb utility
- Management Studio command line
- opening SQL Server Management Studio
ms.assetid: aafda520-9e2a-4e1e-b936-1b165f1684e8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: edb7ea682ebef5d99cee7a248681be80fc433312
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63126996"
---
# <a name="ssms-utility"></a>Utilità Ssms
  L'utilità **Ssms** apre [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Se specificato, **Ssms** anche una connessione a un server e apre query, script, file, progetti e soluzioni.  
  
 È possibile specificare file che includono query, progetti o soluzioni. I file contenenti query vengono automaticamente connessi a un server se si specificano le informazioni di connessione e il tipo di file è associato al tipo corrispondente di server. Ad esempio, i file sql apriranno una finestra Editor di query SQL in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], mentre i file mdx apriranno una finestra Editor di query MDX in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. **Soluzioni e progetti di SQL Server** si aprirà in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
> [!NOTE]  
>  L'utilità **Ssms** non esegue query. Per eseguire query dalla riga di comando, usare l'utilità **sqlcmd** .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
      Ssms  
    [scriptfile] [projectfile] [solutionfile]  
    [-Sservername] [-ddatabasename] [-Uusername] [-Ppassword]   
    [-E] [-nosplash] [-log[filename]?] [-?]  
```  
  
## <a name="arguments"></a>Argomenti  
 *scriptfile*  
 Specifica uno o più file script da aprire. Il parametro deve includere il percorso completo dei file.  
  
 *projectfile*  
 Specifica un progetto script da aprire. Il parametro deve includere il percorso completo del file del progetto script.  
  
 *solutionfile*  
 Specifica una soluzione da aprire. Il parametro deve includere il percorso completo del file di soluzione.  
  
 [**-S** _nomeserver_]  
 Nome server  
  
 [**-d** _databasename_]  
 Nome database  
  
 [**-U** _username_]  
 Nome utente utilizzato per la connessione tramite l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 [**-P** _password_]  
 Password utilizzata per la connessione tramite l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 [**-E**]  
 Stabilisce la connessione utilizzando l'autenticazione di Windows  
  
 [**-nosplash**]  
 Se si specifica questa opzione, in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] non viene visualizzata la grafica della schermata iniziale all'apertura. Utilizzare questa opzione in caso di connessione al computer che esegue [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per mezzo di Servizi terminal tramite una connessione a larghezza di banda limitata. Questo argomento non supporta la distinzione tra maiuscole e minuscole e può trovarsi prima o dopo altri argomenti.  
  
 [**-log**_[filename]?_]  
 L'attività [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] viene registrata nel file specificato per la risoluzione dei problemi  
  
 [**-?**]  
 Visualizza informazioni della Guida relative alla riga di comando.  
  
## <a name="remarks"></a>Note  
 Tutte le opzioni sono facoltative e devono essere separate da uno spazio, a differenza dei file che devono essere separati da virgole. Se non viene specificata alcuna opzione, **Ssms** apre [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] in base alle impostazioni definite in **Opzioni** nel menu **Strumenti** . Ad esempio, se l'opzione **All'avvio** della pagina **Ambiente/Generale** specifica **Apri nuova finestra Query**, **Ssms** viene aperto con un editor di query vuoto.  
  
 L'opzione **-log** deve essere visualizzata alla fine della riga di comando, dopo tutte le altre opzioni. L'argomento del nome del file è facoltativo. Se il nome del file è specificato e il file non esiste, il file viene creato. Se non è possibile creare il file, ad esempio a causa dell'accesso in scrittura insufficiente, il log viene invece scritto nella posizione APPDATA non localizzata (vedere di seguito). Se l'argomento del nome del file non viene specificato, i file vengono scritti nella cartella di dati dell'applicazione non localizzata dell'utente corrente. La cartella di dati dell'applicazione non localizzata per SQL Server può essere individuata tramite la variabile di ambiente APPDATA. Ad esempio, per SQL Server 2012, la cartella è \<unità di sistema>:\Users\\<nomeutente\>\AppData\Roaming\Microsoft\AppEnv\10.0\\. Per impostazione predefinita, i due file sono denominati ActivityLog.xml e ActivityLog.xsl. Nel primo sono contenuti i dati del log attività e il secondo è un foglio di stile XML tramite cui risulta più semplice la visualizzazione del file XML. Usare i passaggi seguenti per visualizzare il file di log nel visualizzatore XML predefinito, ad esempio Internet Explorer:  fare clic su Start, scegliere Esegui..., quindi digitare "\<unità di sistema>:\Users\\<nomeutente\>\AppData\Roaming\Microsoft\AppEnv\10.0\ActivityLog.xml" nel campo visualizzato e quindi premere Invio.  
  
 Verrà richiesto di connettere i file contenenti query a un server se si specificano le informazioni di connessione e il tipo di file è associato al tipo corrispondente di server. Ad esempio, i file sql apriranno una finestra Editor di query SQL in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], mentre i file mdx apriranno una finestra Editor di query MDX in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. **Soluzioni e progetti di SQL Server** si aprirà in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 Nella tabella seguente viene eseguito il mapping dei tipi di server alle estensioni di file.  
  
|Tipo server|Estensione|  
|-----------------|---------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|.sql|  
|SQL Server Analysis Services|mdx<br /><br /> xmla|  
  
## <a name="examples"></a>Esempi  
 Lo script seguente apre [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] da un prompt dei comandi in base alle impostazioni predefinite.  
  
```  
Ssms  
  
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
 [Utilizzo di SQL Server Management Studio](../database-engine/use-sql-server-management-studio.md)  
  
  
