---
title: Scaricare gli aggiornamenti Microsoft - sistema di piattaforma Analitica | Microsoft Docs
description: In questo argomento illustra come scaricare gli aggiornamenti dal catalogo Microsoft Update per Windows Server Update Services (WSUS) e applicare gli aggiornamenti nei server appliance del sistema di piattaforma Analitica. Microsoft Update installerà tutti gli aggiornamenti per Windows e SQL Server. Windows Server Update Services è installato nella macchina virtuale VMM dell'appliance.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d71a6ddc965b422f0f96f40788352213501b4db2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042323"
---
# <a name="download-and-apply-microsoft-updates-for-analytics-platform-system"></a>Scaricare e applicare gli aggiornamenti Microsoft per il sistema di piattaforma Analitica
In questo argomento illustra come scaricare gli aggiornamenti dal catalogo Microsoft Update per Windows Server Update Services (WSUS) e applicare gli aggiornamenti nei server appliance del sistema di piattaforma Analitica. Microsoft Update installerà tutti gli aggiornamenti per Windows e SQL Server. Windows Server Update Services è installato nella macchina virtuale VMM dell'appliance.  
  
## <a name="TOP"></a>Prima di iniziare  
  
> [!WARNING]  
> Non tentare di applicare gli aggiornamenti se l'appliance o qualsiasi componente di appliance è inattivo o non riuscito sullo stato. In tal caso, contattare il supporto tecnico per assistenza.  
>   
> Non si applicano Microsoft Updates mentre il dispositivo è in uso. Applicazione degli aggiornamenti può causare nodi di appliance da riavviare. Gli aggiornamenti da applicare durante una finestra di manutenzione quando non viene utilizzata l'appliance.  
  
### <a name="prerequisites"></a>Prerequisiti  
Prima di eseguire questi passaggi, è necessario:  
  
-   Configurazione di WSUS nell'appliance seguendo le istruzioni disponibili nel [configurare Windows Server Update Services &#40;WSUS&#41; &#40;sistema di piattaforma Analitica&#41;](configure-windows-server-update-services-wsus.md).  
  
-   Conoscenza delle informazioni di accesso account amministratore di dominio dell'infrastruttura.  
  
-   Avere un account di accesso con le autorizzazioni per accedere alla Console di Amministrazione sistema piattaforma Analitica e visualizzare le informazioni sullo stato di appliance.  
  
-   Nella maggior parte dei casi, è necessario che WSUS accedere ai server all'esterno dell'appliance. Per supportare il DNS di sistema di piattaforma Analitica può essere configurato per supportare un server d'inoltro nome esterno che consentirà al sistema di piattaforma Analitica host e macchine virtuali (VM) da usare server DNS esterni per risolvere i nomi all'esterno di questo scenario di utilizzo di Appliance. Per altre informazioni, vedere [usare un server d'inoltro di DNS per risolvere nomi DNS Non di Appliance &#40;sistema di piattaforma Analitica&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
## <a name="bkmk_ImportUpdates"></a>Per scaricare e applicare gli aggiornamenti Microsoft  
  
#### <a name="verify-the-appliance-state-indicators"></a>Verificare gli indicatori di stato delle appliance  
  
1.  Aprire la Console di amministrazione e passare alla pagina di stato dello strumento. Per altre informazioni, vedere [monitorare l'Appliance usando la Console di amministrazione &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
2.  Verificare gli indicatori di stato per tutti i nodi dello stato dell'Appliance.  
  
    -   È possibile continuare con verde o indicatori NA senza problemi.  
  
    -   Restituire errori avviso (giallo) non critici. In alcuni casi i messaggi di avviso non blocca gli aggiornamenti. Se è presente un errore di volume del disco non critiche che non è nell'unità C:\, è possibile procedere al passaggio successivo prima di aver risolto l'errore di volume del disco.  
  
    -   La maggior parte degli indicatori rossi devono essere risolto prima di continuare. Se sono presenti errori del disco, utilizzare la pagina avvisi della Console amministrazione per verificare che vi sia non più di un errore del disco all'interno di ogni server o un array SAN. Se si verifica un errore di non più di un disco all'interno di ogni server o un array SAN, è possibile procedere al passaggio successivo prima di correggere gli errori del disco. Assicurarsi di contattare il supporto Microsoft per risolvere gli errori del disco appena possibile.  
  
#### <a name="synchronize-the-wsus-server"></a>Sincronizzare il server WSUS  
  
1.  Accedere alla macchina virtuale VMM come amministratore di dominio.  
  
2.  Nel **Dashboard di Server Manager**via il **Tools** dal menu fare clic su **Windows Server Update Services** (**wsus.msc**).  
  
3.  Nella Console di amministrazione di WSUS fare clic su **sincronizzazioni**.  
  
4.  Se la sincronizzazione non è in esecuzione, fare clic su **Sincronizza adesso** nel riquadro di destra. Nel riquadro inferiore, esisterà un stato di sincronizzazione. Attendere la sincronizzazione è stata completata.  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>Approvare gli aggiornamenti Microsoft in Windows Server Update Services  
  
1.  Nel riquadro sinistro della console di WSUS, fare clic su **tutti gli aggiornamenti**.  
  
2.  Nel **tutti gli aggiornamenti** riquadro, fare clic sui **approvazione** dal menu a discesa, set **approvazione** a **tutti tranne i rifiutati**. Fare clic sui **lo stato** dal menu a discesa, set **stato** a **qualsiasi**. Fare clic su **Aggiorna**.  
  
    Fare doppio clic il **Title** colonna e selezionare **lo stato del File** per verificare lo stato del file dopo aver completato il download.  
  
    È anche possibile selezionare **gli aggiornamenti critici** oppure **gli aggiornamenti della sicurezza** nei sinistro riquadro e visualizzare gli aggiornamenti disponibili per queste categorie.  
  
    ![Selezionare tutti gli aggiornamenti e impostare lo stato su qualsiasi. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
3.  Selezionare tutti gli aggiornamenti e quindi scegliere il **Approva** collegamento nel riquadro di destra.  
  
    È possibile anche fare doppio clic sugli aggiornamenti selezionati e quindi fare clic su **Approva**. Potrebbe essere richiesto di accettare il "Software condizioni di licenza Microsoft". In questo caso, fare clic su **accetto** nella finestra di continuare.  
  
    ![Selezionare tutti gli aggiornamenti applicabili e fare clic su Approva. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
4.  Selezionare il gruppo di server di appliance creato nella [configurare Windows Server Update Services &#40;WSUS&#41; &#40;sistema di piattaforma Analitica&#41;](configure-windows-server-update-services-wsus.md).  
  
5.  Fare clic su **approvato per l'installazione**, quindi fare clic su **OK**.  
  
    ![Approvare gli aggiornamenti per il gruppo di computer. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
6.  Nel **stato approvazione** della finestra di dialogo quando il processo di approvazione è stato completato, fare clic su **Chiudi**.  
  
    ![Chiudi finestra quando gli aggiornamenti vengono approvati. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>Verificare che gli aggiornamenti WSUS  
  
-  Verificare lo stato del file di tutti gli aggiornamenti. Ogni file deve avere un'icona di freccia verde a sinistra del titolo. Indica che il file è pronto per l'installazione.  
  
    ![Lo stato del file ha esito positivo](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    Prima di installare gli aggiornamenti, assicurarsi che siano tutti scaricati e resi disponibili nella console di WSUS.  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>Per verificare che tutti gli aggiornamenti vengono scaricati  
  
-  Verificare i **Scarica stato** degli aggiornamenti nella console di WSUS come illustrato nello screenshot seguente. Verificare che **aggiornamenti che richiedono file** deve essere 0 per verificare che tutti gli aggiornamenti vengono scaricati. Se questo numero è maggiore di zero, si potrebbe essere necessario tornare indietro e approvare aggiornamenti aggiuntivi.  
  
    ![Verificare che tutti gli aggiornamenti vengono scaricati. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>Applicare aggiornamenti Microsoft  
  
1.  Prima di iniziare, aprire il [monitorare l'Appliance usando la Console di amministrazione &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-the-admin-console.md), fare clic sui **stato dello strumento** scheda e verificare che il  **Cluster** e **rete** colonne Mostra verde (o NA) per tutti i nodi. In presenza di eventuali avvisi in una di queste colonne, l'appliance potrebbe non essere in grado di installare gli aggiornamenti in modo corretto. Risolvere tutti gli avvisi esistenti nel **Cluster** e **rete** colonne prima di procedere.  
  
2.  Accedere al _< nome_dominio >_**-HST01** nodo come l'amministratore di dominio di Fabric.  
  
3.  Per applicare tutti gli aggiornamenti approvati per Windows Server Update Services, eseguire il programma di aggiornamento. Visualizzare [eseguire il programma di aggiornamento](#RunUpdateWizard) sotto per le istruzioni.  
  
#### <a name="verify-the-updates-on-all-nodes"></a>Verificare gli aggiornamenti in tutti i nodi  
  
1.  Dal nodo di VMM, avviare la Console di amministrazione di WSUS. Questa applicazione sono disponibili in **avviare**, **strumenti di amministrazione**, **Windows Server Update Services**.  
  
2.  Espandere **computer**.  
  
3.  Espandere **tutti i computer**.  
  
4.  Selezionare il gruppo di server di appliance creato nella [configurare Windows Server Update Services &#40;WSUS&#41; &#40;sistema di piattaforma Analitica&#41;](configure-windows-server-update-services-wsus.md).  
  
5.  Nel **lo stato** elenco a discesa dal menu **qualsiasi** e fare clic su **Aggiorna**.  
  
6.  Espandere **servizi di aggiornamento**, *<appliance name>*- VMM **aggiornamenti**, **tutti gli aggiornamenti**, dove *<appliance name>* è il nome dell'appliance.  
  
7.  Nel **tutti gli aggiornamenti** finestra set **approvazione** al **tutti tranne i rifiutati**.  
  
8.  Nel **tutti gli aggiornamenti** impostare nella finestra **stato** al **non è stato possibile o necessario**.  
  
9. Fare clic su **Aggiorna**.  
  
10. Se **aggiornamenti necessari** è maggiore di zero, contattare il supporto tecnico per assistenza.  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>Assicurarsi che non siano presenti avvisi critici nella Console di amministrazione di SQL Server PDW  
  
1.  Aprire la Console di amministrazione, fare clic sulla scheda stato dello strumento. Visualizzare [monitorare l'Appliance usando la Console di amministrazione &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-the-admin-console.md).  
  
2.  Verificare che il **Cluster** e **rete** colonne Mostra verde (o NA) per tutti i nodi. In presenza di eventuali avvisi in una di queste colonne, l'appliance potrebbe non essere in grado di installare gli aggiornamenti in modo corretto. Contattare il supporto tecnico se esistono eventuali avvisi critici.  
  
## <a name="RunUpdateWizard"></a>Eseguire il programma di aggiornamento  
Seguire queste istruzioni per eseguire il programma di aggiornamento del sistema della piattaforma Analitica.  
  
> [!NOTE]  
> Il sistema di Windows Server Update Services è progettato per eseguire in modo asincrono potrebbe richiedere alcuni minuti per applicare completamente tutti gli aggiornamenti. Avviare un aggiornamento consente di pianificare un aggiornamento ma non garantisce l'attività di aggiornamento immediato.  
  
1.  Assicurarsi che si è connessi al nodo HST01 come l'amministratore di dominio di Fabric.  
  
2.  Aprire una finestra del prompt dei comandi e immettere i comandi seguenti. Sostituire *<parameter>* con le informazioni designate.  
  
**Per eseguire l'aggiornamento di Microsoft:**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**Per segnalare lo stato di Microsoft Update:**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>Vedere anche  
[Disinstallare gli aggiornamenti di Microsoft &#40;sistema di piattaforma Analitica&#41;](uninstall-microsoft-updates.md)  
[Applicare gli hotfix del sistema di piattaforma Analitica &#40;sistema di piattaforma Analitica&#41;](apply-analytics-platform-system-hotfixes.md)  
[Disinstallare gli aggiornamenti rapidi del sistema di piattaforma Analitica &#40;sistema di piattaforma Analitica&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Manutenzione software &#40;sistema di piattaforma Analitica&#41;](software-servicing.md)  
  
