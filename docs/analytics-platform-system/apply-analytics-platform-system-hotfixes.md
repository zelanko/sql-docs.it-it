---
title: Applicare aggiornamenti rapidi di sistema di piattaforma Analitica | Microsoft Docs
description: Questo articolo illustra come applicare gli aggiornamenti rapidi per il software del sistema di piattaforma Analitica.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d6af4a1eaf1e9891356fae40a3d3bb7f11e41dc6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961422"
---
# <a name="apply-analytics-platform-system-hotfixes"></a>Applicare gli aggiornamenti rapidi della piattaforma di strumenti analitici
Questo articolo illustra come applicare gli aggiornamenti rapidi per il software del sistema di piattaforma Analitica.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
> [!WARNING]  
> Non tentare di applicare un hotfix del sistema di piattaforma Analitica se l'appliance o qualsiasi componente di appliance è inattivo o non riuscito sullo stato. In tal caso, contattare il supporto tecnico per assistenza.  
  
> [!WARNING]  
> Non applicare un hotfix del sistema di piattaforma Analitica mentre il dispositivo è in uso. Applicare un hotfix potrebbe nodi di appliance da riavviare. L'hotfix deve essere applicata in una finestra di manutenzione quando il dispositivo non è in uso.  
  
### <a name="prerequisites"></a>Prerequisiti  
Per eseguire questi passaggi, è necessario:  
  
-   Un account di accesso di sistema di piattaforma Analitica con le autorizzazioni per accedere alla Console di amministrazione che consentono di monitorare lo stato di appliance. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   Conoscenza dell'account amministratore di dominio dell'infrastruttura per la connessione per il _< nome_dominio >_ **-HST01** nodo.  
  
## <a name="HowToInstallPDW"></a>Per applicare un hotfix del sistema di piattaforma Analitica  
A differenza di Microsoft Update, le correzioni rapide per il software di sistema di piattaforma Analitica non vengono gestite tramite WSUS. Hanno un flusso di lavoro diverso e vengono installati tramite l'esecuzione di un pacchetto di hotfix.  
  
1.  **Verificare gli indicatori di stato di appliance.**  
  
    1.  Aprire la Console di amministrazione e passare alla pagina di stato dello strumento. Per altre informazioni, vedere [monitorare l'Appliance usando la Console di amministrazione &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  Tutti gli indicatori rossi o gialli devono essere risolto prima di procedere al passaggio successivo. Due eccezioni sono:  
  
        -   Se sono presenti errori del disco, utilizzare la pagina avvisi della Console amministrazione per verificare che vi sia non più di un errore del disco all'interno di ogni server o un array SAN. Se si verifica un errore di non più di un disco all'interno di ogni server o un array SAN, è possibile procedere al passaggio successivo prima di correggere gli errori di disco. Assicurarsi di contattare il supporto Microsoft per risolvere gli errori il disco appena possibile.  
  
        -   Se si verifica un errore di volume non critico del disco (giallo) che non è nell'unità C:\, è possibile procedere al passaggio successivo prima di aver risolto l'errore di volume del disco.  
  
2.  **Installare l'hotfix di sistema di piattaforma Analitica**  
  
    1.  Account di accesso per la <*appliance_domain*>-nodo HST01 come amministratore di dominio.  
  
    2.  Usare la **Esegui come amministratore** opzione per aprire un prompt dei comandi.  
  
    3.  Eseguire il comando seguente, sostituendo *<HotfixPackageName>* con il nome del pacchetto eseguibile della correzione e sostituendo gli altri elementi segnaposto *< >* con le informazioni appropriate.  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  Seguire la procedura presentata dal pacchetto di hotfix.  
  
## <a name="see-also"></a>Vedere anche  
[Scaricare e applicare gli aggiornamenti di Microsoft &#40;sistema di piattaforma Analitica&#41;](download-and-apply-microsoft-updates.md)  
[Disinstallare gli aggiornamenti di Microsoft &#40;sistema di piattaforma Analitica&#41;](uninstall-microsoft-updates.md)  
[Disinstallare gli aggiornamenti rapidi del sistema di piattaforma Analitica &#40;sistema di piattaforma Analitica&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Manutenzione software &#40;sistema di piattaforma Analitica&#41;](software-servicing.md)  
  
