---
title: Parti del report (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10543"
ms.assetid: 957f664c-8a7a-4532-b5a6-5f859c5840bd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5b07fb1c133bbed21fd74936a38b97fa1778e5ad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104545"
---
# <a name="report-parts-report-builder-and-ssrs"></a>Parti del report (Generatore report e SSRS)
  È possibile pubblicare come *parti di report*elementi quali tabelle, matrici, grafici e immagini. Le parti di report sono elementi pubblicati separatamente in un server di report e che possono essere riutilizzati in altri report. Le parti di report hanno un'estensione di file rsc.  
  
 Le parti di report consentono ai gruppi di lavoro di sfruttare i diversi ruoli e competenze dei membri del team. Ad esempio, se si è responsabili della creazione di grafici, è possibile salvarli come parti separate che possono essere riutilizzate da altri utenti in altri report. Le parti di report possono essere pubblicate su un server di report o su un sito di SharePoint integrato con un server di report; inoltre, possono essere riutilizzate in più report ed essere aggiornate nel server.  
  
 La parte di report aggiunta al report in uso consente di gestire una relazione con l'istanza della parte di report sul sito o sul server tramite un ID univoco. Dopo aver aggiunto delle parti a un report da un sito o un server, è possibile modificarle indipendentemente dalla parte di report originale sul sito o sul server. È possibile accettare aggiornamenti che altri utenti hanno apportato alla parte di report sul sito o sul server e salvare di nuovo la parte di report modificata nel sito o nel server, aggiungendone una nuova o scrivendo sull'originale, se si dispone delle autorizzazioni sufficienti.  
  
 Per iniziare rapidamente con parti di report, vedere i video [3 di parti di Report in SQL Server 2008 R2 Report Builder](https://technet.microsoft.com/edge/Video/ff711300) e [procedura: Creazione di parti di Report riutilizzabili con Generatore Report SQL Server](https://technet.microsoft.com/sqlserver/ff634166.aspx).  
  
##  <a name="ComponentWorkflow"></a> Ciclo di vita di una parte di report  
 ![rs_ComponentCreation](media/rs-componentcreation.gif "rs_ComponentCreation")  
  
1.  Un utente A crea un report con un grafico che dipende da un set di dati incorporato.  
  
2.  L'utente A sceglie di pubblicare il grafico nel server di report. Mediante Generatore report viene assegnato un ID univoco al grafico pubblicato. L'utente A non sceglie di condividere il set di dati che rimane pertanto incorporato nel grafico.  
  
3.  Un utente B crea un report vuoto, esegue le ricerche nella raccolta relativa alle parti di report, trova il grafico e lo aggiunge al report. A questo punto il grafico è parte del report dell'utente B, insieme al set di dati incorporato. L'utente B può modificare le istanze del grafico e del set di dati contenuti nel report. Questa operazione non avrà effetto sulle istanze del grafico e del set di dati sul server di report, né interromperà la relazione tra le istanze nel report e sul server di report.  
  
     ![rs_componentupdate](media/rs-componentupdate.gif "rs_componentupdate")  
  
4.  Un utente C aggiunge il grafico a un report modificando tale grafico nel report da grafico a barre a grafico a torta.  
  
5.  L'utente C dispone delle autorizzazioni per sovrascrivere il grafico nel server ed esegue tale operazione, ripubblicandolo nel server. In questo modo la copia pubblicata del grafico nel server viene aggiornata. L'utente C non sceglie di condividere neanche il set di dati che rimane pertanto incorporato nel grafico.  
  
6.  L'utente B accetta il grafico aggiornato dal server sovrascrivendo così le modifiche che l'utente B ha apportato al grafico nel report dell'utente B.  

##  <a name="PublishingComponents"></a> Pubblicazione di parti di report  
 Quando si pubblica una parte di report, Generatore report consente di assegnarle un ID univoco, che è diverso dal nome della parte di report, e di gestirlo, a prescindere dalle modifiche che si stanno apportando alla parte di report. L'ID consente di collegare l'elemento del report originale nel report alla parte di report. Quando altri autori del report riutilizzano la parte di report, tramite l'ID è anche possibile collegare la parte di report nel report in uso alla parte di report sul server di report.  
  
 È possibile pubblicare come parti di report gli elementi di report riportati di seguito.  
  
-   Grafici  
  
-   Misuratori  
  
-   Immagini  
  
-   Mappe  
  
-   Parametri  
  
-   Rettangoli  
  
-   Tabelle  
  
-   Matrici  
  
-   Elenchi  
  
 Quando si pubblica e si salva un elemento del report che consente di visualizzare dati, ad esempio una tabella, una matrice o un grafico, viene salvato anche, come set di dati incorporato, il set di dati dal quale dipende. Inoltre, è possibile salvare il set di dati separatamente come set di dati condiviso che può essere utilizzato da altri utenti come base per altre parti di report. Per altre informazioni, vedere [Parti del report e set di dati in Generatore report](report-data/report-parts-and-datasets-in-report-builder.md).  
  
 Alcune parti del report possono contenere altri elementi del report. Ad esempio, una tabella può contenere un grafico e un rettangolo può contenere una matrice e un grafico. Quando si pubblica un elemento del report che contiene altri elementi del report, questi ultimi vengono salvati come un'unità. Gli altri elementi del report vengono salvati incorporati nella parte di report contenitore. Non è possibile aggiornarli separatamente e non è possibile salvare gli elementi nel contenitore come parti di report separate.  
  
 Per altre informazioni sulla pubblicazione delle parti di report, vedere [Pubblicare e ripubblicare parti del report &#40;Generatore report e SSRS&#41;](report-parts-report-builder-and-ssrs.md)elementi quali tabelle, matrici, grafici e immagini.  
  
### <a name="modifying-report-part-metadata"></a>Modifica dei metadati della parte di report  
 È possibile pubblicare parti di report con le impostazioni predefinite in un percorso predefinito o salvare ogni parte di report in un percorso diverso e modificare i metadati, ad esempio il titolo e la descrizione.  
  
 È opportuno attribuire alla parte di report un nome e una descrizione che siano chiari quando la si pubblica in modo da facilitarne l'identificazione da parte degli utenti durante la ricerca. Potrebbero essere disponibili molte parti di report con nomi simili sul sito o sul server. Provare a utilizzare convenzioni di denominazione per illustrare le relazioni tra le parti di report e gli elementi dipendenti.  
  
 Inoltre, provare a salvare le origini dati condivise, i set di dati condivisi e le parti di report da cui dipendono nella stessa cartella.  
  
 È possibile modificare anche la descrizione nel riquadro Proprietà.  

##  <a name="ReusingComponents"></a> Riutilizzo di parti di report  
 Il modo più semplice per creare un report consiste nell'aggiungere una parte di report esistente, ad esempio una tabella o un grafico, al report in uso dalla raccolta relativa alle parti di report. Dopo avere aggiunto la parte di report, è possibile modificarla in base alle necessità o accettare gli aggiornamenti provenienti dal server. La modifica dell'elemento del report nel report non influirà sull'istanza della parte di report pubblicata nel sito o nel server, né interromperà la relazione tra l'istanza nel report e sul sito o server. Se si dispone di autorizzazioni sufficienti, è possibile salvare di nuovo la copia aggiornata nel sito o nel server. Se un altro utente modifica la copia nel sito o nel server, è possibile decidere di tenere la copia invariata o di aggiornarla in modo che sia identica alla copia che si trova nel sito o nel server.  
  
### <a name="searching-for-report-parts"></a>Ricerca di parti di report  
 È possibile cercare le parti di report da aggiungere al report nella relativa raccolta. È possibile filtrare le parti di report in base al nome completo o parziale della parte, all'autore della parte, all'utente che ha apportato l'ultima modifica, alla data dell'ultima modifica, alla posizione in cui è archiviata o in base al tipo di parte di report. Ad esempio, è possibile cercare tutti i grafici creati nell'ultima settimana da parte di uno dei colleghi.  
  
 È possibile visualizzare i risultati della ricerca come anteprime o come elenco e ordinare i risultati della ricerca in base al nome, alle date di creazione e di modifica e all'autore. Per altre informazioni, vedere [Ricerca di parti del report e impostazione di una cartella predefinita &#40;Generatore report e SSRS&#41;](report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)elementi quali tabelle, matrici, grafici e immagini.  
  
### <a name="what-comes-with-a-report-part"></a>Elementi forniti con una parte di report  
 Quando una parte di report viene aggiunta al report in uso, vengono aggiunti anche tutti gli elementi necessari affinché funzioni. Ad esempio, un qualsiasi oggetto che consente la visualizzazione dei dati dipende da un set di dati, ovvero una query e una connessione a un'origine dati. È possibile che disponga anche di più parametri. Tutti gli elementi dai quali dipende sono le relative *dipendenze*e tutti questi elementi o i relativi puntatori sono inclusi nella parte di report quando quest'ultima viene aggiunta al report in uso. I set di dati e i parametri sono elencati nel riquadro dei dati del report del report.  
  
 Il set di dati per la parte di report può essere incorporato nella parte di report o è possibile che sia un set di dati separato, condiviso a cui punta la parte di report. Se è incorporato nella parte di report, è possibile modificarlo. Se è un set di dati condiviso, è un oggetto separato per il quale sono necessarie autorizzazioni. Per altre informazioni sulle condivisi e incorporati, vedere [aggiungere dati a un Report &#40;Generatore Report e SSRS&#41;](report-data/report-datasets-ssrs.md).  
  
### <a name="resolving-naming-conflicts"></a>Risoluzione dei conflitti dei nomi  
 Quando si aggiunge una parte di report, è possibile risolvere qualsiasi conflitto di nome mediante Generatore report. Ad esempio, se si dispone già di un elemento Chart1 nel report e si aggiunge una parte di report denominata Chart1, mediante Generatore report la nuova parte di report viene rinominata automaticamente Chart2. Se si dispone già di un elemento Dataset1 nel report e si aggiunge una parte di report che fa riferimento a un set di dati diverso denominato anch'esso Dataset1, Generatore report consente di rinominare il nuovo set di dati Dataset2 e di aggiornare i riferimenti.  
  
### <a name="adding-more-than-one-report-part"></a>Aggiunta di più parti di report  
 Nel report è possibile aggiungere un numero illimitato di parti di report. Tuttavia, è possibile aggiungere una sola parte di report alla volta. È possibile anche aggiungere più istanze di una parte di report allo stesso report. Tutte le istanze avranno nomi univoci, ma saranno tutte istanze della stessa parte di report sul server e avranno lo stesso ID univoco.  
  
 Quando si aggiunge un'altra parte di report che utilizza un set di dati identico a un altro già presente nel report, la procedura guidata non consente di aggiungere un'altra versione di quel set di dati al report reindirizzando i riferimenti nella parte di report al set di dati esistente. Per altre informazioni, vedere [Parti del report e set di dati in Generatore report](report-data/report-parts-and-datasets-in-report-builder.md).  

##  <a name="UpdatingComponents"></a> Aggiornamento di parti di report con modifiche dal server  
 Ogni volta che si apre un report in Generatore report, viene eseguita la verifica dello stato di aggiornamento delle istanze del server delle parti di report in quel report. Consente di verificare inoltre le modifiche negli elementi dipendenti delle parti di report, ad esempio nel set di dati e nei parametri. Se eventuali parti di report pubblicate o le relative dipendenze sono state aggiornate sul server, in una barra informazioni del report in uso viene visualizzato il numero di quelle interessate dall'aggiornamento. È possibile scegliere di visualizzare e accettare, o rifiutare, gli aggiornamenti oppure di ignorare la barra informazioni. Se si sceglie di visualizzare gli aggiornamenti, viene visualizzata un'anteprima della parte di report con la data e il nome dell'autore dell'ultima modifica. È quindi possibile accettare alcuni o tutti gli elementi aggiornati.  
  
> [!NOTE]  
>  La barra può essere disabilitata ed è quindi possibile non venire informati di eventuali modifiche a una parte del report. Questa opzione può essere impostata quando si aggiunge la parte di report al report. Anche se la barra informazioni è stata disabilitata, è ancora possibile verificare gli aggiornamenti. Per altre informazioni, vedere [verificare la presenza di aggiornamenti o disattivare gli aggiornamenti &#40;Generatore Report e SSRS&#41;](../../2014/reporting-services/check-for-updates-or-turn-updates-off-report-builder-and-ssrs.md).  
  
 Generatore report consente di verificare le differenze tra la data dell'ultimo aggiornamento apportato alla parte di report nel server e la data dell'ultima sincronizzazione della parte di report con il server. Non consente di controllare la data di modifica della parte di report nel report. Pertanto, la parte di report nel report in uso e la parte di report sul server potrebbero essere completamente diverse, tuttavia quando si esegue la verifica degli aggiornamenti mediante Generatore report, non ne verrà rilevato alcuno.  
  
### <a name="accepting-updates"></a>Accettazione degli aggiornamenti  
 Quando si accetta un aggiornamento per una parte di report, questa viene completamente sostituita con la copia della parte di report già presente nel report. Non è possibile combinare caratteristiche della parte di report nel report con quelle della parte di report pubblicata sul server. Tuttavia, se è stata modificata una delle dipendenze della parte di report, ad esempio un set di dati incorporato, Generatore report non consente di copiare sulla dipendenza già presente nel report. Viene scaricata una nuova copia della dipendenza e viene aggiornata la parte di report per puntare alla nuova copia.  
  
### <a name="reverting-to-a-previous-version-of-a-report-part"></a>Ripristino di una versione precedente di una parte di report  
 Se è stata modificata una versione di una parte di report nel report e si decide di sostituirla con la versione che è nel server, non è possibile utilizzare la finestra di dialogo **Aggiorna** . L'aggiornamento è solo per parti di report che sono state modificate nel server quando scaricate.  
  
 Per ripristinare la versione sul server, è sufficiente eliminare la versione che si ha nel report per poi aggiungerla nuovamente.  

##  <a name="RepublishingComponents"></a> Aggiornamento di parti di report già sul server  
 È possibile scegliere di aggiornare una parte di report esistente nel server o pubblicarla come nuova parte di report senza sostituire quella esistente. Quando si aggiorna la parte di report nel server, le copie della parte di report negli altri report non vengono modificate automaticamente. Se altri autori del report hanno aggiunto quella parte di report a un report, vengono informati della modifica alla successiva apertura di quel report e possono accettare o meno le modifiche.  
  
 Se si sceglie di pubblicarla come nuova parte di report, a quest'ultima sarà assegnato un nuovo ID univoco e verrà eliminato il collegamento alla parte di report originale.  
  
 Se il set di dati è incorporato nella parte di report, ogni volta che si pubblica la parte di report, il set di dati sarà visualizzato nella finestra di dialogo **Pubblica parti di report** . I set di dati condivisi non sono visualizzati nella finestra di dialogo **Pubblica parti di report** .  

##  <a name="RptPartsRptDesigner"></a> Utilizzo di parti di report in Progettazione report  
 Le parti di report funzionano in modo diverso in Progettazione report in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. In Progettazione report la pubblicazione è unidirezionale: è possibile pubblicare una parte di report, ma non è possibile riutilizzare una parte di report esistente. Per altre informazioni, vedere [Parti del report in Progettazione report &#40;SSRS&#41;](report-design/report-parts-in-report-designer-ssrs.md).  
  
##  <a name="HowTo"></a> Procedure  
 [Pubblicare e ripubblicare parti del report &#40;Generatore report e SSRS&#41;](report-parts-report-builder-and-ssrs.md)  
  
 [Ricerca di parti del report e impostazione di una cartella predefinita &#40;Generatore report e SSRS&#41;](report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)  
  
 [Verificare o gli aggiornamenti Turn Off &#40;Report e SSRS&#41;](../../2014/reporting-services/check-for-updates-or-turn-updates-off-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Parti del report e set di dati in Generatore report](report-data/report-parts-and-datasets-in-report-builder.md)   
 [Risolvere i problemi di parti del Report &#40;Report e SSRS&#41;](../../2014/reporting-services/troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [Gestione di parti di Report](report-design/managing-report-parts.md)   
 [Report Builder 3 parti di Report in SQL Server 2008 R2 (video)](https://technet.microsoft.com/edge/Video/ff711300)   
 [Procedura: Creare parti di Report riutilizzabili con Generatore Report di SQL Server (video)](https://technet.microsoft.com/sqlserver/ff634166.aspx)  
  
  
