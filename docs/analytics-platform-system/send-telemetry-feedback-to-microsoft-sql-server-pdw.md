---
title: Feedback sulla telemetria - sistema di piattaforma Analitica | Microsoft Docs
description: Inviare commenti e suggerimenti dati di telemetria a Microsoft per il sistema di piattaforma Analitica.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 442505d470d1c7b7a82a02610d650d9f0b8c8d07
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591141"
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>Inviare commenti e suggerimenti dati di telemetria a Microsoft per il sistema di piattaforma Analitica
Sistema di piattaforma Analitica dispone di una funzionalità di telemetria facoltativo che invia i dati della Console di amministrazione di Microsoft. 
  
> [!NOTE]  
> In questa versione, Microsoft non attivamente sta monitorando i dati di telemetria. I dati vengono raccolti solo a scopo di analisi.  
  
## <a name="privacy"></a>Privacy  
Per garantire la protezione della privacy massimo, i punti di accesso viene fornito senza abilitare la telemetria. Prima di abilitare questa funzionalità, vedere prima la [informativa sulla Privacy di Microsoft Analitica Platform System](https://go.microsoft.com/fwlink/?LinkId=400902). A tale scopo, eseguire lo script di PowerShell descritto di seguito.  
  
## <a name="enable"></a>Abilitare la telemetria  
**Inoltro di DNS:** L'invio di dati di telemetria a Microsoft richiede il sistema di piattaforma Analitica per la connessione a internet tramite un server d'inoltro DNS. Per abilitare questa funzionalità, è necessario abilitare DNS di inoltro in tutti gli host e macchine virtuali del carico di lavoro. Richiama il `Enable-RemoteMonitoring` comando con il `SetupDnsForwarder` opzione per configurare l'inoltro di DNS e abilitare la telemetria correttamente. Richiama il `Enable-RemoteMonitoring` comando senza il `SetupDnsForwarder` opzione quando è già configurato l'inoltro di DNS e si desidera abilitare il monitoraggio Heartbeat.  
  
> [!IMPORTANT]  
> Abilitare l'inoltro DNS consente di aprire la connessione a internet per tutti gli host e macchine virtuali del carico di lavoro.  
  
#### <a name="to-enable-feedback"></a>Per abilitare i commenti e suggerimenti  
  
1.  Usando un account di amministratore di dominio appliance, connettersi al nodo di controllo (<strong>*appliance_domain*-CTL01</strong>) e aprire un prompt dei comandi utilizzando le credenziali di amministratore di Windows.  
  
2.  Passare alla directory seguente: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Importare il modulo `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Per l'importazione è necessario utilizzare due punti nel comando.  
  
    **Esempio:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Richiamare il `Enable-RemoteMonitoring` comando.  
  
    > [!NOTE]  
    > Lo script si presuppone che la connessione internet funziona correttamente e non convalida la connessione a internet.  
  
    1.  La prima volta che si abilita la telemetria, usare il comando seguente per verificare che tutti i server d'inoltro DNS siano configurati correttamente. In questo esempio sostituire l'indirizzo IP DNS inoltrati `xx.xx.xx.xx` con l'indirizzo IP del server d'inoltro DNS nel proprio ambiente.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  Quando i server d'inoltro DNS sono già configurati, ad esempio riabilitazione disabilitata in precedenza i dati di telemetria, usare il comando seguente per abilitare la telemetria senza configurare l'inoltro di DNS.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  Richiederà a leggere e confermare che i punti di accesso verranno raccolte informazioni sull'appliance. Sarà presente un collegamento all'informativa sulla privacy di punti di accesso che è possibile copiare e incollare in qualsiasi browser internet per la revisione.  
  
6.  Immettere **Y** per accettare e acconsentire esplicitamente a commenti e suggerimenti oppure premere **N** per non accettare.  
  
7.  Se è stato immesso **Y** sarà presente una serie di comandi da eseguire in modo da consentire i dati di telemetria (e facoltativamente il server d'inoltro DNS) funzionalità nell'appliance. Se eventuali errori o informazioni riconducibili credere che il comando non è riuscito a contattare il tecnico CSS per ottenere assistenza.  
  
Se è stato immesso **N**, non verrà eseguito alcun comando e non verrà abilitata la funzionalità e non è necessario effettuare altre.  
  
Non causa problemi nell'esecuzione di `Enable-RemoteMonitoring` comando più volte. Se il server d'inoltro DNS è già impostato si riceverà un messaggio di avviso che indica che è il caso.  
  
## <a name="disable"></a>Disabilitare la telemetria  
Disabilitazione della telemetria interromperà tutte le operazioni che comunicano informazioni sullo stato dell'appliance per il monitoraggio del servizio nel cloud i punti di accesso.  
  
> [!IMPORTANT]  
> Eseguire questa operazione non vengono disabilitati i server d'inoltro DNS o una connessione internet che può essere usato da altre funzionalità nell'appliance.  
  
#### <a name="to-disable-telemetry"></a>Per disabilitare la telemetria  
  
1.  Usando un account di amministratore di dominio appliance, connettersi al nodo di controllo (<strong>*appliance_domain*-CTL01</strong>) e aprire una finestra di PowerShell con privilegi di amministratore.  
  
2.  Passare alla directory seguente: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Importare il modulo `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Per l'importazione è necessario utilizzare due punti nel comando.  
  
    **Esempio:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Richiamare il `Disable-RemoteMonitoring` comando senza parametri. Questo comando interromperà l'invio di commenti e suggerimenti. (Questa operazione non modificherà il monitoraggio locale.) Tuttavia, il comando verrà non disabilitare il server d'inoltro DNS e/o disabilitare qualsiasi connettività internet. Questa operazione deve essere eseguita manualmente dopo la disattivazione è stata di commenti e suggerimenti.  
  
    **Esempio:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
Se eventuali errori o informazioni riconducibili credere che il comando non è riuscito a contattare il tecnico CSS per ottenere assistenza.  
  
Non causa problemi nell'esecuzione di `Disable-RemoteMonitoring` comando più volte.  
  
## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni, vedere:
- [Monitorare l'Appliance usando la Console di amministrazione &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [Monitorare l'Appliance usando le viste di sistema &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-system-views.md)  
- [Monitorare l'Appliance usando System Center Operations Manager &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [Usare un server d'inoltro DNS per risolvere i nomi DNS Non Appliance &#40;sistema di piattaforma Analitica&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
