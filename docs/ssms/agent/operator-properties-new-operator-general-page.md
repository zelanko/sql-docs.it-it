---
description: Proprietà Operatore - Nuovo operatore (pagina Generale)
title: Proprietà del nuovo operatore (pagina Generale)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.operator.general.f1
ms.assetid: c036d1c9-83d1-4a95-b67e-29d283b1a046
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b66b4f303572e5eaad5d8b6a8d0e85c3f725015d
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034894"
---
# <a name="operator-properties---new-operator-general-page"></a>Proprietà Operatore - Nuovo operatore (pagina Generale)

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di SQL di Azure](/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte ma non tutte le funzionalità di SQL Server Agent. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita di SQL di Azure e SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Usare questa pagina per visualizzare e modificare le proprietà generali degli operatori di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opzioni  
**Nome**  
Consente di modificare il nome dell'operatore.  
  
**Enabled**  
Consente di abilitare l'operatore. Se non è abilitato, all'operatore non verranno inviate notifiche.  
  
**Indirizzo posta elettronica**  
Specifica l'indirizzo di posta elettronica dell'operatore.  
  
**Indirizzo Net Send**  
Specifica l'indirizzo da usare per **Net Send**.  
  
**Indirizzo cercapersone**  
Specifica l'indirizzo di posta elettronica da utilizzare per il cercapersone dell'operatore.  
  
**Pianificazione cercapersone per operatore in servizio**  
Consente di impostare gli orari in cui il cercapersone è attivo.  
  
**Lunedì - Domenica**  
Consente di selezionare i giorni in cui il cercapersone è attivo.  
  
**Inizio giornata lavorativa**  
Consente di selezionare l'ora a partire da cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent invierà messaggi al cercapersone.  
  
**Fine giornata lavorativa**  
Consente di selezionare l'ora oltre cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non invierà più messaggi al cercapersone.  
  
## <a name="see-also"></a>Vedere anche  
[Operatori](../../ssms/agent/operators.md)  
