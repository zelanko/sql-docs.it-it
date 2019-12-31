---
title: Disinstalla hotfix
description: Disinstalla gli hotfix del sistema della piattaforma di analisi.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ef6929aeb06c9472eb3ff210de016117a9636ded
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399759"
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>Disinstalla hotfix del sistema della piattaforma di analisi 
I passaggi seguenti descrivono come disinstallare un hotfix del sistema di piattaforma di analisi installato in precedenza.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
### <a name="prerequisites"></a>Prerequisiti  
Per eseguire questi passaggi, sarà necessario:  
  
-   Un account di accesso del sistema della piattaforma Analytics con le autorizzazioni per accedere alla console di amministrazione per monitorare l'appliance.  
  
-   Account amministratore di dominio per accedere al nodo <em><appliance_domain></em> **-HST01** .  
  
-   Numero dell'articolo della Knowledge base per l'hotfix da disinstallare.  
  
## <a name="HowToUninstallPDW"></a>Per disinstallare un hotfix SQL Server PDW  
  
1.  Accedere al <em><appliance_domain nodo></em> **-HST01** come amministratore di dominio dell'infrastruttura.  
  
2.  Utilizzare l'opzione Esegui come amministratore per aprire un prompt dei comandi.  
  
3.  Modificare le directory `C:\PDWINST\Patches\<kbarticle>\media` in *<kbarticle>* dove è il numero di articolo della Knowledge base per l'hotfix da disinstallare.  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  Per rimuovere l'hotfix, eseguire il comando seguente.  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>Vedere anche  
[Scaricare e applicare Microsoft Updates &#40;Platform Analytics System&#41;](download-and-apply-microsoft-updates.md)  
[Disinstallare Microsoft Updates &#40;piattaforma del sistema di analisi&#41;](uninstall-microsoft-updates.md)  
[Applicare gli hotfix del sistema di piattaforma di analisi &#40;piattaforma di strumenti analitici&#41;](apply-analytics-platform-system-hotfixes.md)  
[Servizio software &#40;piattaforma di strumenti di analisi&#41;](software-servicing.md)  
  
