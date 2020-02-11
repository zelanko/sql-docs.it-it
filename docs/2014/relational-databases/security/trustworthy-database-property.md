---
title: Proprietà di database TRUSTWORTHY | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- TRUSTWORTHY database property
ms.assetid: 64b2a53d-4416-4a19-acc0-664a61b45348
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 04f4dbeee8c160e968ee4b9df29e96d21d857e58
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63184390"
---
# <a name="trustworthy-database-property"></a>Proprietà di database TRUSTWORTHY
  La proprietà di database TRUSTWORTHY consente di indicare se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera attendibile il database e il relativo contenuto. Per impostazione predefinita, questa impostazione ha valore OFF, ma è possibile impostarla su ON tramite l'istruzione ALTER DATABASE. Ad esempio: `ALTER DATABASE AdventureWorks2012 SET TRUSTWORTHY ON;`.  
  
> [!NOTE]  
>  Per impostare questa opzione è necessario essere un membro del ruolo predefinito **sysadmin** del server.  
  
 Questa proprietà può essere utilizzata per limitare i rischi che possono derivare dal collegamento a un database contenente uno degli oggetti seguenti:  
  
-   Assembly dannosi con un'impostazione di autorizzazione EXTERNAL_ACCESS o UNSAFE. Per altre informazioni, vedere [Sicurezza per l'integrazione con CLR](../clr-integration/security/clr-integration-security.md).  
  
-   Moduli dannosi definiti in modo da essere eseguiti con un account utente con privilegi elevati. Per altre informazioni, vedere [Clausola EXECUTE AS &#40;Transact-SQL&#41;](/sql/t-sql/statements/execute-as-clause-transact-sql).  
  
 Entrambe le situazioni richiedono un livello di privilegi specifico e vengono evitate grazie a meccanismi appropriati quando tali componenti vengono utilizzati nel contesto di un database già collegato a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se però il database è offline, un utente che ha accesso al file di database è potenzialmente in grado di collegarlo a un'istanza arbitraria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aggiungervi contenuto dannoso. Quando i database vengono scollegati e collegati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sui dati e sui file di log vengono impostate determinate autorizzazioni che limitano l'accesso ai file di database.  
  
 Poiché un database che viene collegato a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non può essere considerato immediatamente attendibile, non può accedere a risorse esterne al proprio ambito fino a quando non verrà esplicitamente contrassegnato come attendibile. Sono inoltre previsti ulteriori requisiti per l'esecuzione dei moduli progettati per accedere a risorse esterne al database e degli assembly con impostazione di autorizzazione EXTERNAL_ACCESS e UNSAFE.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Centro sicurezza per il motore di Database di SQL Server e il Database SQL di Azure](security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
