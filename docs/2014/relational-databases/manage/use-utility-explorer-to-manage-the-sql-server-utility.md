---
title: Usare Esplora utilità per gestire Utilità SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 74012c90-b42e-4171-b27a-9c30cf69ff98
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fee3411a65d7e2b5f91e503b1314aa004b6a12bb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85023184"
---
# <a name="use-utility-explorer-to-manage-the-sql-server-utility"></a>Utilizzo di Esplora utilità per gestire Utilità SQL Server
  Gestione Utilità, un componente di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], consente di connettersi alle istanze del [!INCLUDE[ssDE](../../includes/ssde-md.md)] per fornire una visualizzazione albero di tutti gli oggetti in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il riquadro del contenuto di Esplora utilità fornisce diverse soluzioni per visualizzare dati riepilogativi e dettagliati sullo stato dell'integrità delle istanze gestite di SQL Server. Esplora utilità fornisce anche un'interfaccia utente per visualizzare e gestire le definizioni dei criteri. Le funzionalità di Esplora utilità variano leggermente a seconda degli oggetti di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ma generalmente includono oggetti, dati e criteri gestiti da Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Attività e funzionalità di Utilità SQL Server](sql-server-utility-features-and-tasks.md).  
  
## <a name="create-utility-control-point"></a>Creazione di un punto di controllo dell'utilità  
 Per poter usare Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario creare un punto di controllo dell'utilità. Per altre informazioni, vedere [Attività e funzionalità di Utilità SQL Server](sql-server-utility-features-and-tasks.md) o [Creare un punto di controllo dell'Utilità SQL Server &#40;Utilità SQL Server&#41;](create-a-sql-server-utility-control-point-sql-server-utility.md).  
  
## <a name="enroll-an-instance-of-sql-server-or-a-data-tier-application-from-utility-explorer"></a>Registrazione di un'istanza di SQL Server o di un'applicazione del livello dati da Esplora utilità  
 È possibile registrare facilmente un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In Esplora utilità fare clic con il pulsante destro del mouse sul nodo **Istanze gestite** e quindi scegliere **Add Managed Instance**(Aggiungi istanza gestita). Per completare l'operazione, eseguire i passaggi della procedura guidata. Per altre informazioni, vedere [Registrare un'istanza di SQL Server &#40;Utilità SQL Server&#41;](enroll-an-instance-of-sql-server-sql-server-utility.md).  
  
 Per distribuire un'applicazione livello dati in un'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fare clic sulla scheda **Esplora oggetti**, espandere il nodo **Gestione** quindi fare clic con il pulsante destro del mouse sul nodo **Applicazioni livello dati**. Scegliere **Distribuisci applicazione livello dati**dal menu di scelta rapida. Per altre informazioni, vedere [Distribuire un'applicazione livello dati](../data-tier-applications/deploy-a-data-tier-application.md).  
  
## <a name="viewing-utility-explorer"></a>Visualizzazione di Esplora utilità  
 Esplora utilità non è visualizzato per impostazione predefinita in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] . Se non è visualizzato nell'interfaccia utente di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , scegliere **Esplora utilità** dal menu **Visualizza**. Per visualizzare il riquadro del contenuto di Esplora utilità, nel menu **Visualizza** fare clic su **Contenuto Esplora utilità**.  
  
## <a name="viewing-objects-in-utility-explorer"></a>Visualizzazione di oggetti in Esplora utilità  
 Nel riquadro di navigazione e nel riquadro del contenuto di Esplora utilità vengono visualizzati dati, oggetti e criteri gestiti da Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Usare il riquadro di navigazione per specificare le informazioni da visualizzare nel dashboard e nei punti di visualizzazione, quindi usare il riquadro del contenuto e le schede dei dettagli per accedere ai dati e alle informazioni sui criteri per gli oggetti gestiti da Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="sql-server-utility-navigation-pane"></a>Riquadro di navigazione di Utilità SQL Server  
 Il riquadro di navigazione di Esplora utilità fornisce una visualizzazione albero degli oggetti di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , raggruppati per punto di controllo dell'utilità. Per espandere le cartelle, fare clic sul segno più (+) o fare doppio clic sul nome del punto di controllo dell'utilità nel riquadro di navigazione di Esplora utilità. Fare clic con il pulsante destro del mouse su cartelle o oggetti per eseguire attività comuni. I nodi nella visualizzazione albero sono i seguenti:  
  
-   Il nodo principale della visualizzazione albero è il punto di controllo dell'utilità. Il nome del nodo viene costruito come: "Nome_Utilità (NomeComputer\Nome_Istanza_PuntoControllo)." Se non è presente un punto di controllo dell'utilità, è necessario crearlo. Se non si è connessi a Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario connettersi. Per altre informazioni, vedere [Attività e funzionalità di Utilità SQL Server](sql-server-utility-features-and-tasks.md). Fare clic sul nome del punto di controllo dell'utilità nella visualizzazione albero per popolare il riquadro del contenuto di Esplora utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con i dati della visualizzazione dashboard. Per altre informazioni, vedere [Dashboard Utilità &#40;Utilità SQL Server&#41;](../../database-engine/utility-dashboard-sql-server-utility.md).  
  
     Fare clic con il pulsante destro del mouse sul nodo del punto di controllo dell'utilità per aggiornare i dati nel dashboard.  
  
-   Fare clic sul nodo **Deployed Data-tier Applications** (Applicazioni livello dati distribuite) nella visualizzazione albero per accedere ai dati della visualizzazione elenco nel riquadro del contenuto di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Le schede dei dettagli nella parte inferiore del riquadro del contenuto includono i dati di utilizzo della CPU e dello spazio di archiviazione e l'accesso alle definizioni dei criteri e ai dettagli delle proprietà per le singole applicazioni del livello dati in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Dettagli delle applicazioni livello dati distribuite &#40;Utilità SQL Server&#41;](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md)  
  
     Fare clic con il pulsante destro del mouse sul nodo **Deployed Data-tier Applications** (Applicazioni livello dati distribuite) nella visualizzazione albero per accedere alle impostazioni di filtro o per aggiornare i dati della visualizzazione elenco.  
  
-   Fare clic sul nodo **Istanze gestite** nella visualizzazione albero per accedere ai dati della visualizzazione elenco nel riquadro del contenuto di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Le schede dei dettagli nella parte inferiore del riquadro del contenuto includono i dati relativi all'utilizzo della CPU e dello spazio dei volumi di archiviazione e all'accesso alle definizioni dei criteri e ai dettagli delle proprietà per le singole istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Dettagli di istanze gestite &#40;Utilità SQL Server&#41;](../../database-engine/managed-instance-details-sql-server-utility.md).  
  
     Fare clic con il pulsante destro del mouse sul nodo **Istanze gestite** nella visualizzazione albero per aggiungere istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], per accedere alle impostazioni di filtro o per aggiornare i dati della visualizzazione elenco.  
  
-   Fare clic sul nodo **Amministrazione utilità** nella visualizzazione albero per accedere alle definizioni dei criteri globali per tutte le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e delle applicazioni livello dati distribuite in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], per visualizzare le informazioni sull'amministratore del punto di controllo dell'utilità e per accedere alle impostazioni di configurazione per il data warehouse di gestione di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Amministrazione utilità &#40;Utilità SQL Server&#41;](../../database-engine/utility-administration-sql-server-utility.md). È inoltre possibile utilizzare i controlli della scheda **Criteri** per modificare le impostazioni per la segnalazione delle violazioni dei criteri. Per altre informazioni, vedere [Ridurre le segnalazioni non significative nei criteri di utilizzo della CPU &#40;Utilità SQL Server&#41;](reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Fare clic con il pulsante destro del mouse sul nodo **Amministrazione utilità** nella visualizzazione albero per aggiornare i dati nel riquadro del contenuto.  
  
### <a name="sql-server-utility-dashboard"></a>Dashboard dell'Utilità SQL Server  
 Selezionando il nodo del punto di controllo dell'utilità nella visualizzazione albero Gestione Utilità, è possibile popolare il dashboard di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con i dati del riquadro del contenuto di Gestione Utilità. Il dashboard include un riepilogo generale dello stato di tutte le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e delle applicazioni livello dati in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nonché dell'utilizzo dello spazio di archiviazione complessivo per gli oggetti gestiti da Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Dashboard Utilità &#40;Utilità SQL Server&#41;](../../database-engine/utility-dashboard-sql-server-utility.md). Per registrare o rimuovere un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Registrare un'istanza di SQL Server &#40;Utilità SQL Server&#41;](enroll-an-instance-of-sql-server-sql-server-utility.md), [Distribuire un'applicazione livello dati](../data-tier-applications/deploy-a-data-tier-application.md) o [Rimuovere un'istanza di SQL Server da Utilità SQL Server](remove-an-instance-of-sql-server-from-the-sql-server-utility.md).  
  
### <a name="filtering-the-list-of-objects-in-utility-explorer-contents"></a>Applicazione di filtri all'elenco degli oggetti in Esplora utilità  
 Quando un nodo contiene un numero elevato di oggetti, potrebbe risultare difficile trovare l'oggetto desiderato. In questo caso, è possibile usare la caratteristica di filtro di Esplora utilità per ridurre le dimensioni dell'elenco. Se, ad esempio, si vuole trovare un'istanza specifica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o solo i computer con spazio file sottoutilizzato, fare clic con il pulsante destro del mouse sulla cartella alla quale applicare il filtro e quindi scegliere **Impostazioni filtro** per aprire la finestra di dialogo Impostazioni filtro di Esplora utilità. È possibile filtrare l'elenco in base al nome, alla CPU del computer, alla CPU dell'istanza, allo spazio occupato dai file, allo spazio del volume, alle impostazioni di esclusione dei criteri o all'ultima ora registrata. Le colonne **Operatore** e **Valore** includono operatori di filtro aggiuntivi in un elenco a discesa.  
  
### <a name="starting-powershell"></a>Avvio di PowerShell  
 È possibile avviare una sessione di PowerShell facendo clic con il pulsante destro del mouse sulla maggior parte delle cartelle e degli oggetti nell'albero di Esplora oggetti e scegliendo **Avvia Powershell**. Verrà avviata una sessione di PowerShell in cui è abilitato il supporto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell e con il percorso impostato sull'oggetto su cui si è fatto clic con il pulsante destro del mouse in Esplora oggetti. È quindi possibile immettere comandi di PowerShell in un ambiente di PowerShell interattivo. Per altre informazioni, vedere [SQL Server PowerShell](../../powershell/sql-server-powershell.md).  
  
 In PowerShell non è inclusa una Guida sensibile al contesto, ma è disponibile un cmdlet **Get-Help** che fornisce informazioni sull'uso di PowerShell. Per altre informazioni, vedere [Visualizzare la Guida di SQL Server PowerShell](../../database-engine/get-help-sql-server-powershell.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e funzionalità di Utilità SQL Server](sql-server-utility-features-and-tasks.md)   
 [Configurare i criteri di integrità &#40;Utilità SQL Server&#41;](configure-health-policies-sql-server-utility.md)   
 [Esplora oggetti](../../ssms/object/object-explorer.md)  
  
  
