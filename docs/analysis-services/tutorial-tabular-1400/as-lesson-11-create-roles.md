---
title: 'Analysis Services tutorial-lezione 11: Creare ruoli | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfiles"
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 6466eca2be66a20dfcab23f2097b71a2d0fc1cec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148943"
---
# <a name="create-roles"></a>Creazione di ruoli

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In questa lezione verranno creati ruoli. I ruoli forniscono protezione dati e oggetti del database modello, limitando l'accesso solo agli utenti che sono membri del ruolo. Ogni ruolo è definito con una singola autorizzazione: Nessuna, lettura, lettura ed elaborare, processo o amministratore. I ruoli possono essere definiti durante la creazione di modelli tramite Gestione ruoli. Dopo aver distribuito un modello, è possibile gestire ruoli tramite SQL Server Management Studio (SSMS). Per altre informazioni, vedere [Modello](../tabular-models/roles-ssas-tabular.md).
  
> [!NOTE]  
> La creazione di ruoli non è necessaria per completare questa esercitazione. Per impostazione predefinita, l'account che è stato effettuato con privilegi di amministratore per il modello. Per altri utenti nell'organizzazione esplorare utilizzando uno strumento client, tuttavia, è necessario creare almeno un ruolo con autorizzazioni lettura e aggiungere tali utenti come membri.  
  
Vengono creati tre ruoli:  
  
-   **Responsabile vendite** -questo ruolo può includere gli utenti dell'organizzazione per il quale si desidera disporre dell'autorizzazione lettura per tutti i dati e oggetti modello.  
  
-   **Sales Analyst US** -questo ruolo può includere gli utenti dell'organizzazione per il quale si desidera solo essere in grado di esplorare i dati relativi alle vendite negli Stati Uniti. Per questo ruolo, utilizzare una formula DAX per definire un *filtro di riga*, che consente ai membri di esplorare i dati solo per gli Stati Uniti.  
  
-   **Amministratore** -questo ruolo può includere gli utenti per cui si desidera avere autorizzazioni di amministratore, che garantisce accesso illimitato e autorizzazioni per eseguire attività amministrative sul database modello.  
  
Poiché gli account di gruppo e utente di Windows nell'organizzazione sono univoci, è possibile aggiungere account dell'organizzazione specifica ai membri. Tuttavia, per questa esercitazione, è anche possibile lasciare i membri vuoti. Testare l'effetto di ogni ruolo in un secondo momento nella lezione 12: Analizza in Excel.  
  
Tempo stimato per il completamento della lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  

Questo articolo fa parte di un'esercitazione di modellazione tabulare, che deve essere completata nell'ordine. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 10: Creare partizioni](../tutorial-tabular-1400/as-lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Creazione di ruoli  
  
#### <a name="to-create-a-sales-manager-user-role"></a>Per creare un ruolo utente Sales Manager  
  
1.  In Esplora modelli tabulari, fare doppio clic su **ruoli** > **ruoli**.  
  
2.  In Gestione ruoli fare clic su **New**.  
  
3.  Fare clic sul nuovo ruolo e quindi il **nome** colonna, rinominare il ruolo **Sales Manager**.  
  
4.  Nella colonna **Autorizzazioni** fare clic nell'elenco a discesa, quindi selezionare l'autorizzazione **Lettura** . 

    ![as-lesson11-new-role](../tutorial-tabular-1400/media/as-lesson11-new-role.png) 
  
5.  Facoltativo: Scegliere il **membri** scheda e quindi fare clic su **Add**. Nella finestra di dialogo **Selezione utenti o gruppi** immettere i gruppi o gli utenti di Windows dell'organizzazione che si desidera includere nel ruolo.  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>Per creare un ruolo utente Sales Analyst US  
  
1.  In Gestione ruoli fare clic su **New**.    
  
2.  Rinominare il ruolo **Sales Analyst US**.  
  
3.  Assegnare a questo ruolo **lettura** l'autorizzazione.  
  
4.  Fare clic sulla scheda filtri di riga e quindi per la **DimGeography** tabella solo nella colonna filtro DAX digitare la formula seguente:  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    Una formula di filtro di riga deve essere risolta in un valore booleano (TRUE/FALSE). Con questa formula, si specifica che solo le righe con il valore di Country Region Code "US" sono visibili all'utente.  
    ![as-lesson11-role-filter](../tutorial-tabular-1400/media/as-lesson11-role-filter.png) 
  
6.  Facoltativo: Scegliere il **membri** scheda e quindi fare clic su **Add**. Nella finestra di dialogo **Selezione utenti o gruppi** immettere i gruppi o gli utenti di Windows dell'organizzazione che si desidera includere nel ruolo.  
  
#### <a name="to-create-an-administrator-user-role"></a>Per creare un ruolo utente amministratore  
  
1.  Fare clic su **Nuovo**.  
  
2.  Rinominare il ruolo **amministratore**.  
  
3.  Assegnare a questo ruolo **amministratore** l'autorizzazione.  
  
4.  Facoltativo: Scegliere il **membri** scheda e quindi fare clic su **Add**. Nella finestra di dialogo **Selezione utenti o gruppi** immettere i gruppi o gli utenti di Windows dell'organizzazione che si desidera includere nel ruolo. 
  
  
## <a name="whats-next"></a>Quali sono le operazioni successive?

[Lezione 12: Analizza in Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md).

  
  
