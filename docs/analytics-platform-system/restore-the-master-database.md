---
title: Ripristinare il database master - sistema di piattaforma Analitica | Microsoft Docs
description: Ripristinare il database master nel sistema di piattaforma Analitica.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 184184f332225e76e152c2d909cfff788b4fea91
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62678442"
---
# <a name="restore-the-master-database-in-analytics-platform-system"></a>Ripristinare il database master nel sistema di piattaforma Analitica
Il **Restore Master** pagina di Gestione configurazione SQL Server PDW consente di ripristinare il database master da un backup.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
> [!IMPORTANT]  
> Per eseguire il ripristino, SQL Server PDW è necessario eliminare il database master corrente, che contiene le informazioni di sicurezza utente e il catalogo del database. È consigliabile effettuare un backup del database master corrente prima di eseguire il ripristino.  
  
## <a name="to-restore-the-master-database"></a>Per ripristinare il database master  
  
1.  Avviare Gestione configurazione. Per altre informazioni, vedere [avviare Gestione configurazione &#40;sistema di piattaforma Analitica&#41;](launch-the-configuration-manager.md).  
  
2.  Nel riquadro a sinistra di Configuration Manager, fare clic su **Restore Master**.  
  
3.  Selezionare il master di backup da ripristinare.  
  
4.  Fare clic su **Applica**.  
  
5.  Per eseguire il ripristino, SQL Server PDW arresterà tutti i servizi di appliance e disconnettere tutti gli utenti. Al termine del ripristino, SQL Server PDW verrà riavviato i servizi di appliance.  
  
![DWConfig Appliance PDW Restore master](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
