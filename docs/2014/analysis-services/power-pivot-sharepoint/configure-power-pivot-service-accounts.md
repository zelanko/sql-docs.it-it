---
title: Configurare gli account del servizio PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 76a85cd0-af93-40c9-9adf-9eb0f80b30c1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2883427b45cb408323db91935ebbccee0792825f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52526658"
---
# <a name="configure-powerpivot-service-accounts"></a>Configurare gli account del servizio PowerPivot
  In un'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] sono inclusi due servizi che supportano le operazioni server. Il **SQL Server Analysis Services (PowerPivot)** è un servizio Windows che fornisce l'elaborazione dei dati PowerPivot e supporto query in un server applicazioni. L'account di accesso per questo servizio viene sempre specificato durante l'installazione di SQL Server quando si installa Analysis Services in modalità integrata SharePoint.  
  
 È necessario specificare un secondo account per l'applicazione del servizio PowerPivot, un servizio Web condiviso eseguito in un'identità del pool di applicazioni in una farm SharePoint. Questo account viene specificato quando si configura un'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] usando lo strumento di configurazione PowerPivot o PowerShell.  
  
 Ogni servizio deve essere eseguito in un account dedicato in modo da poter controllare le connessioni o abilitare il protocollo di autenticazione Kerberos nella farm.  
  
 Dopo aver impostato gli account di servizio, eventuali modifiche a uno di questi account devono essere apportate tramite Amministrazione centrale SharePoint. Se si usano strumenti alternativi (quali l'applicazione console Servizi, Gestione IIS o Gestione configurazione SQL Server), le autorizzazioni non saranno aggiornate per l'accesso al database nella farm o per l'accesso al file locale sul server fisico.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Aggiornare una password scaduta per l'istanza di SQL Server Analysis Services (PowerPivot)](#bkmk_passwordssas)  
  
 [Aggiornare una password scaduta per l'applicazione di servizio PowerPivot](configure-power-pivot-service-accounts.md#bkmk_passwordapp)  
  
 [Modificare l'account usato per l'esecuzione di ogni servizio](#bkmk_newacct)  
  
 [Creare o modificare il pool di applicazioni per un'applicazione di servizio PowerPivot](#bkmk_appPool)  
  
 [Requisiti e autorizzazioni relativi all'account](#requirements)  
  
 [Risoluzione dei problemi: Concedere manualmente autorizzazioni amministrative](#updatemanually)  
  
 [Risoluzione dei problemi: Risolvere HTTP 503 errori dovuti alle password scadute per amministrazione centrale o SharePoint Foundation al servizio dell'applicazione Web](#expired)  
  
##  <a name="bkmk_passwordssas"></a> Aggiornare una password scaduta per l'istanza di SQL Server Analysis Services (PowerPivot)  
  
1.  Fare clic sul pulsante Start, scegliere **Strumenti di amministrazione**, quindi fare clic su **Servizi**. Fare doppio clic su **SQL Server Analysis Services (PowerPivot)**. Scegliere **Accesso**, quindi immettere la nuova password per l'account.  
  
2.  Nella sezione Sicurezza di Amministrazione centrale scegliere **Configura account gestiti**.  
  
3.  Fare clic su **Modifica** per modificare un account specifico.  
  
4.  Selezionare **Cambia password**.  
  
5.  Selezionare **Imposta password account sul nuovo valore**. In tutti i servizi eseguiti nell'account gestito verranno usate le credenziali aggiornate.  
  
##  <a name="bkmk_passwordapp"></a> Aggiornare una password scaduta per l'applicazione di servizio PowerPivot  
  
1.  Nella sezione Sicurezza di Amministrazione centrale scegliere **Configura account gestiti**.  
  
2.  Fare clic su **Modifica** per modificare un account specifico.  
  
3.  Selezionare **Cambia password**.  
  
4.  Selezionare **Imposta password account sul nuovo valore**. In tutti i servizi eseguiti nell'account gestito verranno usate le credenziali aggiornate.  
  
##  <a name="bkmk_newacct"></a> Modificare l'account usato per l'esecuzione di ogni servizio  
  
1.  Nella sezione Sicurezza di Amministrazione centrale scegliere **Configura account di servizio**.  
  
2.  Selezionare **Windows Service - SQL Server Analysis Services** (Servizio Windows - SQL Server Analysis Services) per modificare l'account del servizio Analysis Services.  
  
3.  In **Selezionare un account per questo servizio**scegliere un account gestito esistente o crearne uno nuovo. L'account deve essere un account utente di dominio.  
  
4.  Selezionare **Pool di applicazioni di servizio - sistema dei servizi Web SharePoint** per modificare l'identità del pool di applicazione di servizio PowerPivot predefinita. A seconda della modalità di configurazione dell'installazione, il servizio potrebbe essere eseguito in un pool di applicazioni del servizio esistente creato per i servizi SharePoint. Per impostazione predefinita, lo strumento di configurazione PowerPivot registrare il servizio come **applicazione di servizio PowerPivot predefinita (applicazione del servizio PowerPivot)**.  
  
     Se il servizio è stato configurato manualmente da un amministratore di SharePoint, in esso è molto probabilmente disponibile un relativo pool di applicazioni.  
  
5.  In **Selezionare un account per questo servizio**scegliere un account gestito esistente o crearne uno nuovo. L'account deve essere un account utente di dominio.  
  
6.  Fare clic su **OK**.  
  
##  <a name="bkmk_appPool"></a> Creare o modificare il pool di applicazioni per un'applicazione di servizio PowerPivot  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Selezionare l'applicazione del servizio PowerPivot (ma non fare clic su di essa). Se si fa clic sul nome dell'applicazione viene aperto il dashboard di gestione PowerPivot in cui non è incluso alcun collegamento alla pagina delle proprietà in cui è specificato il pool di applicazioni.  È possibile fare clic sullo spazio vuoto nella riga oppure sul nome del tipo per selezionare l'applicazione del servizio PowerPivot.  
  
3.  Sulla barra multifunzione fare clic su **Proprietà** .  
  
4.  Selezionare **Crea un nuovo pool di applicazioni**. Specificare un nome per il pool di applicazioni e un account gestito per la relativa identità.  
  
##  <a name="requirements"></a> Requisiti e autorizzazioni relativi all'account  
 Quando si pianifica una distribuzione di PowerPivot per SharePoint, è necessario pianificare i seguenti account di servizio.  
  
-   Account del servizio Analysis Services. Analysis Services consente di elaborare query e processi di aggiornamento dei dati PowerPivot nella farm. Questo account viene sempre specificato durante l'installazione di SQL Server quando si installa PowerPivot per SharePoint.  
  
-   Pool di applicazioni di servizio PowerPivot. Un'applicazione del servizio PowerPivot è associata a un servizio di sistema PowerPivot che fornisce l'infrastruttura e l'integrazione SharePoint per l'elaborazione di query PowerPivot in una farm. Il pool di applicazioni specificato per un'applicazione del servizio PowerPivot è l'identità di servizio del servizio di sistema PowerPivot. È possibile disporre di più applicazioni di servizio PowerPivot in una farm. Ognuna di queste applicazioni create deve essere eseguita nel relativo pool di applicazioni.  
  
#### <a name="analysis-services-service-account"></a>Account del servizio Analysis Services  
  
|Requisito|Descrizione|  
|-----------------|-----------------|  
|Requisito di provisioning|Questo account deve essere specificato durante l'installazione di SQL Server usando il **Analysis Services - pagina di configurazione** nell'installazione guidata (o `ASSVCACCOUNT` parametro di installazione in un'installazione dalla riga di comando).<br /><br /> È possibile modificare il nome utente o la password tramite Amministrazione centrale, PowerShell o lo strumento di configurazione PowerPivot. Non è consentito usare altri strumenti per modificare account e password.|  
|Requisito dell'account utente di dominio|Questo account deve essere un account utente di dominio Windows. Gli account del computer predefiniti, ad esempio Servizio di rete o Servizio locale, non sono consentiti. Tramite il programma di installazione di SQL Server viene applicato il requisito dell'account utente di dominio bloccando l'installazione ogni volta che viene specificato un account computer.|  
|Requisiti relativi alle autorizzazioni|Questo account deve essere un membro di SQLServerMSASUser$\<server > gruppo di sicurezza $PowerPivot e i gruppi di sicurezza WSS_WPG nel computer locale. Queste autorizzazioni devono essere concesse automaticamente. Per altre informazioni su come controllare o concedere le autorizzazioni, vedere [concedere PowerPivot Service Account manualmente le autorizzazioni amministrative](#updatemanually) in questo argomento e [iniziale di configurazione &#40;PowerPivot per SharePoint &#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md).|  
|Requisiti relativi alla distribuzione con scalabilità orizzontale|Se si installano più istanze del server PowerPivot per SharePoint in una farm, tutte le istanze del server Analysis Services devono essere in esecuzione con lo stesso account utente di dominio. Se si configura, ad esempio, l'esecuzione della prima istanza del [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] come Contoso\ssas-srv01, anche tutte le istanze del [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] aggiuntive distribuite successivamente nella stessa farm devono essere eseguite come Contoso\ssas-srv01 (o qualsiasi altro account corrente).<br /><br /> La configurazione dell'esecuzione di tutte le istanze del servizio con lo stesso account consente al servizio di sistema PowerPivot di allocare l'elaborazione di query o i processi di aggiornamento dei dati a qualsiasi istanza del servizio Analysis Services nella farm. Inoltre, consente l'utilizzo della funzionalità relativa all'account gestito in Amministrazione centrale per le istanze del server Analysis Services. Usando lo stesso account per tutte le istanze del [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] , è possibile modificare l'account o la password una volta, mentre tutte le istanze del servizio in cui vengono usate quelle credenziali vengono aggiornate automaticamente.<br /><br /> Il programma di installazione di SQL Server consente di applicare il requisito dello stesso account. In una distribuzione con scalabilità orizzontale in cui una farm di SharePoint dispone già di un'istanza di PowerPivot per SharePoint installata, la nuova installazione verrà bloccata dal programma di installazione se l'account del [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] specificato è diverso da quello già usato nella farm.|  
  
#### <a name="powerpivot-service-application-pool"></a>Pool di applicazioni del servizio PowerPivot  
  
|Requisito|Descrizione|  
|-----------------|-----------------|  
|Requisito di provisioning|Il servizio di sistema PowerPivot è una risorsa condivisa nella farm che diventa disponibile quando si crea un'applicazione di servizio. Il pool di applicazioni del servizio deve essere specificato quando viene creata l'applicazione di servizio. Può essere specificato in due modi, cioè tramite lo strumento di configurazione PowerPivot o i comandi PowerShell.<br /><br /> È probabile che l'identità del pool di applicazioni sia stata configurata in modo da essere eseguita in un account univoco. Ma se non è stato fatto, è consigliabile modificarla ora per l'esecuzione con un account diverso.|  
|Requisito dell'account utente di dominio|Questa identità del pool di applicazioni deve essere un account utente di dominio Windows. Gli account del computer predefiniti, ad esempio Servizio di rete o Servizio locale, non sono consentiti.|  
|Requisiti relativi alle autorizzazioni|Per questo account non sono richieste autorizzazioni di amministratore di sistema locale nel computer. Questo account deve, tuttavia, disporre delle autorizzazioni dell'amministratore di sistema di Analysis Services nel [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] locale installato nello stesso computer. Queste autorizzazioni vengono concesse automaticamente dal programma di installazione di SQL Server o quando si imposta o modifica l'identità del pool di applicazioni in Amministrazione centrale.<br /><br /> Le autorizzazioni amministrative sono necessarie per inoltrare query al [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]. Sono necessarie anche per il monitoraggio dell'integrità, per la chiusura di sessioni inattive e per l'attesa degli eventi di traccia.<br /><br /> L'account deve disporre di autorizzazioni di connessione, lettura e scrittura per il database dell'applicazione del servizio PowerPivot. Queste autorizzazioni vengono concesse automaticamente quando si crea l'applicazione e aggiornate automaticamente quando si modificano gli account o le password in Amministrazione centrale.<br /><br /> L'applicazione del servizio PowerPivot verifica che un utente SharePoint sia autorizzato a visualizzare i dati prima di recuperare il file, ma non rappresenta l'utente. Non esistono requisiti relativi alle autorizzazioni per la rappresentazione.|  
|Requisiti relativi alla distribuzione con scalabilità orizzontale|Nessuna.|  
  
##  <a name="updatemanually"></a> Risoluzione dei problemi: Concedere manualmente le autorizzazioni amministrative  
 Le autorizzazioni amministrative non vengono aggiornate se l'utente che aggiorna le credenziali non è l'amministratore locale del computer. In questo caso, è possibile concedere manualmente le autorizzazioni amministrative. Il modo più semplice per eseguire questa operazione consiste nell'eseguire Processo timer configurazione PowerPivot in Amministrazione centrale. In questo modo è possibile reimpostare le autorizzazioni per tutti i server PowerPivot nella farm. Si noti che questo approccio funziona solo se il processo timer SharePoint è in esecuzione come amministratore della farm e come amministratore locale nel computer.  
  
1.  In Monitoraggio scegliere **Rivedi definizioni processi**.  
  
2.  Selezionare **processo Timer configurazione PowerPivot**.  
  
3.  Fare clic su **Esegui**.  
  
 Come ultima risorsa, è possibile assicurare autorizzazioni corrette concedendo le autorizzazioni Amministrazione sistema di Analysis Services all'applicazione di servizio PowerPivot e quindi aggiungere specificamente l'identità dell'applicazione di servizio SQLServerMSASUser$\< NomeServer > gruppo di sicurezza di Windows $PowerPivot. È necessario ripetere questi passaggi per ogni istanza di Analysis Services integrata con la farm SharePoint.  
  
 È necessario essere un amministratore locale per poter aggiornare i gruppi di sicurezza di Windows.  
  
1.  In SQL Server Management Studio, connettersi all'istanza di Analysis Services come \<nome server > \powerpivot.  
  
2.  Fare clic con il pulsante destro del mouse sul nome del server e scegliere **Proprietà**.  
  
3.  Fare clic su **Sicurezza**.  
  
4.  Scegliere **Aggiungi**.  
  
5.  Digitare il nome dell'account che viene usato per pool di applicazioni di servizio PowerPivot e quindi fare clic su **OK**.  
  
6.  Da Strumenti di amministrazione scegliere **Gestione computer**.  
  
7.  Aprire **Utenti e gruppi locali**.  
  
8.  Aprire **Gruppi**.  
  
9. Double-click SQLServerMSASUser$\<servername>$PowerPivot.  
  
10. Scegliere **Aggiungi**.  
  
11. Digitare il nome dell'account che viene usato per pool di applicazioni di servizio PowerPivot e quindi fare clic su **OK**.  
  
##  <a name="expired"></a> Risoluzione dei problemi: Risolvere gli errori HTTP 503 dovuti alle password scadute per Amministrazione centrale o il servizio di applicazione Web di SharePoint  
 Se il servizio Amministrazione centrale o il servizio di applicazione Web di SharePoint Foundation smettono di funzionare a causa della reimpostazione di un account o della scadenza di una password, verrà generato un messaggio di errore HTTP 503 "Servizio non disponibile" quando si tenta di aprire Amministrazione centrale SharePoint o un sito di SharePoint. Per riportare online il server, eseguire le operazioni seguenti: Quando Amministrazione centrale è disponibile, è possibile aggiornare le informazioni scadute relative all'account.  
  
1.  In Strumenti di amministrazione fare clic su **Gestione Internet Information Services**.  
  
2.  Se l'identità del sito o del pool di applicazioni di Amministrazione centrale è un account utente di dominio la cui password è scaduta, eseguire le operazioni seguenti:  
  
    1.  Fare clic con il pulsante destro del mouse sul nome del pool di applicazioni e selezionare **Impostazioni avanzate**.  
  
    2.  Selezionare **identità** e scegliere il... per aprire la finestra di dialogo identità Pool di applicazioni.  
  
    3.  Fare clic su **Imposta**.  
  
    4.  Digitare un nome utente e una password.  
  
3.  Eseguire IISRESET. A tale scopo, aprire un prompt dei comandi Amministratore e digitare `iisreset`.  
  
4.  Nella sezione Sicurezza di Amministrazione centrale di SharePoint scegliere **Configura account gestiti**.  
  
5.  Fare clic su **Modifica** per aggiornare le informazioni dell'account gestito con la password scaduta.  
  
6.  Selezionare **Cambia password**.  
  
7.  Fare clic su **Usa password esistente**.  
  
8.  Digitare la password, quindi fare clic su **OK**.  
  
 Se Reporting Services è installato, usare Gestione configurazione Reporting Services per aggiornare le password per il server di report e la connessione al database del server di report. Per altre informazioni, vedere [Configurazione e amministrazione di un server di report &#40;modalità SharePoint di Reporting Services&#41;](../../reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare o arrestare un PowerPivot per SharePoint Server](start-or-stop-a-power-pivot-for-sharepoint-server.md)   
 [Configurare PowerPivot Account di aggiornamento dati automatico &#40;PowerPivot per SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)  
  
  
