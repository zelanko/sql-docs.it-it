---
title: Imposta Active Directory password
description: Impostare Active Directory la password di accesso dell'amministratore in modalità ripristino servizi directory in strumenti di piattaforma analitica (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbbf42106602a25b03072a9c9abfb04f04d3c49
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400328"
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>Impostare la password amministratore per l'accesso ai nodi AD in modalità ripristino servizi directory-sistema di piattaforma Analytics
La modalità ripristino servizi directory è una modalità di avvio per il ripristino o il recupero di Active Directory Domain Services (AD DS). Viene usato per accedere ai nodi AD dell'appliance dopo che servizi di dominio Active Directory ha avuto esito negativo o quando è necessario ripristinare servizi di dominio Active Directory. La password per la modalità ripristino servizi directory è stata inizializzata durante la configurazione dell'appliance nel sito del fornitore dell'hardware e deve essere modificata dall'amministratore dell'appliance. Il sistema di piattaforma di analisi dispone di due servizi di dominio Active Directory (Domain Controller); ** _appliance_domain_-ad01** e ** _appliance_domain_-ad02**. Per ogni nodo AD dell'appliance, modificare la password della modalità ripristino servizi directory usando la procedura seguente.  
  
## <a name="HowToDSRM"></a>Per reimpostare la password dell'amministratore  
  
1.  Aprire una finestra del prompt dei comandi in un nodo AD del dispositivo <strong> _appliance_domain_AD_xx_</strong>macchina virtuale.  
  
2.  Al prompt dei comandi digitare `ntdsutil`.  
  
3.  Al prompt di **Ntdsutil** Digitare `set dsrm password`.  
  
4.  Alla richiesta di **reimpostazione della password amministratore:** Digitare `reset password on server null`.  
  
5.  Al prompt dei comandi digitare la nuova password.  
  
6.  Ripetere i passaggi 1-5 precedenti per ogni appliance macchina virtuale AD.  
  
    > [!WARNING]  
    > Analytics Platform System non supporta il simbolo di dollaro ($) nelle password di amministratore di dominio o di amministratore locale. Una password contenente un segno di dollaro verrà convalidata e sarà utilizzabile, ma potrà bloccare le attività di aggiornamento e di manutenzione.  
  
> [!NOTE]  
> Se la Active Directory Domain Services o la macchina virtuale viene danneggiata per una macchina virtuale AD specifica, l'esecuzione di **ReplaceVM** per la macchina virtuale di Active Directory interessata è l'azione di correzione consigliata. Per assistenza, contattare il servizio CSS.  
  
## <a name="see-also"></a>Vedere anche  
[Reimpostazione della password &#40;sistema della piattaforma di analisi&#41;](password-reset.md)  
  
