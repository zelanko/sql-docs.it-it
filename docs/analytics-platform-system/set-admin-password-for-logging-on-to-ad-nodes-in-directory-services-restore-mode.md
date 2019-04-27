---
title: Impostare la password di Active Directory - sistema di piattaforma Analitica | Microsoft Docs
description: Imposta password di accesso amministratore di Active Directory i nodi in modalità ripristino servizi Directory nel sistema di piattaforma Analitica (AP).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3df6203a4d98bace5d23a92e70a596a34dedb60e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678350"
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>Impostare la Password amministratore per l'accesso ai nodi AD in servizi di Directory modalità (DSRM) - sistema di piattaforma Analitica di ripristino
La modalità ripristino servizi directory (DSRM) è una modalità di avvio per il ripristino o il ripristino di Active Directory Domain Services (AD DS). Viene utilizzato per accedere ai nodi di appliance AD dopo Active Directory Domain Services non è riuscita oppure quando è necessario ripristinare Active Directory Domain Services. La password modalità ripristino servizi directory è stata inizializzata durante la configurazione di appliance presso il sito del fornitore di hardware e debba essere modificata dall'amministratore del dispositivo. Sistema di piattaforma Analitica ha due Active Directory Domain Services (controller di dominio).  **_appliance_domain_-AD01** e  **_appliance_domain_-AD02**. Per ogni nodo di appliance Active Directory, modificare la password modalità ripristino servizi directory usando la procedura seguente.  
  
## <a name="HowToDSRM"></a>Per reimpostare la password dell'amministratore  
  
1.  Aprire una finestra del prompt dei comandi in un nodo AD appliance  <strong>_appliance_domain_-AD_xx_</strong>macchina virtuale.  
  
2.  Al prompt dei comandi digitare `ntdsutil`.  
  
3.  Nel **ntdsutil** digitare `set dsrm password`.  
  
4.  Nel **Reimposta Password amministratore:** digitare `reset password on server null`.  
  
5.  Al prompt, digitare la nuova password.  
  
6.  Ripetere i passaggi 1-5 in precedenza per ogni macchina virtuale appliance AD.  
  
    > [!WARNING]  
    > Sistema di piattaforma Analitica non supporta il carattere di segno di dollaro ($) nell'amministratore di dominio o le password di amministratore locale. Una password contenente un segno di dollaro verrà convalidato e verrà essere utilizzabile ma possa bloccare le attività di aggiornamento e manutenzione.  
  
> [!NOTE]  
> Se i servizi di dominio Active Directory o la macchina virtuale viene danneggiata per una macchina virtuale AD specifica, in esecuzione **ReplaceVM** per interessato AD macchina virtuale è l'azione correttiva consigliata. Contatto CSS per ottenere assistenza.  
  
## <a name="see-also"></a>Vedere anche  
[La reimpostazione della password &#40;sistema di piattaforma Analitica&#41;](password-reset.md)  
  
