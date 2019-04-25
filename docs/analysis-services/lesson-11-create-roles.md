---
title: 'Lezione 12: Creare ruoli | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a2f507e9f22e4d090407b0b0849f69a8e7914e8d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62469136"
---
# <a name="lesson-11-create-roles"></a>Lezione 11: Creazione di ruoli
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In questa lezione verranno creati ruoli. I ruoli forniscono la sicurezza per i dati e gli oggetti del database modello, limitando l'accesso unicamente agli utenti di Windows che sono membri del ruolo. Ogni ruolo è definito con una singola autorizzazione: Nessuna, lettura, lettura ed elaborare, processo o amministratore. I ruoli possono essere definiti durante la creazione di modelli tramite Gestione ruoli. Dopo la distribuzione di un modello, è possibile gestire i ruoli tramite [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [Modello](../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
> [!NOTE]  
> La creazione di ruoli non è necessaria per completare questa esercitazione. Per impostazione predefinita, l'account con il quale è stato attualmente effettuato l'accesso dispone di privilegi di amministratore nel modello. Tuttavia, per consentire ad altri utenti nell'organizzazione di esplorare il modello usando uno strumento client, è necessario creare almeno un ruolo con autorizzazioni lettura e aggiungere tali utenti come membri.  
  
Verranno creati tre ruoli:  
  
-   **Responsabile vendite** -questo ruolo può includere gli utenti dell'organizzazione per il quale si desidera disporre dell'autorizzazione lettura per tutti i dati e oggetti modello.  
  
-   **Sales Analyst US** -questo ruolo può includere gli utenti dell'organizzazione per il quale si desidera solo essere in grado di esplorare i dati relativi alle vendite negli Stati Uniti. Per questo ruolo, si utilizzerà una formula DAX per definire un *Filtro di riga*che consente ai membri di esplorare solo i dati per gli Stati Uniti.  
  
-   **Amministratore** -questo ruolo può includere gli utenti per cui si desidera avere autorizzazioni di amministratore, che garantisce accesso illimitato e autorizzazioni per eseguire attività amministrative sul database modello.  
  
Poiché gli account di gruppo e utente di Windows nell'organizzazione sono univoci, è possibile aggiungere account dell'organizzazione specifica ai membri. Tuttavia, per questa esercitazione, è anche possibile lasciare i membri vuoti. Sarà comunque in grado di testare l'effetto di ogni ruolo in un secondo momento nella lezione 12: Analizza in Excel.  
  
Tempo stimato per il completamento della lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 10: Creare partizioni](../analysis-services/lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Creazione di ruoli  
  
#### <a name="to-create-a-sales-manager-user-role"></a>Per creare un ruolo utente Sales Manager  
  
1.  In Esplora modelli tabulari, fare doppio clic su **ruoli** > **ruoli**.  
  
2.  In Gestione ruoli fare clic su **New**.  
  
3.  Fare clic sul nuovo ruolo, quindi nella **Name** colonna, rinominare il ruolo **responsabile vendite**.  
  
4.  Nella colonna **Autorizzazioni** fare clic nell'elenco a discesa, quindi selezionare l'autorizzazione **Lettura** . 

    ![as-tabular-lesson11-new-role](../analysis-services/media/as-tabular-lesson11-new-role.png) 
  
5.  Facoltativo: Scegliere il **membri** scheda e quindi fare clic su **Add**. Nella finestra di dialogo **Selezione utenti o gruppi** immettere i gruppi o gli utenti di Windows dell'organizzazione che si desidera includere nel ruolo.  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>Per creare un ruolo utente Sales Analyst US  
  
1.  In Gestione ruoli fare clic su **New**.    
  
2.  Rinominare il ruolo **Sales Analyst US**.  
  
3.  Assegnare a questo ruolo **lettura** l'autorizzazione.  
  
4.  Fare clic sulla scheda filtri di riga, quindi per la **DimGeography** tabella solo nella colonna filtro DAX digitare la formula seguente:  
  
    ```
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    Una formula di filtro di riga deve essere risolta in un valore booleano (TRUE/FALSE). Con questa formula, si specifica che solo le righe con il valore di Country Region Code "US" sia visibile all'utente.  
    ![as-tabular-lesson11-role-filter](../analysis-services/media/as-tabular-lesson11-role-filter.png) 
  
6.  Facoltativo: Fare clic sulla scheda **Membri** , quindi su **Aggiungi**. Nella finestra di dialogo **Selezione utenti o gruppi** immettere i gruppi o gli utenti di Windows dell'organizzazione che si desidera includere nel ruolo.  
  
#### <a name="to-create-an-administrator-user-role"></a>Per creare un ruolo utente amministratore  
  
1.  Fare clic su **Nuovo**.  
  
2.  Rinominare il ruolo **amministratore**.  
  
3.  Assegnare a questo ruolo **amministratore** l'autorizzazione.  
  
4.  Facoltativo: Fare clic sulla scheda **Membri** , quindi su **Aggiungi**. Nella finestra di dialogo **Selezione utenti o gruppi** immettere i gruppi o gli utenti di Windows dell'organizzazione che si desidera includere nel ruolo. 
  
  
## <a name="whats-next"></a>Quali sono le operazioni successive?
Passare alla lezione successiva: [Lezione 12: Analizza in Excel](../analysis-services/lesson-12-analyze-in-excel.md).

  
  
