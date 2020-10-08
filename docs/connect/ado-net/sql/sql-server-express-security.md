---
title: Sicurezza di SQL Server Express
description: Vengono illustrate le considerazioni sulla sicurezza relative a SQL Server Express.
ms.date: 09/26/2019
ms.assetid: cf9cf6d9-4b05-43e9-ac7b-6cefbfcd6d4e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: ed42778724b468892ff72203695e976d176459b2
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725567"
---
# <a name="sql-server-express-security"></a>Sicurezza di SQL Server Express

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Microsoft SQL Server Express Edition (SQL Server Express) è basato su Microsoft SQL Server e supporta la maggior parte delle funzionalità del motore di database. È progettato in modo che le funzionalità non essenziali e la connettività di rete siano disattivate per impostazione predefinita. In questo modo si riduce la superficie di attacco disponibile per un attacco da parte di utenti malintenzionati.  
  
SQL Server Express viene in genere installato come istanza denominata. Il nome predefinito dell'istanza è `SQLExpress`. Un'istanza denominata viene identificata dal nome di rete del computer e dal nome dell'istanza specificato durante l'installazione.  
  
## <a name="network-access"></a>Accesso alla rete  
Per motivi di sicurezza, i protocolli di rete sono disabilitati per impostazione predefinita in SQL Server Express. In questo modo si evitano gli attacchi provenienti da utenti esterni che potrebbero compromettere il computer che ospita l'istanza di SQL Server Express. È necessario abilitare in modo esplicito la connettività di rete e avviare il servizio SQL Server Browser per connettersi a un'istanza di SQL Server Express da un altro computer.  
  
Dopo aver abilitato la connettività di rete, un'istanza di SQL Server Express presenta gli stessi requisiti di sicurezza delle altre edizioni di SQL Server.  
  
## <a name="user-instances"></a>Istanze utente  
Un'istanza utente è un'istanza separata del motore di database SQL Server Express generata da un'istanza padre di SQL Server Express. L'obiettivo principale di un'istanza utente è quello di consentire agli utenti che eseguono Windows con un account utente con privilegi minimi di avere i privilegi di amministratore di sistema (`sysadmin`) nell'istanza di SQL Server Express nel computer locale. Le istanze utente non sono destinate agli utenti che sono amministratori di sistema nei propri computer.  
  
Un'istanza utente viene generata da un'istanza primaria di SQL Server o SQL Server Express per conto di un utente. L'istanza viene eseguita come processo utente nel contesto di protezione di Windows dell'utente, non come servizio. Gli account di accesso di SQL Server non sono consentiti. Sono supportati solo gli account di accesso di Windows. In questo modo si impedisce che il software eseguito in un'istanza utente apporti modifiche a livello di sistema per cui l'utente non ha le autorizzazioni necessarie. L'istanza utente è chiamata anche istanza figlio o client e a volte viene fatto riferimento all'istanza usando l'acronimo RANU (Run As Normal User).  
  
Ogni istanza utente è isolata dall'istanza padre e da qualsiasi altra istanza utente eseguita nello stesso computer. I database installati nelle istanze utente vengono aperti solo in modalità utente singolo; non è possibile la connessione di più utenti. La replica, le query distribuite e le connessioni remote sono disabilitate per le istanze utente. Quando si è connessi a un'istanza utente, gli utenti non hanno privilegi speciali per l'istanza di SQL Server Express padre.  
  
## <a name="external-resources"></a>Risorse esterne  
Per altre informazioni su SQL Server Express, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|
|-|-|  
|[Documentazione online di Microsoft SQL Server 2005 Express Edition](/previous-versions/sql/sql-server-2005/ms165706(v=sql.90))|Documentazione completa di SQL Server 2005 Express Edition.|  
|[Istanze utente per non amministratori](/previous-versions/sql/sql-server-2008/ms143684(v=sql.100)) nella documentazione online di SQL Server|Descrive come creare e distribuire le istanze utente.|  
|[Istanze utente di SQL Server Express](sql-server-express-user-instances.md)|Descrive le funzionalità dell'istanza utente in un'applicazione ADO.NET. Offre informazioni su come abilitare un'istanza utente, su connettersi a un'istanza utente usando <xref:Microsoft.Data.SqlClient.SqlConnection>, sulla durata dell'istanza utente e sugli scenari dell'istanza utente.|  
  
## <a name="next-steps"></a>Passaggi successivi
- [Sicurezza di SQL Server](sql-server-security.md)
- [Istanze utente di SQL Server Express](sql-server-express-user-instances.md)