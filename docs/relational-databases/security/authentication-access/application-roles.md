---
title: Ruoli applicazione | Microsoft Docs
description: Usare i ruoli applicazione per consentire l'accesso ai dati solo agli utenti che si collegano attraverso un'applicazione specifica in SQL Server.
ms.custom: ''
ms.date: 08/06/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- application roles [SQL Server], about application roles
- principals [SQL Server], application roles
- credentials [SQL Server], roles
- application roles [SQL Server]
- roles [SQL Server], application
- permissions [SQL Server], roles
- users [SQL Server], application roles
- authentication [SQL Server], roles
- groups [SQL Server], roles
ms.assetid: dca18b8a-ca03-4b7f-9a46-8474d5b66f76
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 340ea589ac9032b1aa85de02b0056f82805a147e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468572"
---
# <a name="application-roles"></a>Ruoli applicazione
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Un ruolo applicazione è un'entità di database che consente a un'applicazione di funzionare con proprie autorizzazioni simili a quelle per utenti. I ruoli applicazione possono essere utilizzati per consentire l'accesso a dati specifici solo agli utenti che si collegano attraverso un'applicazione particolare. A differenza dei ruoli di database, i ruoli applicazione non contengono membri e sono inattivi per impostazione predefinita. I ruoli applicazione vengono abilitati usando **sp_setapprole**, che richiede una password. Poiché si tratta di entità a livello di database, i ruoli applicazione possono accedere ad altri database solo tramite le autorizzazioni concesse in questi database all'account utente **guest**. Ogni database in cui l'account utente **guest** è stato disabilitato non sarà quindi accessibile ai ruoli applicazione di altri database.  
  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]i ruoli applicazione non possono accedere ai metadati a livello di server perché non sono associati a un'entità a livello di server. Per disabilitare questa limitazione e consentire quindi ai ruoli applicazione di accedere ai metadati a livello di server, impostare il flag globale 4616. Per altre informazioni, vedere [Flag di traccia &#40;Transact-SQL&#41;](../../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) e [DBCC TRACEON &#40;Transact-SQL&#41;](../../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md).  
  
## <a name="connecting-with-an-application-role"></a>Connessione attraverso un ruolo applicazione  
 Il passaggio da un contesto di sicurezza all'altro da parte di un ruolo applicazione si svolge nel modo seguente:  
  
1.  Un utente esegue un'applicazione client.  
  
2.  L'applicazione client si collega a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come utente.  
  
3.  L'applicazione esegue quindi la stored procedure **sp_setapprole** con una password nota solo all'applicazione.  
  
4.  Se il nome del ruolo applicazione e la password sono validi, il ruolo applicazione viene abilitato.  
  
5.  A questo punto la connessione perde le autorizzazioni dell'utente e assume le autorizzazioni del ruolo applicazione.  

 Le autorizzazioni acquisite attraverso il ruolo applicazione rimangono valide per tutta la durata della connessione.  
  
 Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], l'unico modo per un utente di ritornare al contesto di sicurezza originale dopo l'avvio di un ruolo applicazione consiste nel disconnettersi e riconnettersi a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A partire da [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], **sp_setapprole** dispone di un'opzione che crea un cookie. Il cookie contiene informazioni di contesto precedenti all'abilitazione del ruolo applicazione. Questo cookie può essere usato da **sp_unsetapprole** per riportare la sessione al contesto originale. Per informazioni su questa nuova opzione e un esempio, vedere [sp_setapprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md).  
  
> [!IMPORTANT]  
>  L'opzione ODBC **encrypt** non è supportata da **SqlClient**. Per trasmettere informazioni riservate su una rete, usare TLS (Transport Layer Security), noto in precedenza come SSL (Secure Sockets Layer) o IPSec per crittografare il canale. Se è necessario mantenere le credenziali nell'applicazione client, crittografarle utilizzando le funzioni Crypto API. In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versioni successive, il parametro *password* è archiviato come hash unidirezionale.  
  
## <a name="related-tasks"></a>Attività correlate  
  
| Attività | Type |
| ---- | ---- |
|Creare un ruolo applicazione.|[Creare un ruolo applicazione](../../../relational-databases/security/authentication-access/create-an-application-role.md) e [CREATE APPLICATION ROLE & #40; Transact-SQL & #41;](../../../t-sql/statements/create-application-role-transact-sql.md)|  
|Modificare un ruolo applicazione.|[ALTER APPLICATION ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-application-role-transact-sql.md)|  
|Eliminare un ruolo applicazione.|[DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-application-role-transact-sql.md)|  
|Utilizzo di un ruolo applicazione.|[sp_setapprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza di SQL Server](../../../relational-databases/security/securing-sql-server.md)  
  
  
