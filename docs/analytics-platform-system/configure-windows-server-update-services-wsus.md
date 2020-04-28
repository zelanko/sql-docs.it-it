---
title: Configurare WSUS
description: Queste istruzioni illustrano i passaggi per l'uso della configurazione guidata di Windows Server Update Services (WSUS) per configurare WSUS per il sistema di piattaforma di analisi.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 089b76d7167b8561c93b01837dc2189c833362fd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "76761905"
---
# <a name="configure-windows-server-update-services-wsus-in-analytics-platform-system"></a>Configurare Windows Server Update Services (WSUS) nel sistema della piattaforma Analytics
Queste istruzioni illustrano i passaggi per l'uso della configurazione guidata di Windows Server Update Services (WSUS) per configurare WSUS per il sistema di piattaforma di analisi. Prima di poter applicare gli aggiornamenti software al dispositivo, è necessario configurare WSUS. WSUS è già installato nella macchina virtuale VMM del dispositivo.  
  
Per ulteriori informazioni sulla configurazione di WSUS, vedere la [Guida all'installazione dettagliata di WSUS](https://go.microsoft.com/fwlink/?LinkId=202417) nel sito Web WSUS. Dopo aver configurato WSUS, vedere [scaricare e applicare Microsoft updates &#40;&#41;Platform System](download-and-apply-microsoft-updates.md) per avviare un aggiornamento.  
  
> [!WARNING]  
> Se si verificano errori durante il processo di configurazione, arrestare e contattare il supporto tecnico per assistenza. Non ignorare gli errori o continuare il processo dopo la ricezione degli errori.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
Per configurare WSUS, è necessario:  
  
-   Ottenere le informazioni di accesso dell'account amministratore di dominio dell'appliance di sistema della piattaforma Analytics.  
  
-   Avere un account di accesso del sistema della piattaforma Analytics con le autorizzazioni per accedere alla **console di amministrazione** e visualizzare le informazioni sullo stato dell'appliance.  
  
-   Conosce l'indirizzo IP del server WSUS upstream se si prevede di sincronizzare gli aggiornamenti da un server WSUS upstream invece di sincronizzare gli aggiornamenti direttamente da Microsoft Update. Verificare che il server WSUS upstream sia impostato in modo da consentire connessioni anonime e supporta SSL.  
  
-   Conosce l'indirizzo IP del server proxy se l'appliance utilizzerà un server proxy per accedere al server upstream o Microsoft Update.  
  
-   Nella maggior parte dei casi WSUS deve accedere ai server all'esterno dell'appliance. Per supportare questo scenario di utilizzo, è possibile configurare il DNS del sistema della piattaforma di analisi per supportare un server di un server d'utilità esterno che consentirà agli host e alle macchine virtuali di sistema della piattaforma di analisi di usare server DNS esterni per risolvere i nomi all'esterno dell'appliance. Per altre informazioni, vedere [usare un server di trasmissione DNS per risolvere i nomi DNS non Appliance &#40;&#41;del sistema della piattaforma di analisi ](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
## <a name="to-configure-windows-server-update-services-wsus"></a>Per configurare Windows Server Update Services (WSUS)  
  
1.  Accedere alla **console di amministrazione**. Nella scheda **stato Appliance** verificare che le colonne **cluster** e **rete** mostrino il verde (o **na**) per tutti i nodi. Verificare gli indicatori di stato per tutti i nodi nello **stato dell'appliance**.  
  
    -   È possibile continuare con gli indicatori verde o NA.  
  
    -   Valutare gli errori di avviso non critici (giallo). In alcuni casi, i messaggi di avviso non bloccano gli aggiornamenti. Se si verifica un errore non critico del volume del disco che non si trova nel C:\ è possibile procedere al passaggio successivo prima di risolvere l'errore relativo al volume del disco.  
  
    -   Prima di continuare, è necessario risolvere la maggior parte degli indicatori rossi. Se sono presenti errori del disco, usare la pagina **avvisi della console di amministrazione** per verificare che non siano presenti più errori del disco in ogni server o matrice San. Se non è presente più di un errore del disco in ogni server o matrice SAN, è possibile procedere al passaggio successivo prima di correggere gli errori del disco. Assicurarsi di contattare il supporto tecnico Microsoft per correggere gli errori del disco il prima possibile.  
  
2.  Accedere alla macchina virtuale VMM come amministratore di dominio dell'appliance.  
  
3.  Avviare la configurazione guidata.  
  
    #### <a name="to-launch-the-configuration-wizard"></a>Per avviare la configurazione guidata  
  
    1.  Nel **Dashboard Server Manager**scegliere **Windows Server Update Services**dal menu **strumenti** .  
  
    2.  Nel riquadro sinistro della finestra **Update Services** fare clic per espandere il server del nodo di gestione della macchina virtuale (**_appliance_domain_-VMM**), quindi fare clic su **Opzioni**.  
  
    3.  Nel riquadro **Opzioni** fare clic su **Configurazione guidata server WSUS** per avviare la configurazione guidata.  
  
        ![Menu del dashboard di Gestione server](./media/configure-windows-server-update-services-wsus/WSUS_Wiz0.png "WSUS_Wiz0")  
  
    4.  Se è la prima volta che si esegue la procedura guidata WSUS, è possibile che venga richiesto di configurare una directory per l'archiviazione degli aggiornamenti. `C:\wsus`è un percorso appropriato. Tuttavia, è possibile specificare un percorso diverso.  
  
        ![WSUS - Percorso](./media/configure-windows-server-update-services-wsus/WSUS_Wiz1.png "WSUS_Wiz1")  
  
    5.  Prima di completare la procedura guidata, esaminare **prima di iniziare** l'elenco degli elementi da completare.  
  
        ![WSUS - Prima di iniziare](./media/configure-windows-server-update-services-wsus/WSUS_Wiz2.png "WSUS_Wiz2")  
  
    6.  Nella pagina **partecipa al programma di miglioramento del Microsoft Update** selezionare **Sì, desidero partecipare al programma di analisi del Microsoft Update**, quindi fare clic su **Avanti**.  
  
        ![WSUS - Programma di aggiornamento](./media/configure-windows-server-update-services-wsus/WSUS_Wiz3.png "WSUS_Wiz3")  
  
    A questo punto verrà visualizzata la pagina **scegliere un server upstream** . Lo screenshot seguente è il punto di partenza della configurazione guidata.  
  
    ![WSUS - Sincronizzazione server a monte](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
4.  Scegliere il server upstream.  
  
    Nella pagina **Selezione server upstream** della configurazione guidata WSUS è possibile selezionare il modo in cui WSUS nel nodo di gestione della macchina virtuale si connetterà a un server upstream per ottenere gli aggiornamenti software. Le due opzioni per sincronizzare il server upstream con [Microsoft Update](https://go.microsoft.com/fwlink/?LinkId=133349) o per sincronizzare gli aggiornamenti con un altro server Windows Server Update Services.  
  
    #### <a name="to-update-by-using-microsoft-update"></a>Per eseguire l'aggiornamento usando Microsoft Update  
  
    1.  Se si sceglie di eseguire la sincronizzazione con Microsoft Update, non è necessario apportare alcuna modifica alla pagina **Scegli server upstream** . Fare clic su **Avanti**.  
  
        ![WSUS - Sincronizzazione server a monte](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
    #### <a name="to-update-from-another-wsus-server"></a>Per eseguire l'aggiornamento da un altro server WSUS  
  
    1.  Se si sceglie di eseguire la sincronizzazione con un'origine diversa da Microsoft Update (un server upstream), specificare il server (immettere l'indirizzo IP) e la porta su cui il server comunicherà con il server upstream.  
  
        ![WSUS - Sincronizzazione server a monte da WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4b.png "WSUS_Wiz4b")  
  
    2.  Per usare Secure Sockets Layer (SSL), selezionare la casella di controllo **Usa SSL per la sincronizzazione delle informazioni sugli aggiornamenti** . In tal caso, i server utilizzeranno la porta 443 per la sincronizzazione.  
  
        ![WSUS - Sincronizzazione server a monte da WSUS SSL](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4c.png "WSUS_Wiz4c")  
  
    3.  Se si tratta di un server di replica, selezionare la casella di controllo **Replica del server upstream**. È possibile selezionare entrambi **Usa SSL per la sincronizzazione delle informazioni di aggiornamento** ed **è una replica del server upstream**.  
  
        ![WSUS - Replica server a monte](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4d.png "WSUS_Wiz4d")  
  
    4.  A questo punto, è stata completata la configurazione del server upstream. Fare clic su **Avanti**oppure selezionare **Specifica server proxy** nel riquadro di spostamento a sinistra.  
  
5.  Specificare il server proxy.  
  
    Se il server richiede un server proxy per accedere a Microsoft Update o a un altro server upstream, è possibile configurare le impostazioni del server proxy qui. in caso contrario, fare clic su **Avanti**.  
  
    ![WSUS - Proxy](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5a.png "WSUS_Wiz5a")  
  
    #### <a name="to-configure-proxy-server-settings"></a>Per configurare le impostazioni del server proxy  
  
    1.  Nella pagina **Specifica server proxy** della configurazione guidata selezionare la casella di controllo **Usa un server proxy** per la sincronizzazione, quindi digitare l'indirizzo IP del server proxy (non il nome) e il numero di porta (porta 80 per impostazione predefinita) nelle caselle corrispondenti.  
  
    2.  Se si desidera utilizzare le credenziali di un utente specifico per la connessione al server proxy, selezionare la casella di controllo **Usa credenziali utente per la connessione al server proxy** e quindi immettere il nome utente, il domino e la password dell'utente nelle caselle corrispondenti. Se si desidera abilitare l'autenticazione di base per l'utente si connette al server proxy, selezionare il **Consenti autenticazione di base (password inviata in testo non crittografato)** casella di controllo.  
  
        ![WSUS - Credenziali proxy](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5b.png "WSUS_Wiz5b")  
  
    3.  A questo punto, è stata completata la configurazione del server proxy. Fare clic su **Avanti** per accedere alla pagina successiva, in cui è possibile avviare la configurazione del processo di sincronizzazione.  
  
6.  Avviare la connessione.  
  
    ![WSUS - Connessione avvio proxy](./media/configure-windows-server-update-services-wsus/WSUS_Wiz6.png "WSUS_Wiz6")  
  
    Fare clic su **Avvia connessione**.  
  
    Una volta completata la connessione, fare clic su **Avanti** per passare alla pagina successiva, in cui è possibile scegliere le lingue.  
  
7.  Scegliere lingue.  
  
    Selezionare **Scarica aggiornamenti solo nelle lingue seguenti**.  
  
    Selezionare **inglese**, quindi fare clic su **Avanti**.  
  
    ![Scegliere i linguaggi](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseLanguages.png "SQL_Server_PDW_WSUSChooseLanguages")  
  
8.  Scegliere prodotti.  
  
    > [!NOTE]  
    > Se si utilizza un server upstream, potrebbe non essere possibile scegliere i prodotti. Se questa opzione non è disponibile, ignorare questo passaggio.

    > [!WARNING]  
    > Escludere eventuali aggiornamenti di SQL Server 2016.
  
    Deseleziona tutti gli aggiornamenti selezionati.  
  
    Selezionare **SQL Server 2012**, **SQL Server 2014**, **Windows Server 2012 R2**e **System Center 2012 R2-Virtual Machine Manager**, quindi fare clic su **Avanti**.  
  
9. Scegliere classificazioni.  
  
    > [!NOTE]  
    > Se si utilizza un server upstream, potrebbe non essere possibile scegliere le classificazioni.  Se questa opzione non è disponibile, ignorare questo passaggio.  
  
    Deseleziona tutti gli aggiornamenti selezionati in precedenza.  
  
    Selezionare **gli aggiornamenti critici** e **gli aggiornamenti della sicurezza** per gli aggiornamenti che verranno sincronizzati per l'appliance del sistema della piattaforma Analytics, quindi fare clic su **Avanti**.  
  
    ![Scegliere le classificazioni](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseClassifications.png "SQL_Server_PDW_WSUSChooseClassifications")  
  
10. Configurare la pianificazione della sincronizzazione.  
  
    Selezionare **Sincronizza manualmente**, quindi fare clic su **Avanti**.  
  
    ![Impostare la pianificazione della sincronizzazione](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSyncSchedule.png "SQL_Server_PDW_WSUSSyncSchedule")  
  
11. Avviare la sincronizzazione iniziale.  
  
    Selezionare **inizia sincronizzazione iniziale**, quindi fare clic su **Avanti**.  
  
12. Fine.  
  
    Fare clic su **Fine**.  
  
## <a name="group-the-appliance-servers-in-wsus"></a><a name="bkmk_WSUSGroup"></a>Raggruppare i server appliance in WSUS  
Dopo aver configurato WSUS per il sistema di piattaforma di analisi, il passaggio successivo consiste nel raggruppare i server appliance. Con l'aggiunta di tutti i server appliance a un gruppo, WSUS sarà in grado di applicare gli aggiornamenti software a tutti i server nell'appliance.  
  
> [!NOTE]  
> Il sistema WSUS è progettato per essere eseguito in modo asincrono. L'attività di avvio non sempre comporta un aggiornamento immediato. Pertanto, potrebbe essere necessario attendere qualche minuto prima che i computer siano visibili nelle finestre di dialogo WSUS. L'esecuzione `setup.exe /action=ReportMicrosoftUpdateClientStatus /DomainAdminPassword="<password>"` del comando descritto alla fine dell'argomento [download e Apply Microsoft Updates &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md) può consentire l'aggiornamento delle finestre di dialogo.  
  
#### <a name="to-group-the-appliance-servers"></a>Per raggruppare i server appliance  
  
1.  Aprire la console di WSUS, fare clic con il pulsante destro del mouse su **tutti i computer** , quindi scegliere **Aggiungi gruppo di computer**.  
  
    ![Aggiungere un gruppo di computer.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSAddComputerGroup.png "SQL_Server_PDW_WSUSAddComputerGroup")  
  
2.  Immettere il nome "APS" per il gruppo di computer, quindi fare clic su **Aggiungi**.  
  
    ![Immettere il nome del nuovo gruppo di computer.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSpecifyGroupName.png "SQL_Server_PDW_WSUSSpecifyGroupName")  
  
3.  Fare **di nuovo clic su** **tutti i computer** , modificare lo stato nel menu a discesa **stato** e quindi fare clic su **Aggiorna**. Per visualizzare il nuovo gruppo appena aggiunto, potrebbe essere necessario espandere **tutti i computer** facendo clic su di esso nel controllo struttura ad albero a sinistra.  
  
    ![Modificare lo stato in qualsiasi e fare clic su Aggiorna.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusToAny.png "SQL_Server_PDW_WSUSChangeStatusToAny")  
  
4.  Selezionare tutti i computer che fanno parte dell'appliance, fare clic con il pulsante destro del mouse su, quindi scegliere **modifica appartenenza**.  
  
    ![Modificare l'appartenenza per tutti i computer PDW.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeMembership.png "SQL_Server_PDW_WSUSChangeMembership")  
  
5.  Selezionare il nuovo gruppo di computer creato facendo clic sulla casella di controllo e quindi su **OK**.  
  
    ![Impostare Appartenenza al gruppo di computer](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSetComputerGroupMembership.png "SQL_Server_PDW_WSUSSetComputerGroupMembership")  
  
6.  Selezionare il nuovo gruppo di computer, modificarne **lo stato** su **qualsiasi**, quindi fare clic su **Aggiorna**. Tutti i computer verranno ora assegnati a questo gruppo ed elencati nel riquadro di destra. È in genere possibile continuare quando i nodi visualizzano avvisi come **il nodo non ha ancora segnalato lo stato**.  
  
    ![Impostare lo stato su Qualsiasi e fare clic su Aggiorna.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusAnyRefresh.png "SQL_Server_PDW_WSUSChangeStatusAnyRefresh")  
  
