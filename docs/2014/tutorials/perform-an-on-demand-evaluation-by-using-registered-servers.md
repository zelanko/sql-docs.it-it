---
title: Eseguire una valutazione su richiesta utilizzando Server registrati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: c14034ef-6e0b-4df5-8072-bfb8d90b3172
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a3a79a6ec655e91264d6fcc00db5a920ad82a21e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66822377"
---
# <a name="perform-an-on-demand-evaluation-by-using-registered-servers"></a>Esecuzione di una valutazione su richiesta utilizzando Server registrati

  È possibile eseguire una valutazione su richiesta dei criteri per procedure consigliate in una o più istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tramite Server registrati. È possibile utilizzare gruppi di server locali o un server di gestione centrale.  
  
> [!NOTE]  
>  È possibile eseguire una valutazione su richiesta dei criteri per procedure consigliate in membri del gruppo di server che eseguono [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] o una versione più recente di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Tuttavia, è possibile ricevere un errore di eccezione se i criteri fanno riferimento a proprietà non supportate in [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] o [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)].  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa attività è necessario aver configurato una o più registrazioni di server in Server registrati. Per altre informazioni, vedere gli argomenti seguenti:  
  
-   [Creare o modificare un gruppo di server &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [Registrare un server connesso &#40;&#41;SQL Server Management Studio ](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md).  
  
-   [Creare un server di gestione centrale e un gruppo di server &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-evaluate-best-practices-policies-against-a-server-group"></a>Per valutare i criteri per procedure consigliate in un gruppo di server  
  
1.  In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]scegliere **Server registrati** dal menu **Visualizza**.  
  
2.  Espandere **motore di database**, quindi espandere gruppi di **server locali**o server di **gestione centrale**, a seconda della configurazione.  
  
3.  Effettuare una delle operazioni seguenti:  
  
    -   Per valutare i criteri in tutti i server gestiti dal gruppo di server locale o dal server di gestione centrale, fare clic con il pulsante destro del mouse sul nome del gruppo di server locale o sul nome del server di gestione centrale, quindi scegliere **Valuta criteri**.  
  
        > [!NOTE]  
        >  Quando si valutano i criteri mediante un server di gestione centrale, tali criteri non vengono valutati nel server di gestione centrale stesso.  
  
    -   Per valutare i criteri rispetto a un server o a un gruppo di server specifico, espandere **gruppi di server locali** o il nome del server di gestione centrale, fare clic con il pulsante destro del mouse sul server o sul gruppo di server a cui si desidera valutare i criteri, quindi scegliere **Valuta criteri**.  
  
4.  Nella finestra di dialogo **Valuta criteri** , accanto alla casella **origine** , fare clic sul pulsante con i puntini di sospensione (**...**).  
  
5.  Nella finestra di dialogo **Seleziona origine** è possibile selezionare i **file** o il **server** come origine dei file di criteri da valutare. Se si fa clic su **Server**, è possibile eseguire una valutazione su richiesta dei criteri per procedure consigliate importati in precedenza nella gestione basata su criteri in un server locale o remoto. In questa esercitazione si fa clic su **file**, quindi si selezionano i singoli file dei criteri che si desidera valutare. A questo scopo, seguire questa procedura:  
  
    1.  Fare clic su **file**.  
  
    2.  Accanto a **file**fare clic sul pulsante con i puntini di sospensione (**...**).  
  
    3.  Selezionare uno o più file di criteri con estensione XML da valutare, quindi fare clic su **Apri**.  
  
         L'elenco dei file selezionati viene visualizzato nella casella **file** .  
  
    4.  Nella finestra di dialogo **Seleziona origine** fare clic su **OK**.  
  
    5.  Se viene visualizzata la finestra di dialogo **caricamento dei criteri** , fare clic su **Chiudi**.  
  
     I criteri selezionati vengono elencati nella pagina di **selezione dei criteri** . L'icona di avviso accanto ai criteri indica che questi contengono script.  
  
6.  Fare clic su **valuta** per valutare i criteri.  
  
7.  Per alcuni errori relativi ai criteri, la gestione basata su criteri consente di applicare immediatamente la conformità di criteri nella destinazione. Per questo tipo di errori verrà visualizzata una casella di controllo accanto ai criteri che presentano errori. Se si seleziona la casella di controllo o si fa clic sulla riga con il criterio non riuscito, le caselle di controllo vengono visualizzate nel riquadro dei **Dettagli di destinazione** accanto alle istanze di destinazione che non hanno superato la valutazione. Se una delle caselle di controllo è selezionata, il pulsante **applica** diventa disponibile. Quando si fa clic su **applica**, l'impostazione non conforme verrà automaticamente aggiornata nelle istanze di destinazione selezionate.  
  
    > [!CAUTION]  
    >  Assicurarsi di aver compreso a pieno tutte le impostazioni dei criteri prima di aggiornare automaticamente un'istanza di destinazione. Dopo aver selezionato una o più caselle di controllo, è consigliabile fare clic su **script**e scegliere un percorso di output in modo che sia possibile esaminare [!INCLUDE[tsql](../includes/tsql-md.md)] il codice sottostante prima di applicare le modifiche.  
  
8.  Per visualizzare i risultati dettagliati per un criterio, fare clic sul criterio nella tabella **dei risultati** . La tabella **Dettagli destinazione** Mostra i dettagli per ogni istanza.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 2: Valutazione di criteri per procedure consigliate in base a una pianificazione prestabilita](../../2014/tutorials/lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)   
 [Amministrare più server tramite server di gestione centrale](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
