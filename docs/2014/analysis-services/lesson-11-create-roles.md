---
title: 'Lezione 12: Creare ruoli | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 984face4-00fc-46d3-8ae1-9755bf737bdf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4eec5e4f93a085ab784135593c139410f5911e1e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52506769"
---
# <a name="lesson-12-create-roles"></a>Lezione 12: Creazione di ruoli
  In questa lezione verranno creati ruoli. I ruoli forniscono la sicurezza per i dati e gli oggetti del database modello, limitando l'accesso unicamente agli utenti di Windows che sono membri del ruolo. Ogni ruolo è definito con una singola autorizzazione: Nessuna, lettura, lettura ed elaborare, processo o amministratore. È possibile definire i ruoli durante la creazione del modello tramite la finestra di dialogo Gestione ruoli in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Dopo la distribuzione di un modello, è possibile gestire i ruoli tramite [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [Ruoli &#40;SSAS tabulare&#41;](tabular-models/roles-ssas-tabular.md).  
  
> [!NOTE]  
>  La creazione di ruoli non è necessaria per completare questa esercitazione. Per impostazione predefinita, l'account con il quale è stato attualmente effettuato l'accesso dispone di privilegi di amministratore nel modello. Per consentire ad altri utenti nell'organizzazione di esplorare il modello utilizzando un'applicazione client di creazione di report, è tuttavia necessario creare almeno un ruolo che disponga di autorizzazioni di lettura e aggiungere tali utenti come membri.  
  
 Verranno creati tre ruoli:  
  
-   Responsabile vendite - questo ruolo può includere gli utenti dell'organizzazione per il quale si desidera disporre dell'autorizzazione lettura per tutti i dati e oggetti modello.  
  
-   Sales Analyst US: questo ruolo può includere gli utenti dell'organizzazione per il quale si desidera solo essere in grado di esplorare i dati relativi alle vendite negli Stati Uniti (Stati Uniti). Per questo ruolo, si utilizzerà una formula DAX per definire un *Filtro di riga*che consente ai membri di esplorare solo i dati per gli Stati Uniti.  
  
-   Amministratore - questo ruolo può includere gli utenti per cui si desidera avere autorizzazioni di amministratore, che garantisce accesso illimitato e autorizzazioni per eseguire attività amministrative sul database modello.  
  
 Poiché gli account di gruppo e utente di Windows nell'organizzazione sono univoci, è possibile aggiungere account dell'organizzazione specifica ai membri. Tuttavia, per questa esercitazione, è anche possibile lasciare i membri vuoti. Sarà comunque in grado di testare l'effetto di ogni ruolo in un secondo momento nella lezione 12: Analizza in Excel.  
  
 Tempo stimato per il completamento della lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
 Questo argomento fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 11: Creare partizioni](lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Creazione di ruoli  
  
#### <a name="to-create-a-sales-manager-user-role"></a>Per creare un ruolo utente Sales Manager  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]scegliere **Ruoli** dal menu **Modello**.  
  
2.  Nella finestra di dialogo **Gestione ruoli** fare clic su **Nuovo**.  
  
     All'elenco verrà aggiunto un nuovo ruolo con l'autorizzazione Nessuno.  
  
3.  Fare clic sul nuovo ruolo, quindi nella **Name** colonna, rinominare il ruolo in `Internet Sales Manager`.  
  
4.  Nella colonna **Autorizzazioni** fare clic nell'elenco a discesa, quindi selezionare l'autorizzazione **Lettura** .  
  
5.  Facoltativo: Fare clic sulla scheda **Membri** , quindi su **Aggiungi**.  
  
6.  Nella finestra di dialogo **Selezione utenti o gruppi** immettere i gruppi o gli utenti di Windows dell'organizzazione che si desidera includere nel ruolo.  
  
7.  Verificare le opzioni selezionate, quindi fare clic su **OK**  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>Per creare un ruolo utente Sales Analyst US  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]scegliere **Ruoli** dal menu **Modello**.  
  
2.  Nella finestra di dialogo **Gestione ruoli** fare clic su **Nuovo**.  
  
     All'elenco verrà aggiunto un nuovo ruolo con l'autorizzazione Nessuno.  
  
3.  Fare clic sul nuovo ruolo, quindi nella **Name** colonna, rinominare il ruolo in `Internet Sales US`.  
  
4.  Nella colonna **Autorizzazioni** fare clic nell'elenco a discesa, quindi selezionare l'autorizzazione **Lettura** .  
  
5.  Fare clic sulla scheda Filtri di riga, quindi, solo per la tabella **Geography** , digitare la formula seguente nella colonna Filtro DAX:  
  
     `=Geography[Country Region Code] = "US"`  
  
     Una formula di filtro di riga deve essere risolta in un valore booleano (TRUE/FALSE). Con questa formula, si specifica che solo le righe con il valore di Country Region Code "US" sia visibile all'utente.  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
6.  Facoltativo: Fare clic sulla scheda **Membri** , quindi su **Aggiungi**.  
  
7.  Nella finestra di dialogo **Selezione utenti o gruppi** immettere i gruppi o gli utenti di Windows dell'organizzazione che si desidera includere nel ruolo.  
  
8.  Verificare le opzioni selezionate, quindi fare clic su **OK**  
  
#### <a name="to-create-an-administrator-role"></a>Per creare un ruolo di amministratore  
  
1.  Nella finestra di dialogo **Gestione ruoli** fare clic su **Nuovo**.  
  
2.  Fare clic sul nuovo ruolo, quindi nella **Name** colonna, rinominare il ruolo in `Internet Sales Administrator`.  
  
3.  Nella colonna **Autorizzazioni** fare clic nell'elenco a discesa, quindi selezionare l'autorizzazione **Amministratore** .  
  
4.  Fare clic sulla scheda **Membri** , quindi su **Aggiungi**.  
  
5.  Facoltativo: Nella finestra di dialogo **Selezione utenti o gruppi** immettere i gruppi o gli utenti di Windows dell'organizzazione che si desidera includere nel ruolo.  
  
6.  Verificare le opzioni selezionate, quindi fare clic su **OK**  
  
## <a name="next-steps"></a>Passaggi successivi  
 Per continuare questa esercitazione, passare alla lezione successiva: Lezione: [Lezione 13: Analizza in Excel](lesson-12-analyze-in-excel.md).  
  
  
