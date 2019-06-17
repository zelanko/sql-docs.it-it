---
title: Creare e gestire ruoli (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.rolemanager.f1
- sql12.asvs.bidtoolset.roledb.f1
ms.assetid: e23d27a8-e968-4082-9dbe-963fc724b5d9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 664f0cdc9f01bf27e8f20c6799097948b0c100c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067471"
---
# <a name="create-and-manage-roles-ssas-tabular"></a>Creare e gestire ruoli (SSAS tabulare)
  I ruoli, nei modelli tabulari, consentono di definire le autorizzazioni dei membri per un modello. I ruoli vengono definiti per un progetto di modello tramite la finestra di dialogo Gestione ruoli di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Quando viene distribuito un modello, gli amministratori del database possono gestire i ruoli tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Le attività di questo argomento descrivono come creare e gestire i ruoli durante la creazione di modelli tramite la finestra di dialogo Gestione ruoli in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Per altre informazioni sulla gestione dei ruoli in un database modello distribuito, vedere [Ruoli nei modelli tabulari &#40;SSAS Tabulare&#41;](roles-ssas-tabular.md).  
  
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
    >  I membri dei ruoli possono anche essere aggiunti a un modello distribuito tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [Gestire ruoli tramite SSMS &#40;SSAS tabulare&#41;](manage-roles-by-using-ssms-ssas-tabular.md).  
  
8.  Nella finestra di dialogo **Selezione utenti o gruppi** immettere oggetti utente o gruppo di Windows come membri.  
  
9. Scegliere **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Ruoli &#40;SSAS tabulare&#41;](roles-ssas-tabular.md)   
 [Prospettive &#40;SSAS tabulare&#41;](perspectives-ssas-tabular.md)   
 [Analizzare in Excel &#40;SSAS tabulare&#41;](analyze-in-excel-ssas-tabular.md)   
 [USERNAME Function &#40;DAX&#41;](https://msdn.microsoft.com/library/hh230954.aspx)   
 [Funzione CUSTOMDATA &#40;DAX&#41;](https://msdn.microsoft.com/library/hh213140.aspx)  
  
  
