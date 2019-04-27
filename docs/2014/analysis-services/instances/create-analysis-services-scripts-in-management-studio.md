---
title: Creare script per Analysis Services in Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services objects, scripts
- objects [Analysis Services], scripts
- scripts [Analysis Services], objects
ms.assetid: 4f1b965c-9ca6-427b-8f4d-0ce1eea7c0fe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d419a09c34998165f13fbc9e43c9b561602b69aa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62730208"
---
# <a name="create-analysis-services-scripts-in-management-studio"></a>Creare script per Analysis Services in Management Studio
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] include funzionalità di generazione di script, modelli ed editor che è possibile usare per generare script per oggetti e attività di Analysis Services.  
  
## <a name="script-analysis-services-tasks-in-management-studio"></a>Generare script per attività di Analysis Services in Management Studio  
 La generazione di script per attività in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] viene effettuata facendo clic su una delle opzioni Script in una finestra di dialogo orientata all'attività. Tutte le finestre di dialogo utilizzate per eseguire attività quali backup o ripristino del database, elaborazione di un oggetto o progettazione di un'aggregazione includono un'opzione Script nella parte superiore. La selezione di una di queste opzioni consente di generare uno script XMLA basato sulle informazioni e le impostazioni nella finestra di dialogo.  
  
 Per impostazione predefinita, lo script viene generato e posizionato in un editor di query XMLA, ma è anche possibile espandere l'elenco di opzioni Script per indirizzare lo script in un file o negli Appunti di Windows.  
  
#### <a name="to-script-an-analysis-services-task"></a>Per generare uno script per un'attività di Analysis Services  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse e quindi scegliere **Backup**. Viene aperta la finestra di dialogo Backup database. Specificare un nome per il file di backup e scegliere le opzioni desiderate per questo backup.  
  
3.  Fare clic su **Script** nella parte superiore della finestra di dialogo. La funzionalità Script fa parte di tutte le finestre di dialogo basate su attività in Management Studio. Include le opzioni seguenti: **Creare uno script azione in nuova finestra Query** per aprire la finestra dell'editor di query, **genera Script azione nel File** per salvare lo script XMLA in un file, o **genera Script azione negli Appunti** per salvare lo script XMLA per il Appunti.  
  
     Notare che l'opzione **Genera script azione nel processo** elencata come un'opzione per script in Management Studio non è supportata per gli script di Analysis Services.  
  
4.  Se si seleziona l'opzione predefinita, **Genera script azione in nuova finestra Query**, lo script generato viene posizionato in una finestra di query XMLA.  
  
     È ora possibile chiudere la finestra di dialogo Backup database e modificare o eseguire direttamente lo script XMLA.  
  
## <a name="script-analysis-services-objects-in-management-studio"></a>Generare script per oggetti di Analysis Services in Management Studio  
 Per generare script per oggetti in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è necessario fare clic con il pulsante destro del mouse su un oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e scegliere **Genera codice per istruzione CREATE in**, **Genera codice per istruzione ALTER in**o **Genera codice per istruzione DELETE in**. Ognuno di questi comandi può essere indirizzato a una finestra o un file, ma indipendentemente dalla destinazione dello script, il formato sarà quello di uno script DDL in un wrapper XMLA. Un importante vantaggio offerto da questo tipo di script è che possono essere eseguiti su qualsiasi server specificato. Inoltre, è possibile modificare i nomi negli script ed eseguire gli script in modo iterativo per creare, modificare o eliminare oggetti in massa.  
  
 Tra gli oggetti per i quali è possibile generare script vi sono gli elementi di un database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , inclusi origini dati, viste origine dati, cubi, dimensioni, strutture di data mining e ruoli.  
  
 I prerequisiti includono la comprensione di XML for Analysis (XMLA). In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è disponibile una funzionalità che consente di creare automaticamente lo script XMLA necessario per la creazione di oggetti, ad esempio, i cubi. Questa funzionalità di automazione facilita la riduzione della curva di apprendimento per XMLA. Per altre informazioni su come usare XMLA, vedere [Sviluppo con XMLA in Analysis Services](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md). Per altre informazioni su come usare XMLA, vedere [Sviluppo con XMLA in Analysis Services](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md).  
  
> [!IMPORTANT]  
>  Durante la creazione di script per l'oggetto ruolo, tenere presente che le autorizzazioni di sicurezza sono contenute negli oggetti da esse protetti anziché nel ruolo di sicurezza a cui sono associate.  
  
#### <a name="to-script-analysis-services-objects"></a>Per creare script per gli oggetti di Analysis Services  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
2.  Individuare l'oggetto per cui si desidera creare lo script da utilizzare per creare, modificare o eliminare oggetti.  
  
3.  Pulsante destro del mouse dell'oggetto, scegliere **crea Script per cubo**, scegliere **CREATE in**, **ALTER To**, o **Elimina a**e quindi fare clic su uno del le opzioni seguenti: **Nuova finestra Editor di Query** per aprire la finestra dell'editor di query, **File** per salvare lo script XMLA in un file, o **Appunti** per salvare lo script XMLA negli Appunti.  
  
    > [!NOTE]  
    >  In genere, è consigliabile selezionare **File** per creare più versioni diverse del file.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare script per le attività amministrative in Analysis Services](../script-administrative-tasks-in-analysis-services.md)   
 [Editor di query XMLA &#40;Analysis Services - Dati multidimensionali&#41;](../xmla-query-editor-analysis-services-multidimensional-data.md)  
  
  
