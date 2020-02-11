---
title: Configurare InfiniBand
description: Viene descritto come configurare le schede di rete InfiniBand in un server client non Appliance per la connessione al nodo di controllo in Parallel data warehouse (PDW). Usare queste istruzioni per la connettività di base e per la disponibilità elevata, in modo che il caricamento, il backup e altri processi si connettano automaticamente alla rete InfiniBand attiva.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 583d7617c0620d5d1ec24d60fbf10435a547616d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401297"
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>Configurare le schede di rete InfiniBand per il sistema di piattaforma Analytics
Viene descritto come configurare le schede di rete InfiniBand in un server client non Appliance per la connessione al nodo di controllo in Parallel data warehouse (PDW). Usare queste istruzioni per la connettività di base e per la disponibilità elevata, in modo che il caricamento, il backup e altri processi si connettano automaticamente alla rete InfiniBand attiva.  
  
## <a name="Basics"></a>Descrizione  
Queste istruzioni illustrano come trovare e quindi impostare gli indirizzi IP InfiniBand e le subnet mask corretti sul server connesso a InfiniBand. Spiegano inoltre come impostare il server per l'uso del DNS del dispositivo APS, in modo che la connessione venga risolta nella rete InfiniBand attiva.  
  
Per la disponibilità elevata, gli APS hanno due reti InfiniBand, una attiva e una passiva. Ogni rete InfiniBand ha un indirizzo IP diverso per il nodo di controllo. Se la rete InfiniBand attiva si interrompe, la rete InfiniBand passiva diventa la rete attiva. Quando si verifica questo errore, uno script o un processo si connette automaticamente alla rete InfiniBand attiva senza modificare i parametri dello script.  
  
In particolare, in questo articolo è possibile:  
  
1.  Trovare gli indirizzi IP InfiniBand dei server DNS APS (appliance_domain-AD01 e appliance_domain *-AD02). A tale scopo, accedere ai server AD01 e AD02 e ottenere gli indirizzi IP per ogni rete InfiniBand. Gli indirizzi IP InfiniBand nel nodo AD sono gli indirizzi IP DNS.  
  
2.  Configurare ogni scheda di rete per l'utilizzo di un indirizzo IP disponibile nelle reti InfiniBand APS.  
  
    1.  Se si dispone di due schede di rete InfiniBand, configurare una scheda con un indirizzo IP disponibile nella prima rete InfiniBand denominata TeamIB1 e l'altra scheda con un indirizzo IP disponibile nella seconda rete InfiniBand denominata TeamIB2. Usare l'indirizzo IP appliance_domain-AD01 TeamIB1 come server DNS preferito e appliance_domain-AD02 TeamIB1 indirizzo IP come server DNS alternativo per la scheda di rete TeamIB1. Usare l'indirizzo IP appliance_domain-AD01 TeamIB2 come server DNS preferito e appliance_domain-AD02 TeamIB2 indirizzo IP come server DNS alternativo per la scheda di rete TeamIB2.  
  
    2.  Se si dispone di una sola scheda di rete InfiniBand, configurare l'adapter con un indirizzo IP disponibile da una delle reti InfiniBand. Quindi si configurano i server DNS preferiti e alternativi in questa scheda usando appliance_domain-AD01 TeamIB1 e appliance_domain-AD02 TeamIB1 o usando appliance_domain-AD01 TeamIB2 e appliance_domain-AD02 TeamIB2 a seconda di quale sia lo stesso rete come adapter configurato come i server DNS preferiti e alternativi rispettivamente.  
  
3.  Configurare la scheda di rete InfiniBand per l'utilizzo dei server DNS APS per risolvere la connessione alla rete InfiniBand attiva.  
  
    1.  Per configurare questa impostazione, è possibile usare le impostazioni TCP/IP avanzate per aggiungere il suffisso DNS del dominio dell'appliance all'inizio dell'elenco dei suffissi DNS nel server client. Questa operazione deve essere configurata solo in una delle schede di rete. l'impostazione si applica a entrambe le schede.  
  
Dopo aver configurato le schede di rete InfiniBand, i processi client possono connettersi al nodo di controllo nella rete InfiniBand `PDW_region-SQLCTL01` utilizzando per l'indirizzo del server. Il server aggiunge il suffisso DNS del sistema della piattaforma di analisi oppure è possibile immettere l'indirizzo completo `PDW_region-SQLCTL01.appliance_domain.pdw.local`, ovvero.  
  
Ad esempio, se il nome dell'area PDW è MyPDW e il nome del dispositivo è MyAPS, la specifica del server dwloader per il caricamento dei dati è una delle seguenti:  
  
-   `dwloader -S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader -S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>Prima di iniziare  
  
### <a name="requirements"></a>Requisiti  
È necessario un account di dominio del dispositivo APS per accedere al nodo AD01. Ad esempio, F12345 * \Administrator.  
  
È necessario disporre di un account di Windows nel server client che disponga dell'autorizzazione per configurare le schede di rete.  
  
### <a name="prerequisites"></a>Prerequisites  
Queste istruzioni presuppongono che il server client sia già stato rack e cablato alla rete InfiniBand dell'appliance. Per istruzioni su rack e cablaggio, vedere [acquisire e configurare un server di caricamento](acquire-and-configure-loading-server.md).  
  
### <a name="general-remarks"></a>Osservazioni generali  
Con SQLCTL01, il DNS del sistema della piattaforma di analisi connette il server client al nodo di controllo tramite la rete InfiniBand attiva. Si applica solo alla connessione. Se la rete InfiniBand viene arrestata durante un caricamento o un backup, è necessario riavviare il processo.  
  
Per soddisfare i requisiti aziendali, è anche possibile aggiungere il server client al proprio gruppo di lavoro non Appliance o dominio Windows.  
  
## <a name="Sec1"></a>Passaggio 1: ottenere le impostazioni di rete InfiniBand dell'appliance  
*Per ottenere le impostazioni di rete InfiniBand dell'appliance*  
  
1.  Accedere al nodo AD01 del dispositivo usando l'account appliance_domain \Administrator.  
  
2.  Nel nodo AD01 del dispositivo aprire il pannello di controllo, selezionare rete e Internet, selezionare Centro rete e condivisione *, quindi selezionare Modifica impostazioni scheda.  
  
3.  Nella finestra connessioni di rete fare clic con il pulsante destro del mouse su Team IB1 e scegliere Proprietà.  
  
    ![Connessioni InfiniBand sul nodo di gestione](media/network-teamib.png "Connessioni InfiniBand sul nodo di gestione")  
  
4.  Dalla Finestra Proprietà protocollo Internet versione 4 (TCP/IPv4), annotare i valori per l' **indirizzo IP** e la **subnet mask**.  L'indirizzo IP del nodo ** _dominio\_Appliance_-ad01** è l'indirizzo IP del server DNS del sistema della piattaforma di analisi.  
  
5.  Ripetere i passaggi 1-5 precedenti per l'adattatore TeamIB1 nel server del ** _dominio Appliance\__-ad02** .  
  
    ![Proprietà InfiniBand 1 del nodo di gestione PDW](media/network-ip1-properties.png "Proprietà InfiniBand 1 del nodo di gestione PDW")  
  
6.  Fare clic su Annulla per chiudere la finestra.  
  
7.  Trovare un indirizzo IP non usato nella rete TeamIB1 e annotarlo.  
  
    Per trovare un indirizzo IP non usato, aprire una finestra di comando e provare a effettuare il ping degli indirizzi IP all'interno dell'intervallo di indirizzi del dispositivo. In questo esempio, l'indirizzo IP della rete TeamIB1 è 172.16.14.30. Trovare un indirizzo IP che inizia con 172.16.14 che non è usato. Ad esempio, dalla riga di comando immettere "ping 172.16.14.254". Se la richiesta ping ha esito negativo, l'indirizzo IP è disponibile.  
  
8.  Eseguire la stessa operazione per TeamIB2. Nella finestra * connessioni di rete fare clic con il pulsante destro del mouse su Team IB2 e scegliere Proprietà.  
  
9. Dalla Finestra Proprietà protocollo Internet versione 4 (TCP/IPv4), annotare i valori per l'indirizzo IP e la subnet mask per TeamIB2.  
  
10. Ripetere i passaggi 8-9 precedenti per l'adattatore TeamIB2 nel server appliance_domain-AD02.  
  
    ![Proprietà per TeamIB2](media/network-ip2-properties.png "Proprietà per TeamIB2")  
  
11. Trovare un indirizzo IP non usato nella rete **TeamIB2** e annotarlo.  
  
    Per trovare un indirizzo IP non usato, aprire una finestra di comando e provare a effettuare il ping degli indirizzi IP all'interno dell'intervallo di indirizzi del dispositivo. In questo esempio, l'indirizzo IP della rete TeamIB2 è 172.16.18.30. Trovare un indirizzo IP che inizia con 172.16.18 che non è usato. Ad esempio, dalla riga di comando immettere "ping 172.16.18.254". Se la richiesta ping ha esito negativo, l'indirizzo IP è disponibile.  
  
## <a name="Sec2"></a>Passaggio 2: configurare le impostazioni della scheda di rete InfiniBand nel server client  

### <a name="notes"></a>Note  
  
-   Questi passaggi illustrano come registrare il server con i server DNS APS.  
  
-   Per soddisfare le proprie esigenze di rete, è anche possibile aggiungere il server client al proprio gruppo di lavoro non Appliance o dominio Windows.  
  
-   Istruzioni dettagliate per la configurazione di due schede di rete in ogni server.  Se si dispone di una sola scheda di rete, selezionare una delle reti da configurare nella scheda di rete e quindi aggiungere il secondo indirizzo IP DNS come server DNS alternativo.  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>Per configurare le impostazioni della scheda di rete InfiniBand nel server client  
  
1.  Accedere come amministratore di Windows al caricamento, al backup o a un altro server client nella rete InfiniBand dell'appliance.  
  
2.  Aprire il riquadro di controllo *, selezionare Centro rete e condivisione, quindi selezionare Modifica impostazioni scheda.  
  
### <a name="to-configure-the-first-network-adapter"></a>Per configurare la prima scheda di rete  
  
1.  Nella finestra connessioni di rete fare clic con il pulsante destro del mouse su uno degli slot di rete non identificati per l'adattatore Mellanox e selezionare Proprietà.  
  
    ![Selezione delle reti InfiniBand](media/network-connections.png "Selezione delle reti InfiniBand")  
  
2.  Nella Finestra Proprietà  
  
    1.  Nella scheda Generale impostare l'indirizzo IP sull'indirizzo IP verificato come disponibile nel test di ping per TeamIB1. Per i valori di esempio usati in questo articolo, immettere 172.16.14.254.  
  
    2.  Impostare il subnet mask sul subnet mask annotato per TeamIB1.  
  
    3.  Impostare il server DNS preferito sull'indirizzo IP di TeamIB1 annotato in precedenza dal nodo appliance_domain *-AD01.  
  
    4.  Impostare il server DNS alternativo sull'indirizzo IP di TeamIB1 annotato in precedenza dal nodo appliance_domain *-AD02.  
  
        ![Proprietà della scheda di rete InfiniBand 1](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  Fare clic su OK per applicare le modifiche.  
  
### <a name="to-configure-the-second-network-adapter"></a>Per configurare la seconda scheda di rete  
  
1.  Ignorare questa sezione se si dispone di una sola scheda di rete.  
  
2.  Nella finestra connessioni di rete fare clic con il pulsante destro del mouse sul secondo slot di rete non identificato per l'adattatore Mellanox e selezionare Proprietà.  
  
    ![Selezione delle reti InfiniBand](media/network-connections.png "Selezione delle reti InfiniBand")  
  
3.  Nella Finestra Proprietà  
  
    1.  Nella scheda Generale impostare l'indirizzo IP sull'indirizzo IP verificato come disponibile nel test di ping per TeamIB2. Per i valori di esempio usati in questo articolo, immettere 172.16.18.254.  
  
    2.  Impostare il subnet mask sul subnet mask annotato per TeamIB2.  
  
    3.  Impostare il server DNS preferito sull'indirizzo IP di TeamIB2 annotato in precedenza dal nodo appliance_domain *-AD01.  
  
    4.  Impostare il server DNS alternativo sull'indirizzo IP di TeamIB2 annotato in precedenza dal nodo appliance_domain *-AD02.  
  
        > [!NOTE]  
        > Se è presente una sola scheda di rete, configurare i server DNS preferiti e alternativi usando il dispositivo AD01 TeamIB1 e appliance AD02 TeamIB1 come preferito e i server DNS alternativi rispettivamente oppure usare il dispositivo AD01 TeamIB2 e Appliance AD02 TeamIB2 come i server DNS preferiti e alternativi, a seconda che sia stato eseguito il failover della macchina virtuale AD.  
  
        ![Proprietà della scheda di rete InfiniBand 1](media/network-ib1-properties.png "Proprietà della scheda di rete InfiniBand 1")  
  
    5.  Fare clic su OK per applicare le modifiche.  
  
### <a name="to-configure-the-dns-suffix"></a>Per configurare il suffisso DNS  
  
1.  Nella finestra connessioni di rete fare clic con il pulsante destro del mouse su uno degli slot di rete per l'adattatore Mellanox e selezionare Proprietà.  
  
2.  Fai clic sul pulsante Avanzate... pulsante.  
  
3.  Nella finestra Impostazioni avanzate TCP/IP, se l'opzione Accoda i suffissi DNS (in ordine) non è disattivata, selezionare la casella di controllo Aggiungi questi suffissi DNS (in ordine):, selezionare il suffisso del dominio Appliance e fare clic su Aggiungi. Il suffisso del dominio dell'appliance è`appliance_domain.local`  
  
4.  Se l'opzione Aggiungi questi suffissi DNS (nell'ordine): l'opzione è disattivata, è possibile aggiungere il dominio APS al server modificando la chiave del registro di sistema HKEY_LOCAL_MACHINE \SOFTWARE\Policies\Microsoft\Windows NT\DNSClient.  
  
    ![Impostazioni TCP/IP](media/network-tcpip.png "Impostazioni TCP/IP")  
  
5.  Per una risoluzione più rapida degli indirizzi, è consigliabile trasferire il suffisso dell'appliance nella parte superiore dell'elenco.  
  
6.  Fare clic su OK.  
  
7.  A questo punto, è possibile connettersi alla rete InfiniBand dell'appliance `PDW_region-SQLCTL01.appliance_domain.local`usando o semplicemente `appliance_domain-SQLCTL01`. La connessione può essere stabilita più velocemente se ci si connette con il nome completo e il suffisso DNS.  
  
    Esempi per un appliance denominato MyAPS con un'area di MyPDW PDW:  
  
    -   MyPDW-SQLCTL01. MyAPS. local  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>Vedere anche  
[Acquisire e configurare un server di caricamento](acquire-and-configure-loading-server.md)  
  
