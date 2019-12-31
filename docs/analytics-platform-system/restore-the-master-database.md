---
title: Ripristinare il database master
description: Ripristinare il database master in Analytics Platform System (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6d122881f5283da86f66494ee2f049756d151551
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400448"
---
# <a name="restore-the-master-database-in-analytics-platform-system-aps"></a>Ripristinare il database master in Analytics Platform System (APS)
La pagina **Ripristina Master** della SQL Server PDW Configuration Manager consente di ripristinare il database master da un backup.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
> [!IMPORTANT]  
> Per eseguire il ripristino, SQL Server PDW necessario eliminare il database master corrente, che contiene le informazioni sulla sicurezza dell'utente e il catalogo del database. Prima di eseguire il ripristino, è consigliabile eseguire un backup del database master corrente.  
  
## <a name="to-restore-the-master-database"></a>Per ripristinare il database master  
  
1.  Avviare il Configuration Manager. Per ulteriori informazioni, vedere [la pagina relativa all'avvio del&#41;di sistema della piattaforma Configuration Manager &#40;Analytics ](launch-the-configuration-manager.md).  
  
2.  Nel riquadro sinistro della Configuration Manager fare clic su **Ripristina Master**.  
  
3.  Selezionare il backup master da ripristinare.  
  
4.  Fare clic su **Applica**  
  
5.  Per eseguire il ripristino, SQL Server PDW arresterà tutti i servizi Appliance e disconnetterà tutti gli utenti. Al termine del ripristino SQL Server PDW riavvierà i servizi Appliance.  
  
![Ripristino master PDW strumento DWConfig](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
