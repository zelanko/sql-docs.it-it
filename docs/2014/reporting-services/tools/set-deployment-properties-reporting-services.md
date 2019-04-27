---
title: Impostare le proprietà di distribuzione (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], deploying
- publishing reports [Reporting Services]
- properties [Reporting Services], deployment
- deploying reports [Reporting Services]
ms.assetid: 18201ca0-bf4a-484f-b3a2-95d1046a6a9b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ab927ca95e32f1ad2a34a6e7910dd35a498eec0e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62634465"
---
# <a name="set-deployment-properties-reporting-services"></a>Impostare le proprietà di distribuzione (Reporting Services)
  In[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]è necessario specificare il server di report e facoltativamente le cartelle per i report e le origini dati condivise in modo da poter pubblicare gli elementi di un progetto del server di report in un server di report. Le proprietà e i valori necessari in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] per compilare, visualizzare in anteprima e distribuire i report vengono archiviati nelle configurazioni di progetto del progetto server di report. È possibile creare più set denominati per queste proprietà del progetto, in modo da poter passare da un set di proprietà all'altro in base alle esigenze. Ogni set di proprietà è una configurazione. È possibile ad esempio disporre di una configurazione per la pubblicazione di report in un server di prova e di una configurazione diversa per la pubblicazione di report in un server di produzione.  
  
 Utilizzare Gestione configurazione per creare e gestire set di proprietà del progetto nelle configurazioni di progetto. Gestione configurazione è una caratteristica supportata da [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], su cui si basa [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] .  
  
> [!NOTE]  
>  Non confondere questa caratteristica con Gestione configurazione Reporting Services, utilizzato per configurare Reporting Services dopo l'installazione. Per altre informazioni, vedere [Configurare e amministrare un server di report &#40;modalità nativa SSRS&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md).  
  
> [!NOTE]  
>  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]l'azione di pubblicazione di report da una soluzione o da un progetto server di report è nota come *distribuzione di report*.  
  
### <a name="to-set-deployment-properties"></a>Per impostare le proprietà di distribuzione  
  
1.  Fare clic con il pulsante destro del mouse sul progetto report e quindi scegliere **Proprietà**.  
  
2.  Nella finestra di dialogo **Pagine delle proprietà** del progetto selezionare una configurazione da modificare dall'elenco **Configurazione** . Le configurazioni comuni sono **DebugLocal**, **Debug**e **Release**.  
  
    > [!NOTE]  
    >  È possibile utilizzare più configurazioni per passare velocemente da un server di report a un altro oppure da un'impostazione a un'altra.  
  
3.  Nel **OutputPath** casella di testo digitare o incollare il percorso nel file system locale per archiviare la definizione del report utilizzata nella verifica della compilazione, distribuzione e anteprima dei report. Il percorso deve essere diverso dal percorso utilizzato per il progetto e da un percorso relativo che rappresenta una sottocartella nel percorso del progetto.  
  
4.  Nel **ErrorLevel** casella di testo, digitare la gravità della compilazione problemi vengono segnalati come errori. I livelli di problemi che si verificano durante la creazione di report, origini dati o altre risorse del progetto con gravità minore o uguale al valore di **ErrorLevel** vengono segnalati come errori; in caso contrario, i problemi vengono segnalati come avvisi. Qualsiasi errore comporterà l'interruzione dell'attività di compilazione. I livelli di gravità validi sono compresi tra 0 e 4. Il valore predefinito è 2.  
  
     È possibile usare**ErrorLevel** per aumentare o ridurre la sensibilità della compilazione. Ad esempio, quando viene compilato un report con una mappa durante la distribuzione in un server di report di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] , per impostazione predefinita viene visualizzato un errore e la compilazione del report non viene completata. Se si riduce il valore di **ErrorLevel** , la mappa viene rimossa dal report, viene visualizzato un avviso e la compilazione del report prosegue.  
  
5.  Nel **StartItem** elencare, selezionare un report da visualizzare nella finestra di anteprima o in una finestra del browser quando si esegue il progetto report.  
  
6.  Nell'elenco **OverwriteDataSources** selezionare **True** per sovrascrivere l'origine dati condivisa nel server ogni volta che vengono pubblicate origini dati condivise oppure selezionare **False** per mantenere l'origine dati nel server.  
  
7.  Nel **TargetServerVersion** elencare, selezionare la [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] versione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] oppure selezionare **rileva versione** per determinare automaticamente la versione installata nel il server identificato dal **TargetServer URL** proprietà. Il valore predefinito è **SQL Server 2008 R2**.  
  
     Usare **TargetServerVersion** per personalizzare i report compilati, posizionati nel percorso specificato in OutputPath, per la versione del server di report specificata in **TargetServer URL**.  
  
8.  Nella casella di testo **TargetDataSourceFolder** digitare la cartella del server di report in cui inserire le origini dati condivise pubblicate. Il valore predefinito di **TargetDataSourceFolder** è Origini dati. Se non si specifica alcun valore, le origini dati verranno pubblicate nel percorso specificato in **TargetReportFolder**.  
  
9. Nella casella di testo **TargetReportFolder** digitare la cartella del server di report in cui inserire i report pubblicati. Il valore predefinito per **TargetReportFolder** è il nome del progetto report.  
  
    > [!NOTE]  
    >  Per un server di report in esecuzione in modalità nativa, per poter pubblicare i report nella cartella di destinazione è necessario disporre delle autorizzazioni **Pubblica** , che vengono fornite tramite un'assegnazione di ruolo che esegue il mapping dell'account utente a un ruolo che include operazioni di pubblicazione. Per altre informazioni, vedere [Creare e gestire assegnazioni di ruolo](../security/create-and-manage-role-assignments.md). Per un server di report in esecuzione in modalità integrata SharePoint, è necessario disporre dell'autorizzazione **Membro** o **Proprietario** per il sito di SharePoint. Per altre informazioni, vedere [Informazioni di riferimento sulle autorizzazioni relative a elenchi e siti di SharePoint per gli elementi del server di report](../security/sharepoint-site-and-list-permission-reference-for-report-server-items.md).  
  
10. Nella casella di testo **TargetServerURL** digitare l'URL del server di report di destinazione. Prima di pubblicare un report, è necessario impostare questa proprietà su un URL valido per il server di report. Quando si pubblica in un server di report in esecuzione in modalità nativa, usare l'URL della directory virtuale del server di report, ad esempio http:*//server/serverdireport* o https:*//server/serverdireport*. In questa casella è necessario impostare la directory virtuale del server di report e non di Gestione report.  
  
     Per la pubblicazione su un server di report in cui è attiva la modalità integrata SharePoint, utilizzare l'URL di un sito principale o secondario di SharePoint. Se non si specifica un sito, verrà usato il sito principale predefinito, ad esempio http://*nomeserver*, http://*nomeserver*/*sito* o http://*nomeserver*/*sito*/*sitosecondario*.  
  
### <a name="to-set-configuration-manager-properties"></a>Per impostare le proprietà di Gestione configurazione  
  
1.  Fare clic con il pulsante destro del mouse sul progetto report e quindi scegliere **Proprietà**.  
  
2.  Nella finestra di dialogo **Pagine delle proprietà** del progetto fare clic su **Gestione configurazione**.  
  
3.  Nella finestra di dialogo **Gestione configurazione** selezionare la configurazione da modificare. La configurazione attualmente attiva è visualizzata come **Attiva(***\<configurazione>***)**.  
  
4.  Per ogni progetto nella soluzione, in **Contesti progetto**selezionare o deselezionare la casella di controllo **Compila** o **Distribuisci**.  
  
    > [!NOTE]  
    >  Se si seleziona la casella di controllo **Compila** , Progettazione report compila il progetto report ed esegue il controllo degli errori prima di visualizzare il report in anteprima o di pubblicarlo in un server di report. Se si seleziona la casella di controllo **Distribuisci** , Progettazione report pubblica i report nel server di report in base alle impostazioni delle proprietà di distribuzione. Se non si seleziona la casella di controllo **Distribuisci** , Progettazione report visualizza il report specificato nella proprietà **StartItem** in una finestra di anteprima locale.  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicazione di origini dati e report](../reports/publishing-data-sources-and-reports.md)   
 [Anteprima dei report](../reports/previewing-reports.md)   
 [Guida sensibile al contesto di Progettazione report](report-designer-f1-help.md)   
 [Esempi di URL per elementi di report pubblicati in un server di report in modalità SharePoint &#40;SSRS&#41;](url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [Finestra di dialogo Pagine delle proprietà del progetto](project-property-pages-dialog-box.md)   
 [Pubblicazione dei report in un server di report](../reports/publishing-reports-to-a-report-server.md)  
  
  
