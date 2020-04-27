---
title: Distribuire i criteri pianificati in più istanze | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
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
  
-   I server in cui si desidera distribuire i criteri pianificati devono essere registrati in Server registrati nel nodo **gruppi di server locali** o **server di gestione centrale** . Per altre informazioni, vedere gli argomenti seguenti:  
  
    -   [Creare o modificare un gruppo di server &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
    -   [Registrare un server connesso &#40;&#41;SQL Server Management Studio ](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md).  
  
    -   [Creare un server di gestione centrale e un gruppo di server &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-export-the-scheduled-policies-as-xml-files"></a>Per esportare i criteri pianificati come file xml  
  
1.  Nel server in cui sono stati configurati i criteri pianificati nell'attività precedente espandere **gestione**, **Gestione criteri**, quindi fare clic su **criteri**.  
  
2.  Scegliere **Dettagli Esplora oggetti** dal menu **Visualizza**.  
  
3.  Nel riquadro **dettagli Esplora oggetti** selezionare tutti i criteri per procedure consigliate pianificati che si desidera distribuire in altri server tramite Server registrati.  
  
    > [!NOTE]  
    >  È possibile fare clic sull'intestazione **categoria** per ordinare i criteri per categoria.  
  
4.  Fare clic con il pulsante destro del mouse sulla selezione, quindi scegliere **Esporta criteri**.  
  
5.  Se sono stati selezionati più criteri da esportare, nella finestra di dialogo **Sfoglia per cartelle** selezionare una cartella di destinazione o creare una nuova cartella. Per questa lezione, creare una nuova cartella con il percorso **c:\ Scheduled_BP_Policies**e quindi fare clic su **OK**.  
  
     Se è stato selezionato un solo criterio da esportare, nella finestra di dialogo **Esporta criteri** creare una nuova cartella con il percorso **c:\ Scheduled_BP_Policies**, fare clic su **Apri**e quindi su **Salva**.  
  
     I file xml dei criteri vengono creati nel percorso della cartella.  
  
### <a name="to-deploy-the-scheduled-policies-to-servers-that-are-managed-through-registered-servers"></a>Per distribuire i criteri pianificati in server gestiti mediante Server registrati  
  
1.  Scegliere **Server registrati** dal menu **Visualizza**.  
  
2.  Espandere **motore di database**, espandere **gruppi di server locali** o **server di gestione centrale**, fare clic con il pulsante destro del mouse sul nodo in cui si desidera distribuire i criteri e quindi fare clic su **Importa criteri**.  
  
    > [!NOTE]  
    >  Se si fa clic con il pulsante destro del mouse su **gruppi di server locali** o sul server di gestione centrale stesso, i criteri verranno distribuiti in tutti i server gestiti. Se si fa clic con il pulsante destro del mouse su un gruppo di server specifico, i criteri verranno distribuiti solo in tale gruppo. Se si fa clic con il pulsante destro del mouse su un server registrato specifico, i criteri verranno distribuiti solo in tale server.  
  
3.  Accanto a **file da importare**fare clic sul pulsante con i puntini di sospensione (**...**).  
  
4.  Nella finestra di dialogo **Seleziona criterio** passare al percorso della cartella in cui sono stati salvati i criteri pianificati. Per questo esempio, passare al percorso **c:\ Scheduled_BP_Policies**.  
  
5.  Selezionare i criteri che si desidera importare nelle istanze di destinazione, quindi fare clic su **Apri**.  
  
6.  Nella finestra di dialogo **Importa** selezionare lo stato dei criteri desiderato nell'elenco **stato criteri** . È possibile scegliere di mantenere lo stato dei criteri, abilitare o disabilitare i criteri durante l'importazione. Tenere presente che i criteri devono essere abilitati per poter essere eseguiti in base a una pianificazione.  
  
7.  Fare clic su **OK** per importare i criteri in tutte le istanze di destinazione.  
  
    > [!NOTE]  
    >  Se si verificano errori, la finestra di dialogo **Importa** non scomparirà. Fare clic sulla pagina **log** per esaminare i messaggi. Fare clic su **Annulla**per chiudere la finestra di dialogo.  
  
8.  Per visualizzare i criteri da un'istanza di destinazione, connettersi all'istanza di, aprire Esplora oggetti, espandere **gestione**, quindi espandere **criteri**. Verranno visualizzati i criteri importati nel nodo **criteri** . Se si fa doppio clic su ciascuno dei criteri, è possibile visualizzare la pianificazione o modificare le impostazioni.  
  
    > [!NOTE]  
    >  Per visualizzare i risultati di valutazione dopo l'esecuzione di criteri pianificati, aprire il log Cronologia criteri nell'istanza di destinazione. Per aprire il log, fare clic con il pulsante destro del mouse su **Gestione criteri**, quindi scegliere **Visualizza cronologia**.  
  
## <a name="summary"></a>Riepilogo  
 In questa esercitazione è stato illustrato come eseguire valutazioni su richiesta e pianificate dei criteri per procedure consigliate per una o più istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="next"></a>Avanti  
 L'esercitazione è completata. Per tornare all'inizio, vedere [esercitazione: valutazione delle procedure consigliate tramite la gestione basata su criteri](../../2014/tutorials/tutorial-evaluating-best-practices-by-using-policy-based-management.md).  
  
 Per visualizzare un elenco delle [!INCLUDE[ssDE](../includes/ssde-md.md)] esercitazioni, fare clic su [motore di database esercitazioni](../relational-databases/database-engine-tutorials.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Amministrazione di server tramite la gestione basata su criteri](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
