---
title: Creare e gestire partizioni di modelli tabulari | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7067449c0de9958e98a7a9dc5cc09c7f89f33fa9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472293"
---
# <a name="create-and-manage-tabular-model-partitions"></a>Creare e gestire partizioni di modelli tabulari
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  Le partizioni consentono di dividere una tabella in parti logiche. Ogni partizione può quindi essere elaborata (aggiornata) indipendentemente dalle altre. Le partizioni definite per un modello durante la relativa creazione vengono duplicate in un modello distribuito. Una volta distribuite, tali partizioni possono essere gestite tramite la finestra di dialogo **Partizioni** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o tramite uno script. Nelle attività presentate in questo argomento viene descritto come creare e gestire partizioni per un modello distribuito.  
  
  > [!NOTE]  
>  Partizioni nei modelli tabulari creati al livello di compatibilità 1400 vengono definite utilizzando un'istruzione di query M. Per altre informazioni, vedere [riferimento M](https://msdn.microsoft.com/library/mt211003.aspx). 
>
  
## <a name="tasks"></a>Attività  
 Per creare e gestire partizioni per un database modello tabulare distribuito si utilizzerà la finestra di dialogo **Partizioni** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per visualizzare la finestra di dialogo **Partizioni** , in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]fare clic con il pulsante destro del mouse su una tabella, quindi selezionare **Partizioni**.  
  
###  <a name="bkmk_create_new"></a> Per creare una nuova partizione  
  
1.  Nella finestra di dialogo **Partizioni** fare clic sul pulsante **Nuova** .  
  
2.  In **Nome partizione**digitare un nome per la partizione. Per impostazione predefinita, il nome della partizione predefinita sarà numerato in modo incrementale per ogni nuova partizione.  
  
3.  Nelle **istruzione Query**digitare o incollare un'istruzione di query SQL o M che definisce le colonne e tutte le clausole che si desidera includere nella partizione nella finestra di query.  
  
4.  Per convalidare l'istruzione, fare clic su **Controlla sintassi**.  
  
###  <a name="bkmk_copy"></a> Per copiare una partizione  
  
1.  Nell'elenco **Partizioni** della **relativa finestra** di dialogo selezionare la partizione che si desidera copiare, quindi fare clic sul pulsante **Copia**.   
  
2.  In **Nome partizione**digitare un nuovo nome per la partizione.  
  
3.  Nelle **istruzione Query**, modificare l'istruzione della query.  
  
###  <a name="bkmk_merge"></a> Per unire due o più partizioni  
  
-   Nel **partizioni** nella finestra di dialogo il **partizioni** elenco, usare Ctrl + fare clic per selezionare le partizioni da unire e quindi fare clic sui **Merge** pulsante.  
  
> [!IMPORTANT]  
>  L'unione delle partizioni non consente di aggiornare i metadati della partizione. È necessario modificare l'istruzione SQL o M per la partizione risultante per assicurarsi che tutti i dati nella partizione unita di elaborare le operazioni di elaborazione.  
  
###  <a name="bkmk_delete"></a> Per eliminare una partizione  
  
-   Nell'elenco **Partizioni** della **relativa finestra** di dialogo selezionare la partizione che si desidera eliminare, quindi fare clic sul pulsante **Elimina**.  
  
## <a name="see-also"></a>Vedere anche  
 [Partizioni di modelli tabulari](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Partizioni di modelli tabulari processo](../../analysis-services/tabular-models/process-tabular-model-partitions-ssas-tabular.md)  
  
  
