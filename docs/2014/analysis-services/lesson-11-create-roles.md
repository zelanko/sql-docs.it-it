---
title: 'Lezione 12: creare ruoli | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 984face4-00fc-46d3-8ae1-9755bf737bdf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec4bad8ef036e8f19ce0a856f3d9c04bafd0e7c5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66079272"
---
# <a name="lesson-12-create-roles"></a>Lezione 12: Creazione di ruoli
  In questa lezione verranno creati ruoli. I ruoli forniscono la sicurezza per i dati e gli oggetti del database modello, limitando l'accesso unicamente agli utenti di Windows che sono membri del ruolo. Ogni ruolo è definito con una sola autorizzazione: Nessuna, Lettura, Lettura ed elaborazione, Elaborazione o Amministratore. È possibile definire i ruoli durante la creazione del modello tramite la finestra di dialogo Gestione ruoli in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Dopo la distribuzione di un modello, è possibile gestire i ruoli tramite [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [Ruoli &#40;SSAS tabulare&#41;](tabular-models/roles-ssas-tabular.md).  
  
> [!NOTE]  
>  La creazione di ruoli non è necessaria per completare questa esercitazione. Per impostazione predefinita, l'account con cui si esegue l'accesso avrà i privilegi di Amministratore per il modello. Per consentire ad altri utenti nell'organizzazione di esplorare il modello utilizzando un'applicazione client di creazione di report, è tuttavia necessario creare almeno un ruolo che disponga di autorizzazioni di lettura e aggiungere tali utenti come membri.  
  
 Verranno creati tre ruoli:  
  
-   Responsabile vendite-questo ruolo può includere gli utenti dell'organizzazione per i quali si desidera disporre dell'autorizzazione di lettura per tutti gli oggetti e i dati del modello.  
  
-   Sales Analyst US: questo ruolo può includere gli utenti dell'organizzazione per i quali si desidera solo essere in grado di esplorare i dati relativi alle vendite negli Stati Uniti (Stati Uniti). Per questo ruolo, si utilizzerà una formula DAX per definire un *Filtro di riga*che consente ai membri di esplorare solo i dati per gli Stati Uniti.  
  
-   Amministratore: questo ruolo può includere gli utenti per i quali si desidera disporre dell'autorizzazione di amministratore, che consente l'accesso illimitato e autorizzazioni per l'esecuzione di attività amministrative sul database modello.  
  
 Poiché gli account di gruppo e utente di Windows nell'organizzazione sono univoci, è possibile aggiungere account dell'organizzazione specifica ai membri. Tuttavia, per questa esercitazione, è anche possibile lasciare i membri vuoti. Sarà ancora possibile verificare gli effetti di ciascun ruolo più avanti nella Lezione 12: Analizzare in Excel.  
  
 Tempo previsto per il completamento della lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
 Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire le attività in questa lezione è necessario aver completato la lezione precedente: [Lezione 11: Creare partizioni](lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Creazione di ruoli  
  
#### <a name="to-create-a-sales-manager-user-role"></a>Per creare un ruolo utente Sales Manager  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]scegliere **Ruoli** dal menu **Modello**.  
  
2.  Nella finestra di dialogo **Gestione ruoli** fare clic su **Nuovo**.  
  
     Un nuovo ruolo con l'autorizzazione Nessuna verrà aggiunto all'elenco.  
  
3.  Fare clic sul nuovo ruolo e quindi nella colonna **nome** rinominare il ruolo in `Internet Sales Manager`.  
  
4.  Nella colonna **Autorizzazioni** fare clic nell'elenco a discesa e quindi selezionare l'autorizzazione **Lettura**.  
  
5.  Facoltativo: fare clic sulla scheda **Membri** e quindi fare clic su **Aggiungi**.  
  
6.  Nella finestra di dialogo **Seleziona utenti o gruppi** immettere gli utenti o i gruppi di Windows dell'organizzazione che si vuole includere nel ruolo.  
  
7.  Verificare le selezioni e quindi fare clic su **OK** .  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>Per creare un ruolo utente Sales Analyst US  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]scegliere **Ruoli** dal menu **Modello**.  
  
2.  Nella finestra di dialogo **Gestione ruoli** fare clic su **Nuovo**.  
  
     Un nuovo ruolo con l'autorizzazione Nessuna verrà aggiunto all'elenco.  
  
3.  Fare clic sul nuovo ruolo e quindi nella colonna **nome** rinominare il ruolo in `Internet Sales US`.  
  
4.  Nella colonna **Autorizzazioni** fare clic nell'elenco a discesa e quindi selezionare l'autorizzazione **Lettura**.  
  
5.  Fare clic sulla scheda Filtri di riga, quindi, solo per la tabella **Geography** , digitare la formula seguente nella colonna Filtro DAX:  
  
     `=Geography[Country Region Code] = "US"`  
  
     Una formula per il filtro di riga deve restituire un valore booleano (TRUE/FALSE). Con questa formula, si specifica che solo le righe con il valore "US" del codice dell'area paese saranno visibili all'utente.  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
6.  Facoltativo: fare clic sulla scheda **Membri** e quindi fare clic su **Aggiungi**.  
  
7.  Nella finestra di dialogo **Seleziona utenti o gruppi** immettere gli utenti o i gruppi di Windows dell'organizzazione che si vuole includere nel ruolo.  
  
8.  Verificare le selezioni e quindi fare clic su **OK** .  
  
#### <a name="to-create-an-administrator-role"></a>Per creare un ruolo di amministratore  
  
1.  Nella finestra di dialogo **Gestione ruoli** fare clic su **Nuovo**.  
  
2.  Fare clic sul nuovo ruolo e quindi nella colonna **nome** rinominare il ruolo in `Internet Sales Administrator`.  
  
3.  Nella colonna **Autorizzazioni** fare clic nell'elenco a discesa, quindi selezionare l'autorizzazione **Amministratore** .  
  
4.  Fare clic sulla scheda **Membri** , quindi su **Aggiungi**.  
  
5.  Facoltativo: nella finestra di dialogo **Seleziona utenti o gruppi** immettere i gruppi o gli utenti di Windows dell'organizzazione da includere nel ruolo.  
  
6.  Verificare le selezioni e quindi fare clic su **OK** .  
  
## <a name="next-steps"></a>Passaggi successivi  
 Per continuare questa esercitazione, passare alla lezione successiva: [Lezione 13: Analizza in Excel](lesson-12-analyze-in-excel.md).  
  
  
