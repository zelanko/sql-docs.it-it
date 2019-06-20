---
title: Creare e gestire i ruoli nei modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3723d83fb28f6d2824be921906326d719e705478
ms.sourcegitcommit: a6949111461eda0cc9a71689f86b517de3c5d4c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263407"
---
# <a name="create-and-manage-roles"></a>Creare e gestire ruoli 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  I ruoli, nei modelli tabulari, consentono di definire le autorizzazioni dei membri per un modello. I ruoli vengono definiti per un progetto di modello tramite la finestra di dialogo Gestione ruoli di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. 

> [!IMPORTANT]
> Se si distribuisce il progetto in Azure Analysis Services, usare **area di lavoro integrata** come il database dell'area di lavoro. Per altre informazioni, vedere [database dell'area di lavoro](workspace-database-ssas-tabular.md).
  
 L'attività in questo articolo viene descritto come creare e gestire i ruoli durante la creazione di modelli tramite la finestra di dialogo Gestione ruoli in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Per informazioni sulla gestione dei ruoli in un database modello distribuito, vedere [ruoli nei modelli tabulari](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md).  
  
## <a name="tasks"></a>Attività  
 Per creare, modificare, copiare ed eliminare ruoli, usare la finestra di dialogo **Gestione ruoli** . Per visualizzare la finestra di dialogo **Gestione ruoli** di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], fare clic sul menu **Modello** e quindi su **Gestione ruoli**.  
  
###  <a name="bkmk_new_role"></a> Per creare un nuovo ruolo  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]fare clic sul menu **Modello** e quindi su **Gestione ruoli**.  
  
2.  Nella finestra di dialogo **Gestione ruoli** fare clic su **Nuovo**.  
  
     All'elenco Ruoli verrà aggiunto un nuovo ruolo evidenziato.  
  
3.  Nel campo **Nome** dell'elenco **Ruoli** digitare un nome per il ruolo.  
  
     Per impostazione predefinita, il nome del ruolo predefinito sarà numerato in modo incrementale per ogni nuovo ruolo. È consigliabile digitare un nome che consente di identificare chiaramente il tipo di membro, ad esempio Responsabili finanze o Esperti di risorse umane.  
  
4.  Nel campo **Autorizzazioni** fare clic sulla freccia GIÙ e quindi selezionare uno dei tipi di autorizzazioni seguenti:  
  
    |Autorizzazione|Descrizione|  
    |----------------|-----------------|  
    |**None**|I membri non possono apportare alcuna modifica allo schema del modello, né eseguire query sui dati.|  
    |**Lettura**|I membri possono eseguire query sui dati in base ai filtri di riga, ma non possono apportare alcuna modifica allo schema del modello.|  
    |**Lettura ed elaborazione**|I membri possono eseguire query sui dati in base ai filtri a livello di riga ed effettuare le operazioni relative alle opzioni Elabora ed Elabora tutto, ma non possono apportare alcuna modifica allo schema del modello.|  
    |**Process**|I membri possono effettuare le operazioni relative alle opzioni Elabora ed Elabora tutto, ma non possono modificare lo schema del modello, né eseguire query sui dati.|  
    |**Amministratore**|I membri possono apportare modifiche allo schema del modello ed eseguire query su tutti i dati.|  
  
5.  Per immettere una descrizione per il ruolo, fare clic sul campo **Descrizione** e quindi digitare una descrizione.  
  
6.  Se il ruolo in fase di creazione dispone dell'autorizzazione Lettura o di lettura ed elaborazione, è possibile aggiungere filtri di riga utilizzando una formula DAX. Per aggiungere filtri di riga, fare clic sulla scheda **Filtri di riga** , selezionare una tabella, fare clic sul campo **Filtro DAX** e quindi digitare una formula DAX.  
  
7.  Per aggiungere membri al ruolo, fare clic sulla scheda **Membri** e quindi fare clic su **Aggiungi**.  
  
    > [!NOTE]  
    >  I membri dei ruoli possono anche essere aggiunti a un modello distribuito tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [gestire ruoli tramite SSMS](../../analysis-services/tabular-models/manage-roles-by-using-ssms-ssas-tabular.md).  
  
8.  Nella finestra di dialogo **Selezione utenti o gruppi** immettere oggetti utente o gruppo di Windows come membri.  
  
9. Scegliere **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Ruoli](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [Prospettive](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Modello](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)   
 [Funzione USERNAME (DAX)](/dax/username-function-dax)   
 [Funzione CUSTOMDATA (DAX)](/dax/customdata-function-dax)  
  
  
