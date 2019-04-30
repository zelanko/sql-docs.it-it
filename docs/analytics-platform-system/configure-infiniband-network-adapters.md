---
title: Configurare InfiniBand - sistema di piattaforma Analitica | Microsoft Docs
description: Viene descritto come configurare le schede di rete InfiniBand in un server non appliance client per connettersi al nodo di controllo in Parallel Data Warehouse (PDW). Usare queste istruzioni per la connettività di base e per la disponibilità elevata, in modo che il caricamento, i processi di backup e altri si connettono automaticamente alla rete InfiniBand attiva.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 9e52e3962fa1928d7f7680a750d6c1efe5201c6f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63057192"
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>Configurare le schede di rete InfiniBand per il sistema di piattaforma Analitica
Viene descritto come configurare le schede di rete InfiniBand in un server non appliance client per connettersi al nodo di controllo in Parallel Data Warehouse (PDW). Usare queste istruzioni per la connettività di base e per la disponibilità elevata, in modo che il caricamento, i processi di backup e altri si connettono automaticamente alla rete InfiniBand attiva.  
  
## <a name="Basics"></a>Descrizione  
Queste istruzioni mostrano come trovare e quindi impostare i corretto InfiniBand IP indirizzi e subnet mask sul server connesse a InfiniBand. Viene inoltre illustrato come impostare il server per usare l'appliance APS DNS in modo che la connessione venga risolta la rete InfiniBand attive.  
  
Per la disponibilità elevata, i punti di accesso dispone di due reti InfiniBand, uno attivo e uno passivo. Ogni rete InfiniBand dispone di un indirizzo IP diverso per il nodo di controllo. Se la rete InfiniBand attiva diventa inattivo, la rete InfiniBand passiva diventa la rete attiva. In questo caso uno script o un processo si connette automaticamente alla rete InfiniBand attiva senza modificare i parametri dello script.  
  
In particolare, in questo articolo è:  
  
1.  Trovare gli indirizzi IP InfiniBand del DNS APS server (appliance_domain AD01 e appliance_domain *-AD02). A tale scopo accedere al server AD01 e AD02 e ottenere gli indirizzi IP per ogni rete InfiniBand. Gli indirizzi IP InfiniBand nel nodo Active Directory sono gli indirizzi IP DNS.  
  
2.  Configurare ogni scheda di rete per usare un indirizzo IP disponibile nella rete InfiniBand di APS.  
  
    1.  Se si dispone di due schede di rete InfiniBand, si configura una scheda con un indirizzo IP disponibile nella prima rete InfiniBand che viene chiamato TeamIB1, mentre l'altra con un indirizzo IP disponibile nella rete InfiniBand secondo cui viene chiamata TeamIB2. Usa il TeamIB1 appliance_domain AD01 indirizzo IP come server DNS preferito e appliance_domain AD02 TeamIB1 indirizzo IP del server DNS alternativo per la scheda di rete TeamIB1. Usa il TeamIB2 appliance_domain AD01 indirizzo IP come server DNS preferito e appliance_domain AD02 TeamIB2 indirizzo IP del server DNS alternativo per TeamIB2 scheda di rete.  
  
    2.  Se si dispone di una sola scheda di rete InfiniBand, si configura l'adapter con un indirizzo IP disponibile da una delle reti InfiniBand. Quindi configurare il valore desiderato e i server DNS alternativi nella scheda usando TeamIB1 appliance_domain AD01 e TeamIB1 appliance_domain AD02 o TeamIB2 appliance_domain AD01 e appliance_domain AD02 TeamIB2 seconda di quale sia nello stesso computer rete rispettivamente come l'adapter configurato come il valore desiderato e i server DNS alternativi.  
  
3.  Configurare la scheda di rete InfiniBand per usare server DNS APS per risolvere la connessione alla rete InfiniBand active.  
  
    1.  Per configurare questa impostazione è usare le impostazioni avanzate TCP/IP per aggiungere il suffisso DNS del dominio appliance all'inizio dell'elenco dei suffissi DNS sul server del client. Questa operazione deve solo essere configurato in una delle schede di rete; l'impostazione si applica a entrambe le schede.  
  
Dopo aver configurato le schede di rete InfiniBand, i processi client possono connettersi al nodo di controllo nella rete InfiniBand tramite `PDW_region-SQLCTL01` per l'indirizzo del server. Il server aggiunge il suffisso DNS del sistema di piattaforma Analitica, o è possibile immettere l'indirizzo completo ovvero `PDW_region-SQLCTL01.appliance_domain.pdw.local`.  
  
Ad esempio, se il nome dell'area PDW è MyPDW e il nome dell'appliance è MyAPS, la specifica del server dwloader per il caricamento dei dati è uno dei seguenti:  
  
-   `dwloader -S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader -S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>Prima di iniziare  
  
### <a name="requirements"></a>Requisiti  
È necessario un account di dominio appliance APS per accedere al nodo AD01. Ad esempio, F12345 * \administrator.  
  
È necessario un account di Windows nel server client che dispone dell'autorizzazione per configurare le schede di rete.  
  
### <a name="prerequisites"></a>Prerequisiti  
Queste istruzioni si presuppone il server di client è già sia collegato alla rete InfiniBand appliance. Per installare e le istruzioni di cablaggio, vedere [acquisire e configurare un Server di caricamento](acquire-and-configure-loading-server.md).  
  
### <a name="general-remarks"></a>Osservazioni generali  
Usando SQLCTL01, il DNS di sistema di piattaforma Analitica collega il server di client per il nodo di controllo tramite la rete InfiniBand active. Si applica solo al recupero collegati; Se la rete InfiniBand diventa inattiva durante un backup o il carico, è necessario riavviare il processo.  
  
Per soddisfare i requisiti aziendali specifici, è anche possibile aggiungere il server di client a un dominio di Windows o il proprio gruppo di lavoro non appliance.  
  
## <a name="Sec1"></a>Passaggio 1: Ottenere le impostazioni di rete InfiniBand dell'appliance  
*Per ottenere l'appliance le impostazioni di rete InfiniBand*  
  
1.  Accedere all'appliance AD01 nodo con l'account appliance_domain\Administrator.  
  
2.  Nel nodo AD01 appliance, aprire il pannello di controllo, selezionare rete e Internet selezionare rete e condivisione Center *, quindi Modifica impostazioni scheda.  
  
3.  Nella finestra connessioni di rete su IB1 Team e scegliere Proprietà.  
  
    ![Connessioni InfiniBand nel nodo di gestione](media/network-teamib.png "connessioni InfiniBand nel nodo di gestione")  
  
4.  Dalla finestra Proprietà protocollo Internet versione 4 (TCP/IPv4), prendere nota dei valori per il **indirizzo IP** e **Subnet mask**.  L'indirizzo IP del  **_appliance\_domain_-AD01** nodo è l'indirizzo IP del server DNS di sistema di piattaforma Analitica.  
  
5.  Ripetere i passaggi da 1 a 5 precedenti per l'adapter TeamIB1 sul  **_appliance\_domain_-AD02** server.  
  
    ![Proprietà InfiniBand 1 nodo Gestione PDW](media/network-ip1-properties.png "proprietà InfiniBand 1 nodo Gestione PDW")  
  
6.  Fare clic su Annulla per chiudere la finestra.  
  
7.  Trovare un indirizzo IP inutilizzato nella rete TeamIB1 e prenderne nota.  
  
    Per trovare un indirizzo IP inutilizzato, aprire una finestra di comando e provare a effettuare il ping degli indirizzi IP all'interno dell'intervallo di indirizzi per l'appliance. In questo esempio, l'indirizzo IP della rete TeamIB1 è 172.16.14.30. Trovare un indirizzo IP che inizia con 172.16.14 non usato. Immettere ad esempio dalla riga di comando "ping 172.16.14.254". Se la richiesta di ping ha esito negativo, l'indirizzo IP è disponibile.  
  
8.  Eseguire la stessa operazione per TeamIB2. Nel * finestra connessioni di rete, fare clic sul Team IB2 e selezionare proprietà.  
  
9. Dalla finestra Proprietà protocollo Internet versione 4 (TCP/IPv4), prendere nota dei valori per l'indirizzo IP e Subnet mask per TeamIB2.  
  
10. Ripetere i passaggi da 8 a 9 per la scheda TeamIB2 appliance_domain AD02 server.  
  
    ![Proprietà per TeamIB2](media/network-ip2-properties.png "proprietà per TeamIB2")  
  
11. Trovare un indirizzo IP inutilizzato sul **TeamIB2** di rete e prenderne nota.  
  
    Per trovare un indirizzo IP inutilizzato, aprire una finestra di comando e provare a effettuare il ping degli indirizzi IP all'interno dell'intervallo di indirizzi per l'appliance. In questo esempio, l'indirizzo IP della rete TeamIB2 è 172.16.18.30. Trovare un indirizzo IP che inizia con 172.16.18 non usato. Immettere ad esempio dalla riga di comando "ping 172.16.18.254". Se la richiesta di ping ha esito negativo, l'indirizzo IP è disponibile.  
  
## <a name="Sec2"></a>Passaggio 2: Configurare le impostazioni della scheda di rete InfiniBand nel Server Client  

### <a name="notes"></a>Note  
  
-   Questi passaggi illustrano come registrare il server con i server DNS APS.  
  
-   Per soddisfare le proprie esigenze di rete, è anche possibile aggiungere il server di client a un dominio di Windows o il proprio gruppo di lavoro non appliance.  
  
-   Il passaggio di istruzioni tramite la configurazione di due schede di rete in ogni server.  Se si dispone solo di una scheda di rete, selezionare una delle reti da configurare nella scheda di rete e quindi aggiungere il secondo indirizzo IP DNS come un server DNS alternativo.  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>Per configurare le impostazioni della scheda di rete InfiniBand nel server client  
  
1.  Accedere come amministratore di Windows per il caricamento, copia di backup o altri server client nell'appliance di rete InfiniBand.  
  
2.  Aprire il riquadro controllo *, selezionare centro rete e condivisione, quindi Modifica impostazioni scheda.  
  
### <a name="to-configure-the-first-network-adapter"></a>Per configurare la prima scheda di rete  
  
1.  Nella finestra di connessioni di rete, fare clic su uno degli slot rete non identificata per la scheda Mellanox e selezionare proprietà.  
  
    ![Selezione delle reti InfiniBand](media/network-connections.png "selezione delle reti InfiniBand")  
  
2.  Nella finestra proprietà  
  
    1.  Nella scheda Generale, impostare l'indirizzo IP per l'indirizzo IP che verificato come disponibile nel test di ping per TeamIB1. Per i valori di esempio usati in questo articolo, si desidera immettere 172.16.14.254.  
  
    2.  Impostare la subnet mask per la subnet mask che si è preso nota per TeamIB1.  
  
    3.  Impostare il server DNS preferito per l'indirizzo IP del TeamIB1 che si è preso nota in precedenza da appliance_domain *-AD01 nodo.  
  
    4.  Impostare il server DNS alternativo per l'indirizzo IP del TeamIB1 che si è preso nota in precedenza da appliance_domain *-AD02 nodo.  
  
        ![InfiniBand 1 Network Adapter Properties](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  Fare clic su OK per applicare le modifiche.  
  
### <a name="to-configure-the-second-network-adapter"></a>Per configurare la seconda scheda di rete  
  
1.  Se si dispone solo di una scheda di rete, ignorare questa sezione.  
  
2.  Nella finestra di connessioni di rete, fare clic sul secondo slot rete non identificata per la scheda Mellanox e selezionare proprietà.  
  
    ![Selezione delle reti InfiniBand](media/network-connections.png "selezione delle reti InfiniBand")  
  
3.  Nella finestra proprietà  
  
    1.  Nella scheda Generale, impostare l'indirizzo IP per l'indirizzo IP che verificato come disponibile nel test di ping per TeamIB2. Per i valori di esempio usati in questo articolo, si desidera immettere 172.16.18.254.  
  
    2.  Impostare la subnet mask per la subnet mask che si è preso nota per TeamIB2.  
  
    3.  Impostare il server DNS preferito per l'indirizzo IP del TeamIB2 che si è preso nota in precedenza da appliance_domain *-AD01 nodo.  
  
    4.  Impostare il server DNS alternativo per l'indirizzo IP del TeamIB2 che si è preso nota in precedenza da appliance_domain *-AD02 nodo.  
  
        > [!NOTE]  
        > Se presente una sola scheda di rete, configurare il valore desiderato e i server DNS alternativi utilizzando rispettivamente le appliance AD01 TeamIB1 e appliance TeamIB1 AD02 come il valore desiderato e i server DNS alternativi o usare l'appliance TeamIB2 AD01 e Appliance TeamIB2 AD02 come il valore desiderato e i server DNS alternativi a seconda se la macchina virtuale di Active Directory ha eseguito il failover.  
  
        ![Proprietà dell'Adapter 1 rete InfiniBand](media/network-ib1-properties.png "proprietà dell'Adapter 1 rete InfiniBand")  
  
    5.  Fare clic su OK per applicare le modifiche.  
  
### <a name="to-configure-the-dns-suffix"></a>Per configurare il suffisso DNS  
  
1.  Nella finestra di connessioni di rete, fare clic su uno degli slot rete per la scheda Mellanox e selezionare proprietà.  
  
2.  Fare clic su avanzate pulsante.  
  
3.  Nella finestra Impostazioni TCP/IP avanzate, se l'operazione di Accodamento opzione questi suffissi DNS (in ordine) non è disattivata, la casella denominata controllo Aggiungi questi suffissi DNS (in ordine): selezionare il suffisso di dominio di appliance e fare clic su Aggiungi... È il suffisso del dominio appliance `appliance_domain.local`  
  
4.  Se l'operazione di Accodamento questi DNS suffissi (nell'ordine indicato): opzione è disattivata, è possibile aggiungere il dominio dei punti di accesso a questo server modificando la chiave del Registro di sistema HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\DNSClient.  
  
    ![Impostazioni TCP/IP](media/network-tcpip.png "impostazioni TCP/IP")  
  
5.  Per la risoluzione degli indirizzi più veloce, è consigliabile spostare il suffisso di appliance in cima all'elenco.  
  
6.  Fare clic su OK.  
  
7.  A questo punto, è possibile connettersi alla rete Infiniband appliance usando `PDW_region-SQLCTL01.appliance_domain.local`, o semplicemente `appliance_domain-SQLCTL01`. La connessione può essere stabilita più velocemente se ci si connette con il nome completo e il suffisso DNS.  
  
    Esempi per un'appliance denominato MyAPS con un'area PDW MyPDW:  
  
    -   MyPDW-SQLCTL01.MyAPS.local  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>Vedere anche  
[Acquisire e configurare un Server di caricamento](acquire-and-configure-loading-server.md)  
  
