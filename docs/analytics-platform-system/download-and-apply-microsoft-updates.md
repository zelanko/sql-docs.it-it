---
title: Scarica gli aggiornamenti Microsoft
description: In questo argomento viene illustrato come scaricare gli aggiornamenti dal catalogo Microsoft Update in Windows Server Update Services (WSUS) e come applicare tali aggiornamenti ai server degli appliance del sistema della piattaforma di analisi. Microsoft Update installerà tutti gli aggiornamenti applicabili per Windows e SQL Server. WSUS è installato nella macchina virtuale VMM del dispositivo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2b24d55720d6db5997bfa85c2621f0e8d58c5f95
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401197"
---
# <a name="download-and-apply-microsoft-updates-for-analytics-platform-system"></a>Scaricare e applicare Microsoft Updates for Analytics Platform System
In questo argomento viene illustrato come scaricare gli aggiornamenti dal catalogo Microsoft Update in Windows Server Update Services (WSUS) e come applicare tali aggiornamenti ai server degli appliance del sistema della piattaforma di analisi. Microsoft Update installerà tutti gli aggiornamenti applicabili per Windows e SQL Server. WSUS è installato nella macchina virtuale VMM del dispositivo.  
  
## <a name="before-you-begin"></a><a name="TOP"></a>Prima di iniziare  
  
> [!WARNING]  
> Non tentare di applicare gli aggiornamenti se il dispositivo o qualsiasi componente dell'appliance non è attivo o si trova in uno stato di failover. In tal caso, contattare il supporto tecnico per assistenza.  
>   
> Non applicare gli aggiornamenti Microsoft mentre l'appliance è in uso. L'applicazione di aggiornamenti può causare il riavvio del nodo Appliance. Gli aggiornamenti devono essere applicati durante una finestra di manutenzione quando l'appliance non è in uso.  
  
### <a name="prerequisites"></a>Prerequisiti  
Prima di eseguire questi passaggi, è necessario:  
  
-   Configurare WSUS nell'appliance seguendo le istruzioni riportate in [configure Windows Server Update Services &#40;wsus&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md).  
  
-   Conoscenza delle informazioni di accesso di un account amministratore di dominio infrastruttura.  
  
-   Disporre di un account di accesso con le autorizzazioni per accedere alla console di amministrazione del sistema Analytics Platform e visualizzare le informazioni sullo stato dell'appliance.  
  
-   Nella maggior parte dei casi WSUS deve accedere ai server all'esterno dell'appliance. Per supportare questo scenario di utilizzo, è possibile configurare il DNS del sistema della piattaforma di analisi per supportare un server di un server d'utilità esterno che consentirà agli host e alle macchine virtuali di sistema della piattaforma di analisi di usare server DNS esterni per risolvere i nomi all'esterno dell'appliance. Per altre informazioni, vedere [usare un server di trasmissione DNS per risolvere i nomi DNS non Appliance &#40;&#41;del sistema della piattaforma di analisi ](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
## <a name="to-download-and-apply-microsoft-updates"></a><a name="bkmk_ImportUpdates"></a>Per scaricare e applicare gli aggiornamenti Microsoft  
  
#### <a name="verify-the-appliance-state-indicators"></a>Verificare gli indicatori di stato dell'appliance  
  
1.  Aprire la console di amministrazione e passare alla pagina stato dell'appliance. Per altre informazioni, vedere [monitorare l'appliance usando la console di amministrazione &#40;il sistema di piattaforma di analisi&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
2.  Verificare gli indicatori di stato per tutti i nodi nello stato dell'appliance.  
  
    -   È possibile continuare con gli indicatori verde o NA.  
  
    -   Valutare gli errori di avviso non critici (giallo). In alcuni casi, i messaggi di avviso non bloccano gli aggiornamenti. Se si verifica un errore non critico del volume del disco che non si trova nel C:\ è possibile procedere al passaggio successivo prima di risolvere l'errore relativo al volume del disco.  
  
    -   Prima di continuare, è necessario risolvere la maggior parte degli indicatori rossi. Se sono presenti errori del disco, usare la pagina avvisi della console di amministrazione per verificare che non siano presenti più errori del disco in ogni server o matrice SAN. Se non è presente più di un errore del disco in ogni server o matrice SAN, è possibile procedere al passaggio successivo prima di correggere gli errori del disco. Assicurarsi di contattare il supporto tecnico Microsoft per correggere gli errori del disco il prima possibile.  
  
#### <a name="synchronize-the-wsus-server"></a>Sincronizzare il server WSUS  
  
1.  Accedere alla macchina virtuale VMM come amministratore di dominio.  
  
2.  Nel **Dashboard Server Manager**scegliere **Windows Server Update Services** (**WSUS. msc**) dal menu **strumenti** .  
  
3.  Nella console di amministrazione di WSUS fare clic su **sincronizzazioni**.  
  
4.  Se la sincronizzazione non è in esecuzione, fare clic su **Sincronizza ora** nel riquadro di destra. Nel riquadro inferiore sarà presente uno stato di sincronizzazione. Attendere il completamento della sincronizzazione.  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>Approva gli aggiornamenti Microsoft in WSUS  
  
1.  Nel riquadro sinistro della console di WSUS fare clic su **tutti gli aggiornamenti**.  
  
2.  Nel riquadro **tutti gli aggiornamenti** , fare clic sul menu a discesa **approvazione** , impostare **approvazione** su **any eccetto rifiutato**. Fare clic sul menu a discesa **stato** , impostare **stato** su **any**. Fare clic su **Aggiorna**.  
  
    Fare clic con il pulsante destro del mouse sulla colonna **title** e selezionare **stato file** per verificare lo stato del file al termine del download.  
  
    È anche possibile selezionare **gli aggiornamenti critici** o **gli aggiornamenti della sicurezza** nel riquadro sinistro e visualizzare gli aggiornamenti disponibili per queste categorie.  
  
    ![Selezionare tutti gli aggiornamenti e impostare lo stato su Qualsiasi.](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
3.  Selezionare tutti gli aggiornamenti, quindi fare clic sul collegamento **approva** nel riquadro di destra.  
  
    È anche possibile fare clic con il pulsante destro del mouse sugli aggiornamenti selezionati, quindi scegliere **approva**. Potrebbe essere richiesto di accettare le condizioni di licenza software Microsoft. In tal caso, fare clic su **Accetto** nella finestra per continuare.  
  
    ![Selezionare tutti gli aggiornamenti applicabili e fare clic su Approva.](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
4.  Selezionare il gruppo di Server Appliance creato in [configurare Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md).  
  
5.  Fare clic su **Approvato per l'installazione**e quindi su **OK**.  
  
    ![Approvare gli aggiornamenti per il gruppo di computer.](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
6.  Quando il processo di approvazione è completo nella finestra di dialogo **stato approvazione** , fare clic su **Chiudi**.  
  
    ![Chiudere la finestra una volta approvati gli aggiornamenti.](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>Verificare che gli aggiornamenti siano in WSUS  
  
-  Verificare lo stato del file di tutti gli aggiornamenti. Ogni file deve avere un'icona a freccia verde a sinistra del titolo. Indica che il file è pronto per l'installazione.  
  
    ![Lo stato del file è corretto](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    Prima di installare gli aggiornamenti, assicurarsi che siano tutti scaricati e disponibili nella console di WSUS.  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>Per verificare che tutti gli aggiornamenti vengano scaricati  
  
-  Verificare lo **stato di download** degli aggiornamenti nella console WSUS come illustrato nello screenshot seguente. Verificare che **gli aggiornamenti necessari per i file** siano 0 per confermare che tutti gli aggiornamenti vengano scaricati. Se questo numero è maggiore di zero, potrebbe essere necessario tornare indietro e approvare altri aggiornamenti.  
  
    ![Verificare che tutti gli aggiornamenti vengano scaricati.](./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>Applicare gli aggiornamenti Microsoft  
  
1.  Prima di iniziare, aprire il [monitoraggio dell'appliance usando la console di amministrazione &#40;&#41;di sistema della piattaforma di analisi ](monitor-the-appliance-by-using-the-admin-console.md), fare clic sulla scheda **stato dell'appliance** e verificare che le colonne **cluster** e **rete** mostrino il verde (o na) per tutti i nodi. Se sono presenti avvisi in una di queste colonne, l'appliance potrebbe non essere in grado di installare correttamente gli aggiornamenti. Prima di procedere, indirizzare tutti gli avvisi esistenti nel **cluster** e nelle colonne di **rete** .  
  
2.  Accedere al _<domain_name nodo>_ **-HST01** come amministratore di dominio dell'infrastruttura.  
  
3.  Per applicare tutti gli aggiornamenti approvati per WSUS, eseguire il programma di aggiornamento. Per istruzioni, vedere [eseguire il programma di aggiornamento](#RunUpdateWizard) riportato di seguito.  
  
#### <a name="verify-the-updates-on-all-nodes"></a>Verificare gli aggiornamenti in tutti i nodi  
  
1.  Dal nodo VMM avviare la console di amministrazione di WSUS. Questa applicazione è disponibile in **Start**, **strumenti di amministrazione** **Windows Server Update Services**.  
  
2.  Espandere **computer**.  
  
3.  Espandere **tutti i computer**.  
  
4.  Selezionare il gruppo di Server Appliance creato in [configurare Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md).  
  
5.  Nel menu a discesa **stato** selezionare **any** , quindi fare clic su **Aggiorna**.  
  
6.  Espandere **Update Services**, *<appliance name>*-VMM, **Updates**, **All Updates**, dove *<appliance name>* è il nome dell'appliance.  
  
7.  Nella finestra **tutti gli aggiornamenti** impostare **approvazione** su **any eccetto rifiutato**.  
  
8.  Nella finestra **tutti gli aggiornamenti** impostare **stato** su **non riuscito o necessario**.  
  
9. Fare clic su **Aggiorna**.  
  
10. Se **gli aggiornamenti necessari** sono maggiori di zero, contattare il supporto tecnico per assistenza.  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>Verificare che non siano presenti avvisi critici nella console di amministrazione di SQL Server PDW  
  
1.  Aprire la console di amministrazione e fare clic sulla scheda stato Appliance. Vedere [monitorare l'appliance usando la console di amministrazione &#40;&#41;di sistema della piattaforma di analisi ](monitor-the-appliance-by-using-the-admin-console.md).  
  
2.  Verificare che le colonne **cluster** e **rete** mostrino il verde (o na) per tutti i nodi. Se sono presenti avvisi in una di queste colonne, l'appliance potrebbe non essere in grado di installare correttamente gli aggiornamenti. Se sono presenti avvisi critici, contattare il supporto tecnico.  
  
## <a name="run-the-update-program"></a><a name="RunUpdateWizard"></a>Eseguire il programma di aggiornamento  
Seguire queste istruzioni per eseguire il programma di aggiornamento del sistema della piattaforma di analisi.  
  
> [!NOTE]  
> Il sistema WSUS è progettato per essere eseguito in modo asincrono e può richiedere del tempo per applicare completamente tutti gli aggiornamenti. Quando si avvia un aggiornamento, viene pianificato un aggiornamento, ma non viene garantita l'attività di aggiornamento immediato.  
  
1.  Assicurarsi di essere connessi al nodo HST01 come amministratore di dominio dell'infrastruttura.  
  
2.  Aprire una finestra del prompt dei comandi e immettere i comandi seguenti. Sostituire *<parameter>* con le informazioni designate.  
  
**Per eseguire la Microsoft Update:**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**Per segnalare lo stato Microsoft Update:**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>Vedere anche  
[Disinstallare Microsoft Updates &#40;piattaforma del sistema di analisi&#41;](uninstall-microsoft-updates.md)  
[Applicare gli hotfix del sistema di piattaforma di analisi &#40;piattaforma di strumenti analitici&#41;](apply-analytics-platform-system-hotfixes.md)  
[Disinstalla hotfix del sistema della piattaforma di analisi &#40;piattaforma di strumenti analitici&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Servizio software &#40;piattaforma di strumenti di analisi&#41;](software-servicing.md)  
  
