---
title: Proprietà server (pagina Sicurezza) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverproperties.security.f1
ms.assetid: b8a131c7-e7bd-4203-bf26-234f1ebfe622
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3a42d496a59f489238d270fcb6bb17f3e1ff6421
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62809005"
---
# <a name="server-properties-security-page"></a>Proprietà server (pagina sicurezza)
  Utilizzare questa pagina per visualizzare o modificare le opzioni di sicurezza del server.  
  
## <a name="server-authentication"></a>Autenticazione del server  
 **Autenticazione di Windows**  
 Consente di utilizzare l'autenticazione di Windows per convalidare i tentativi di connessione. Se la password **sa** è vuota quando si modifica la modalità di sicurezza, all'utente viene chiesto di immettere una password **sa** .  
  
> [!IMPORTANT]  
>  L'autenticazione di Windows offre una sicurezza decisamente maggiore rispetto all'autenticazione di SQL Server. Se possibile, utilizzare l'autenticazione di Windows.  
  
 **Autenticazione di SQL Server e di Windows**  
 Consente di utilizzare una modalità di autenticazione mista per la verifica dei tentativi di connessione. È disponibile per motivi di compatibilità con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se la password **sa** è vuota quando si modifica la modalità di sicurezza, all'utente viene chiesto di immettere una password **sa** .  
  
> [!NOTE]  
>  la modifica della configurazione di sicurezza richiede il riavvio del servizio. Quando si passa dall'autenticazione server a SQL Server e all'autenticazione di Windows, l'account SA non viene abilitato automaticamente. Per usare l'account SA, eseguire [ALTER LOGIN](/sql/t-sql/statements/alter-login-transact-sql) con l'opzione ENABLE.  
  
## <a name="login-auditing"></a>Controllo accessi  
 **None**  
 Consente di disattivare il controllo degli accessi.  
  
 **Solo accessi non riusciti**  
 Consente di controllare solo gli accessi non riusciti.  
  
 **Solo accessi riusciti**  
 Consente di controllare solo gli accessi riusciti.  
  
 **Accessi riusciti e non riusciti**  
 Consente di controllare tutti i tentativi di accesso.  
  
> [!NOTE]  
>  la modifica del livello di controllo richiede il riavvio del server.  
  
## <a name="server-proxy-account"></a>Account proxy server  
 **Abilita account proxy server**  
 Abilita un account per l'uso da parte di **xp_cmdshell**. Gli account proxy consentono la rappresentazione di account di accesso, ruoli del server e ruoli del database durante l'esecuzione di un comando del sistema operativo.  
  
> [!CAUTION]  
>  l'account di accesso utilizzato dall'account proxy server deve disporre dei privilegi minimi necessari per l'esecuzione del lavoro designato. Privilegi eccessivi per l'account proxy potrebbero essere utilizzati da utenti malintenzionati per compromettere la sicurezza del sistema.  
  
 **Account proxy**  
 Consente di specificare l'account proxy utilizzato.  
  
 **Password**  
 Consente di specificare la password per l'account proxy.  
  
## <a name="options"></a>Opzioni  
 **Abilita traccia di controllo C2**  
 Consente di tenere traccia di tutti i tentativi di accesso a istruzioni e oggetti, nonché di registrarli in un file nella directory \MSSQL\Data per le istanze predefinite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o nella directory \MSSQL$*nomeistanza*\Data per le istanze denominate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Opzione di configurazione del server c2 audit mode](c2-audit-mode-server-configuration-option.md).  
  
 **Concatenamento della proprietà tra database**  
 Selezionare questa opzione per impostare il database come origine o destinazione di un concatenamento di proprietà tra database. Per altre informazioni, vedere [Opzione di configurazione del server cross db ownership chaining](cross-db-ownership-chaining-server-configuration-option.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
