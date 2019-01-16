---
title: Disinstallazione di aggiornamenti Microsoft - sistema di piattaforma Analitica | Microsoft Docs"
description: Disinstallazione di aggiornamenti Microsoft nel sistema di piattaforma Analitica (AP).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4739d05b1878c8b7fc9f66f2e0b8145ff1044e54
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54254766"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>Disinstallazione di aggiornamenti Microsoft nel sistema di piattaforma Analitica
Questo articolo descrive come disinstallare un aggiornamento installato precedentemente Microsoft nell'appliance di sistema di piattaforma Analitica.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
### <a name="prerequisites"></a>Prerequisiti  
Per eseguire questi passaggi, è necessario:  
  
-   Un account di accesso di sistema di piattaforma Analitica con le autorizzazioni per accedere alla Console di amministrazione che consentono di monitorare l'appliance.  
  
-   Conoscenza dell'account amministratore di dominio dell'infrastruttura per accedere al <em> <Fabric Domain> </em> **-HST01** nodo.  
  
## <a name="HowToUninstallMSFT"></a>Per disinstallare gli aggiornamenti Microsoft  
  
1.  Accedi per il <em> <Fabric Domain> </em> **-HST01** nodo come l'amministratore di dominio di Fabric.  
  
2.  Per disinstallare tutti gli aggiornamenti approvati per disinstallare WSUS, aprire una finestra del prompt dei comandi e immettere il comando seguente. Sostituire gli elementi segnaposto *< >* con le informazioni appropriate.  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni, vedere:
- [Scaricare e applicare gli aggiornamenti di Microsoft &#40;sistema di piattaforma Analitica&#41;](download-and-apply-microsoft-updates.md) 
- [Applicare gli hotfix del sistema di piattaforma Analitica &#40;sistema di piattaforma Analitica&#41;](apply-analytics-platform-system-hotfixes.md)  
- [Disinstallare gli aggiornamenti rapidi del sistema di piattaforma Analitica &#40;sistema di piattaforma Analitica&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [Manutenzione software &#40;sistema di piattaforma Analitica&#41;](software-servicing.md)  
  
