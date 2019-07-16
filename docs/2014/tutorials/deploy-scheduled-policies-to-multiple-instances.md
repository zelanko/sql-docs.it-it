---
title: Distribuire criteri pianificati a istanze Multiple | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: f551b8e8-3668-4ed4-852f-bae826254f4f
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8d37dafd5501a289e45a119323eed61242707184
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68185805"
---
# <a name="deploy-scheduled-policies-to-multiple-instances"></a>Distribuzione di criteri pianificati in istanze multiple
  Tramite Server registrati è possibile distribuire criteri pianificati a server gestiti da una posizione centralizzata. È possibile distribuire i criteri pianificati da un gruppo di server locali o da un server di gestione centrale.  
  
 In questa attività, verranno effettuate le operazioni seguenti:  
  
1.  Esportazione in una cartella dei criteri pianificati nell'attività precedente.  
  
2.  Distribuzione dei criteri pianificati a istanze di destinazione gestite mediante Server registrati.  
  
 Tali attività verranno eseguite nel computer utilizzato per completare le attività precedenti di questa lezione.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Di seguito vengono indicati i prerequisiti di questa attività:  
  
-   È necessario avere completato le attività precedenti di questa lezione.  
  
-   È necessario che nelle istanze in cui si desidera distribuire i criteri pianificati sia in esecuzione [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] o versione successiva. Ai fini dell'automazione è necessario che i criteri siano archiviati localmente, operazione non supportata nelle versioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
-   Il server in cui si desidera distribuire i criteri pianificati devono essere registrati in server registrati in entrambi i **gruppi di Server locali** o il **server di gestione centrale** nodo. Per altre informazioni, vedere i seguenti argomenti:  
  
    -   [Creare o modificare un gruppo di server &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
    -   [Registrare un Server connesso &#40;SQL Server Management Studio&#41;](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md).  
  
    -   [Creare un server di gestione centrale e un gruppo di server &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-export-the-scheduled-policies-as-xml-files"></a>Per esportare i criteri pianificati come file xml  
  
1.  Nel server in cui sono configurati criteri pianificati nell'attività precedente, espandere **Management**, espandere **gestione dei criteri**e quindi fare clic su **criteri**.  
  
2.  Scegliere **Dettagli Esplora oggetti** dal menu **Visualizza**.  
  
3.  Nel **dettagli Esplora oggetti** riquadro, selezionare tutte le procedure consigliate pianificati i criteri che si desidera distribuire in altri server tramite server registrati.  
  
    > [!NOTE]  
    >  È possibile scegliere il **categoria** intestazione per ordinare i criteri in base alla categoria.  
  
4.  Fare doppio clic la selezione e quindi fare clic su **Esporta criteri**.  
  
5.  Se si seleziona più criteri da esportare, nella **Sfoglia per cartelle** nella finestra di dialogo selezionare una cartella di destinazione oppure creare una nuova cartella. Per questa lezione, creare una nuova cartella nel percorso **C:\Scheduled_BP_Policies**, quindi fare clic su **OK**.  
  
     Se è selezionato un solo criterio da esportare, nella **Esporta criteri** finestra di dialogo casella, creare una nuova cartella con il percorso **C:\Scheduled_BP_Policies**, fare clic su **Open**, quindi fare clic su **Salvare**.  
  
     I file xml dei criteri vengono creati nel percorso della cartella.  
  
### <a name="to-deploy-the-scheduled-policies-to-servers-that-are-managed-through-registered-servers"></a>Per distribuire i criteri pianificati in server gestiti mediante Server registrati  
  
1.  Scegliere **Server registrati** dal menu **Visualizza**.  
  
2.  Espandere **motore di Database**, espandere **gruppi di Server locali** oppure **server di gestione centrale**, pulsante destro del mouse il nodo che si desidera distribuire i criteri e quindi Fare clic su **Importa criteri**.  
  
    > [!NOTE]  
    >  Se facendo clic **gruppi di Server locali** o il Server di gestione centrale stesso, i criteri verranno distribuiti a tutti i server gestiti. Se si fa clic con il pulsante destro del mouse su un gruppo di server specifico, i criteri verranno distribuiti solo in tale gruppo. Se si fa clic con il pulsante destro del mouse su un server registrato specifico, i criteri verranno distribuiti solo in tale server.  
  
3.  Accanto a **i file da importare**, fare clic sul pulsante con puntini di sospensione ( **...** ).  
  
4.  Nel **Seleziona criteri** della finestra di dialogo Sfoglia per il percorso della cartella in cui è stato salvato i criteri pianificati. Per questo esempio, passare al percorso **C:\Scheduled_BP_Policies**.  
  
5.  Selezionare i criteri che si desidera importare per le istanze di destinazione e quindi fare clic su **aperto**.  
  
6.  Nel **importazione** nella finestra di dialogo il **lo stato dei criteri** selezionare lo stato dei criteri desiderati. È possibile scegliere di mantenere lo stato dei criteri, abilitare o disabilitare i criteri durante l'importazione. Tenere presente che i criteri devono essere abilitati per poter essere eseguiti in base a una pianificazione.  
  
7.  Fare clic su **OK** per importare i criteri a tutte le istanze di destinazione.  
  
    > [!NOTE]  
    >  Se sono presenti errori, il **importazione** nella finestra di dialogo non scomparsa. Scegliere il **Log** pagina per esaminare i messaggi. Fare clic su **annullare** per chiudere la finestra di dialogo.  
  
8.  Per visualizzare i criteri da un'istanza di destinazione, connettersi all'istanza, aprire Esplora oggetti, espandere **Management**, quindi espandere **criteri**. Si dovrebbero vedere i criteri importati i **criteri** nodo. Se si fa doppio clic su ciascuno dei criteri, è possibile visualizzare la pianificazione o modificare le impostazioni.  
  
    > [!NOTE]  
    >  Per visualizzare i risultati di valutazione dopo l'esecuzione di criteri pianificati, aprire il log Cronologia criteri nell'istanza di destinazione. Per aprire il log, fare doppio clic su **criteri di gestione**, quindi fare clic su **Visualizza cronologia**.  
  
## <a name="summary"></a>Riepilogo  
 In questa esercitazione è stato illustrato come eseguire valutazioni su richiesta e pianificate dei criteri per procedure consigliate per una o più istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="next"></a>Avanti  
 L'esercitazione è completata. Per tornare all'inizio, vedere [esercitazione: La valutazione di procedure consigliate tramite la gestione basata su criteri](../../2014/tutorials/tutorial-evaluating-best-practices-by-using-policy-based-management.md).  
  
 Per visualizzare un elenco dei [!INCLUDE[ssDE](../includes/ssde-md.md)] esercitazioni, fare clic su [esercitazioni del motore di Database](../relational-databases/database-engine-tutorials.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione di server tramite la gestione basata su criteri](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
