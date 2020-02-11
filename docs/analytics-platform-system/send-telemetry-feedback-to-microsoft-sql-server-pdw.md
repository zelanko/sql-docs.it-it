---
title: Feedback di telemetria
description: Invia il feedback di telemetria a Microsoft per il sistema di piattaforma di analisi.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 639eb4e9e5c531e154b9eb7f91165af365bc519f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400367"
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>Invia il feedback di telemetria a Microsoft per il sistema di piattaforma di analisi
Analytics Platform System ha una funzionalità di telemetria facoltativa che invia i dati della console di amministrazione a Microsoft. 
  
> [!NOTE]  
> In questa versione, Microsoft non monitora attivamente i dati di telemetria. I dati vengono raccolti solo a scopo di analisi.  
  
## <a name="privacy"></a>Privacy  
Per garantire la massima protezione della privacy, APS viene fornito senza abilitare la telemetria. Prima di abilitare questa funzionalità, esaminare l' [informativa sulla Privacy piattaforma di strumenti analitici Microsoft](https://go.microsoft.com/fwlink/?LinkId=400902). Per acconsentire esplicitamente, eseguire lo script di PowerShell descritto di seguito.  
  
## <a name="enable"></a>Abilita telemetria  
**Inoltri DNS:** Per inviare dati di telemetria a Microsoft, è necessario che il sistema di piattaforma di analisi si connetta a Internet tramite un server d'inoltro DNS. Per abilitare questa funzionalità, è necessario abilitare l'invio DNS su tutti gli host e le macchine virtuali del carico di lavoro. Richiamare il `Enable-RemoteMonitoring` comando con l' `SetupDnsForwarder` opzione per configurare correttamente l'invio DNS e abilitare la telemetria. Richiamare il `Enable-RemoteMonitoring` comando senza l' `SetupDnsForwarder` opzione quando l'invio DNS è già configurato e si desidera abilitare il monitoraggio heartbeat.  
  
> [!IMPORTANT]  
> L'abilitazione dell'invio DNS apre la connessione Internet per tutti gli host e le macchine virtuali del carico di lavoro.  
  
#### <a name="to-enable-feedback"></a>Per abilitare il feedback  
  
1.  Usando un account di amministratore di dominio del dispositivo, connettersi al nodo di controllo (<strong>*appliance_domain*-CTL01</strong>) e aprire un prompt dei comandi usando le credenziali di amministratore di Windows.  
  
2.  Passare alla directory seguente: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Importare il modulo`Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Per importare è necessario usare due punti nel comando.  
  
    **Esempio:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Richiamare il `Enable-RemoteMonitoring` comando.  
  
    > [!NOTE]  
    > Lo script presuppone che la connessione a Internet funzioni correttamente e non convalidi la connessione Internet.  
  
    1.  La prima volta che si abilitano i dati di telemetria, utilizzare il comando seguente per assicurarsi che tutti i server di avvio DNS siano configurati correttamente. In questo esempio, sostituire l'indirizzo `xx.xx.xx.xx` IP del server di trasmissione DNS con l'indirizzo IP del server di trasmissione DNS nell'ambiente in uso.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  Quando sono già configurati i server d'esportazione DNS, ad esempio riabilitando la telemetria disabilitata in precedenza, usare il comando seguente per abilitare la telemetria senza configurare l'invio DNS.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  Verrà richiesto di leggere e confermare che APS raccoglierà informazioni sull'appliance. Sarà disponibile un collegamento all'informativa sulla privacy di APS, che è possibile copiare e incollare in qualsiasi browser Internet per la revisione.  
  
6.  Immettere **Y** per accettare e acconsentire esplicitamente al feedback oppure immettere **N** per non accettarlo.  
  
7.  Se è stato immesso **Y** , sarà presente una serie di comandi che verranno eseguiti per abilitare la funzionalità di telemetria (e, facoltativamente, il server d'avvio DNS) nel dispositivo. Se vengono visualizzati errori o informazioni che portano a ritenere che il comando non abbia avuto esito positivo, contattare CSS per assistenza.  
  
Se è stato immesso **n**, non verrà eseguito alcun comando e la funzionalità non sarà abilitata e non sono necessarie altre operazioni.  
  
Non si verifica alcun problema nell'esecuzione `Enable-RemoteMonitoring` del comando più volte. Se il server d'invio DNS è già impostato, verrà visualizzato un messaggio di avviso che indica il caso.  
  
## <a name="disable"></a>Disabilitare la telemetria  
La disabilitazione della telemetria arresterà tutte le operazioni che comunicano informazioni sullo stato dell'appliance al servizio di monitoraggio APS nel cloud.  
  
> [!IMPORTANT]  
> L'esecuzione di questa operazione non disabilita il server di trasmissione DNS o la connessione Internet che può essere usata da altre funzionalità nell'appliance.  
  
#### <a name="to-disable-telemetry"></a>Per disabilitare la telemetria  
  
1.  Usando un account di amministratore di dominio del dispositivo, connettersi al nodo di controllo (<strong>*appliance_domain*-CTL01</strong>) e aprire una finestra di PowerShell con privilegi di amministratore.  
  
2.  Passare alla directory seguente: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Importare il modulo`Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Per importare è necessario usare due punti nel comando.  
  
    **Esempio:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Richiamare il `Disable-RemoteMonitoring` comando senza parametri. Questo comando smetterà di inviare commenti e suggerimenti. Questa operazione non influirà sul monitoraggio locale. Tuttavia, il comando non disabilita il server di trasmissione DNS e/o Disabilita la connettività Internet. Questa operazione deve essere eseguita manualmente dopo aver disabilitato correttamente il feedback.  
  
    **Esempio:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
Se vengono visualizzati errori o informazioni che portano a ritenere che il comando non abbia avuto esito positivo, contattare CSS per assistenza.  
  
Non si verifica alcun problema nell'esecuzione `Disable-RemoteMonitoring` del comando più volte.  
  
## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni, vedere:
- [Monitorare l'appliance usando la console di amministrazione &#40;sistema della piattaforma di analisi&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [Monitorare l'appliance usando le viste di sistema &#40;sistema della piattaforma di analisi&#41;](monitor-the-appliance-by-using-system-views.md)  
- [Monitorare l'appliance usando System Center Operations Manager sistema di piattaforma &#40;Analytics&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [Usare un server d'invio DNS per risolvere i nomi DNS non Appliance &#40;sistema di piattaforma di analisi&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
