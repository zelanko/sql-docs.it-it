---
title: Proprietà di database TRUSTWORTHY | Microsoft Docs
description: Informazioni sulla proprietà di database TRUSTWORTHY, che indica se l'istanza di SQL Server considera attendibile il database e il relativo contenuto. Il valore predefinito è OFF.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- TRUSTWORTHY database property
ms.assetid: 64b2a53d-4416-4a19-acc0-664a61b45348
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4db2515c51085e79d67e6ace4cbbe1abedc91023
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85736965"
---
# <a name="trustworthy-database-property"></a>Proprietà di database TRUSTWORTHY
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  La proprietà di database TRUSTWORTHY consente di indicare se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera attendibile il database e il relativo contenuto. Per impostazione predefinita, questa impostazione ha valore OFF, ma è possibile impostarla su ON tramite l'istruzione ALTER DATABASE. Ad esempio: `ALTER DATABASE AdventureWorks2012 SET TRUSTWORTHY ON;`.  
  
> [!NOTE]  
>  Per impostare questa opzione è necessario essere un membro del ruolo predefinito **sysadmin** del server.  
  
 Questa proprietà può essere utilizzata per limitare i rischi che possono derivare dal collegamento a un database contenente uno degli oggetti seguenti:  
  
-   Assembly dannosi con un'impostazione di autorizzazione EXTERNAL_ACCESS o UNSAFE. Per altre informazioni, vedere [Sicurezza per l'integrazione con CLR](../../relational-databases/clr-integration/security/clr-integration-security.md).  
  
-   Moduli dannosi definiti in modo da essere eseguiti con un account utente con privilegi elevati. Per altre informazioni, vedere [Clausola EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
 Entrambe le situazioni richiedono un livello di privilegi specifico e vengono evitate grazie a meccanismi appropriati quando tali componenti vengono utilizzati nel contesto di un database già collegato a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se però il database è offline, un utente che ha accesso al file di database è potenzialmente in grado di collegarlo a un'istanza arbitraria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aggiungervi contenuto dannoso. Quando i database vengono scollegati e collegati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sui dati e sui file di log vengono impostate determinate autorizzazioni che limitano l'accesso ai file di database.  
  
 Poiché un database che viene collegato a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non può essere considerato immediatamente attendibile, non può accedere a risorse esterne al proprio ambito fino a quando non verrà esplicitamente contrassegnato come attendibile. Pertanto, se si esegue il backup o lo scollegamento di un database con l'opzione TRUSTWORTHY impostata su ON e si collega o ripristina il database alla stessa o ad un'altra istanza di SQL Server, la proprietà TRUSTWORTHY verrà impostata su OFF al termine del collegamento/ripristino. Sono inoltre previsti ulteriori requisiti per l'esecuzione dei moduli progettati per accedere a risorse esterne al database e degli assembly con impostazione di autorizzazione EXTERNAL_ACCESS e UNSAFE.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Centro sicurezza per il motore di Database di SQL Server e il Database SQL di Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
