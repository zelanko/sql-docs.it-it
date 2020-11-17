---
title: Dashboard del gruppo di disponibilità in SSMS
description: Informazioni sulla pagina Opzioni visualizzata nella pagina Dashboard di SQL Server Always On in SQL Server Management Studio.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Alwayson.Dashboard
ms.assetid: 4369b588-e982-4b57-80a1-beb2e879ce0b
author: cawrites
ms.author: chadam
ms.openlocfilehash: 1b34fcb55625bf2283389abe129fe33e0aa5c6ef
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584109"
---
# <a name="options-sql-server-always-on-dashboard-page"></a>Opzioni (SQL Server AlwaysOn, pagina Dashboard)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  Usare la pagina del **dashboard AlwaysOn** della finestra di dialogo **Opzioni** di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] per configurare il dashboard AlwaysOn.  
  
 **Per accedere alla pagina:**  
  
 Nel menu **Strumenti** fare clic su **Opzioni**, espandere la cartella **SQL Server AlwaysOn** e quindi fare clic su **Dashboard**.  
  
## <a name="on-this-page"></a>In questa pagina  
 **Abilitare l'aggiornamento automatico.**  
 Fare clic per abilitare l'aggiornamento automatico. Le opzioni disponibili sono le seguenti:  
  
-   Il campo **Intervallo di aggiornamento (in secondi)** visualizza il numero di secondi trascorsi i quali il dashboard viene aggiornato. Il valore predefinito è 30. Quando l'aggiornamento automatico è abilitato, è possibile modificare il campo per modificare l'intervallo di aggiornamento.  
  
-   Nel campo **Numero di tentativi di connessione** viene visualizzato il numero di tentativi effettuati dal dashboard per connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che ospita una replica di disponibilità per un gruppo di disponibilità monitorato tramite il dashboard. Il valore predefinito è 65535. Quando l'aggiornamento automatico è abilitato, è possibile modificare il campo per cambiare il numero di tentativi di connessione.  
  
 **Abilita criteri AlwaysOn definiti dall'utente**  
 Se sono stati definiti criteri AlwaysOn, fare clic su questa opzione per abilitarli.  
  
## <a name="see-also"></a>Vedere anche  
 [Usare il dashboard Always On &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
