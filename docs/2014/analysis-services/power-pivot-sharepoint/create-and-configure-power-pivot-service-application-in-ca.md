---
title: Creare e configurare un'applicazione di servizio PowerPivot in Amministrazione centrale | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: b2e5693e-4af3-453f-83f3-07481ab1ac6a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac1b7ad9e5308437dacf51b7960822e7636ab3e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62749380"
---
# <a name="create-and-configure-a-powerpivot-service-application-in-central-administration"></a>Creare e configurare un'applicazione del servizio PowerPivot in Amministrazione centrale
  Un'applicazione del servizio PowerPivot è un'istanza del servizio condiviso del servizio di sistema PowerPivot. Ogni applicazione del servizio possiede impostazioni di configurazione, proprietà, un'identità e un sistema di archiviazione dati interno propri.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Determinare se creare una nuova applicazione di servizio PowerPivot](#determine)  
  
 [Creare un'applicazione di servizio PowerPivot](#CreateApp)  
  
 [Configurare l'applicazione di servizio PowerPivot](#ConfigApp)  
  
 [Assegnare un'applicazione di servizio PowerPivot a un'applicazione Web](#AssignGSA)  
  
 [Modificare le proprietà dell'applicazione di servizio](#EditGSA)  
  
##  <a name="determine"></a> Determinare se creare una nuova applicazione di servizio PowerPivot  
 Nella farm di un'installazione di PowerPivot per SharePoint deve essere presente almeno un'applicazione di servizio PowerPivot. Un'applicazione del servizio viene creata automaticamente se è stato utilizzato lo strumento di configurazione PowerPivot per configurare il server. In caso contrario, è necessario creare manualmente un'applicazione del servizio PowerPivot in Amministrazione centrale.  
  
 Creando un'applicazione di servizio si rende disponibile il servizio e si genera il database dell'applicazione di servizio. A seconda delle opzioni selezionate durante la creazione dell'applicazione di servizio, una connessione al servizio PowerPivot viene aggiunta al gruppo di connessioni predefinito del servizio. A tutte le applicazioni Web di SharePoint sottoscritte al gruppo di connessioni predefinito del servizio sarà concesso l'accesso immediato all'applicazione di servizio PowerPivot.  
  
 È possibile creare più applicazioni di servizio PowerPivot. Sebbene un'applicazione di servizio sia sufficiente per la maggior parte degli scenari di distribuzione, considerare la possibilità di creare un'applicazione di servizio PowerPivot aggiuntiva se i requisiti aziendali includono gli elementi seguenti:  
  
-   Utilizzo di un account di aggiornamento dati automatico PowerPivot diverso per ogni applicazione.  
  
-   Utilizzo di timeout, cronologia dell'utilizzo e soglie diversi per report di risposta alle query.  
  
-   Delega dell'amministrazione del servizio a utenti diversi. Un amministratore vedrà la cronologia dell'aggiornamento dati, i dati di utilizzo e le altre proprietà solo per l'applicazione che sta amministrando. Se è necessario isolare i dati per applicazioni Web di SharePoint diverse, ad esempio se la società è un servizio di hosting che deve garantire l'isolamento dei dati per le applicazioni Web di SharePoint appartenenti a clienti diversi, la creazione di applicazioni di servizio PowerPivot distinte può aiutare a raggiungere i requisiti di isolamento garantendo che ciascun amministratore possa vedere solo le impostazioni e le proprietà di configurazione per le applicazioni che gestisce.  
  
 La creazione di un'applicazione di servizio aggiuntiva introduce nuovi requisiti per la gestione delle associazioni di servizio, richiedendo che si creino e utilizzino elenchi di associazione di servizio personalizzati per ogni applicazione di servizio aggiuntiva.  
  
 Se non esiste alcun motivo specifico per cui creare un'applicazione di servizio PowerPivot aggiuntiva, è preferibile utilizzare una sola applicazione di servizio per tutte le applicazioni Web della farm.  
  
##  <a name="CreateApp"></a> Creare un'applicazione di servizio PowerPivot  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Nella barra multifunzione **Applicazioni di servizio** fare clic su **Nuovo**.  
  
3.  Selezionare **applicazione di servizio PowerPivot SQL Server**. Se non è presente nell'elenco, PowerPivot per SharePoint non è installato o configurato correttamente.  
  
4.  Nel **Crea nuova applicazione del servizio PowerPivot** pagina, immettere un nome per l'applicazione. Il valore predefinito è PowerPivotServiceApplication\<numero >. Se si creano più applicazioni di servizio PowerPivot, un nome descrittivo sarà utile per capire come viene utilizzata l'applicazione.  
  
5.  In Pool di applicazioni, creare un nuovo pool di applicazioni per l'applicazione (consigliato). Selezionare o creare un account gestito di sicurezza per il pool di applicazioni. Assicurarsi di specificare un account utente di dominio. Un account utente di dominio permette di utilizzare la funzionalità dell'account gestito di SharePoint, che consente di aggiornare password e informazioni sull'account da un'unica posizione. Gli account di dominio sono inoltre obbligatori se si prevede di ridimensionare la distribuzione per includere istanze del servizio aggiuntive da eseguire con la stessa identità.  
  
6.  In **Server di database**il valore predefinito è l'istanza del Motore di database di SQL Server che esegue l'hosting dei database di configurazione della farm. È possibile utilizzare questo server o sceglierne uno diverso.  
  
7.  Nelle **sicurissimo**, il valore predefinito è PowerPivotServiceApplication1_\<guid >. È necessario creare un database univoco per ogni applicazione di servizio PowerPivot. Il nome del database predefinito corrisponde al nome predefinito dell'applicazione di servizio. Se è stato immesso un nome univoco per l'applicazione del servizio, seguire una convenzione di denominazione simile per il nome del database in modo da poterli gestire insieme.  
  
8.  In **Autenticazione database**l'impostazione predefinita è Autenticazione di Windows. Se si sceglie **Autenticazione di SQL Server**, fare riferimento alla guida dell'amministratore di SharePoint per le procedure consigliate sull'utilizzo di questo tipo di autenticazione in una distribuzione di SharePoint.  
  
9. Facoltativamente, selezionare la casella di controllo **aggiunge il proxy per questa applicazione di servizio PowerPivot al gruppo di proxy della farm predefinita.** La connessione all'applicazione di servizio verrà aggiunta al gruppo predefinito di connessioni al servizio.  
  
     È necessario selezionare questa casella di controllo, se si crea la prima applicazione di servizio PowerPivot. Per assicurare il corretto funzionamento del dashboard di gestione PowerPivot, è necessario che almeno un'applicazione di servizio PowerPivot sia presente nel gruppo di connessioni predefinito.  
  
     Non aggiungere l'applicazione di servizio PowerPivot al gruppo di connessioni predefinito se ne esiste già una. L'aggiunta di più voci dello stesso tipo di applicazione di servizio non è una configurazione supportata e potrebbe provocare errori. Se si creano applicazioni di servizio aggiuntive, è necessario lasciarle fuori dal gruppo di connessioni predefinito e aggiungerle invece agli elenchi personalizzati.  
  
     Per altre informazioni sulle associazioni di servizio, vedere [connettere un'applicazione di servizio PowerPivot a un'applicazione Web SharePoint in Amministrazione centrale](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md).  
  
10. Scegliere **OK.** Il servizio verrà visualizzato con altri servizi gestiti nell'elenco di applicazioni di servizio della farm.  
  
##  <a name="ConfigApp"></a> Configurare l'applicazione di servizio PowerPivot  
 Un'applicazione di servizio PowerPivot viene creata utilizzando una configurazione predefinita. Le impostazioni predefinite sono consigliate per la maggior parte degli scenari. Modificarle solo in caso di connessioni interrotte o tempi di risposta lunghi o se si intende variare la configurazione del servizio PowerPivot per applicazioni Web di SharePoint specifiche.  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
     Nell'elenco di applicazioni di servizio dovrebbe essere presente l'applicazione di servizio appena creata e a cui è stato assegnato un nome. Il nome predefinito è **PowerPivotServiceApplication1**.  
  
2.  Fare clic sull'applicazione di servizio PowerPivot. Verrà aperto il dashboard di gestione PowerPivot.  
  
3.  Nell'elenco **Azioni** nell'angolo superiore destro del dashboard fare clic su **Configura impostazioni dell'applicazione di servizio**.  
  
4.  Nelle **Timeout caricamento Database**aumentare o diminuire il valore per modificare quanto tempo il servizio PowerPivot attende una risposta dall'istanza di SQL Server Analysis Services (PowerPivot) a cui è stata inoltrata una richiesta di caricamento dati. Poiché lo spostamento di set di dati di dimensioni molto elevate richiede tempo, è necessario consentire un tempo sufficiente all'istanza del servizio PowerPivot per recuperare la cartella di lavoro di Excel e spostare i dati PowerPivot in un'istanza di Analysis Services per l'elaborazione delle query. Poiché i dati PowerPivot possono avere dimensioni insolitamente elevate, il valore predefinito è 30 minuti.  
  
5.  In **Timeout pool di connessioni**aumentare o diminuire il valore per modificare per quanti minuti rimarrà aperta una connessione dati inattiva. Il valore predefinito è 30 minuti. Durante questo periodo di tempo, la connessione dati inattiva verrà riutilizzata per le richieste in sola lettura provenienti dallo stesso utente SharePoint per gli stessi dati PowerPivot. Se non vengono ricevute ulteriori richieste di dati durante il periodo specificato, la connessione viene rimossa dal pool. I valori validi sono compresi tra 1 e 3600 secondi. Per altre informazioni sui pool di connessione, vedere [riferimento all'impostazione di configurazione &#40;PowerPivot per SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md).  
  
6.  Nelle **dimensioni massime Pool di connessioni utente**aumentare o diminuire il valore per modificare il numero massimo di connessioni inattive nel pool di connessioni singoli per ogni utente di SharePoint, set di dati PowerPivot, verrà creato il servizio PowerPivot e combinazione di versione.  
  
     Il valore predefinito è 1000 connessioni inattive. I valori validi sono -1 (senza limiti), 0 (pool di connessioni utente disabilitati) oppure un valore compreso tra 1 e 10000.  
  
     Questi pool di connessioni consentono al servizio di supportare in modo più efficiente connessioni in corso agli stessi dati in sola lettura da parte dello stesso utente. Se si disabilita pool di connessioni, ogni connessione sarà creata di nuovo.  
  
     La modifica del limite sulle dimensioni dei pool di connessioni, anche se impostata a 0, non causa l'interruzione delle connessioni. I pool di connessioni hanno la funzione di ridurre i tempi di attesa durante la connessione ai dati. Tramite il servizio PowerPivot non verrà mai negata una connessione in base alle impostazioni del pool di connessioni.  
  
7.  Nelle **massima dimensione Pool di connessioni amministrative**aumentare o diminuire il valore per modificare il numero di connessioni aperte in un pool di connessioni creato per una connessione del servizio PowerPivot a Analysis Services. In ogni istanza del servizio PowerPivot viene aperta una connessione amministrativa separata all'istanza di Analysis Services nello stesso computer. Il servizio PowerPivot consente di creare un pool separato per riutilizzare le connessioni amministrative allo scopo di verificare la presenza di connessioni inattive e monitorare l'integrità del server. Il valore predefinito è 200 connessioni. I valori validi sono -1 (senza limiti), 0 (pool di connessioni amministrative disabilitati) oppure un valore compreso tra 1 e 10000. Se si seleziona 0, ogni connessione verrà creata da zero.  
  
8.  Nelle **metodo di allocazione**, è possibile specificare uno schema che utilizza il servizio di sistema PowerPivot per selezionare un'applicazione di servizio PowerPivot specifica per il bilanciamento del carico di una richiesta iniziale di bilanciamento del carico. L'impostazione predefinita è **Basato sull'integrità**che consente di allocare le richieste in base allo stato del server, misurato dalla memoria disponibile e dall'utilizzo del processore. In alternativa, è possibile scegliere l'opzione **Round robin** per allocare le richieste ai server nello stesso ordine ripetuto, indipendentemente dal fatto che un server sia inattivo o meno.  
  
9. In **Orario di ufficio**di Aggiornamento dati è possibile specificare un intervallo di ore che consente di definire un giorno lavorativo. Le pianificazioni dell'aggiornamento dati possono essere eseguite al termine di un giorno lavorativo per selezionare i dati transazionali generati durante il normale orario di ufficio.  
  
10. Nelle **Account dati automatico PowerPivot di aggiornamento**, è possibile specificare un'applicazione di destinazione Secure Store Service predefinita che archivia un account predefinito per l'esecuzione di processi di aggiornamento dati PowerPivot. Assicurarsi di specificare il nome dell'applicazione di destinazione e non l'ID. L'applicazione di destinazione per l'aggiornamento dati automatico viene creata automaticamente tramite il programma di installazione di SQL Server se PowerPivot per SharePoint è stato installato utilizzando l'opzione Nuovo server. In caso contrario, è necessario creare manualmente l'applicazione di destinazione. Per istruzioni su come configurare l'account, vedere [configurare l'Account di aggiornamento dati PowerPivot automatico &#40;PowerPivot per SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md).  
  
11. In **Consenti agli utenti di immettere credenziali di Windows personalizzate**è possibile selezionare o deselezionare la casella di controllo per specificare se i proprietari delle pianificazioni possono immettere credenziali di Windows arbitrarie per eseguire una pianificazione dell'aggiornamento dati. Se si seleziona questa casella di controllo, l'applicazione del servizio PowerPivot consentirà di creare e gestire un'applicazione di destinazione per ciascun set di credenziali archiviate. Per altre informazioni, vedere [configurare le credenziali archiviate per l'aggiornamento dati PowerPivot &#40;PowerPivot per SharePoint&#41;](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
12. In **Lunghezza massima cronologia di elaborazione**è possibile specificare per quanto tempo mantenere un record cronologico dell'aggiornamento dati. Queste informazioni vengono visualizzate nelle pagine della cronologia dell'aggiornamento dati mantenute per ogni cartella di lavoro per cui viene utilizzato l'aggiornamento dati. Vengono inoltre visualizzate nel dashboard di gestione PowerPivot.  
  
13. In Raccolta dati su utilizzo, in **Intervallo di report query**specificare un intervallo di tempo per la creazione di report di statistiche sulle query. Le statistiche sulle query vengono inserite nei report come un solo evento per ridurre la comunicazione tra server.  
  
14. In Cronologia dati di utilizzo specificare per quanto tempo mantenere un record cronologico dei dati sull'utilizzo. Le informazioni sull'utilizzo verranno visualizzate nel dashboard di gestione PowerPivot. I report saranno meno efficaci se si specifica un valore troppo basso per la cronologia dei dati di utilizzo.  
  
15. In Raccolta dati di utilizzo, in ogni soglia di risposta alle query specificare un limite massimo per stabilire l'arresto di una categoria e l'inizio di un'altra. Queste categorie stabiliscono una linea di base rispetto alla quale viene misurato il comportamento delle query. È possibile utilizzare queste categorie per monitorare le tendenze nei tempi di risposta alle query per il sistema. Queste informazioni verranno visualizzate nel dashboard di gestione PowerPivot.  
  
16. Scegliere **OK** per salvare le modifiche.  
  
     Le modifiche apportate al timeout di caricamento o al metodo di allocazione vengono applicate unicamente alle nuove richieste in arrivo. Le richieste già in corso sono soggette ai valori che erano attivi nel momento in cui era stata ricevuta la richiesta.  
  
##  <a name="AssignGSA"></a> Assegnare un'applicazione di servizio PowerPivot a un'applicazione Web  
 Dopo avere configurato un'applicazione di servizio PowerPivot, è possibile assegnarla a un'applicazione Web aggiungendola all'elenco di connessioni all'applicazione di servizio per quell'applicazione Web. Questa operazione può essere eseguita in due modi:  
  
-   Aggiungere l'applicazione di servizio al gruppo di connessioni **predefinito** . Il *gruppo di connessioni predefinito* è una raccolta di connessioni all'applicazione di servizio disponibili a qualsiasi applicazione Web che fa riferimento a tale gruppo. È necessario aggiungere un'applicazione di servizio PowerPivot a questo elenco.  
  
-   Creare un elenco di connessioni **personalizzato** per un'applicazione Web specifica. Se sono state create più applicazioni di servizio PowerPivot, è possibile scegliere quale utilizzare selezionandola in un elenco personalizzato.  
  
 Il gruppo di connessioni predefinito accetterà più di un'applicazione di servizio dello stesso tipo. Tenere presente, tuttavia, che l'aggiunta di più di un'applicazione di servizio PowerPivot a questo elenco non è supportata.  
  
1.  In **Gestione applicazioni**di Amministrazione centrale fare clic su **Gestisci applicazioni Web**.  
  
2.  Selezionare l'applicazione per la quale si desidera assegnare una connessione, ad esempio SharePoint -80.  
  
3.  Fare clic su **Connessioni servizio**.  
  
4.  In **Edit the following group of associations**(Modifica il gruppo di associazioni seguente) selezionare **default** o **[custom]**.  
  
5.  Per **[custom]**, selezionare la casella di controllo accanto a ogni connessione all'applicazione di servizio che si desidera usare. Se sono presenti più applicazioni di servizio PowerPivot (indicato dal tipo impostato su `PowerPivot Service Application Proxy`), assicurarsi di sceglierne una sola.  
  
6.  Fare clic su **OK**.  
  
##  <a name="EditGSA"></a> Modificare le proprietà dell'applicazione di servizio  
 Utilizzare le istruzioni seguenti per aprire nuovamente la pagina delle proprietà contenente il nome dell'applicazione di servizio, il pool di applicazioni, le impostazioni del database e le associazioni del servizio.  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Selezionare l'applicazione del servizio PowerPivot (ma non fare clic su di essa). È possibile fare clic sul nome del tipo per selezionare l'intera riga.  
  
3.  Sulla barra multifunzione fare clic su **Proprietà** .  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione e configurazione del server PowerPivot in Amministrazione centrale](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
