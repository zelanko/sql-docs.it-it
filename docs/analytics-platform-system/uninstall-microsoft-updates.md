---
title: Disinstallare gli aggiornamenti Microsoft
description: Disinstallare Microsoft Updates in Analytics Platform System (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a5ebe1ee911f7500505cdbd1962d28c35461a635
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74399460"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>Disinstallare gli aggiornamenti Microsoft nel sistema della piattaforma Analytics
Questo articolo descrive come disinstallare un aggiornamento di Microsoft Update installato in precedenza nell'appliance del sistema della piattaforma di analisi.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
### <a name="prerequisites"></a>Prerequisiti  
Per eseguire questi passaggi, sarà necessario:  
  
-   Un account di accesso del sistema della piattaforma Analytics con le autorizzazioni per accedere alla console di amministrazione per monitorare l'appliance.  
  
-   Conoscenza dell'account amministratore di dominio dell'infrastruttura per accedere al <em> <Fabric Domain> </em>nodo **-HST01** .  
  
## <a name="to-uninstall-microsoft-updates"></a><a name="HowToUninstallMSFT"></a>Per disinstallare gli aggiornamenti Microsoft  
  
1.  Accedere al <em> <Fabric Domain> </em>nodo **-HST01** come amministratore di dominio dell'infrastruttura.  
  
2.  Per disinstallare tutti gli aggiornamenti approvati per la disinstallazione di WSUS, aprire una finestra del prompt dei comandi e immettere il comando seguente. Sostituire gli elementi segnaposto *<  >* con le informazioni appropriate.  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni, vedi:
- [Scaricare e applicare Microsoft Updates &#40;Platform Analytics System&#41;](download-and-apply-microsoft-updates.md) 
- [Applicare gli hotfix del sistema di piattaforma di analisi &#40;piattaforma di strumenti analitici&#41;](apply-analytics-platform-system-hotfixes.md)  
- [Disinstalla hotfix del sistema della piattaforma di analisi &#40;piattaforma di strumenti analitici&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [Servizio software &#40;piattaforma di strumenti di analisi&#41;](software-servicing.md)  
  
