---
description: Proprietà del proxy - Nuovo account proxy (pagina Generale)
title: Proprietà del proxy - Nuovo account proxy (pagina Generale)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.proxy.general.f1
ms.assetid: 5cd81265-bf59-413b-8397-150ddc70d0c7
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: efff382c4b65711f71e619ff33cee26c13210c87
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474402"
---
# <a name="proxy-account-properties---new-proxy-account-general-page"></a>Proprietà del proxy - Nuovo account proxy (pagina Generale)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di SQL di Azure](/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte ma non tutte le funzionalità di SQL Server Agent. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita di SQL di Azure e SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Usare questa pagina per visualizzare o modificare le proprietà di un account proxy di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opzioni  
**Nome proxy**  
Consente di digitare il nome del proxy.  
  
**Nome credenziali**  
Consente di digitare il nome delle credenziali per il proxy.  
  
> [!NOTE]  
> Il nome delle credenziali fornito deve essere il nome di credenziali esistenti. Per informazioni sulla creazione di credenziali, vedere [Procedura: Creare un proxy](../../relational-databases/security/authentication-access/create-a-credential.md)  
  
**...**  
Apre la finestra di dialogo **Seleziona credenziali** .  
  
**Descrizione**  
Consente di digitare la descrizione per il proxy.  
  
**Attivo nei sottosistemi seguenti**  
Consente di selezionare i sottosistemi ai quali ha accesso l'account proxy.  
  
**Riassegna i passaggi del processo a**  
Consente di selezionare il proxy al quale riassegnare i passaggi del processo. Questo elenco è abilitato quando si revoca l'accesso a un sottosistema al quale il proxy aveva accesso in precedenza.  
  
## <a name="see-also"></a>Vedere anche  
[Creazione di un proxy di SQL Server Agent](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
