---
title: Protezione della proprietà intellettuale di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- protecting intellectual property
- intellectual property
ms.assetid: 174a646a-d65c-4074-8249-d783e91be2dd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: afe179023f72ec509af5828bb89afb51f93b53a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986597"
---
# <a name="protecting-your-sql-server-intellectual-property"></a>Protezione della proprietà intellettuale di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Gli sviluppatori di software spesso si interrogano su come distribuire le proprie applicazioni [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] impedendo eventuali operazioni di analisi e decodificazione. Il problema principale è il fatto che la protezione della proprietà intellettuale rappresenta una questione legale molto importante che può essere gestita solo mediante un contratto di licenza. Quando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] viene installato in un computer amministrato da altri utenti, si perdono intrinsecamente alcuni aspetti del controllo sull'applicazione. 

## <a name="nature-of-the-problem"></a>Natura del problema
Il proprietario o l'amministratore di un computer può accedere sempre all'istanza di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] installata nel proprio computer. Se si distribuisce un'applicazione nel computer di un cliente, tale cliente ne è l'amministratore e pertanto può connettersi a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] come membro del ruolo predefinito del server **sysadmin**. In qualità di amministratore sarà in grado di concedere autorizzazioni, gestire i backup, ripristinare i backup in altri computer, decrittografare e spostare i file di dati e così via. Per altre informazioni, vedere [Connettersi a SQL Server se gli amministratori di sistema sono bloccati](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md). 

Le stored procedure e i dati possono essere crittografati, ma la struttura dei dati non può essere nascosta. Pertanto, gli utenti in grado di associare un debugger al processo server possono recuperare procedure e dati decrittografati dalla memoria durante il runtime.

Se i client non sono amministratori dei computer, è possibile impedire loro l'accesso. È possibile usare la [crittografia dati trasparente](../../relational-databases/security/encryption/transparent-data-encryption.md) per crittografare i file di dati e i backup, nonché per controllare le azioni di tutti gli utenti. Tuttavia, gli amministratori di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e gli amministratori del computer [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] possono annullare queste azioni.

## <a name="solution"></a>Soluzione
Sono disponibili vari modi per configurare l'accesso ai dati client senza installare [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] nel computer client. Il modo più semplice prevede l'uso di [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)] (in questo caso i client non sono amministratori), in combinazione con la crittografia [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Per altre informazioni sui concetti introduttivi di [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], vedere [Informazioni sul database SQL Introduzione al database SQL](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview).  

È inoltre possibile ospitare un'istanza di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] in rete e consentire ai client di accedere ai dati mediante la rete, direttamente o tramite un'applicazione Web.

## <a name="see-also"></a>Vedere anche

[Centro di sicurezza per il motore di database di SQL Server e il database SQL di Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
[Sicurezza di SQL Server](../../relational-databases/security/securing-sql-server.md)  

