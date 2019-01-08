---
title: Power Pivot Authentication and Authorization | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2f6568e39b364b0e7d486e0d9e0318709141be63
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52402646"
---
# <a name="power-pivot-authentication-and-authorization"></a>Autenticazione e autorizzazione di Power Pivot
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Una distribuzione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint eseguita in una farm di SharePoint 2010 usa il sottosistema di autenticazione e il modello di autorizzazione forniti dai server SharePoint. L'infrastruttura di sicurezza di SharePoint si estende al contenuto e alle operazioni di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] poiché tutto il contenuto correlato a [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]viene archiviato nei database del contenuto di SharePoint e tutte le operazioni correlate a [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]vengono eseguite dai servizi condivisi [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nella farm. L'autenticazione degli utenti che richiedono una cartella di lavoro contenente dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] avviene tramite un'identità utente di SharePoint basata sull'identità utente di Windows. Le autorizzazioni di visualizzazione nella cartella di lavoro consentono di determinare se la richiesta viene concessa o negata.  
  
 Poiché per l'analisi di dati in modalità self-service viene richiesta l'integrazione con Excel Services, per la protezione di un server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] è necessario conoscere anche i meccanismi di sicurezza di Excel Services. Quando un utente esegue una query in una tabella pivot che dispone di una connessione dati a dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , tramite Excel Services viene inoltrata una richiesta di connessione dati a un server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nella farm per caricare i dati. Per tale interazione tra i server è necessario comprendere la modalità di configurazione delle impostazioni di sicurezza per entrambi i server.  
  
 Fare clic sui collegamenti seguenti per leggere sezioni specifiche di questo argomento:  
  
 [Autenticazione di Windows utilizzando l'accesso in modalità classica](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md#bkmk_auth)  
  
 [Operazioni di Power Pivot per cui è richiesta l'autorizzazione utente](#UserConnections)  
  
 [Autorizzazioni di SharePoint per l'accesso ai dati di Power Pivot](#Permissions)  
  
 [Considerazioni sulla sicurezza di Excel Services per le cartelle di lavoro di Power Pivot](#excel)  
  
##  <a name="bkmk_auth"></a> Autenticazione di Windows utilizzando l'accesso in modalità classica  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint supporta un set ridotto di opzioni di autenticazione disponibili in SharePoint. Tra le opzioni di autenticazione disponibili, solo l'autenticazione di Windows è supportata per una distribuzione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint. Inoltre, l'applicazione Web tramite cui si verifica l'accesso deve essere configurata per la modalità classica.  
  
 L'autenticazione di Windows è necessaria poiché è l'unica supportata dal motore dati di Analysis Services in una distribuzione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint. Excel Services consente di stabilire le connessioni a Analysis Services tramite il provider OLE DB MSOLAP utilizzando un'identità utente di Windows autenticata tramite il protocollo NTLM o Kerberos.  
  
 Il secondo requisito, ovvero l'autenticazione della modalità classica nell'applicazione Web, è necessario per assicurare il funzionamento del servizio Web [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Il servizio Web è un componente che viene eseguito in un front-end Web e consente il reindirizzamento HTTP a un server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint nella farm. Il servizio Web è in grado di riconoscere attestazioni per le comunicazioni tra servizi, ma non per le richieste di connessione dati indirizzate a un servizio condiviso [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nella farm. Le richieste di caricamento di dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] sono supportate solo per le connessioni autenticate derivanti dall'uso di un'identità di Windows in IIS. L'accesso in modalità classica all'applicazione Web consente una connessione corretta dal servizio Web [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ai servizi condivisi [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nella farm.  
  
 Sebbene l'accesso in modalità classica non sia necessario per lo scenario di accesso ai dati più comune, nel quale i dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] vengono estratti dalla stessa cartella di lavoro di Excel che ne esegue il rendering, non tentare di usare [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint con applicazioni Web SharePoint configurate per l'uso di altri provider di autenticazione. Questo tentativo comporterebbe un errore di connessione ogni volta che gli utenti tentano di connettersi alle cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] come un'origine dati esterna.  
  
 Senza l'accesso in modalità classica, i tipi seguenti di richieste gestite dal servizio Web [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] avranno esito negativo:  
  
-   Richieste di dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] che hanno origine dall'esterno della farm, ad esempio la creazione di un report in Progettazione report o Generatore report, in cui l'origine dati è un URL di SharePoint di una cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
-   Richieste interne alla farm da un'applicazione client o da un report che usa la cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] come origine dati esterna, ad esempio la creazione di una cartella di lavoro nell'applicazione desktop Excel, usando come origine dati una seconda cartella di lavoro pubblicata di Excel contenente dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
### <a name="how-to-check-the-authentication-provider-for-your-application"></a>Modalità di verifica del provider di autenticazione per l'applicazione  
 Quando si creano nuove applicazioni Web, assicurarsi di selezionare l'opzione **Autenticazione in modalità classica** nella pagina Crea nuova applicazione Web.  
  
 Per le applicazioni Web esistenti, utilizzare le istruzioni seguenti per verificare che l'applicazione Web sia configurata per l'utilizzo dell'autenticazione di Windows.  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni Web**.  
  
2.  Selezionare l'applicazione Web.  
  
3.  Fare clic su **Provider di autenticazione**.  
  
4.  Verificare che si disponga di un provider per ogni area e che l'area predefinita sia impostata su Windows.  
  
##  <a name="UserConnections"></a> Operazioni di Power Pivot per cui è richiesta l'autorizzazione utente  
 L'autorizzazione di SharePoint viene usata esclusivamente per tutti i livelli di accesso all'elaborazione di query e dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Il modello di autorizzazione basato sui ruoli di Analysis Services non è supportato. Non è disponibile alcuna autorizzazione basata sui ruoli per i dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a livello di cella, riga o tabella. Non è possibile proteggere parti diverse della cartella di lavoro per concedere o negare a utenti specifici l'accesso ai dati sensibili di tale cartella. Gli utenti che dispongono di autorizzazioni di visualizzazione per la cartella di lavoro di Excel in una raccolta di SharePoint hanno accesso completo ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] incorporati.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint nei casi seguenti:  
  
-   Query in tabelle pivot o grafici pivot con connessioni dati a un database [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , in cui un'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] consente di stabilire connessioni per conto di un utente a un'istanza specifica del servizio condiviso [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] tramite cui vengono elaborati i dati.  
  
-   Caricamento di dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] dalla cache o da una raccolta se i dati non sono disponibili altrimenti. Se viene eseguita una richiesta di connessione dati per i dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] che non sono stati ancora caricati nel sistema, nell'istanza di [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] sarà usata l'identità dell'utente di SharePoint per recuperare l'origine dati da una raccolta contenuto e caricarla in memoria.  
  
-   Operazioni di aggiornamento dei dati che consentono di salvare una copia aggiornata dell'origine dati nella cartella di lavoro di una raccolta contenuto. In questo caso, viene effettuata una vera operazione di accesso con il nome utente e la password recuperati da un'applicazione di destinazione nel servizio di archiviazione sicura. Le credenziali possono essere costituite da un account di aggiornamento dati automatico [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o da credenziali archiviate con la pianificazione dell'aggiornamento dati al momento della creazione. Per altre informazioni, vedere [Configurare le credenziali archiviate per l'aggiornamento dati Power Pivot (Power Pivot per SharePoint)](http://msdn.microsoft.com/987eff0f-bcfe-4bbd-81e0-9aca993a2a75) e [Configurare l'account di aggiornamento dati automatico Power Pivot (Power Pivot per SharePoint)](http://msdn.microsoft.com/81401eac-c619-4fad-ad3e-599e7a6f8493).  
  
##  <a name="Permissions"></a> Autorizzazioni di SharePoint per l'accesso ai dati di Power Pivot  
 La pubblicazione, la gestione e la protezione di una cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] sono supportate solo tramite l'integrazione con SharePoint. I server SharePoint forniscono sottosistemi di autenticazione e autorizzazione che garantiscono l'accesso legittimo ai dati. Non sono supportati scenari che consentano di distribuire in modo protetto una cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] all'esterno di una farm di SharePoint.  
  
 L'accesso utente ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] è di sola lettura nel server tramite le autorizzazioni di visualizzazione o superiori. Le autorizzazioni di collaborazione consentono di aggiungere e modificare il file. Per apportare modifiche ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] è necessario scaricare la cartella di lavoro in un'applicazione desktop di Excel in cui sia installato [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per Excel. Le autorizzazioni di collaborazione sul file consentiranno di determinare se l'utente può scaricare il file in locale e, successivamente, salvare le modifiche in SharePoint.  
  
 I livelli di autorizzazione di collaborazione e di sola visualizzazione consentono pertanto di definire il set di autorizzazioni valido per l'accesso utente ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Gli altri livelli di autorizzazione consentono un determinato livello di accesso in base alle autorizzazioni di Collaborazione e Solo visualizzazione in essi inclusi. Poiché nel livello Lettura, ad esempio, sono incluse le autorizzazioni Solo visualizzazione, un utente assegnato a tale livello disporrà dello stesso tipo di accesso garantito per Solo visualizzazione.  
  
 La tabella seguente riepiloga i livelli di autorizzazione che determinano l'accesso ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e alle operazioni del server:  
  
|Livello di autorizzazione|Attività consentite|  
|----------------------|------------------------|  
|Amministratore di farm o di servizio|Installazione, abilitazione e configurazione di servizi e applicazioni.<br /><br /> Uso del dashboard di gestione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e visualizzazione dei report amministrativi.|  
|Controllo completo|Attivazione dell'integrazione delle caratteristiche di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a livello di raccolta siti.<br /><br /> Creazione di un libreria della Raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Creazione di una libreria di feed di dati.|  
|Collaborazione|Aggiunta, modifica,eliminazione e download di cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Configurazione dell'aggiornamento dati.<br /><br /> Creazione di nuove cartelle di lavoro e report basati sulle cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in un sito di SharePoint.<br /><br /> Creazione di documenti di servizio dati in una libreria di feed di dati|  
|lettura|Accesso [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cartelle di lavoro come un'origine dati esterna, dove l'URL della cartella di lavoro viene immesso in modo esplicito in una finestra di dialogo di connessione (ad esempio, nella connessione guidata dati di Excel).|  
|Solo visualizzazione|Visualizzazione delle cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Visualizzazione della cronologia dell'aggiornamento dati.<br /><br /> Connessione di una cartella di lavoro locale a una cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] su un sito di SharePoint, per la ridefinizione degli scopi dei relativi dati in altri modi.<br /><br /> Download di uno snapshot della cartella di lavoro. Lo snapshot è una copia statica dei dati, senza filtri dei dati, filtri, formule o connessioni dati. Il contenuto dello snapshot è simile alla copia di valori cella dalla finestra del browser.|  
  
##  <a name="excel"></a> Considerazioni sulla sicurezza di Excel Services per le cartelle di lavoro di Power Pivot  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] L'elaborazione di query sul lato server di è strettamente associata a Excel Services. L'integrazione del prodotto inizia a livello di documento, poiché le cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] sono file della cartella di lavoro di Excel (con estensione xlsx) in cui sono contenuti dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o riferimenti a essi. Non esiste alcuna estensione di file separata per una cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Quando una cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] viene aperta su un sito di SharePoint, tramite Excel Services viene letta la stringa di connessione dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] incorporata e inoltrata la richiesta al provider OLE DB per SQL Server Analysis Services locale. Il provider consente quindi di passare le informazioni di connessione a un server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nella farm. Affinché le richieste vengano trasmesse senza interruzioni tra i due server, Excel Services deve essere configurato per l'uso delle impostazioni richieste da [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint.  
  
 In Excel Services le impostazioni di configurazione correlate alla sicurezza vengono specificate in percorsi attendibili, provider di dati attendibili e raccolte connessioni dati attendibili. Nella tabella seguente vengono descritte le impostazioni che abilitano o migliorano l'accesso ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Se un'impostazione non rientra tra quelle elencate, non avrà alcun effetto sulle connessioni del server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Per istruzioni su come specificare in modo dettagliato queste impostazioni, vedere la sezione "Abilitare Excel Services" in [Configurazione iniziale (Power Pivot per SharePoint)](http://msdn.microsoft.com/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146).  
  
> [!NOTE]  
>  La maggior parte delle impostazioni correlate alla sicurezza si applicano ai percorsi attendibili. Se si desidera mantenere valori predefiniti o usare valori diversi per siti differenti, è possibile creare un percorso attendibile aggiuntivo per siti che contengono dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , quindi configurare le impostazioni seguenti solo per quel sito. Per altre informazioni, vedere [Creare un percorso attendibile per i siti PowerPivot in Amministrazione centrale](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
|Area|Impostazione|Descrizione|  
|----------|-------------|-----------------|  
|Applicazione Web|Provider di autenticazione di Windows|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] converte un token delle attestazioni ottenute da Excel Services in un'identità utente di Windows. Qualsiasi applicazione Web che utilizza Excel Services come risorsa deve essere configurata per l'utilizzo del provider di autenticazione di Windows.|  
|Percorso attendibile|Tipo percorso|È necessario impostare questo valore su **Microsoft SharePoint Foundation**. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] recuperano una copia del file con estensione xlsx e la caricano su un server Analysis Services nella farm. Il server può recuperare solo file con estensione xlsx da una raccolta contenuto.|  
||Impostazione dati esterni consentiti|È necessario impostare questo valore su **Raccolte di connessioni dati attendibili e connessioni incorporate**. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] sono incorporate nella cartella di lavoro. Se non si consentono le connessioni incorporate, gli utenti possono visualizzare la cache della [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , ma non saranno in grado di interagire con i dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
||Avvisa in caso di aggiornamento|È necessario disabilitare questo valore se si usa la Raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per archiviare cartelle di lavoro e report. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] è inclusa una caratteristica di anteprima di documento che funziona meglio se l'aggiornamento all'apertura e l'avviso in caso di aggiornamento sono disabilitati.|  
|Provider di dati attendibili|MSOLAP.4<br /><br /> MSOLAP.5|MSOLAP.4 è incluso per impostazione predefinita, tuttavia per l'accesso ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] viene richiesto che la versione del provider MSOLAP.4 sia SQL Server 2008 R2.<br /><br /> MSOLAP.5 è installato con la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint.<br /><br /> Non rimuovere questi provider dall'elenco di provider di dati attendibili. In alcuni casi, potrebbe essere necessario installare copie aggiuntive di questo provider negli altri server SharePoint della farm. Per altre informazioni, vedere [Installazione del provider OLE DB di Analysis Services nei server di SharePoint](http://msdn.microsoft.com/2c62daf9-1f2d-4508-a497-af62360ee859).|  
|Raccolte connessioni dati attendibili|Facoltativo.|Nelle cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] è possibile usare file ODC (Office Data Connection), con estensione odc. Se si usano file odc per fornire informazioni di connessione alle cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] locali, è possibile aggiungere gli stessi file odc a questa raccolta.|  
|Assembly per la funzione definita dall'utente|Non applicabile.|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint ignora gli assembly per la funzione definita dall'utente compilati e distribuiti per Excel Services. Se si usano assembly definiti dall'utente per un comportamento specifico, tenere presente che per l'elaborazione di query [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] non verranno usate le funzioni definite dall'utente create.|  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare gli account del servizio PowerPivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [Configurare l'account di aggiornamento dati automatico Power Pivot (Power Pivot per SharePoint)](http://msdn.microsoft.com/81401eac-c619-4fad-ad3e-599e7a6f8493)   
 [Creare un percorso attendibile per i siti PowerPivot in Amministrazione centrale](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)   
 [Architettura di sicurezza di Power Pivot](http://go.microsoft.com/fwlink/?linkID=220970)  
  
  
