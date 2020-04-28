---
title: Software antivirus
description: Se la data center richiede software antivirus, attenersi a queste linee guida per installare il software antivirus in strumenti di piattaforma analitici. Si consiglia di non installare software antivirus a meno che non si tratti di un requisito aziendale per i data center.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: c3687b839e52e64350591402c3aa19e9c2c54ac7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401477"
---
# <a name="antivirus-software-for-analytics-platform-system-aps"></a>Software antivirus per il sistema di piattaforma analitica (APS)
Se la data center richiede software antivirus, usare queste linee guida per installare il software antivirus nel sistema della piattaforma di analisi. Si consiglia di non installare software antivirus a meno che non si tratti di un requisito aziendale per i data center.  
  
> [!WARNING]  
> Si consiglia di valutare individualmente i rischi per la sicurezza per ogni computer e per il sistema di piattaforma di analisi nel suo complesso e di selezionare gli strumenti appropriati per il livello di rischio di sicurezza di ogni computer. Inoltre, prima di implementare qualsiasi progetto di protezione da virus, è consigliabile testare l'intero sistema con un carico completo per misurare le modifiche alla stabilità e alle prestazioni.  
>   
> Il software di protezione da virus richiede l'esecuzione di alcune risorse di sistema. È necessario eseguire i test prima e dopo l'installazione del software antivirus per determinare se si è verificato un effetto sulle prestazioni nel sistema della piattaforma di analisi.  
  
Questo argomento è basato sulle istruzioni disponibili in [come scegliere il software antivirus da eseguire nei computer che eseguono SQL Server](https://support.microsoft.com/kb/309422) e l' [articolo 961804 della Knowledge](https://support.microsoft.com/kb/961804/en-us)base.  
  
## <a name="exclusion-list-for-physical-hosts"></a>Elenco di esclusione per gli host fisici  
Per installare il software antivirus negli host fisici, escludere l'elenco seguente di directory e processi. Questi non devono essere analizzati dal software antivirus.  
  
**Escludi le directory seguenti:**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V-directory di configurazione della macchina virtuale  
  
-   Dischi rigidi C:\utenti\public\documents\hyper-V\Virtual Hard-directory di unità disco rigido virtuale predefinita  
  
-   C:\clusterStorage-directory unità disco rigido virtuale  
  
**Escludi questi processi:**  
  
-   Gestione delle macchine virtuali (Vmms. exe)  
  
-   Processi di lavoro delle macchine virtuali (Vmwp. exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>Elenco di esclusioni per macchine virtuali (VM)  
Per installare il software antivirus nelle macchine virtuali, escludere l'elenco seguente di directory e file. Questi non devono essere analizzati dal software antivirus.  
  
**_PDW_region_-CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-AD01** e ** _appliance_domain_-ad02**  
  
-   Nessuna restrizione  
  
**Macchine virtuali del nodo di calcolo**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-VMM**  
  
-   Nessuna restrizione  
  
**_appliance_domain_WDS**  
  
-   Nessuna restrizione  
  
**_appliance_domain_-ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>Vedere anche  
[Attività di gestione degli appliance &#40;sistema di piattaforma di analisi&#41;](appliance-management-tasks.md)  
  
