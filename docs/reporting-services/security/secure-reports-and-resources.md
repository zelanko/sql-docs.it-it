---
title: Garantire la sicurezza di report e risorse | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services], reports
- security [Reporting Services], resources
- reports [Reporting Services], security
- confidential reports [Reporting Services]
- resources [Reporting Services], security
ms.assetid: 63cd55c7-fd2a-49e3-a3f8-59eb1a1c6e83
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e6ad66da4f9741753db693792edefd808f69b0e9
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65570630"
---
# <a name="secure-reports-and-resources"></a>Garantire la sicurezza di report e risorse
  È possibile impostare la sicurezza per singoli report e risorse e controllare quindi i livelli di accesso concessi ai vari utenti per questi elementi. Per impostazione predefinita, solo i membri del gruppo **Administrators** predefinito possono eseguire report, visualizzare risorse, modificare proprietà ed eliminare elementi. Per tutti gli altri utenti è necessario creare assegnazioni di ruolo che consentano l'accesso a un report o a una risorsa.  
  
## <a name="role-based-access-to-reports-and-resources"></a>Accesso basato sui ruoli a report e risorse  
 Per concedere l'accesso a report e risorse, è possibile consentire agli utenti di ereditare le assegnazioni di ruolo esistenti da una cartella padre oppure creare una nuova assegnazione di ruolo nell'elemento stesso.  
  
 Nella maggior parte dei casi, è probabilmente preferibile utilizzare autorizzazioni ereditate da una cartella padre. L'impostazione della sicurezza per singoli report e risorse è in genere necessaria solo se si desidera nascondere questi elementi agli utenti che non hanno necessità di conoscerne l'esistenza oppure aumentare il livello di accesso all'elemento o al report. Queste due finalità non si escludono a vicenda. È possibile limitare l'accesso a un report a un numero inferiore di utenti e concedere a tutti, o solo ad alcuni, privilegi aggiuntivi per la gestione del report.  
  
 Per ottenere i risultati desiderati, potrebbe essere necessario creare più assegnazioni di ruolo. Si supponga ad esempio che sia necessario rendere accessibile un determinato report agli utenti Ann e Fernando e al gruppo Responsabili risorse umane. Ann e Fernando devono essere in grado di gestire il report, mentre gli utenti del gruppo Responsabili risorse umane devono solo essere autorizzati a eseguirlo. Per gestire queste diverse tipologie di utenti, è necessario creare tre assegnazioni di ruolo distinte: una per assegnare ad Ann il ruolo Gestione contenuto per il report, un'altra per assegnare a Fernando il ruolo Gestione contenuto per il report e la terza per consentire attività di sola lettura al gruppo Responsabili risorse umane.  
  
 Quando si imposta la sicurezza per un report o una risorsa, le impostazioni rimangono associate all'elemento anche se lo si sposta in una nuova posizione. Se, ad esempio, si sposta un report accessibile solo da un numero limitato di utenti, il report rimarrà disponibile solo per tali utenti anche se viene spostato in una cartella con criteri di sicurezza meno restrittivi.  
  
## <a name="mitigating-html-injection-attacks-in-a-published-report-or-document"></a>Riduzione del rischio di attacchi intrusivi nel codice HTML in un documento o in un report pubblicato  
 In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]i report e le risorse vengono elaborati con l'identità di sicurezza dell'utente che sta eseguendo il report. Se il report contiene espressioni, script, elementi del report personalizzati o assembly personalizzati, il codice viene eseguito con le credenziali dell'utente. Se una risorsa è un documento HTML che contiene script, lo script viene eseguito quando l'utente apre il documento nel server di report. La possibilità di eseguire codice o script contenuti in un report è una caratteristica potente che comporta un determinato livello di rischio. Se il codice è dannoso, il server di report e l'utente che sta eseguendo il report sono vulnerabili a un attacco.  
  
 Quando si concede l'accesso a report e risorse elaborati in formato HTML, è importante considerare che i report vengono eseguiti con attendibilità totale e pertanto potrebbero venire inviati al client script potenzialmente dannosi. In base alle impostazioni del browser, il codice HTML viene eseguito dal client con il livello di attendibilità impostato nel browser.  
  
 È possibile ridurre il rischio di esecuzione di script dannosi adottando le precauzioni seguenti:  
  
-   Essere selettivi quando si definiscono gli utenti che possono pubblicare contenuti in un server di report. Poiché esiste la possibilità di pubblicare contenuti dannosi, è necessario limitare gli utenti che possono pubblicare i contenuti a un numero ristretto di utenti trusted.  
  
-   Evitare in tutti i server di pubblicazione la pubblicazione di report e risorse provenienti da origini sconosciute o non attendibili. Se necessario, aprire il file in un editor di testo e verificare se sono presenti URL o script sospetti.  
  
## <a name="report-parameters-and-script-injection"></a>Attacchi intrusivi nei parametri e nel codice di script del report  
 I parametri del report offrono la flessibilità necessaria per la progettazione e l'esecuzione complessive del report. In alcuni casi, questa stessa flessibilità può tuttavia essere sfruttata da un pirata informatico per compiere attacchi luring. Per ridurre il rischio di esecuzione involontaria di script dannosi, aprire esclusivamente i report visualizzabili provenienti da origini attendibili. È consigliabile tenere presente lo scenario seguente che costituisce un potenziale attacco di intrusione nel codice di script del renderer HTML:  
  
1.  Un report contiene una casella di testo in cui l'azione del collegamento ipertestuale è impostata sul valore di un parametro che potrebbe contenere testo dannoso.  
  
2.  Il report viene pubblicato in un server di report oppure viene reso disponibile in un modo che potrebbe consentire il controllo del parametro del report dall'URL di una pagina Web.  
  
3.  Un pirata informatico crea un collegamento alla pagina Web o al server di report specificando il valore del parametro nella forma "javascript:\<script dannoso in questo punto>" e invia tale collegamento a un altro utente nell'ambito di un attacco luring.  
  
## <a name="mitigating-script-injection-attacks-in-a-hyperlink-in-a-published-report-or-document"></a>Riduzione del rischio di attacchi intrusivi nel codice di script in un collegamento ipertestuale all'interno di un report o documento pubblicato  
 I report possono contenere collegamenti ipertestuali incorporati nel valore della proprietà Action all'interno di un elemento del report o di una parte di un elemento del report. Quando il report viene elaborato, i collegamenti ipertestuali possono essere associati ai dati recuperati da un'origine dati esterna. Se un utente malintenzionato modifica i dati sottostanti, il collegamento ipertestuale potrebbe essere a rischio di attacchi al codice di script. Se un utente fa clic sul collegamento nel report pubblicato o esportato, lo script dannoso potrebbe venire eseguito.  
  
 Per ridurre il rischio di includere in un report collegamenti che eseguono inavvertitamente script dannosi, associare collegamenti ipertestuali solo ai dati provenienti da origini attendibili. Verificare che i dati restituiti da query ed espressioni che determinano l'associazione di dati a collegamenti ipertestuali non creino collegamenti che possano essere sfruttati da utenti malintenzionati. Ad esempio, non basare un collegamento ipertestuale su un'espressione che concatena dati da più campi del set di dati. Se necessario, passare al report e utilizzare "Visualizza origine" per verificare la presenza di script e URL sospetti.  
  
## <a name="mitigating-sql-injection-attacks-in-a-parameterized-report"></a>Riduzione del rischio di attacchi intrusivi nel codice SQL in un report con parametri  
 In qualsiasi report che includa un parametro di tipo **String**accertarsi di usare un elenco di valori disponibili, anche detto elenco di valori validi, e assicurarsi che ogni utente che esegue il report disponga solo delle autorizzazioni necessarie per visualizzare i dati del report. Quando si definisce un parametro di tipo **String**, viene visualizzata una casella di testo che può accettare qualsiasi valore. Un elenco di valori disponibili consente di limitare i valori che è possibile immettere. Se un parametro di report è correlato a un parametro di query e non si utilizza un elenco di valori disponibili, un utente potrebbe digitare nella casella di testo sintassi SQL, esponendo il report e il server a un potenziale attacco intrusivo nel codice SQL. Se l'utente dispone di autorizzazioni sufficienti per eseguire la nuova istruzione SQL, è possibile che nel server si verifichino risultati non desiderati.  
  
 Se un parametro di report non è correlato a un parametro di query e i valori del parametro sono inclusi nel report, un utente potrebbe digitare nel valore del parametro un URL o la sintassi di un'espressione ed eseguire il rendering del report in formato Excel o HTML. Se il report viene in seguito visualizzato da un altro utente che fa clic sul contenuto dei parametri di cui è stato eseguito il rendering, è possibile che venga inavvertitamente eseguito il collegamento o lo script dannoso.  
  
 Per ridurre il rischio di eseguire inavvertitamente script dannosi, aprire i report visualizzabili solo da origini attendibili.  
  
> [!NOTE]  
>  Nelle versioni precedenti della documentazione è incluso un esempio di creazione di una query dinamica come espressione. Questo tipo di query crea una vulnerabilità agli attacchi intrusivi nel codice SQL e pertanto non è consigliabile.  
  
## <a name="securing-confidential-reports"></a>sicurezza di report con contenuto riservato  
 È consigliabile proteggere i report che contengono informazioni riservate in corrispondenza del livello di accesso ai dati, richiedendo agli utenti di specificare le credenziali per l'accesso ai dati riservati. Per altre informazioni, vedere [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md). È inoltre possibile proteggere una cartella in modo da renderla inaccessibile agli utenti non autorizzati. Per altre informazioni, vedere [Proteggere le cartelle](../../reporting-services/security/secure-folders.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creare e gestire assegnazioni di ruolo](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [Concessione di autorizzazioni in un server di report in modalità nativa](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Proteggere le origini dei dati condivise](../../reporting-services/security/secure-shared-data-source-items.md)   
 [Archiviare le credenziali in un'origine dati di Reporting Services](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
