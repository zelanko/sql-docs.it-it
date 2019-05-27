---
title: Gestire ruoli tramite (SSAS TABULARE) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 652faac0-1cfc-438b-8119-2f4b090a2381
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 098d9b589396ebd6a9c622f921efd97d0b000929
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067041"
---
# <a name="manage-roles-by-using-ssms-ssas-tabular"></a>Gestire ruoli tramite (SSAS tabulare)
  È possibile creare, modificare e gestire ruoli per un modello tabulare distribuito tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Attività dell'argomento:  
  
-   [Per creare un nuovo ruolo](#bkmk_new_role)  
  
-   [Per copiare un ruolo](#bkmk_copy_role)  
  
-   [Per modificare un ruolo](#bkmk_edit_role)  
  
-   [Per eliminare un ruolo](#bkmk_deletet_role)  
  
> [!CAUTION]  
>  La ridistribuzione di un progetto di modello tabulare con i ruoli definiti tramite Gestione ruoli in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] sovrascriverà i ruoli definiti in un modello tabulare distribuito.  
  
> [!CAUTION]  
>  L'utilizzo di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per gestire un database dell'area di lavoro del modello tabulare mentre il progetto di modello è aperto in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] può causare il danneggiamento del file Model.bim. Quando si creano e gestiscono ruoli per un database dell'area di lavoro del modello tabulare, utilizzare Gestione ruoli di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
###  <a name="bkmk_new_role"></a> Per creare un nuovo ruolo  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]espandere il database del modello tabulare per cui si vuole creare un nuovo ruolo, fare clic con il pulsante destro del mouse su **Ruoli**e quindi fare clic su **Nuovo ruolo**.  
  
2.  Nella finestra Selezione pagina della finestra di dialogo **Crea ruolo** fare clic su **Generale**.  
  
3.  Nel campo **Nome** della finestra delle impostazioni generali digitare un nome per il ruolo.  
  
     Per impostazione predefinita, il nome del ruolo predefinito sarà numerato in modo incrementale per ogni nuovo ruolo. È consigliabile digitare un nome che consente di identificare chiaramente il tipo di membro, ad esempio Responsabili finanze o Esperti di risorse umane.  
  
4.  In **Impostare le autorizzazioni del ruolo per il database**selezionare una delle opzioni delle autorizzazioni seguenti:  
  
    |Autorizzazione|Descrizione|  
    |----------------|-----------------|  
    |**Controllo completo (amministratore)**|I membri possono apportare modifiche allo schema del modello e visualizzare tutti i dati.|  
    |**Elaborazione database**|I membri possono effettuare le operazioni relative alle opzioni Elabora ed Elabora tutto, ma non possono modificare lo schema del modello, né visualizzare dati.|  
    |**Lettura**|I membri possono visualizzare i dati in base ai filtri di riga, ma non possono apportare alcuna modifica allo schema del modello.|  
  
5.  Nella finestra Selezione pagina della finestra di dialogo **Crea ruolo** fare clic su **Appartenenze**.  
  
6.  Nella finestra delle impostazioni di appartenenza fare clic su **Aggiungi**e quindi, nella finestra di dialogo **Seleziona utenti o gruppi** , aggiungere gli utenti o i gruppi di Windows che si vuole aggiungere come membri.  
  
7.  Se il ruolo in fase di creazione dispone dell'autorizzazione Lettura, è possibile aggiungere filtri di riga per qualsiasi tabella utilizzando una formula DAX. Per aggiungere filtri di riga, il **proprietà ruolo - \<rolename >** nella finestra di dialogo **seleziona una pagina**, fare clic su **filtri di riga**.  
  
8.  Nella finestra filtri di riga, selezionare una tabella, quindi fare clic sul **filtro DAX** campo, quindi nel **filtro DAX - \<NomeTabella >** digitare una formula DAX.  
  
    > [!NOTE]  
    >  Filtro DAX - \<NomeTabella > campo non contiene un editor di query di completamento automatico o funzione caratteristica di inserimento. Per usare il completamento automatico quando si scrive una formula DAX, è necessario usare un editor di formule DAX in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
9. Fare clic su **OK** per salvare il ruolo.  
  
###  <a name="bkmk_copy_role"></a> Per copiare un ruolo  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]espandere il database del modello tabulare che contiene il ruolo da copiare, espandere **Ruoli**, quindi fare clic con il pulsante destro del mouse sul ruolo e fare clic su **Duplica**.  
  
###  <a name="bkmk_edit_role"></a> Per modificare un ruolo  
  
-   In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]espandere il database del modello tabulare che contiene il ruolo da modificare, espandere **Ruoli**, quindi fare clic con il pulsante destro del mouse sul ruolo e fare clic su **Proprietà**.  
  
     Nel **le proprietà del ruolo** \<rolename > finestra di dialogo, è possibile modificare le autorizzazioni, aggiungere o rimuovere membri e i filtri di riga aggiunta/modifica.  
  
###  <a name="bkmk_deletet_role"></a> Per eliminare un ruolo  
  
-   In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]espandere il database del modello tabulare che contiene il ruolo da eliminare, espandere **Ruoli**, quindi fare clic con il pulsante destro del mouse sul ruolo e fare clic su **Elimina**.  
  
## <a name="see-also"></a>Vedere anche  
 [Ruoli &#40;SSAS tabulare&#41;](roles-ssas-tabular.md)  
  
  
