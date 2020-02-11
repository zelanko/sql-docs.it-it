---
title: Manutenzione software
description: Software Servicing in Analytics Platform System (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4325dfa9c16edba12c2bba694b47c1b0875c7c6f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400309"
---
# <a name="software-servicing-in-analytics-platform-system"></a>Manutenzione del software nel sistema della piattaforma Analytics
In questa sezione vengono riepilogati i requisiti di manutenzione del software per le appliance del sistema della piattaforma di analisi, tra cui WSUS e gli hotfix del sistema della piattaforma Analytics.  
  
## <a name="Basics"></a>Nozioni fondamentali sul servizio software  
**WSUS:** L'appliance del sistema di piattaforma di analisi deve essere configurata in modo da ricevere gli aggiornamenti da Windows Server Update Services (WSUS). Questi aggiornamenti includono importanti modifiche al software dell'appliance. Una volta configurati, molti aggiornamenti verranno installati automaticamente e non richiederanno una gestione pratica. In genere, gli aggiornamenti WSUS vengono configurati durante la [configurazione Windows Server Update Services &#40;wsus&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md) passaggio eseguito durante la configurazione del nuovo Appliance. In caso contrario, questo passaggio di configurazione può essere eseguito in un secondo momento. Per informazioni su WSUS, vedere la [Guida del sito Web WSUS](https://go.microsoft.com/fwlink/?LinkId=202417).  
  
**Aggiornamenti rapidi:** Potrebbe inoltre essere necessario applicare gli hotfix del sistema di piattaforma di analisi. Un *hotfix* è un aggiornamento software creato per un cliente specifico per risolvere un problema con il software del sistema della piattaforma di analisi. Ogni hotfix è un file eseguibile che installa la correzione per il problema specifico del cliente. Ogni hotfix contiene anche un accumulo di tutti gli aggiornamenti software rilasciati in precedenza per Windows, SQL Server e il sistema di piattaforma di analisi. Se è necessario installare un hotfix, il supporto tecnico Microsoft fornirà l'hotfix e le istruzioni.  
  
**Ambito degli aggiornamenti:** L'applicazione di un hotfix o Service Pack al sistema di piattaforma di analisi deve portare offline l'intero dispositivo.  
  
**Adapter di destinazione SSIS e strumenti client:** Quando si applica un hotfix che include modifiche all'identità del servizio gestito dell'adapter di destinazione SSIS o all'identità del servizio gestito degli strumenti client, i file MSI verranno aggiornati nella directory **C:\PDWINST\ClientTools** del nodo di controllo. L'hotfix non installa automaticamente i componenti dai file MSI aggiornati. Per aggiornare tali componenti, il cliente deve disinstallare le versioni precedenti dei componenti e installare le nuove versioni dai file MSI aggiornati. Quando si disinstalla un hotfix che include modifiche all'identità del servizio gestito dell'adapter di destinazione SSIS o all'identità del servizio gestito degli strumenti client, i file MSI per tali componenti verranno ripristinati nelle versioni precedenti. Per ripristinare tali componenti a una versione precedente, il cliente deve disinstallare le versioni esistenti (più recenti) dei componenti e reinstallare le versioni precedenti dai file MSI ripristinati.  
  
## <a name="software-servicing-topics"></a>Argomenti relativi alla manutenzione del software  
Gli argomenti seguenti descrivono come gestire la manutenzione del software nel dispositivo:  
  
-   [Scaricare e applicare Microsoft Updates &#40;Platform Analytics System&#41;](download-and-apply-microsoft-updates.md)  
  
-   [Disinstallare Microsoft Updates &#40;piattaforma del sistema di analisi&#41;](uninstall-microsoft-updates.md)  
  
-   [Applicare gli hotfix del sistema di piattaforma di analisi &#40;piattaforma di strumenti analitici&#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [Disinstalla hotfix del sistema della piattaforma di analisi &#40;piattaforma di strumenti analitici&#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
