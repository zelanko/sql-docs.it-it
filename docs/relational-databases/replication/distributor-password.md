---
title: Password server di distribuzione | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configuredistributionwizard.distributorpassword.f1
ms.assetid: 52787c5e-c9ef-440e-a000-0787111b7dbb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: efaff5ca7858048413440c9cfe774397bdc9069f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128326"
---
# <a name="distributor-password"></a>Password server di distribuzione
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Se nella pagina **Server di pubblicazione** di questa procedura guidata uno più server di pubblicazione sono stati abilitati all'utilizzo del server corrente come server di distribuzione remoto, è necessario specificare una password per la connessione eseguita dalla replica tra il server di pubblicazione e il server di distribuzione remoto utilizzando l'account di accesso **distributor_admin** . È necessario specificare la stessa password per ogni server di pubblicazione che utilizza questo server di distribuzione remoto nella pagina **Password amministrativa** della Creazione guidata nuova pubblicazione o della Configurazione guidata distribuzione. Per altre informazioni sulla sicurezza dei database di distribuzione, vedere [Proteggere il database di distribuzione](../../relational-databases/replication/security/secure-the-distributor.md).  
  
## <a name="options"></a>Opzioni  
 **Password**  
 Consente di immettere una password complessa per la connessione tra il server di pubblicazione e il server di distribuzione remoto.  
  
 **Conferma password**  
 Consente di immettere nuovamente la password per verificarne la corretta immissione.  
  
## <a name="see-also"></a>Vedere anche  
 [Configura distribuzione](../../relational-databases/replication/configure-distribution.md)   
 [Configurare la pubblicazione e la distribuzione](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
  
