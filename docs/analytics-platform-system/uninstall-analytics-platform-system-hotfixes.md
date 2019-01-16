---
title: Disinstallare gli aggiornamenti rapidi di sistema di piattaforma Analitica nel | Microsoft Docs
description: Disinstallare gli aggiornamenti rapidi di sistema di piattaforma Analitica.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5507eae7bb2f8a5ce138223a031ac4946d9f0030
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54255067"
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>Disinstallare gli aggiornamenti rapidi di sistema di piattaforma Analitica 
I passaggi seguenti descrivono come disinstallare un hotfix del sistema di piattaforma Analitica installato in precedenza.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
### <a name="prerequisites"></a>Prerequisiti  
Per eseguire questi passaggi, è necessario:  
  
-   Un account di accesso di sistema di piattaforma Analitica con le autorizzazioni per accedere alla Console di amministrazione che consentono di monitorare l'appliance.  
  
-   L'account amministratore di dominio per eseguire l'accesso per il <em>< appliance_domain ></em>**-HST01** nodo.  
  
-   L'articolo della Knowledge Base numero di articolo per l'aggiornamento rapido per disinstallare.  
  
## <a name="HowToUninstallPDW"></a>Per disinstallare un hotfix di SQL Server PDW  
  
1.  Eseguire l'accesso di <em>< appliance_domain ></em>**-HST01** nodo come l'amministratore di dominio di Fabric.  
  
2.  Usare l'esecuzione come opzione di amministratore per aprire un prompt dei comandi.  
  
3.  Passare alla directory `C:\PDWINST\Patches\<kbarticle>\media` in cui *<kbarticle>* è il numero di articolo della Knowledge Base per l'aggiornamento rapido da disinstallare.  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  Per rimuovere l'aggiornamento rapido, eseguire il comando seguente.  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>Vedere anche  
[Scaricare e applicare gli aggiornamenti di Microsoft &#40;sistema di piattaforma Analitica&#41;](download-and-apply-microsoft-updates.md)  
[Disinstallare gli aggiornamenti di Microsoft &#40;sistema di piattaforma Analitica&#41;](uninstall-microsoft-updates.md)  
[Applicare gli hotfix del sistema di piattaforma Analitica &#40;sistema di piattaforma Analitica&#41;](apply-analytics-platform-system-hotfixes.md)  
[Manutenzione software &#40;sistema di piattaforma Analitica&#41;](software-servicing.md)  
  
