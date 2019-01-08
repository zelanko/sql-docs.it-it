---
title: Configurare gli account del servizio PowerPivot | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 55eb472ef14e980f77a47a2c6989031cebec91e9
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52509546"
---
# <a name="configure-power-pivot-service-accounts"></a>Configurare gli account del servizio PowerPivot
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In un'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]sono inclusi due servizi che supportano le operazioni server. **SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])** è un servizio Windows che offre funzionalità di elaborazione dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e di supporto query in un server applicazioni. L'account di accesso per questo servizio viene sempre specificato durante l'installazione di SQL Server quando si installa Analysis Services in modalità integrata SharePoint.  
  
 È necessario specificare un secondo account per l'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , un servizio Web condiviso eseguito in un'identità del pool di applicazioni in una farm SharePoint. Questo account viene specificato quando si configura un'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]usando lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o PowerShell.  
  
 Ogni servizio deve essere eseguito in un account dedicato in modo da poter controllare le connessioni o abilitare il protocollo di autenticazione Kerberos nella farm.  
  
 Dopo aver impostato gli account di servizio, eventuali modifiche a uno di questi account devono essere apportate tramite Amministrazione centrale SharePoint. Se si usano strumenti alternativi (quali l'applicazione console Servizi, Gestione IIS o Gestione configurazione SQL Server), le autorizzazioni non saranno aggiornate per l'accesso al database nella farm o per l'accesso al file locale sul server fisico.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Aggiornare una password scaduta per un'istanza di SQL Server Analysis Services (PowerPivot)](#bkmk_passwordssas)  
  
 [Aggiornare una password scaduta per l'applicazione del servizio PowerPivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md#bkmk_passwordapp)  
  
 [Modificare l'account usato per l'esecuzione di ogni servizio](#bkmk_newacct)  
  
 [Creare o modificare il pool di applicazioni per un'applicazione del servizio PowerPivot](#bkmk_appPool)  
  
 [Requisiti e autorizzazioni relativi all'account](#requirements)  
  
 [Risoluzione dei problemi: Concedere manualmente autorizzazioni amministrative](#updatemanually)  
  
 [Risoluzione dei problemi: Risolvere HTTP 503 errori dovuti alle password scadute per amministrazione centrale o SharePoint Foundation al servizio dell'applicazione Web](#expired)  
  
##  <a name="bkmk_passwordssas"></a> Aggiornare una password scaduta per un'istanza di SQL Server Analysis Services (PowerPivot)  
  
1.  Fare clic sul pulsante Start, scegliere **Strumenti di amministrazione**, quindi fare clic su **Servizi**. Fare doppio clic su **SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])**. Scegliere **Accesso**, quindi immettere la nuova password per l'account.  
  
2.  Nella sezione Sicurezza di Amministrazione centrale scegliere **Configura account gestiti**.  
  
3.  Fare clic su **Modifica** per modificare un account specifico.  
  
4.  Selezionare **Cambia password**.  
  
5.  Selezionare **Imposta password account sul nuovo valore**. In tutti i servizi eseguiti nell'account gestito verranno usate le credenziali aggiornate.  
  
##  <a name="bkmk_passwordapp"></a> Aggiornare una password scaduta per l'applicazione del servizio PowerPivot  
  
1.  Nella sezione Sicurezza di Amministrazione centrale scegliere **Configura account gestiti**.  
  
2.  Fare clic su **Modifica** per modificare un account specifico.  
  
3.  Selezionare **Cambia password**.  
  
4.  Selezionare **Imposta password account sul nuovo valore**. In tutti i servizi eseguiti nell'account gestito verranno usate le credenziali aggiornate.  
  
##  <a name="bkmk_newacct"></a> Modificare l'account usato per l'esecuzione di ogni servizio  
  
1.  Nella sezione Sicurezza di Amministrazione centrale scegliere **Configura account di servizio**.  
  
2.  Selezionare **Windows Service - SQL Server Analysis Services** (Servizio Windows - SQL Server Analysis Services) per modificare l'account del servizio Analysis Services.  
  
3.  In **Selezionare un account per questo servizio**scegliere un account gestito esistente o crearne uno nuovo. L'account deve essere un account utente di dominio.  
  
4.  Selezionare **Service Application Pool - SharePoint Web Services System** (Pool di applicazioni di servizio - Sistema dei servizi Web di SharePoint) per modificare l'identità del pool di applicazioni dell'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] predefinito. A seconda della modalità di configurazione dell'installazione, il servizio potrebbe essere eseguito in un pool di applicazioni del servizio esistente creato per i servizi SharePoint. Per impostazione predefinita, lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] consente di registrare il servizio come **Default [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Service Application ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Service Application)** (Applicazione del servizio PowerPivot predefinita (applicazione del servizio PowerPivot)).  
  
     Se il servizio è stato configurato manualmente da un amministratore di SharePoint, in esso è molto probabilmente disponibile un relativo pool di applicazioni.  
  
5.  In **Selezionare un account per questo servizio**scegliere un account gestito esistente o crearne uno nuovo. L'account deve essere un account utente di dominio.  
  
6.  Fare clic su **OK**.  
  
##  <a name="bkmk_appPool"></a> Creare o modificare il pool di applicazioni per un'applicazione del servizio PowerPivot  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Selezionare l'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ma non fare clic su di essa. Se si fa clic sul nome dell'applicazione viene aperto il dashboard di gestione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in cui non è incluso alcun collegamento alla pagina delle proprietà in cui è specificato il pool di applicazioni.  È possibile fare clic sullo spazio vuoto nella riga oppure sul nome del tipo per selezionare l'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
3.  Sulla barra multifunzione fare clic su **Proprietà** .  
  
4.  Selezionare **Crea un nuovo pool di applicazioni**. Specificare un nome per il pool di applicazioni e un account gestito per la relativa identità.  
  
##  <a name="requirements"></a> Requisiti e autorizzazioni relativi all'account  
 Quando si pianifica una distribuzione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint, è necessario pianificare gli account di servizio seguenti.  
  
-   Account del servizio Analysis Services. Analysis Services consente di elaborare query e processi di aggiornamento dei dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nella farm. Questo account viene sempre specificato durante l'installazione di SQL Server quando si installa [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint.  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Un'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] è associata a un servizio di sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] che fornisce l'infrastruttura e l'integrazione SharePoint per l'elaborazione di query [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in una farm. Il pool di applicazioni specificato per un'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] è l'identità di servizio del servizio di sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . È possibile avere più applicazioni del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in una farm. Ognuna di queste applicazioni create deve essere eseguita nel relativo pool di applicazioni.  
  
#### <a name="analysis-services-service-account"></a>Account del servizio Analysis Services  
  
|Requisito|Descrizione|  
|-----------------|-----------------|  
|Requisito di provisioning|Questo account deve essere specificato durante l'installazione di SQL Server nella pagina **Configurazione di Analysis Services** dell'installazione guidata o nel parametro di installazione **ASSVCACCOUNT** in un'installazione dalla riga di comando.<br /><br /> È possibile modificare il nome utente o la password tramite Amministrazione centrale, PowerShell o lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Non è consentito usare altri strumenti per modificare account e password.|  
|Requisito dell'account utente di dominio|Questo account deve essere un account utente di dominio Windows. Gli account del computer predefiniti, ad esempio Servizio di rete o Servizio locale, non sono consentiti. Tramite il programma di installazione di SQL Server viene applicato il requisito dell'account utente di dominio bloccando l'installazione ogni volta che viene specificato un account computer.|  
|Requisiti relativi alle autorizzazioni|Questo account deve essere un membro di SQLServerMSASUser$\<server > gruppo di sicurezza $PowerPivot e i gruppi di sicurezza WSS_WPG nel computer locale. Queste autorizzazioni devono essere concesse automaticamente. Per altre informazioni sul controllo o la concessione delle autorizzazioni, vedere [Concedere manualmente le autorizzazioni amministrative dell'account di servizio PowerPivot](#updatemanually) in questo argomento e [Configurazione iniziale (PowerPivot per SharePoint)](http://msdn.microsoft.com/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146).|  
|Requisiti relativi alla distribuzione con scalabilità orizzontale|Se si installano più istanze del server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint in una farm, tutte le istanze del server Analysis Services devono essere in esecuzione con lo stesso account utente di dominio. Se si configura, ad esempio, l'esecuzione della prima istanza del [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] come Contoso\ssas-srv01, anche tutte le istanze del [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] aggiuntive distribuite successivamente nella stessa farm devono essere eseguite come Contoso\ssas-srv01 (o qualsiasi altro account corrente).<br /><br /> La configurazione dell'esecuzione di tutte le istanze del servizio con lo stesso account consente al servizio di sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] di allocare l'elaborazione di query o i processi di aggiornamento dei dati a qualsiasi istanza del servizio Analysis Services nella farm. Inoltre, consente l'utilizzo della funzionalità relativa all'account gestito in Amministrazione centrale per le istanze del server Analysis Services. Usando lo stesso account per tutte le istanze del [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] , è possibile modificare l'account o la password una volta, mentre tutte le istanze del servizio in cui vengono usate quelle credenziali vengono aggiornate automaticamente.<br /><br /> Il programma di installazione di SQL Server consente di applicare il requisito dello stesso account. In una distribuzione con scalabilità orizzontale in cui una farm di SharePoint ha già un'istanza di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint installata, la nuova installazione verrà bloccata dal programma di installazione se l'account del [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] specificato è diverso da quello già usato nella farm.|  
  
#### <a name="power-pivot-service-application-pool"></a>Pool di applicazioni del servizio PowerPivot  
  
|Requisito|Descrizione|  
|-----------------|-----------------|  
|Requisito di provisioning|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] è una risorsa condivisa nella farm che diventa disponibile quando si crea un'applicazione del servizio. Il pool di applicazioni del servizio deve essere specificato quando viene creata l'applicazione di servizio. Può essere specificato in due modi, cioè tramite lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o i comandi PowerShell.<br /><br /> È probabile che l'identità del pool di applicazioni sia stata configurata in modo da essere eseguita in un account univoco. Ma se non è stato fatto, è consigliabile modificarla ora per l'esecuzione con un account diverso.|  
|Requisito dell'account utente di dominio|Questa identità del pool di applicazioni deve essere un account utente di dominio Windows. Gli account del computer predefiniti, ad esempio Servizio di rete o Servizio locale, non sono consentiti.|  
|Requisiti relativi alle autorizzazioni|Per questo account non sono richieste autorizzazioni di amministratore di sistema locale nel computer. Questo account deve, tuttavia, disporre delle autorizzazioni dell'amministratore di sistema di Analysis Services nel [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] locale installato nello stesso computer. Queste autorizzazioni vengono concesse automaticamente dal programma di installazione di SQL Server o quando si imposta o modifica l'identità del pool di applicazioni in Amministrazione centrale.<br /><br /> Le autorizzazioni amministrative sono necessarie per inoltrare query al [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]. Sono necessarie anche per il monitoraggio dell'integrità, per la chiusura di sessioni inattive e per l'attesa degli eventi di traccia.<br /><br /> L'account deve disporre di autorizzazioni di connessione, lettura e scrittura per il database dell'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Queste autorizzazioni vengono concesse automaticamente quando si crea l'applicazione e aggiornate automaticamente quando si modificano gli account o le password in Amministrazione centrale.<br /><br /> L'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] verifica che un utente SharePoint sia autorizzato a visualizzare i dati prima di recuperare il file, ma non rappresenta l'utente. Non esistono requisiti relativi alle autorizzazioni per la rappresentazione.|  
|Requisiti relativi alla distribuzione con scalabilità orizzontale|Nessuna.|  
  
##  <a name="updatemanually"></a> Risoluzione dei problemi: Concedere manualmente le autorizzazioni amministrative  
 Le autorizzazioni amministrative non vengono aggiornate se l'utente che aggiorna le credenziali non è l'amministratore locale del computer. In questo caso, è possibile concedere manualmente le autorizzazioni amministrative. Il modo più semplice per eseguire questa operazione consiste nell'eseguire Processo timer configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in Amministrazione centrale. In questo modo è possibile reimpostare le autorizzazioni per tutti i server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nella farm. Si noti che questo approccio funziona solo se il processo timer SharePoint è in esecuzione come amministratore della farm e come amministratore locale nel computer.  
  
1.  In Monitoraggio scegliere **Rivedi definizioni processi**.  
  
2.  Selezionare **Processo timer configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**.  
  
3.  Fare clic su **Esegui**.  
  
 Come ultima risorsa, è possibile assicurare autorizzazioni corrette concedendo le autorizzazioni Amministrazione sistema di Analysis Services per il [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] applicazione di servizio e quindi aggiungere specificamente l'identità dell'applicazione di servizio SQLServerMSASUser$\<servername > gruppo di sicurezza di Windows $PowerPivot. È necessario ripetere questi passaggi per ogni istanza di Analysis Services integrata con la farm SharePoint.  
  
 È necessario essere un amministratore locale per poter aggiornare i gruppi di sicurezza di Windows.  
  
1.  In SQL Server Management Studio, connettersi all'istanza di Analysis Services come \<nome server > \powerpivot.  
  
2.  Fare clic con il pulsante destro del mouse sul nome del server e scegliere **Proprietà**.  
  
3.  Fare clic su **Sicurezza**.  
  
4.  Scegliere **Aggiungi**.  
  
5.  Digitare il nome dell'account usato per il pool di applicazioni del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , quindi fare clic su **OK**.  
  
6.  Da Strumenti di amministrazione scegliere **Gestione computer**.  
  
7.  Aprire **Utenti e gruppi locali**.  
  
8.  Aprire **Gruppi**.  
  
9. Double-click SQLServerMSASUser$\<servername>$PowerPivot.  
  
10. Scegliere **Aggiungi**.  
  
11. Digitare il nome dell'account usato per il pool di applicazioni del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , quindi fare clic su **OK**.  
  
##  <a name="expired"></a> Risoluzione dei problemi: Risolvere gli errori HTTP 503 dovuti alle password scadute per Amministrazione centrale o il servizio di applicazione Web di SharePoint  
 Se il servizio Amministrazione centrale o il servizio di applicazione Web di SharePoint Foundation smettono di funzionare a causa della reimpostazione di un account o della scadenza di una password, verrà generato un messaggio di errore HTTP 503 "Servizio non disponibile" quando si tenta di aprire Amministrazione centrale SharePoint o un sito di SharePoint. Per riportare online il server, eseguire le operazioni seguenti: Quando Amministrazione centrale è disponibile, è possibile aggiornare le informazioni scadute relative all'account.  
  
1.  In Strumenti di amministrazione fare clic su **Gestione Internet Information Services**.  
  
2.  Se l'identità del sito o del pool di applicazioni di Amministrazione centrale è un account utente di dominio la cui password è scaduta, eseguire le operazioni seguenti:  
  
    1.  Fare clic con il pulsante destro del mouse sul nome del pool di applicazioni e selezionare **Impostazioni avanzate**.  
  
    2.  Selezionare **identità** e scegliere il... per aprire la finestra di dialogo identità Pool di applicazioni.  
  
    3.  Fare clic su **Imposta**.  
  
    4.  Digitare un nome utente e una password.  
  
3.  Eseguire IISRESET. A tale scopo, aprire un prompt dei comandi Amministratore e digitare **iisreset** .  
  
4.  Nella sezione Sicurezza di Amministrazione centrale di SharePoint scegliere **Configura account gestiti**.  
  
5.  Fare clic su **Modifica** per aggiornare le informazioni dell'account gestito con la password scaduta.  
  
6.  Selezionare **Cambia password**.  
  
7.  Fare clic su **Usa password esistente**.  
  
8.  Digitare la password, quindi fare clic su **OK**.  
  
 Se Reporting Services è installato, usare Gestione configurazione Reporting Services per aggiornare le password per il server di report e la connessione al database del server di report. Per altre informazioni, vedere [Configurazione e amministrazione di un server di report &#40;modalità SharePoint di Reporting Services&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare o arrestare un server Power Pivot per SharePoint](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md)   
 [Configurare l'account di aggiornamento dati automatico PowerPivot (PowerPivot per SharePoint)](http://msdn.microsoft.com/81401eac-c619-4fad-ad3e-599e7a6f8493)  
  
  
