---
title: PowerPivot Authentication and Authorization | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 48230cc0-4037-4f99-8360-dadf4bc169bd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f28da387576eee3d9619e4fc817485beb5c8662
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377861"
---
# <a name="powerpivot-authentication-and-authorization"></a>Autenticazione e autorizzazione di PowerPivot
  Una distribuzione PowerPivot per SharePoint eseguita in una farm di SharePoint 2010 utilizza il sottosistema di autenticazione e il modello di autorizzazione forniti dai server SharePoint. L'infrastruttura di sicurezza di SharePoint si estende al contenuto e alle operazioni di PowerPivot poiché tutto il contenuto correlato a PowerPivot viene archiviato nei database del contenuto di SharePoint e tutte le operazioni correlate a PowerPivot vengono effettuate dai servizi condivisi PowerPivot nella farm. L'autenticazione degli utenti che richiedono una cartella di lavoro contenente dati PowerPivot avviene tramite un'identità utente di SharePoint basata sull'identità utente di Windows. Le autorizzazioni di visualizzazione nella cartella di lavoro consentono di determinare se la richiesta viene concessa o negata.  
  
 Poiché per l'analisi di dati in modalità self-service viene richiesta l'integrazione con Excel Services, per la protezione di un server PowerPivot è necessaria anche la comprensione della sicurezza di Excel Services. Quando un utente esegue una query in una tabella pivot che dispone di una connessione dati a dati PowerPivot, tramite Excel Services viene inoltrata una richiesta di connessione dati a un server PowerPivot nella farm per caricare i dati. Per tale interazione tra i server è necessario comprendere la modalità di configurazione delle impostazioni di sicurezza per entrambi i server.  
  
 Fare clic sui collegamenti seguenti per leggere sezioni specifiche di questo argomento:  
  
 [Autenticazione di Windows utilizzando l'accesso in modalità classica](power-pivot-authentication-and-authorization.md#bkmk_auth)  
  
 [Operazioni di PowerPivot che richiede l'autorizzazione utente](#UserConnections)  
  
 [Autorizzazioni di SharePoint per accedere ai dati PowerPivot](#Permissions)  
  
 [Considerazioni sulla sicurezza di Excel Services per le cartelle di lavoro di PowerPivot](#excel)  
  
##  <a name="bkmk_auth"></a> Autenticazione di Windows utilizzando l'accesso in modalità classica  
 PowerPivot per SharePoint supporta un set ridotto di opzioni di autenticazione disponibili in SharePoint. Tra le opzioni di autenticazione disponibili, solo l'autenticazione di Windows è supportata per una distribuzione di PowerPivot per SharePoint. Inoltre, l'applicazione Web tramite cui si verifica l'accesso deve essere configurata per la modalità classica.  
  
 L'autenticazione di Windows è necessaria poiché è l'unica supportata dal motore dati di Analysis Services in una distribuzione di PowerPivot per SharePoint. Excel Services consente di stabilire le connessioni a Analysis Services tramite il provider OLE DB MSOLAP utilizzando un'identità utente di Windows autenticata tramite il protocollo NTLM o Kerberos.  
  
 Il secondo requisito, ovvero l'autenticazione della modalità classica nell'applicazione Web, è necessario per assicurare il funzionamento del servizio Web PowerPivot. Il servizio Web è un componente che viene eseguito in un front-end Web e consente il reindirizzamento HTTP a un server PowerPivot per SharePoint nella farm. Il servizio Web è in grado di riconoscere attestazioni per le comunicazioni tra servizi, ma non per le richieste di connessione dati indirizzate a un servizio condiviso PowerPivot nella farm. Le richieste di caricamento di dati PowerPivot sono supportate solo per le connessioni autenticate derivanti dall'utilizzo di un'identità di Windows in IIS. L'accesso in modalità classica all'applicazione Web consente una connessione corretta dal servizio Web PowerPivot ai servizi condivisi PowerPivot nella farm.  
  
 Sebbene l'accesso in modalità classica non sia necessario per lo scenario di accesso ai dati più comune, nel quale i dati PowerPivot vengono estratti dalla stessa cartella di lavoro di Excel che ne esegue il rendering, non tentare di utilizzare PowerPivot per SharePoint con applicazioni Web SharePoint configurate per l'utilizzo di altri provider di autenticazione. Questo tentativo comporterebbe un errore di connessione ogni volta che gli utenti tentano di connettersi alle cartelle di lavoro di PowerPivot come un'origine dati esterna.  
  
 Senza l'accesso in modalità classica, i tipi seguenti di richieste gestite dal servizio Web PowerPivot avranno esito negativo:  
  
-   Richieste di dati PowerPivot che hanno origine dall'esterno della farm, ad esempio la creazione di un report in Progettazione report o Generatore report, in cui l'origine dati è un URL di SharePoint di una cartella di lavoro di PowerPivot.  
  
-   Richieste interne alla farm da un'applicazione client o da un report che utilizza la cartella di lavoro di PowerPivot come origine dati esterna, ad esempio la creazione di una cartella di lavoro nell'applicazione desktop Excel, utilizzando come origine dati una seconda cartella di lavoro pubblicata di Excel contenente dati PowerPivot.  
  
### <a name="how-to-check-the-authentication-provider-for-your-application"></a>Modalità di verifica del provider di autenticazione per l'applicazione  
 Quando si creano nuove applicazioni Web, assicurarsi di selezionare l'opzione **Autenticazione in modalità classica** nella pagina Crea nuova applicazione Web.  
  
 Per le applicazioni Web esistenti, utilizzare le istruzioni seguenti per verificare che l'applicazione Web sia configurata per l'utilizzo dell'autenticazione di Windows.  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni Web**.  
  
2.  Selezionare l'applicazione Web.  
  
3.  Fare clic su **Provider di autenticazione**.  
  
4.  Verificare che si disponga di un provider per ogni area e che l'area predefinita sia impostata su Windows.  
  
##  <a name="UserConnections"></a> Operazioni di PowerPivot che richiede l'autorizzazione utente  
 L'autorizzazione di SharePoint viene utilizzata esclusivamente per tutti i livelli di accesso all'elaborazione di query e dati PowerPivot.  
  
 Il modello di autorizzazione basato sui ruoli di Analysis Services non è supportato. Non è disponibile alcuna autorizzazione basata sui ruoli per i dati PowerPivot a livello di cella, riga o tabella. Non è possibile proteggere parti diverse della cartella di lavoro per concedere o negare a utenti specifici l'accesso ai dati sensibili di tale cartella. Gli utenti che dispongono di autorizzazioni di visualizzazione per la cartella di lavoro di Excel in una raccolta di SharePoint hanno accesso completo ai dati PowerPivot incorporati.  
  
 Un utente di SharePoint sarà rappresentato da PowerPivot per SharePoint nei casi seguenti:  
  
-   Query in tabelle pivot o grafici pivot con connessioni dati a un database PowerPivot, in cui un'applicazione del servizio PowerPivot consente di stabilire connessioni per conto di un utente a un'istanza specifica del servizio condiviso PowerPivot tramite cui vengono elaborati i dati.  
  
-   Caricamento di dati PowerPivot dalla cache o da una raccolta se i dati non sono disponibili altrimenti. Se viene effettuata una richiesta di connessione dati per i dati PowerPivot che non sono stati ancora caricati nel sistema, nell'istanza di [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] sarà utilizzata l'identità dell'utente di SharePoint per recuperare l'origine dati da una raccolta contenuto e caricarla in memoria.  
  
-   Operazioni di aggiornamento dei dati che consentono di salvare una copia aggiornata dell'origine dati nella cartella di lavoro di una raccolta contenuto. In questo caso, viene effettuata una vera operazione di accesso con il nome utente e la password recuperati da un'applicazione di destinazione nel servizio di archiviazione sicura. Le credenziali possono essere costituite da un account di aggiornamento dati automatico PowerPivot o da credenziali archiviate con la pianificazione dell'aggiornamento dati al momento della creazione. Per altre informazioni, vedere [configurare le credenziali archiviate per l'aggiornamento dati PowerPivot &#40;PowerPivot per SharePoint&#41; ](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md) e [configurare l'Account di aggiornamento dati PowerPivot automatico &#40; PowerPivot per SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md).  
  
##  <a name="Permissions"></a> Autorizzazioni di SharePoint per accedere ai dati PowerPivot  
 La pubblicazione, la gestione e la protezione di una cartella di lavoro di PowerPivot sono supportate solo tramite l'integrazione con SharePoint. I server SharePoint forniscono sottosistemi di autenticazione e autorizzazione che garantiscono l'accesso legittimo ai dati. Non sono supportati scenari che consentano di distribuire in modo protetto una cartella di lavoro di PowerPivot all'esterno di una farm di SharePoint.  
  
 L'accesso utente ai dati PowerPivot è di sola lettura nel server tramite le autorizzazioni di visualizzazione o superiori. Le autorizzazioni di collaborazione consentono di aggiungere e modificare il file. Per apportare modifiche ai dati PowerPivot è necessario scaricare la cartella di lavoro in un'applicazione desktop di Excel in cui sia installato PowerPivot per Excel. Le autorizzazioni di collaborazione sul file consentiranno di determinare se l'utente può scaricare il file in locale e, successivamente, salvare le modifiche in SharePoint.  
  
 I livelli di autorizzazione di collaborazione e di sola visualizzazione consentono pertanto di definire il set di autorizzazioni valido per l'accesso utente ai dati PowerPivot. Gli altri livelli di autorizzazione consentono un determinato livello di accesso in base alle autorizzazioni di Collaborazione e Solo visualizzazione in essi inclusi. Poiché nel livello Lettura, ad esempio, sono incluse le autorizzazioni Solo visualizzazione, un utente assegnato a tale livello disporrà dello stesso tipo di accesso garantito per Solo visualizzazione.  
  
 Nella tabella seguente vengono riepilogati i livelli di autorizzazione che determinano l'accesso ai dati PowerPivot e alle operazioni del server:  
  
|Livello di autorizzazione|Attività consentite|  
|----------------------|------------------------|  
|Amministratore di farm o di servizio|Installazione, abilitazione e configurazione di servizi e applicazioni.<br /><br /> Utilizzo del dashboard di gestione PowerPivot e visualizzazione dei report amministrativi.|  
|Controllo completo|Attivazione dell'integrazione delle caratteristiche di PowerPivot a livello di raccolta siti.<br /><br /> Creazione di una libreria di raccolta PowerPivot.<br /><br /> Creazione di una libreria di feed di dati.|  
|Collaborazione|Aggiunta, modifica e download di cartelle di lavoro di PowerPivot.<br /><br /> Configurazione dell'aggiornamento dati.<br /><br /> Creazione di cartelle di lavoro e report basati sulle cartelle di lavoro di PowerPivot in un sito di SharePoint.<br /><br /> Creazione di documenti di servizio dati in una libreria di feed di dati|  
|lettura|Accedere a cartelle di lavoro di PowerPivot come un'origine dati esterna, dove l'URL della cartella di lavoro viene immesso in modo esplicito in una finestra di dialogo di connessione (ad esempio, nella connessione guidata dati di Excel).|  
|Solo visualizzazione|Visualizzazione delle cartelle di lavoro di PowerPivot.<br /><br /> Visualizzazione della cronologia dell'aggiornamento dati.<br /><br /> Connessione di una cartella di lavoro locale a una cartella di lavoro di PowerPivot su un sito di SharePoint, per la ridefinizione degli scopi dei relativi dati in altri modi.<br /><br /> Download di uno snapshot della cartella di lavoro. Lo snapshot è una copia statica dei dati, senza filtri dei dati, filtri, formule o connessioni dati. Il contenuto dello snapshot è simile alla copia di valori cella dalla finestra del browser.|  
  
##  <a name="excel"></a> Considerazioni sulla sicurezza di Excel Services per le cartelle di lavoro di PowerPivot  
 L'elaborazione di query lato server di PowerPivot è strettamente associata a Excel Services. L'integrazione del prodotto inizia a livello di documento, poiché le cartelle di lavoro di PowerPivot sono file della cartella di lavoro di Excel (con estensione xlsx) in cui sono contenuti dati PowerPivot o riferimenti a essi. Non esiste alcuna estensione di file separata per una cartella di lavoro di PowerPivot.  
  
 Quando una cartella di lavoro di PowerPivot viene aperta su un sito di SharePoint, tramite Excel Services viene letta la stringa di connessione dati PowerPivot incorporata e inoltrata la richiesta al provider OLE DB per SQL Server Analysis Services locale. Il provider consente quindi di passare le informazioni di connessione a un server PowerPivot nella farm. Affinché le richieste vengano trasmesse senza interruzioni tra i due server, Excel Services deve essere configurato per l'utilizzo delle impostazioni richieste da PowerPivot per SharePoint.  
  
 In Excel Services le impostazioni di configurazione correlate alla sicurezza vengono specificate in percorsi attendibili, provider di dati attendibili e raccolte connessioni dati attendibili. Nella tabella seguente vengono descritte le impostazioni che abilitano o migliorano l'accesso ai dati PowerPivot. Se un'impostazione non rientra tra quelle elencate, non avrà alcun effetto sulle connessioni del server PowerPivot. Per istruzioni su come specificare queste impostazioni passo a passo, vedere la sezione "Abilitare Excel Services" nella [la configurazione iniziale &#40;PowerPivot per SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md).  
  
> [!NOTE]  
>  La maggior parte delle impostazioni correlate alla sicurezza si applicano ai percorsi attendibili. Se si desidera mantenere valori predefiniti o utilizzare valori diversi per siti differenti, è possibile creare un percorso attendibile aggiuntivo per siti che contengono dati PowerPivot, quindi configurare le impostazioni seguenti solo per quel sito. Per altre informazioni, vedere [Creare un percorso attendibile per i siti PowerPivot in Amministrazione centrale](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
|Area|Impostazione|Descrizione|  
|----------|-------------|-----------------|  
|Applicazione Web|Provider di autenticazione di Windows|PowerPivot converte un token delle richieste ottenute da Excel Services in un'identità utente di Windows. Qualsiasi applicazione Web che utilizza Excel Services come risorsa deve essere configurata per l'utilizzo del provider di autenticazione di Windows.|  
|Percorso attendibile|Tipo percorso|È necessario impostare questo valore su **Microsoft SharePoint Foundation**. I server PowerPivot recuperano una copia del file con estensione xlsx e la caricano su un server Analysis Services nella farm. Il server può recuperare solo file con estensione xlsx da una raccolta contenuto.|  
||Impostazione dati esterni consentiti|È necessario impostare questo valore su **Raccolte di connessioni dati attendibili e connessioni incorporate**. Le connessioni dati PowerPivot sono incorporate nella cartella di lavoro. Se non si consentono le connessioni incorporate, gli utenti possono visualizzare la cache della tabella pivot, ma non saranno in grado di interagire con i dati PowerPivot.|  
||Avvisa in caso di aggiornamento|È necessario disabilitare questo valore se si utilizza la raccolta PowerPivot per archiviare cartelle di lavoro e report. Nella raccolta PowerPivot è inclusa una caratteristica di anteprima di documento che funziona meglio se l'aggiornamento all'apertura e l'avviso in caso di aggiornamento sono disabilitati.|  
|Provider di dati attendibili|MSOLAP.4<br /><br /> MSOLAP.5|MSOLAP.4 è incluso per impostazione predefinita, tuttavia per l'accesso ai dati PowerPivot viene richiesto che la versione del provider MSOLAP.4 sia SQL Server 2008 R2.<br /><br /> MSOLAP.5 è installato con la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di PowerPivot per SharePoint.<br /><br /> Non rimuovere questi provider dall'elenco di provider di dati attendibili. In alcuni casi, potrebbe essere necessario installare copie aggiuntive di questo provider negli altri server SharePoint della farm. Per altre informazioni, vedere [Installazione del provider OLE DB di Analysis Services nei server di SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).|  
|Raccolte connessioni dati attendibili|Facoltativo.|Nelle cartelle di lavoro di PowerPivot è possibile utilizzare file ODC (Office Data Connection). Se si utilizzano file odc per fornire informazioni di connessione alle cartelle di lavoro di PowerPivot locali, è possibile aggiungere gli stessi file odc a questa raccolta.|  
|Assembly per la funzione definita dall'utente|Non applicabile.|In PowerPivot per SharePoint vengono ignorati gli assembly per la funzione definita dall'utente compilati e distribuiti per Excel Services. Se si utilizzano gli assembly definiti dall'utente per un comportamento specifico, assicurarsi che per l'elaborazione di query PowerPivot non vengano utilizzate le funzioni definite dall'utente create.|  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare gli account del servizio PowerPivot](configure-power-pivot-service-accounts.md)   
 [Configurare PowerPivot Account di aggiornamento dati automatico &#40;PowerPivot per SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)   
 [Creare un percorso attendibile per siti PowerPivot in Amministrazione centrale](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)   
 [Architettura di sicurezza di PowerPivot](https://go.microsoft.com/fwlink/?linkID=220970)  
  
  
