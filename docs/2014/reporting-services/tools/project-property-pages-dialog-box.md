---
title: Finestra di dialogo Pagine delle proprietà del progetto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rpt.rptdesigner.projectpropertypages.general.f1
helpviewer_keywords:
- Project Property Pages dialog box
ms.assetid: 209d9e22-37fc-418f-8739-83adcf447d3f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a76281eead6430ca0dafae8671c7990f3c6c2de3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63201081"
---
# <a name="project-property-pages-dialog-box"></a>pagine delle proprietà del progetto - finestra di dialogo
  Utilizzare le pagine delle proprietà del progetto per configurare le proprietà di distribuzione per un progetto server di report. Per aprire questa finestra di dialogo, dal menu **Progetto** scegliere _\<Nome report progetto>_**Proprietà**.  
  
 Dopo aver definito le proprietà di configurazione, è possibile selezionare una configurazione nell'elenco a discesa **Configurazioni soluzione** sulla barra degli strumenti.  
  
## <a name="options"></a>Opzioni  
 **Configurazione**  
 Consente di selezionare la configurazione da modificare. Inizialmente, sono disponibili le seguenti configurazioni: **Eseguire il debug**, **DebugLocal**, e **versione**. La configurazione attiva viene visualizzata per prima, ad esempio **Active(Debug)**.  
  
 Per visualizzare le proprietà per più configurazioni contemporaneamente, selezionare **Tutte le configurazioni** o **Più configurazioni**.  
  
 Per creare altre configurazioni, fare clic su **Gestione configurazione** sulla barra degli strumenti.  
  
 **Gestione configurazione**  
 Consente di gestire configurazioni per l'intera soluzione o per aggiungere altre configurazioni. Per altre informazioni, vedere la documentazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] .  
  
 **Percorso output**  
 Digitare o incollare il percorso per archiviare la definizione del report utilizzata nella verifica della compilazione, nella distribuzione e nell'anteprima dei report. Il percorso deve essere diverso dal percorso utilizzato per il progetto e da un percorso relativo che rappresenta una sottocartella nel percorso del progetto.  
  
> [!NOTE]  
>  È possibile utilizzare più configurazioni per passare fra i percorsi a seconda dell'attività che viene eseguita.  
  
 **ErrorLevel**  
 Immettere la gravità dei problemi di compilazione segnalati come errori. I problemi con livelli di gravità minori o uguali al valore di **ErrorLevel** vengono segnalati come errori; in caso contrario, vengono segnalati come avvisi. Qualsiasi errore comporterà l'interruzione dell'attività di compilazione. I livelli di gravità validi sono compresi tra 0 e 4. Il valore predefinito è 2.  
  
 **StartItem**  
 Selezionare il report visualizzato nel browser dopo la pubblicazione del progetto nel server di report oppure nella finestra di anteprima quando il progetto viene eseguito in locale. È necessario specificare un elemento iniziale per le configurazioni che comportano la compilazione ma non la distribuzione di un progetto e per l'uso del comando **Debug** (**F5**). Tale elemento è necessario per le configurazioni che comportano la distribuzione del progetto.  
  
 **OverwriteDataSources**  
 Selezionare **True** per sovrascrivere l'origine dati nel server con l'origine dati nel progetto durante la pubblicazione dei report. Selezionare **False** per lasciare l'origine dati esistente nel server.  
  
 **TargetServerVersion**  
 Selezionare il [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] oppure [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] versione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] oppure selezionare **rileva versione** per determinare automaticamente la versione installata nel server identificata dal **TargetServer URL** proprietà. Il valore predefinito è **SQL Server 2008 R2**.  
  
 **TargetDataSourceFolder**  
 Nome della cartella nella quale archiviare le origini dei dati pubblicate. Se non si specifica una cartella, l'origine dei dati viene pubblicata nella stessa cartella del report. Se la cartella non esiste nel server di report, verrà creata durante la pubblicazione dei report.  
  
 Quando si pubblica in un server di report in esecuzione in modalità nativa, specificare il percorso completo della gerarchia di cartelle a partire dalla radice. Ad esempio, Folder1/Folder2/Folder3.  
  
 Per la pubblicazione su un server di report in cui è attiva la modalità integrata SharePoint, utilizzare l'URL della raccolta di SharePoint. Ad esempio, http://*\<nomeserver > /\<sito >*/documenti/MyFolder.  
  
 **TargetReportFolder**  
 Nome della cartella nella quale archiviare i report pubblicati. Per impostazione predefinita, corrisponde al nome del progetto report. Se la cartella non esiste nel server di report, verrà creata durante la pubblicazione dei report.  
  
 Quando si pubblica in un server di report in esecuzione in modalità nativa, specificare il percorso completo della gerarchia di cartelle a partire dalla radice. Se una cartella si trova all'interno di un'altra cartella, includere il percorso della cartella a partire dalla radice, ad esempio Cartella1/Cartella2/Cartella3.  
  
 Per la pubblicazione su un server di report in cui è attiva la modalità integrata SharePoint, utilizzare l'URL della raccolta di SharePoint. Ad esempio, http://*\<nomeserver >*/*\<sito >*/documenti/MyFolder.  
  
 **TargetServerURL**  
 URL del server di report di destinazione. Prima di pubblicare un report, è necessario impostare questa proprietà su un URL valido per il server di report.  
  
 Quando si pubblica in un server di report in esecuzione in modalità nativa, utilizzare l'URL della directory virtuale del server di report. Ad esempio, http://\<server > / reportserver. In questa casella è necessario impostare la directory virtuale del server di report e non di Gestione report. Per impostazione predefinita, il server di report viene installato in una directory virtuale denominata "reportserver".  
  
 Per la pubblicazione su un server di report in cui è attiva la modalità integrata SharePoint, utilizzare l'URL di un sito principale o secondario di SharePoint. Se non si specifica un sito, verrà utilizzato il sito principale predefinito, Ad esempio, http://\<*nomeserver >*, http://&lt*servername*/\<*sito >* o http://\< *servername >*/\<*site >*/\<*sitosecondario >*.  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicazione di report](../publish-reports.md)   
 [Pubblicare un report in una raccolta di SharePoint](../reports/publish-a-report-to-a-sharepoint-library.md)   
 [Impostare le proprietà di distribuzione &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md)   
 [Guida sensibile al contesto di Progettazione report](report-designer-f1-help.md)  
  
  
