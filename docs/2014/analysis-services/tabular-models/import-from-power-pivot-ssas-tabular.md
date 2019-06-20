---
title: Importare da PowerPivot (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.importfromppt.f1
ms.assetid: ac1a6a79-bda3-4122-a717-8b1e2f77da02
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 941155a5e434457cdf9c79bd25c653c7207937a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067023"
---
# <a name="import-from-powerpivot-ssas-tabular"></a>Importare da PowerPivot (SSAS tabulare)
  In questo argomento viene descritto come creare un nuovo progetto di modello tabulare importando i metadati e i dati da una cartella di lavoro di PowerPivot tramite il modello di progetto Importa da PowerPivot disponibile in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="create-a-new-tabular-model-from-a-powerpivot-for-excel-file"></a>Creare un nuovo modello tabulare da un file di PowerPivot per Excel  
 Quando si crea un nuovo progetto di modello tabulare eseguendo un'importazione da una cartella di lavoro di PowerPivot, i metadati medianti i quali viene definita la struttura della cartella di lavoro vengono utilizzati per creare e definire la struttura del progetto di modello tabulare in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Oggetti quali tabelle, colonne, misure e relazioni vengono mantenuti e la relativa visualizzazione nel progetto di modello tabulare sarà uguale a quella della cartella di lavoro di PowerPivot. Non viene apportata alcuna modifica al file della cartella di lavoro con estensione xlsx.  
  
> [!NOTE]  
>  I modelli tabulari non supportano le tabelle collegate. Quando si esegue un'importazione da una cartella di lavoro di PowerPivot contenente una tabella collegata, i dati di tale tabella vengono considerati come dati copiati o incollati e vengono archiviati nel file Model.bim. Quando si visualizzano le proprietà per una tabella copiata o incollata, la proprietà **Origine dati** e la finestra di dialogo **Proprietà tabella** nel menu **Tabella** sono disabilitate.  
>   
>  Esiste un limite di 10.000 righe che è possibile aggiungere ai dati incorporati nel modello. Se si importa un modello da PowerPivot e viene visualizzato l'errore "dati troncati. Tabelle incollate non possono contenere più di 10000 righe"è necessario esaminare il modello PowerPivot spostando i dati incorporati in un'altra origine dati, ad esempio una tabella in SQL Server e quindi ripetere l'importazione.  
  
 Vi sono considerazioni speciali a seconda se il database dell'area di lavoro si trovi o meno in un'istanza di Analysis Services sullo stesso computer (locale) di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o in un'istanza di Analysis Services remota.  
  
 Se il database dell'area di lavoro è in un'istanza locale di Analysis Services, è possibile importare sia i metadati sia i dati dalla cartella di lavoro di PowerPivot. I metadati vengono copiati dalla cartella di lavoro e utilizzati per creare il progetto di modello tabulare. I dati vengono quindi copiati dalla cartella di lavoro e archiviati nel database dell'area di lavoro del progetto (tranne i dati copiati o incollati, che viene archiviati nel file Model. bim).  
  
 Se il database dell'area di lavoro si trova in un'istanza remota di Analysis Services, non è possibile importare dati da una cartella di lavoro di PowerPivot per Excel. È comunque possibile importare i metadati della cartella di lavoro; tuttavia, questa operazione causerà l'esecuzione di uno script nell'istanza remota di Analysis Services. È consigliabile importare solo i metadati da una cartella di lavoro di PowerPivot attendibile. I dati devono essere importati nuovamente da origini definite nelle connessioni all'origine dati. I dati della tabella collegata copiati o incollati nella cartella di lavoro di PowerPivot devono essere copiati e incollati nel progetto di modello tabulare.  
  
#### <a name="to-create-a-new-tabular-model-project-from-a-powerpivot-for-excel-file"></a>Per creare un nuovo progetto di modello tabulare da un file di PowerPivot per Excel  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.  
  
2.  Nel **nuovo progetto** nella finestra di dialogo **modelli installati**, fare clic su **Business Intelligence**, quindi fare clic su **Importa da PowerPivot**.  
  
3.  In  **Nome**digitare un nome per il progetto, quindi specificare un percorso e un nome per la soluzione e scegliere **OK**.  
  
4.  Nella finestra di dialogo **Apri** selezionare il file di [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] in cui sono contenuti i metadati e i dati del modello da importare, quindi fare clic su **Apri**.  
  
## <a name="see-also"></a>Vedere anche  
 [Database dell'area di lavoro &#40;SSAS tabulare&#41;](workspace-database-ssas-tabular.md)   
 [Copiare e incollare dati &#40;SSAS tabulare&#41;](../copy-and-paste-data-ssas-tabular.md)  
  
  
