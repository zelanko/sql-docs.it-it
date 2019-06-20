---
title: Configurare WSUS - sistema di piattaforma Analitica | Microsoft Docs
description: Queste istruzioni illustrano i passaggi per utilizzare la procedura guidata configurazione di Windows Server Update Services (WSUS) per configurare WSUS per il sistema di piattaforma Analitica.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 776859eb291004431a7e4e2743f1c008a7b752dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63134953"
---
# <a name="configure-windows-server-update-services-wsus-in-analytics-platform-system"></a>Configurare Windows Server Update Services (WSUS) nel sistema di piattaforma Analitica
Queste istruzioni illustrano i passaggi per utilizzare la procedura guidata configurazione di Windows Server Update Services (WSUS) per configurare WSUS per il sistema di piattaforma Analitica. È necessario configurare WSUS prima di poter applicare aggiornamenti software per l'appliance. Windows Server Update Services è già installato nella macchina virtuale VMM dell'appliance.  
  
Per altre informazioni sulla configurazione di WSUS, vedere la [Guida all'installazione dettagliata di WSUS](https://go.microsoft.com/fwlink/?LinkId=202417) sul sito Web WSUS. Dopo la configurazione di WSUS, vedere [scaricare e applicare gli aggiornamenti di Microsoft &#40;sistema di piattaforma Analitica&#41; ](download-and-apply-microsoft-updates.md) per avviare un aggiornamento.  
  
> [!WARNING]  
> Se si verificano errori durante questo processo di configurazione, arrestare e contattare il supporto tecnico per assistenza. Non ignorare gli errori o continuare il processo dopo gli errori sono stati ricevuti.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
Per configurare WSUS, è necessario:  
  
-   Disporre le informazioni di accesso Analitica Platform System appliance dominio amministratore account.  
  
-   Avere un account di accesso di sistema di piattaforma Analitica con autorizzazioni di accesso di **Console di amministrazione** e visualizzare le informazioni sullo stato di appliance.  
  
-   Se si prevede di sincronizzare gli aggiornamenti da un server WSUS upstream invece la sincronizzazione degli aggiornamenti direttamente da Microsoft Update, conoscere l'indirizzo IP del server WSUS upstream. Assicurarsi che il server WSUS padre è impostato su Consenti connessioni anonime e supporta SSL.  
  
-   Conoscere l'indirizzo IP del server proxy se il dispositivo utilizzerà un server proxy per accedere al server upstream o Microsoft Update.  
  
-   Nella maggior parte dei casi, è necessario che WSUS accedere ai server all'esterno dell'appliance. Per supportare il DNS di sistema di piattaforma Analitica può essere configurato per supportare un server d'inoltro nome esterno che consentirà al sistema di piattaforma Analitica host e macchine virtuali (VM) da usare server DNS esterni per risolvere i nomi all'esterno di questo scenario di utilizzo di Appliance. Per altre informazioni, vedere [usare un server d'inoltro di DNS per risolvere nomi DNS Non di Appliance &#40;sistema di piattaforma Analitica&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
## <a name="to-configure-windows-server-update-services-wsus"></a>Per configurare Windows Server Update Services (WSUS)  
  
1.  Accedere al **Console di amministrazione**. Nel **lo stato di Appliance** scheda, verificare che il **Cluster** e **rete** colonne mostrano verde (o **NA**) per tutti i nodi. Verificare gli indicatori di stato per tutti i nodi nel **Appliance stato**.  
  
    -   È possibile continuare con verde o indicatori NA senza problemi.  
  
    -   Restituire errori avviso (giallo) non critici. In alcuni casi i messaggi di avviso non blocca gli aggiornamenti. Se è presente un errore di volume del disco non critiche che non è nell'unità C:\, è possibile procedere al passaggio successivo prima di aver risolto l'errore di volume del disco.  
  
    -   La maggior parte degli indicatori rossi devono essere risolto prima di continuare. Se sono presenti errori del disco, usare il **avvisi della Console di amministrazione** pagina per verificare l'errore non più di un disco all'interno di ogni server o un array SAN. Se si verifica un errore di non più di un disco all'interno di ogni server o un array SAN, è possibile procedere al passaggio successivo prima di correggere gli errori del disco. Assicurarsi di contattare il supporto Microsoft per risolvere gli errori del disco appena possibile.  
  
2.  Accedere alla macchina virtuale VMM come amministratore di dominio appliance.  
  
3.  Avviare la configurazione guidata.  
  
    #### <a name="to-launch-the-configuration-wizard"></a>Per avviare la configurazione guidata  
  
    1.  Nel **Dashboard di Server Manager**via il **Tools** dal menu fare clic su **Windows Server Update Services**.  
  
    2.  Nel riquadro sinistro della finestra il **Update Services** finestra, fare clic per espandere il server Virtual Machine Management (**_appliance_domain_- VMM**), quindi fare clic su **Opzioni**.  
  
    3.  Nel **le opzioni** riquadro, fare clic su **configurazione guidata del Server WSUS** per avviare la configurazione guidata.  
  
        ![Menu del Dashboard di Server Manager](./media/configure-windows-server-update-services-wsus/WSUS_Wiz0.png "WSUS_Wiz0")  
  
    4.  Se questa è la prima volta che si esegue la procedura guidata di Windows Server Update Services, potrebbe essere richiesto di configurare una directory per archiviare gli aggiornamenti. `C:\wsus` è una posizione appropriata; Tuttavia è possibile fornire un percorso diverso.  
  
        ![Percorso WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz1.png "WSUS_Wiz1")  
  
    5.  Rivedere le **prima di iniziare** elenco di elementi da completare prima di completare la procedura guidata.  
  
        ![WSUS Before You Begin](./media/configure-windows-server-update-services-wsus/WSUS_Wiz2.png "WSUS_Wiz2")  
  
    6.  Nel **partecipa al programma Analisi utilizzo software di Microsoft Update** pagina, selezionare **Sì, desidero partecipare al programma Analisi utilizzo software di Microsoft Update**, quindi fare clic su **successivo**.  
  
        ![WSUS Improvement Program](./media/configure-windows-server-update-services-wsus/WSUS_Wiz3.png "WSUS_Wiz3")  
  
    Si noterà ora il **scelta Server Upstream** pagina. Lo screenshot seguente è il punto iniziale della procedura guidata configurazione.  
  
    ![WSUS Upstream Server Sync](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
4.  Scegliere il server upstream.  
  
    Nel **scelta Server Upstream** pagina di configurazione guidata WSUS, si selezionerà come Windows Server Update Services nel nodo di gestione delle macchine virtuali si connetterà a un server upstream per ottenere gli aggiornamenti software. Sono disponibili due soluzioni per sincronizzare il server upstream con [Microsoft Update](https://go.microsoft.com/fwlink/?LinkId=133349) o sincronizzare gli aggiornamenti con un altro server Windows Server Update Services.  
  
    #### <a name="to-update-by-using-microsoft-update"></a>Aggiornare tramite Microsoft Update  
  
    1.  Se si sceglie di eseguire la sincronizzazione con Microsoft Update, non occorre apportare modifiche per il **scelta Server Upstream** pagina. Scegliere **Avanti**.  
  
        ![WSUS Upstream Server Sync](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
    #### <a name="to-update-from-another-wsus-server"></a>Aggiornare da un altro server WSUS  
  
    1.  Se si sceglie di eseguire la sincronizzazione con un'origine diversa da Microsoft Update (un server upstream), specificare il server (immettere l'indirizzo IP) e la porta su cui comunicherà il server con il server upstream.  
  
        ![WSUS-sincronizzazione Server a monte da WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4b.png "WSUS_Wiz4b")  
  
    2.  Per utilizzare Secure Sockets Layer (SSL), selezionare la **Usa SSL per la sincronizzazione delle informazioni sugli aggiornamenti** casella di controllo. In tal caso il server userà la porta 443 per la sincronizzazione.  
  
        ![WSUS-sincronizzazione Server a monte da WSUS SSL](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4c.png "WSUS_Wiz4c")  
  
    3.  Se si tratta di un server di replica, selezionare la **si tratta di una replica del server upstream** casella di controllo. È possibile selezionare sia **Usa SSL per la sincronizzazione delle informazioni di aggiornamento** e **si tratta di una replica del server upstream**.  
  
        ![WSUS Upstream Server Replica](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4d.png "WSUS_Wiz4d")  
  
    4.  A questo punto, si è finito con configurazione del server upstream. Fare clic su **successivo**, o selezionare **server proxy specificare** nel riquadro di spostamento a sinistra.  
  
5.  Specificare il server proxy.  
  
    Se questo server richiede un server proxy per accedere a Microsoft Update o un altro server upstream, è possibile configurare le impostazioni del server proxy in questo contesto. in caso contrario, fare clic su **successivo**.  
  
    ![WSUS Proxy](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5a.png "WSUS_Wiz5a")  
  
    #### <a name="to-configure-proxy-server-settings"></a>Per configurare le impostazioni di proxy server  
  
    1.  Nel **specificare il Server Proxy** pagina della procedura guidata configurazione, selezionare la **Usa un server proxy durante la sincronizzazione** casella di controllo e quindi digitare l'indirizzo IP del proxy server (non nome) e il numero di porta (porta 80 per impostazione predefinita) nelle caselle corrispondenti.  
  
    2.  Se si desidera connettersi al server proxy usando le credenziali utente specifico, selezionare la **usare le credenziali dell'utente per connettersi al server proxy** casella di controllo e quindi digitare il nome utente, dominio e password dell'utente nel corrispondente finestre. Se si desidera abilitare l'autenticazione di base per l'utente si connette al server proxy, selezionare la **Consenti autenticazione di base (password inviata in testo non crittografato)** casella di controllo.  
  
        ![WSUS Proxy Credentials](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5b.png "WSUS_Wiz5b")  
  
    3.  A questo punto, si è finito con configurazione del server proxy. Fare clic su **successivo** per passare alla pagina successiva, in cui è possibile iniziare a configurare il processo di sincronizzazione.  
  
6.  Avviare la connessione.  
  
    ![Connessione avvio Proxy WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz6.png "WSUS_Wiz6")  
  
    Fare clic su **avviare la connessione**.  
  
    Dopo la connessione ha avuto esito positivo, fare clic su **successivo** per passare alla pagina successiva, in cui è possibile scegliere le lingue.  
  
7.  Scegliere le lingue.  
  
    Selezionare **Scarica aggiornamenti solo nelle lingue seguenti**.  
  
    Selezionare **inglese**, quindi fare clic su **successivo**.  
  
    ![Scegliere le lingue](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseLanguages.png "SQL_Server_PDW_WSUSChooseLanguages")  
  
8.  Scegliere i prodotti.  
  
    > [!NOTE]  
    > Se si usa un Server Upstream, potrebbe non essere in grado di scegliere i prodotti. Se questa opzione non è disponibile, ignorare questo passaggio.  
  
    Deselezionare tutti gli aggiornamenti selezionati.  
  
    Selezionare **Windows Server 2012 R2**, e **System Center 2012 R2 - Virtual Machine Manager**, quindi fare clic su **Next**.  
  
9. Scegliere le classificazioni.  
  
    > [!NOTE]  
    > Se si usa un Server Upstream, potrebbe non essere in grado di scegliere le classificazioni.  Se questa opzione non è disponibile, ignorare questo passaggio.  
  
    Deselezionare tutti gli aggiornamenti selezionati in precedenza.  
  
    Selezionare **gli aggiornamenti critici** e **gli aggiornamenti della sicurezza** per gli aggiornamenti che verranno sincronizzati per l'appliance del sistema di piattaforma Analitica e quindi fare clic su **Next**.  
  
    ![Scegliere le classificazioni](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseClassifications.png "SQL_Server_PDW_WSUSChooseClassifications")  
  
10. Configurare la pianificazione della sincronizzazione.  
  
    Selezionare **sincronizzare manualmente**, quindi fare clic su **successivo**.  
  
    ![Pianificazione sincronizzazione impostata](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSyncSchedule.png "SQL_Server_PDW_WSUSSyncSchedule")  
  
11. Avvia sincronizzazione iniziale.  
  
    Selezionare **Avvia sincronizzazione iniziale**, quindi fare clic su **successivo**.  
  
12. Fine.  
  
    Scegliere **Fine**.  
  
## <a name="bkmk_WSUSGroup"></a>Raggruppare i server di Appliance in WSUS  
Dopo la configurazione di WSUS per il sistema di piattaforma Analitica, il passaggio successivo consiste nel raggruppare i server di appliance. Quando si aggiungono tutti i server di appliance a un gruppo, Windows Server Update Services sarà in grado di applicare gli aggiornamenti software a tutti i server nell'appliance.  
  
> [!NOTE]  
> Il sistema di Windows Server Update Services è progettato per eseguire in modo asincrono. Avvio di attività non restituisce sempre un aggiornamento immediatamente. Di conseguenza, potrebbe essere necessario attendere qualche minuto, fino a quando i computer saranno visibili nelle finestre di dialogo di Windows Server Update Services. In esecuzione la `setup.exe /action=ReportMicrosoftUpdateClientStatus /DomainAdminPassword="<password>"` comando descritto alla fine dell'argomento [scaricare e applicare gli aggiornamenti Microsoft &#40;sistema di piattaforma Analitica&#41; ](download-and-apply-microsoft-updates.md) consentono di aggiornare le finestre di dialogo.  
  
#### <a name="to-group-the-appliance-servers"></a>Per raggruppare i server di appliance  
  
1.  Aprire la console WSUS, fare doppio clic su **tutti i computer** e quindi fare clic su **Aggiungi gruppo di Computer**.  
  
    ![Add a computer group.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSAddComputerGroup.png "SQL_Server_PDW_WSUSAddComputerGroup")  
  
2.  Immettere il nome "Punti di accesso" per il gruppo di computer e quindi fare clic su **Add**.  
  
    ![Immettere il nome del nuovo gruppo di computer. ] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSpecifyGroupName.png "SQL_Server_PDW_WSUSSpecifyGroupName")  
  
3.  Fare clic su **tutti i computer** anche in questo caso, modificare lo stato nel **lo stato** menu di scelta rapida per **qualsiasi**, quindi fare clic su **Aggiorna**. Potrebbe essere necessario espandere **tutti i computer** facendovi clic sopra su controllo albero sulla sinistra per visualizzare il nuovo gruppo appena aggiunto.  
  
    ![Impostare lo stato su qualsiasi e fare clic su Aggiorna. ] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusToAny.png "SQL_Server_PDW_WSUSChangeStatusToAny")  
  
4.  Selezionare tutti i computer che fanno parte dell'appliance, pulsante destro del mouse e quindi fare clic su **Modifica appartenenza**.  
  
    ![Modificare l'appartenenza per tutti i computer PDW. ] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeMembership.png "SQL_Server_PDW_WSUSChangeMembership")  
  
5.  Selezionare il nuovo gruppo di computer creato facendo clic la casella di controllo e quindi scegliendo **OK**.  
  
    ![Set Computer Group Membership](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSetComputerGroupMembership.png "SQL_Server_PDW_WSUSSetComputerGroupMembership")  
  
6.  Selezionare il nuovo gruppo di computer, modificare relativo **lo stato** a **qualsiasi**, quindi fare clic su **Aggiorna**. Tutti i computer devono essere assegnati a questo gruppo ed elencati nel riquadro di destra. È in genere possibile continuare senza problemi quando i nodi vengono visualizzati avvisi, ad esempio **questo nodo non ha segnalato lo stato ancora**.  
  
    ![Impostare lo stato su qualsiasi e fare clic su Aggiorna. ] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusAnyRefresh.png "SQL_Server_PDW_WSUSChangeStatusAnyRefresh")  
  
