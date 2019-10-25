---
title: Sicurezza di SQL Server Express
description: Vengono illustrate le considerazioni sulla sicurezza relative a SQL Server Express.
ms.date: 09/26/2019
ms.assetid: cf9cf6d9-4b05-43e9-ac7b-6cefbfcd6d4e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 9d6b711109f7d94e3bca8d9cf2bda6d2c124c798
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452023"
---
# <a name="sql-server-express-security"></a>Sicurezza di SQL Server Express

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Microsoft SQL Server Express Edition (SQL Server Express) è basato su Microsoft SQL Server e supporta la maggior parte delle funzionalità del motore di database. È progettato in modo che le funzionalità non essenziali e la connettività di rete siano disattivate per impostazione predefinita. In questo modo si riduce la superficie di attacco disponibile per un attacco da parte di utenti malintenzionati.  
  
SQL Server Express viene in genere installato come istanza denominata. Il nome predefinito dell'istanza è `SQLExpress`. Un'istanza denominata viene identificata dal nome di rete del computer e dal nome dell'istanza specificato durante l'installazione.  
  
## <a name="network-access"></a>Accesso alla rete  
Per motivi di sicurezza, i protocolli di rete sono disabilitati per impostazione predefinita in SQL Server Express. In questo modo si evitano gli attacchi provenienti da utenti esterni che potrebbero compromettere il computer che ospita l'istanza di SQL Server Express. È necessario abilitare in modo esplicito la connettività di rete e avviare il servizio SQL Server Browser per connettersi a un'istanza di SQL Server Express da un altro computer.  
  
Una volta abilitata la connettività di rete, un'istanza di SQL Server Express presenta gli stessi requisiti di sicurezza delle altre edizioni di SQL Server.  
  
## <a name="user-instances"></a>Istanze utente  
Un'istanza utente è un'istanza separata del motore di database SQL Server Express generata da un'istanza padre di SQL Server Express. L'obiettivo principale di un'istanza utente è quello di consentire agli utenti che eseguono Windows con un account utente con privilegi minimi di disporre dei privilegi di amministratore di sistema (`sysadmin`) nell'istanza SQL Server Express sul computer locale. Le istanze utente non sono destinate agli utenti che sono amministratori di sistema nei propri computer.  
  
Un'istanza utente viene generata da un'istanza primaria di SQL Server o SQL Server Express per conto di un utente. Viene eseguita come processo utente nel contesto di sicurezza di Windows dell'utente, non come servizio. Gli account di accesso SQL Server non sono consentiti. sono supportati solo gli account di accesso di Windows. In questo modo si impedisce che il software in esecuzione in un'istanza utente debba apportare modifiche a livello di sistema che l'utente non dispone delle autorizzazioni necessarie. Un'istanza utente è nota anche come istanza figlio o client, a cui a volte viene fatto riferimento tramite l'acronimo di il nome "RunAs Normal User".  
  
Ogni istanza utente è isolata dalla relativa istanza padre e da altre istanze utente in esecuzione nello stesso computer. I database installati nelle istanze utente vengono aperti solo in modalità utente singolo; non è possibile connettersi a più utenti. La replica, le query distribuite e le connessioni remote sono disabilitate per le istanze utente. Quando si è connessi a un'istanza utente, gli utenti non dispongono di privilegi speciali per l'istanza di SQL Server Express padre.  
  
## <a name="external-resources"></a>Risorse esterne  
Per ulteriori informazioni su SQL Server Express, vedere le risorse seguenti.  
  
|||  
|-|-|  
|[Documentazione online di Microsoft SQL Server 2005 Express Edition](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms165706(v=sql.90))|Documentazione completa per SQL Server 2005 Express Edition.|  
|[Istanze utente per non amministratori](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/ms143684(v=sql.100)) nella documentazione online di SQL Server|Viene descritto come creare e distribuire le istanze utente.|  
|[Istanze utente di SQL Server Express](sql-server-express-user-instances.md)|Descrive le funzionalità dell'istanza utente in un'applicazione ADO.NET. Vengono fornite informazioni su come abilitare un'istanza utente, connettersi a un'istanza utente utilizzando una <xref:Microsoft.Data.SqlClient.SqlConnection>, la durata dell'istanza utente e gli scenari dell'istanza utente.|  
  
## <a name="next-steps"></a>Passaggi successivi
- [Sicurezza di SQL Server](sql-server-security.md)
- [Istanze utente di SQL Server Express](sql-server-express-user-instances.md)
