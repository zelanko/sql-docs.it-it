---
title: Visualizzare o modificare le pianificazioni dei set di raccolta (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dc.collectionsetprop.uploads.f1
- sql13.swb.dc.collectionsetprop.description.f1
- sql13.swb.dc.collectionsetprop.general.f1
helpviewer_keywords:
- collection sets [SQL Server], changing schedules
- schedules [SQL Server], changing collection set
- collection sets [SQL Server], viewing schedules
- schedules [SQL Server], viewing collection set
ms.assetid: 26336c98-78c5-414f-8d6a-574fc3af60c4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3c5aa31c50a4589c3ba5087333522955f8bd9110
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67999911"
---
# <a name="view-or-change-collection-set-schedules-sql-server-management-studio"></a>Visualizzazione o modifica delle pianificazioni dei set di raccolta (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È possibile visualizzare o modificare le pianificazioni dei set di raccolta utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 La modalità di raccolta, ovvero in cache o non in cache, determina il tipo di modifiche che è possibile apportare a una pianificazione. La modalità cache utilizza pianificazioni separate per la raccolta e il caricamento. La modalità non in cache utilizza la stessa pianificazione per la raccolta e il caricamento. I tipi di modalità di raccolta per ognuno dei set di raccolta dati di sistema sono i seguenti:  
  
-   **Utilizzo disco** usa la modalità di raccolta non in cache.  
  
-   **Statistiche query** utilizza la modalità di raccolta cache.  
  
-   **Attività Server** utilizza la modalità di raccolta cache.  
  
### <a name="to-view-collection-set-schedules"></a>Per visualizzare le pianificazioni dei set di raccolta  
  
1.  In Esplora oggetti espandere il nodo **Gestione** , **Raccolta dati**, quindi **Set di raccolta dati di sistema**.  
  
2.  Fare clic con il pulsante destro del mouse sul nome di un set di raccolta e selezionare **Proprietà** per aprire la finestra di dialogo [Proprietà set di raccolta dati](#CollectionSet) .  
  
### <a name="to-change-the-schedules-for-a-cached-mode-collection-set"></a>Per modificare le pianificazioni per un set di raccolta in modalità cache  
  
1.  In Esplora oggetti espandere il nodo **Gestione** , **Raccolta dati**, quindi **Set di raccolta dati di sistema**.  
  
2.  Fare clic con il pulsante destro del mouse su un set di raccolta che usa una modalità cache, ad esempio **Statistiche query**e scegliere **Proprietà** per aprire la finestra di dialogo [Proprietà set di raccolta dati](#CollectionSet) .  
  
3.  Per modificare la frequenza di raccolta, utilizzare la pagina **Generale** . A tale scopo, eseguire le operazioni seguenti:  
  
    1.  Nel riquadro dei dettagli fare doppio clic sul numero visualizzato per la colonna **Frequenza di raccolta (sec)** nella tabella **Elementi della raccolta** .  
  
    2.  Per aumentare o ridurre la frequenza di raccolta, digitare un numero minore o maggiore, quindi premere INVIO per archiviare il nuovo valore.  
  
4.  Per modificare la pianificazione di caricamento corrente per il set di raccolta, effettuare le operazioni seguenti:  
  
    1.  Fare clic sulla pagina **Caricamenti** .  
  
    2.  Nel riquadro dei dettagli fare clic su **Seleziona**.  
  
         Verrà visualizzata la finestra di dialogo **Seleziona pianificazione per il processo** . Le pianificazioni disponibili sono visualizzate sotto forma di tabella.  
  
    3.  Fare clic sulla riga contenente la pianificazione desiderata. Per modificare ad esempio la pianificazione su ogni 5 minuti, fare clic sulla riga in cui il nome della pianificazione è **CollectorSchedule_Every_5min.**  
  
        > [!NOTE]  
        >  Per visualizzare e modificare le proprietà per la pianificazione selezionata, fare clic su **Proprietà** per aprire la finestra di dialogo **Proprietà pianificazione processo** per la pianificazione. È possibile utilizzare questa finestra di dialogo per modificare le informazioni sulla pianificazione, ad esempio la frequenza.  
        >   
        >  In alternativa alla modifica di una pianificazione esistente, è possibile creare una nuova pianificazione di caricamento facendo clic su **Nuovo** nella pagina **Caricamenti** . Verrà visualizzata la finestra di dialogo **Nuova pianificazione processo** , in cui è possibile creare una pianificazione personalizzata.  
  
    4.  Dopo aver configurato la pianificazione, fare clic su **OK**.  
  
         Le modifiche apportate vengono visualizzate nella pagina **Caricamenti** .  
  
5.  Fare clic su **OK** per salvare le modifiche apportate alla frequenza di raccolta e alla pianificazione del caricamento, quindi chiudere la finestra di dialogo **Proprietà set di raccolta dati** .  
  
### <a name="to-change-the-schedule-for-a-non-cached-mode-collection-set"></a>Per modificare la pianificazione per un set di raccolta in modalità non in cache  
  
1.  In Esplora oggetti espandere il nodo **Gestione** , **Raccolta dati**, quindi **Set di raccolta dati di sistema**.  
  
2.  Fare clic con il pulsante destro del mouse su un set di raccolta che usa una modalità non cache, ad esempio **Utilizzo disco**e scegliere **Proprietà** per aprire la finestra di dialogo [Proprietà set di raccolta dati](#CollectionSet) .  
  
     Viene visualizzata la finestra di dialogo **Proprietà set di raccolta dati** in una vista a pagine contenente le proprietà del set di raccolta.  
  
3.  Per modificare la pianificazione per il set di raccolta, fare clic su **Seleziona**.  
  
     Verrà visualizzata la finestra di dialogo **Seleziona pianificazione per il processo** . Le pianificazioni disponibili sono visualizzate sotto forma di tabella.  
  
4.  Fare clic sulla riga contenente la pianificazione desiderata. Per modificare ad esempio la pianificazione su ogni 5 minuti, fare clic sulla riga in cui il nome della pianificazione è **CollectorSchedule_Every_5min**.  
  
    > [!NOTE]  
    >  Per visualizzare e modificare le proprietà per la pianificazione selezionata, fare clic su **Proprietà** per aprire la finestra di dialogo **Proprietà pianificazione processo** per la pianificazione. È possibile utilizzare questa finestra di dialogo per modificare le informazioni sulla pianificazione, ad esempio la frequenza.  
    >   
    >  In alternativa alla modifica di una pianificazione esistente, è possibile creare una nuova pianificazione di raccolta e caricamento facendo clic su **Nuovo** nella pagina **Generale** . Verrà visualizzata la finestra di dialogo **Nuova pianificazione processo** .  
  
5.  Dopo aver configurato la pianificazione, fare clic su **OK**.  
  
6.  Fare clic su **OK** per salvare le modifiche e chiudere la finestra di dialogo **Proprietà set di raccolta dati** .  
  
####  <a name="CollectionSet"></a> Finestra di dialogo Proprietà set di raccolta dati  
 **Pagina Generale**  
  
 Utilizzare questa pagina per configurare la modalità di raccolta e caricamento dei dati, le pianificazioni e i periodi di memorizzazione dei dati nel data warehouse di gestione. Questa pagina inoltre fornisce informazioni sui set di raccolte, quali le frequenze di raccolta e i tipi di agente di raccolta, nonché i parametri di input utilizzati per un set di raccolta.  
  
 **Nome**  
 Consente di visualizzare il nome del set di raccolta al quale fa riferimento questa pagina.  
  
 **Raccolta e caricamento dati**  
 Consente di specificare la modalità di raccolta e caricamento dei dati nel data warehouse di gestione. Selezionare una delle opzioni seguenti:  
  
|||  
|-|-|  
|**Non-memorizzato nella cache - Raccogli e carica dati in base alla stessa pianificazione.**|Se viene selezionata questa opzione, specificare uno dei valori seguenti:<br /><br /> **Pianifica** I dati sono raccolti e caricati in base a una pianificazione. Fare clic su **Seleziona** per selezionare da un elenco predefinito di pianificazioni oppure su **Nuovo** per creare una pianificazione nuova.<br /><br /> **Su richiesta**. I dati sono raccolti e caricati su richiesta.|  
|**Memorizzato nella cache - Raccogli e memorizza nella cache i dati in base a un set di frequenze di raccolta. Carica dati memorizzati nella cache in base a una pianificazione separata.**|I dati sono raccolti e memorizzati nella cache in base alla frequenza di raccolta specificata. I dati raccolti sono caricati in base a una pianificazione separata.|  
  
 **Elementi della raccolta**  
 Consente di visualizzare gli elementi del set di raccolta. Per ogni elemento della raccolta sono disponibili le seguenti informazioni:  
  
-   **Nome**  
  
-   **Tipo agente di raccolta**  
  
-   **Frequenza di raccolta** (sec). Questo campo può essere modificato se per **Raccolta e caricamento dati** è configurata la memorizzazione nella cache. Fare doppio clic su questa cella per impostare la frequenza della raccolta.  
  
 **Parametri di input**  
 Consente di visualizzare i parametri di input utilizzati per il set di raccolta.  
  
 **Esegui come**  
 Consente di specificare l'account utilizzato per eseguire il set di raccolta. L'impostazione predefinita corrisponde all'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agente. Se sono definiti account proxy, questo elenco contiene i nomi degli account proxy disponibili.  
  
 **Specificare per quanto tempo mantenere i dati nel data warehouse di gestione.**  
 Consente di specificare per quanto tempo sono mantenuti i dati raccolti. Selezionare una delle opzioni seguenti:  
  
|||  
|-|-|  
|**Mantieni dati per**|Questa opzione è selezionata per impostazione predefinita e il periodo di memorizzazione predefinito è 14 giorni.|  
|**Mantieni i dati per un periodo illimitato**|I dati sono mantenuti senza limiti temporali.|  
  
 **Pagina Caricamenti**  
  
 Utilizzare questa pagina per configurare la pianificazione di caricamento per i dati raccolti da questo set di raccolta.  
  
> [!NOTE]  
>  Questa scheda è abilitata solo se per **Raccolta e caricamento dati** è configurata l'opzione **Nella cache**.  
  
 **Server**  
 Consente di visualizzare il nome del server in cui risiede il data warehouse di gestione. Per altre informazioni, vedere [Configurare il data warehouse di gestione &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md).  
  
 **Data warehouse di gestione**  
 Consente di visualizzare il nome del data warehouse di gestione. Per altre informazioni, vedere [Configurare il data warehouse di gestione &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md).  
  
 **Ultimo caricamento**  
 Consente di visualizzare le informazioni sulla data e ora in cui è stato eseguito l'ultimo caricamento per il set di raccolta.  
  
 **Pianificazione caricamento**  
 Consente di specificare la pianificazione di caricamento per il set di raccolta. Se abilitata, fare clic su **Seleziona** per selezionare da un elenco predefinito di pianificazioni oppure su **Nuovo** per creare una nuova pianificazione.  
  
 **Pagina Descrizione**  
  
 Utilizzare questa pagina per visualizzare una descrizione del set di raccolta a cui fa riferimento questa pagina delle proprietà.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire raccolta dati](../../relational-databases/data-collection/manage-data-collection.md)   
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)  
  
  
