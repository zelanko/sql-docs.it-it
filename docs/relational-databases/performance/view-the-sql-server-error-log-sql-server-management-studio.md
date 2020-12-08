---
title: Visualizzare il log degli errori di SQL Server (SSMS)
description: Informazioni sul log degli errori di SQL Server, che contiene eventi definiti dall'utente e alcuni eventi di sistema utili per la risoluzione dei problemi.
ms.custom: seo-dt-2019
ms.date: 09/29/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- displaying logs
- errors [SQL Server], logs
- logs [SQL Server], SQL Server error logs
- logs [SQL Server], viewing
ms.assetid: 55f468ba-146c-4ab3-95cd-d35d051afd12
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 4727287f27190ad865cf0ebe6142d674730dbc46
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96504875"
---
# <a name="view-the-sql-server-error-log-in-sql-server-management-studio-ssms"></a>Visualizzare il log degli errori di SQL Server in SQL Server Management Studio (SSMS)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
Il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene eventi definiti dall'utente e alcuni eventi di sistema utili per la risoluzione dei problemi. 

## <a name="view-the-logs"></a>Visualizzare i log

1. In SQL Server Management Studio selezionare **Esplora oggetti**. Per aprire **Esplora oggetti** selezionare F8. In alternativa, nel menu principale fare clic su **Visualizza** e quindi selezionare **Esplora oggetti**:
    
    ![Object_Explorer](../../relational-databases/performance/media/object-explorer.png) 

2. In **Esplora oggetti** connettersi a un'istanza di SQL Server e quindi espandere l'istanza.
  
3. Trovare ed espandere la sezione **Gestione** (presupponendo di avere le autorizzazioni necessarie per visualizzarla).

4. Fare clic con il pulsante destro del mouse su **Log di SQL Server**, scegliere **Visualizza** e quindi **Log di SQL Server**.

    ![Visualizza log di SQL server in SSMS](../../relational-databases/performance/media/view-sqlserver-log-ssms.png) 
 
5. Viene visualizzato il **Visualizzatore file di log** (potrebbero essere necessari alcuni minuti), con un elenco dei log che è possibile visualizzare.

  ## <a name="see-also"></a>Vedere anche
  Per altre informazioni, vedere l'utile post di [MSSQLTips.com](https://www.mssqltips.com/)[Identify location of the SQL Server Error Log file (Identificare la posizione del file di log degli errori di SQL Server)](https://www.mssqltips.com/sqlservertip/2506/identify-location-of-the-sql-server-error-log-file/).

