---
title: Avvia Configuration Manager - sistema di piattaforma Analitica | Microsoft Docs
description: Istruzioni per l'avvio dello strumento Configuration Manager per l'appliance del sistema di piattaforma Analitica.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 087360981a7c31de6980755cfee4f98f88f48a15
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63183423"
---
# <a name="launch-the-configuration-manager-in-analytics-platform-system"></a>Avviare Gestione configurazione nel sistema di piattaforma Analitica
Questo argomento fornisce istruzioni per l'avvio di **Configuration Manager** per l'appliance del sistema di piattaforma Analitica.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
### <a name="prerequisites"></a>Prerequisiti  
Il sistema di piattaforma Analitica**Configuration Manager** può essere eseguito solo dall'amministratore di dominio appliance. Per eseguire questo strumento, necessaria la password per l'amministratore di dominio del dispositivo. Per creare altri amministratori di punti di accesso, vedere [creare un amministratore di dominio APS &#40;punti di accesso&#41;](create-an-aps-domain-administrator-aps.md).  
  
## <a name="Accessing"></a>Avviare lo strumento Gestione configurazione  
Per eseguire Gestione configurazione, usare Desktop remoto per connettersi al nodo di controllo di PDW (**_PDW_region_-CTL01**), nodo e Accedi come _appliance_domain_ **\Administrator**. Quando si avvia il **Configuration Manager** del programma, utilizzare il **Esegui come amministratore** opzione per assicurarsi che vengano usate le credenziali di amministratore.  
  
#### <a name="to-launch-from-a-browser-window"></a>Per l'avvio da una finestra del browser  
  
1.  Aprire un browser e passare alla directory `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
2.  Fare doppio clic su `dwconfig.exe` e quindi fare clic su **Esegui come amministratore**.  
  
#### <a name="to-launch-from-a-command-prompt"></a>Per avviare da un prompt dei comandi  
  
1.  Sul desktop, aprire il **avviare** menu, fare clic su **programmi**, fare clic su **Accessori**, fare doppio clic su **prompt dei comandi** e quindi fare clic su  **Esegui come amministratore**.  
  
2.  Al prompt dei comandi, immettere il comando seguente per passare alla directory: `cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"`.  
  
3.  Al prompt dei comandi, immettere `dwconfig.exe`.  
  
Dopo il **Configuration Manager** viene avviato, si noterà tutte le funzionalità disponibili elencate nel riquadro sinistro. Il resto di questa sezione descrive come eseguire le azioni disponibili nello strumento.  
  
Per chiudere e uscire **Configuration Manager**, fare clic su **uscire** nell'angolo in basso a destra di qualsiasi schermata.  
  
![SQL_Server_PDW_DWConfig_ApplTop](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>Vedere anche  
[Monitorare l'Appliance usando la Console di amministrazione &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
