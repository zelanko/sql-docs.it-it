---
title: Configurare PowerPivot (PowerPivot per SharePoint) Account di aggiornamento dati automatico | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 81401eac-c619-4fad-ad3e-599e7a6f8493
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 51cc5f71c3a3e7515238aef08e97316e549c0e70
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53366594"
---
# <a name="configure-the-powerpivot-unattended-data-refresh-account-powerpivot-for-sharepoint"></a>Configurare l'account di aggiornamento dati automatico PowerPivot (PowerPivot per SharePoint)
  L'account di aggiornamento dati automatico PowerPivot è un account progettato per l'esecuzione dei processi di aggiornamento dei dati PowerPivot in una farm di SharePoint. Configurandolo, si abilita il **utilizza l'aggiornamento dati configurato dall'amministratore account** opzione in una pagina di pianificazione di aggiornamento dati (vedere sotto). Gli autori delle cartelle di lavoro che pianificano l'aggiornamento dati possono scegliere questa opzione se desiderano utilizzare l'account di aggiornamento dati automatico per eseguire un processo di aggiornamento dati. Per altre informazioni su come visualizzare le opzioni delle credenziali nella pianificazione dell'aggiornamento dati, vedere [pianificare un aggiornamento dei dati &#40;PowerPivot per SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md).  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint 2010  
  
 A seconda di quali opzioni siano state selezionate durante la configurazione del server, l'account di aggiornamento dati automatico potrebbe essere già stato creato. In una configurazione predefinita, l'identità dell'account di aggiornamento dati automatico viene inizialmente impostata sull'account della farm. È possibile migliorare la sicurezza della distribuzione modificando l'account in modo che venga eseguito come un altro utente. Seguire queste istruzioni per modificare l'account: [Aggiornare le credenziali usate da un PowerPivot esistente account di aggiornamento dati automatico](#bkmk_editUA).  
  
 Per tutti gli altri scenari di installazione è necessario configurare manualmente questo account attenendosi alle istruzioni riportate di seguito.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Prerequisiti](#bkmk_prereq)  
  
 [Passaggio 1: Creare un'applicazione di destinazione e impostare le credenziali](#bkmk_create)  
  
 [Passaggio 2: Specificare l'account automatico nelle pagine di configurazione di server PowerPivot](#bkmk_specifyUA)  
  
 [Passaggio 3: Concessione di autorizzazioni di collaborazione per l'account](#bkmk_grant)  
  
 [Passaggio 4: Concessione di autorizzazioni di lettura per accedere alle origini dati esterne utilizzate nell'aggiornamento dati](#bkmk_dbread)  
  
 [Passaggio 5: Verificare la disponibilità dell'account nelle pagine di configurazione di aggiornamento dati](#bkmk_verify)  
  
 [Account con l'aggiornamento dati automatico PowerPivot](#bkmk_use)  
  
 [Aggiornare le credenziali usate da un PowerPivot esistente account di aggiornamento dati automatico](#bkmk_editUA)  
  
##  <a name="bkmk_prereq"></a> Prerequisiti  
 Il servizio di archiviazione sicura deve essere abilitato e configurato; inoltre, deve essere generata una chiave master. Per istruzioni su come eseguire questa operazione, vedere [aggiornamento dati PowerPivot con SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)  
  
 È necessario decidere in anticipo l'account utente di dominio Windows da utilizzare come account di aggiornamento dati automatico PowerPivot. Dovrebbe essere un account creato in modo specifico per questo scopo in modo da poter monitorare il relativo utilizzo.  
  
 È necessario conoscere l'identità dell'applicazione del servizio di sistema PowerPivot. Questo account del servizio viene fornito **controllo completo** account di aggiornamento dati automatico autorizzazioni quando si crea l'applicazione di destinazione nel passaggio 1. Queste autorizzazioni consentono al servizio di sistema PowerPivot di recuperare le credenziali dell'account di aggiornamento dati automatico durante l'aggiornamento dati. Per ottenere le informazioni sull'account di servizio richiesto, aprire il **configurare gli account del servizio** pagina in Amministrazione centrale e selezionare il pool di applicazioni di servizio usato dall'applicazione di servizio PowerPivot. Per impostazione predefinita, questo è il **Pool di applicazioni di servizio - sistema dei servizi Web SharePoint**.  
  
## <a name="configure-the-unattended-powerpivot-data-refresh-account"></a>Configurare l'account di aggiornamento dati automatico PowerPivot  
 È possibile configurare un solo account di aggiornamento dati automatico PowerPivot per ogni applicazione del servizio PowerPivot. Le informazioni dell'account vengono archiviate nel servizio di archiviazione sicura in un'applicazione di destinazione impostata su un account utente di dominio Windows predefinito. Una volta creata l'applicazione di destinazione, è possibile specificarla come account di aggiornamento dati PowerPivot nelle pagine di configurazione di un'applicazione del servizio PowerPivot.  
  
> [!NOTE]  
>  Quando l'aggiornamento dati viene effettuato nell'account di aggiornamento dati automatico, la cronologia della creazione di report sull'utilizzo e dell'aggiornamento dati viene registrata rispetto all'account utente di Windows utilizzato per l'aggiornamento dati automatico. Se è necessario un record più preciso di utenti che stanno richiedendo l'aggiornamento dati o che sono in possesso di pianificazioni, prendere in considerazione una delle altre opzioni per eseguire l'aggiornamento dati, ovvero richiedere agli utenti di specificare le proprie credenziali (impostazione predefinita) o creare applicazioni di destinazione aggiuntive per archiviare le credenziali di Windows che si desidera utilizzare per l'aggiornamento dati. Per altre informazioni, vedere [configurare le credenziali archiviate per l'aggiornamento dati PowerPivot &#40;PowerPivot per SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
 La creazione dell'account di aggiornamento dati automatico è costituita da cinque operazioni.  
  
-   Creare un'applicazione di destinazione nel servizio di archiviazione sicura per l'account e specificare le credenziali.  
  
-   Specificare l'ID dell'applicazione di destinazione per l'account di aggiornamento dati automatico nella pagina di configurazione del server PowerPivot.  
  
-   Concedere autorizzazioni di collaborazione all'account.  
  
-   Concedere le autorizzazioni di lettura dell'account per accedere alle origini dati esterne durante l'aggiornamento dati.  
  
-   Verificare che l'account sia disponibile nella pagina di pianificazione Gestisci aggiornamento dati per una cartella di lavoro di PowerPivot pubblicata.  
  
###  <a name="bkmk_create"></a> Passaggio 1: Creare un'applicazione di destinazione e impostare le credenziali  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic su **Secure Store Service**.  
  
3.  In Gestione applicazioni di destinazione, fare clic su **New**.  
  
4.  In ID applicazione di destinazione, digitare **PowerPivotDataRefresh**.  
  
5.  In nome visualizzato, digitare **aggiornamento dati PowerPivot**.  
  
6.  In Posta elettronica contatto digitare l'indirizzo di posta elettronica.  
  
7.  Nel tipo di applicazione di destinazione, selezionare **singoli**.  
  
    > [!NOTE]  
    >  Per questo scenario è possibile specificare un tipo di account personale perché solo l'applicazione del servizio PowerPivot richiederà le credenziali dell'account di aggiornamento dati automatico PowerPivot. In pratica, l'applicazione del servizio è l'unico utente dell'account di aggiornamento dati automatico, pertanto il tipo di account personale risulterà la scelta ottimale per questa applicazione di destinazione.  
  
8.  Ignorare l'URL della pagina dell'applicazione di destinazione. Non verrà utilizzato dall'aggiornamento dati PowerPivot.  
  
9. Scegliere **Avanti**.  
  
10. Nel **specificare i campi di credenziali per l'applicazione di destinazione Store sicura** pagina, accettare i valori predefiniti. I tipi e i nomi dei campi devono essere Nome utente Windows e Password Windows  
  
11. Scegliere **Avanti**.  
  
12. In Amministratori dell'applicazione di destinazione specificare l'identità del pool di applicazioni dell'applicazione di servizio PowerPivot. Il servizio richiede **controllo completo** autorizzazioni in modo che sia possibile recuperare dati automatico Aggiorna informazioni sull'account in fase di esecuzione. Specificare inoltre gli account utente di dominio Windows di qualsiasi altro utente di SharePoint che deve disporre dell'accesso di amministratore alle impostazioni dell'applicazione.  
  
13. Fare clic su **OK**.  
  
14. Selezionare l'applicazione di destinazione appena creata, fare clic sulla freccia verso il basso e selezionare **impostare le credenziali.**  
  
15. Nelle **proprietari credenziali**, digitare un account utente di dominio Windows che si desidera disporre delle autorizzazioni per aggiornare le credenziali. Le credenziali vengono usate per azioni di aggiornamento dati e il **proprietari credenziali** dispone delle autorizzazioni per modificare le credenziali.  
  
16. Fare clic su **OK**.  
  
###  <a name="bkmk_specifyUA"></a> Passaggio 2: Specificare l'account automatico nelle pagine di configurazione di server PowerPivot  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Trovare l'applicazione del servizio PowerPivot. È possibile identificare un'applicazione di servizio in base al tipo. Un tipo di applicazione del servizio PowerPivot è **Applicazione del servizio PowerPivot**.  
  
3.  Fare clic sul nome dell'applicazione di servizio PowerPivot. Attendere la visualizzazione del dashboard di gestione PowerPivot.  
  
4.  Nel riquadro azioni, nell'angolo superiore destro, fare clic su **configurare le impostazioni dell'applicazione di servizio**.  
  
5.  In di aggiornamento dati PowerPivot automatico Account di aggiornamento dati digitare l'ID applicazione di destinazione è stato creato nel passaggio precedente: **PowerPivotDataRefresh**.  
  
6.  Fare clic su **OK**.  
  
###  <a name="bkmk_grant"></a> Passaggio 3: Concessione di autorizzazioni di collaborazione per l'account  
 Prima di poter utilizzare l'account di aggiornamento dati automatico PowerPivot è necessario assegnarvi autorizzazioni di collaborazione in tutte le cartelle di lavoro di PowerPivot per le quali viene utilizzato. Questo livello di autorizzazione è necessario per aprire la cartella di lavoro da una libreria, quindi per salvarla di nuovo nella libreria dopo aver aggiornato i dati.  
  
 L'assegnazione di autorizzazioni è un passaggio effettuato dall'amministratore della raccolta siti. Le autorizzazioni di SharePoint possono essere assegnate a livello della raccolta siti radice o a qualsiasi livello inferiore, inclusi singoli documenti ed elementi. La modalità di impostazione delle autorizzazioni varierà a seconda del relativo livello di granularità necessario. Nei passaggi seguenti verrà illustrato un approccio di concessione delle autorizzazioni.  
  
1.  In un sito di SharePoint in Azioni sito fare clic su **autorizzazioni sito**.  
  
2.  Fare clic su **Concedi autorizzazioni**.  
  
3.  In Seleziona utenti digitare il nome dell'account utente di dominio Windows designato come l'account automatico PowerPivot. Si tratta del nome dell'account utente di dominio Windows specificato nell'applicazione di destinazione nel servizio di archiviazione sicura.  
  
4.  In Concedi autorizzazioni selezionare **concedere agli utenti autorizzazioni direttamente**.  
  
5.  Selezionare **collaborazione**, quindi fare clic su **OK**.  
  
###  <a name="bkmk_dbread"></a> Passaggio 4: Concessione di autorizzazioni di lettura per accedere alle origini dati esterne utilizzate nell'aggiornamento dati  
 Durante l'importazione di dati in una cartella di lavoro di PowerPivot, le connessioni a dati esterni spesso si basano su connessioni trusted o connessioni rappresentate in cui viene utilizzata l'identità dell'utente corrente per connettersi all'origine dati. Questi tipi di connessioni funzionano solo quando l'utente corrente dispone dell'autorizzazione di lettura per i dati che importa.  
  
 In uno scenario di aggiornamento dati, la stessa stringa di connessione utilizzata per importare i dati viene ora riutilizzata per aggiornare i dati. Se per la stringa di connessione si presuppone l'utente corrente (ad esempio, una stringa in cui è incluso Integrated_Security=SSPI), tramite il servizio di sistema PowerPivot verrà passata l'identità dell'utente dell'account di aggiornamento dati automatico PowerPivot come utente corrente. Questa connessione riuscirà solo se l'account di aggiornamento dati automatico di PowerPivot dispone di autorizzazioni di lettura per l'origine dati esterna.  
  
 Per questo motivo, è necessario concedere le autorizzazioni di sola lettura dell'account di aggiornamento dati automatico PowerPivot per tutte le origini dati esterne utilizzate in qualsiasi operazione di aggiornamento dati nell'account automatico.  
  
 Un amministratore delle origini dati utilizzate nell'organizzazione può creare un account di accesso e assegnare le autorizzazioni necessarie. In caso contrario, è necessario contattare i proprietari dei dati e fornire le informazioni sull'account. Assicurarsi di specificare l'account utente di dominio Windows di cui viene eseguito il mapping all'account di aggiornamento dati automatico PowerPivot. Si tratta dell'account specificato nel "(Step 1): Creare un'applicazione di destinazione e impostare le credenziali"in questo argomento.  
  
###  <a name="bkmk_verify"></a> Passaggio 5: Verificare la disponibilità dell'account nelle pagine di configurazione di aggiornamento dati  
  
1.  Aprire una pagina di configurazione dell'aggiornamento dati per una cartella di lavoro pubblicata che contiene dati PowerPivot. Per istruzioni su come aprire la pagina, vedere [pianificare un aggiornamento dei dati &#40;PowerPivot per SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md).  
  
2.  Verificare che il **utilizza l'aggiornamento dati configurato dall'amministratore account** opzione è abilitata nella pagina di configurazione dell'aggiornamento dati.  
  
3.  Selezionare il **aggiorna anche appena possibile** casella di controllo, quindi fare clic su **OK**.  
  
4.  Nella raccolta che contiene la cartella di lavoro, selezionare la cartella di lavoro, fare clic sulla freccia giù visualizzata a destra e quindi selezionare **Gestisci aggiornamento dati PowerPivot**. Potrebbe essere necessario attendere alcuni minuti se il processo di aggiornamento dati restituisce una grande quantità di dati.  
  
 Se si verifica un errore, è possibile fare clic su **configura pianificazione** nei dati di aggiornare la pagina della cronologia per provare credenziali diverse. Potrebbe inoltre essere necessario analizzare le informazioni di connessione dell'origine dati nella cartella di lavoro originale per visualizzare la stringa di connessione utilizzata durante l'aggiornamento dati. Nella stringa di connessione vengono fornite informazioni sul percorso del server e sul database che è possibile utilizzare per risolvere il problema.  
  
 Per altre informazioni sulla risoluzione dei problemi, vedere [risoluzione dei problemi di aggiornamento dati PowerPivot](https://go.microsoft.com/fwlink/p/?LinkID=223279) su Wiki di TechNet.  
  
##  <a name="bkmk_use"></a> Account con l'aggiornamento dati automatico PowerPivot  
 Delle tre opzioni relative alle credenziali nella pagina della pianificazione dell'aggiornamento dati PowerPivot, solo la prima corrisponde all'account di aggiornamento dati automatico. Selezionare questa opzione quando si imposta la pianificazione dell'aggiornamento dati.  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 Non utilizzare la terza opzione, ovvero quella che richiede l'immissione dell'ID dell'applicazione di destinazione, per accedere all'account di aggiornamento dati automatico PowerPivot. Esiste un ulteriore controllo di rappresentazione che viene eseguito con questa opzione che genera un errore di convalida se si tenta di utilizzarla con l'account di aggiornamento dati automatico PowerPivot (o qualsiasi applicazione di destinazione basata sul tipo di account personale). Per altre informazioni su come utilizzare la terza opzione, vedere [configurare le credenziali archiviate per l'aggiornamento dati PowerPivot &#40;PowerPivot per SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
##  <a name="bkmk_editUA"></a> Aggiornare le credenziali usate da un PowerPivot esistente account di aggiornamento dati automatico  
 Se l'account di aggiornamento dati automatico è già stato configurato tramite l'installazione o da un amministratore, è possibile aggiornare il nome utente o la password modificando l'applicazione di destinazione in cui sono archiviate le credenziali. Si noti che l'identità di Windows originale in precedenza associata all'account di aggiornamento dati automatico PowerPivot non sarà visibile quando si modificano le credenziali nel servizio di archiviazione sicura. Che si intenda aggiornare una password scaduta o specificare un account diverso, è necessario ridigitare sempre il nome utente e la password per l'applicazione di destinazione nel servizio di archiviazione sicura.  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic su **Secure Store Service**.  
  
3.  Selezionare la casella di controllo accanto a **PowerPivotDataRefresh**.  
  
4.  In credenziali fare clic su **impostare**.  
  
5.  Nelle **proprietari credenziali**, digitare un account utente di dominio Windows che si desidera disporre delle autorizzazioni per aggiornare le credenziali. Le credenziali vengono usate per azioni di aggiornamento dati e il **proprietari credenziali** dispone delle autorizzazioni per modificare le credenziali.  
  
6.  In Nome utente digitare l'account utente del dominio di Windows che farà parte delle credenziali dell'aggiornamento dati automatico.  
  
7.  In Password digitare la password per l'account, quindi digitarla nuovamente per confermarla.  
  
8.  Fare clic su **OK**.  
  
 Se si modifica non solo la password, ma anche il nome utente dell'account, è necessario eseguire ulteriori passaggi di configurazione, ad esempio concedere autorizzazioni di lettura a origini dati esterne e autorizzazioni di SharePoint per aggiornare la cartella di lavoro di PowerPivot. Per istruzioni, passare a questo passaggio nella configurazione dell'account di aggiornamento dati automatico PowerPivot: [Passaggio 3: Concessione di autorizzazioni di collaborazione per l'account](#bkmk_grant)e quindi continuare con tutti i passaggi rimanenti e concludere verificando che l'account sia configurato correttamente.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamento dati PowerPivot con SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)   
 [Pianificare un aggiornamento di dati &#40;PowerPivot per SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [Aggiornamento dei dati PowerPivot](power-pivot-sharepoint/power-pivot-data-refresh.md)  
  
  
