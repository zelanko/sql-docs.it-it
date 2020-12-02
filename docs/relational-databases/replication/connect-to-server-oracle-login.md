---
description: Connetti al server (Oracle), Account di accesso
title: Connetti al server (Oracle), Account di accesso| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.oracleconnection.login.f1
helpviewer_keywords:
- Connect to Server dialog box, replication
ms.assetid: 86ed91a1-a07c-46f2-a913-67317ef2255e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b585e2a17e577aab7ade2c5906bdcd184a12e8dd
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96121355"
---
# <a name="connect-to-server-oracle-login"></a>Connetti al server (Oracle), Account di accesso
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Usare la scheda **Account di accesso** della finestra di dialogo **Connetti al server** per specificare l'account con cui vengono stabilite le connessioni dal server di distribuzione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al server di pubblicazione Oracle. È necessario utilizzare lo stesso account specificato per lo schema utente di amministrazione della replica durante la configurazione del server di pubblicazione. Per altre informazioni, vedere [Configurare un server di pubblicazione Oracle](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="options"></a>Opzioni  
 **Istanza del server**  
 Transparent Network Substrate del server di pubblicazione Oracle specificato durante la configurazione del software client Oracle installato nel server di distribuzione.  
  
 **autenticazione**  
 Consente di selezionare l' **Autenticazione standard Oracle** (scelta consigliata) oppure l' **Autenticazione di Windows**. Se si seleziona l' **Autenticazione di Windows**:  
  
-   Il server Oracle deve essere configurato in modo da consentire le connessioni con le credenziali di Windows. Per ulteriori informazioni, vedere la documentazione di Oracle.  
  
-   È necessario eseguire l'accesso con lo stesso account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows specificato per lo schema utente di amministrazione della replica.  
  
 **Account di accesso** e **Password**  
 Se è stata selezionata l' **Autenticazione standard Oracle** per l'opzione **Autenticazione** , specificare l'account di accesso e la password da utilizzare, che devono corrispondere all'account di accesso e alla password specificati per lo schema utente di amministrazione della replica.  
  
## <a name="see-also"></a>Vedere anche  
 [Glossario dei termini per la pubblicazione Oracle](../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)  
  
  
