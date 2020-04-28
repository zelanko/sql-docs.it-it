---
title: Applicare gli aggiornamenti rapidi della piattaforma di strumenti analitici
description: Questo articolo illustra come applicare aggiornamenti rapidi al software del sistema della piattaforma di analisi.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fd62413ec8542aba9f3973d0e8483cb9c5c9128a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401369"
---
# <a name="apply-analytics-platform-system-hotfixes"></a>Applicare gli aggiornamenti rapidi della piattaforma di strumenti analitici
Questo articolo illustra come applicare aggiornamenti rapidi al software del sistema della piattaforma di analisi.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
> [!WARNING]  
> Non tentare di applicare un hotfix del sistema della piattaforma Analytics se il dispositivo o qualsiasi componente dell'appliance è inattivo o in stato di failover. In tal caso, contattare il supporto tecnico per assistenza.  
  
> [!WARNING]  
> Non applicare un hotfix del sistema della piattaforma Analytics mentre l'appliance è in uso. L'applicazione di un hotfix può causare il riavvio del nodo del dispositivo. L'hotfix deve essere applicato durante una finestra di manutenzione quando l'appliance non è in uso.  
  
### <a name="prerequisites"></a>Prerequisiti  
Per eseguire questi passaggi, sarà necessario:  
  
-   Un account di accesso del sistema della piattaforma Analytics con le autorizzazioni per accedere alla console di amministrazione per monitorare lo stato dell'appliance. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   Conoscenza dell'account amministratore di dominio dell'infrastruttura per la connessione al nodo _<domain_name>_ **-HST01** .  
  
## <a name="to-apply-a-analytics-platform-system-hotfix"></a><a name="HowToInstallPDW"></a>Per applicare un hotfix di System Platform Analytics  
Diversamente dagli aggiornamenti Microsoft, gli hotfix per il software del sistema della piattaforma di analisi non vengono gestiti tramite WSUS. Hanno un flusso di lavoro diverso e vengono installati eseguendo un pacchetto hotfix.  
  
1.  **Verificare gli indicatori di stato dell'appliance.**  
  
    1.  Aprire la console di amministrazione e passare alla pagina stato dell'appliance. Per altre informazioni, vedere [monitorare l'appliance usando la console di amministrazione &#40;il sistema di piattaforma di analisi&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  Prima di procedere con il passaggio successivo, è necessario risolvere tutti gli indicatori rossi o gialli. Ecco alcune eccezioni:  
  
        -   Se sono presenti errori del disco, usare la pagina avvisi della console di amministrazione per verificare che non siano presenti più errori del disco in ogni server o matrice SAN. Se non è presente più di un errore del disco in ogni server o matrice SAN, è possibile procedere al passaggio successivo prima di correggere gli errori del disco. Assicurarsi di contattare il supporto tecnico Microsoft per correggere gli errori del disco appena possibile.  
  
        -   Se si verifica un errore di volume del disco non critico (giallo) che non si trova nel C:\ è possibile procedere al passaggio successivo prima di risolvere l'errore relativo al volume del disco.  
  
2.  **Installare l'hotfix di System Platform Analytics**  
  
    1.  Accedere al nodo <*appliance_domain*>-HST01 come amministratore di dominio.  
  
    2.  Utilizzare l'opzione **Esegui come amministratore** per aprire un prompt dei comandi.  
  
    3.  Eseguire il comando seguente, sostituendo *<HotfixPackageName>* con il nome del pacchetto eseguibile dell'hotfix e sostituendo gli altri elementi segnaposto *<  >* con le informazioni appropriate.  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  Seguire i passaggi presentati dal pacchetto hotfix.  
  
## <a name="see-also"></a>Vedere anche  
[Scaricare e applicare Microsoft Updates &#40;Platform Analytics System&#41;](download-and-apply-microsoft-updates.md)  
[Disinstallare Microsoft Updates &#40;piattaforma del sistema di analisi&#41;](uninstall-microsoft-updates.md)  
[Disinstalla hotfix del sistema della piattaforma di analisi &#40;piattaforma di strumenti analitici&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Servizio software &#40;piattaforma di strumenti di analisi&#41;](software-servicing.md)  
  
