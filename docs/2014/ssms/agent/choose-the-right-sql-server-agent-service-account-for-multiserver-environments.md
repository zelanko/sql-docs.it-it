---
title: Scegliere l'account del servizio SQL Server Agent appropriato per gli ambienti multiserver | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, service accounts
- multiserver environments [SQL Server], SQL Server Agent service account behavior
ms.assetid: a07e2f38-281c-495b-965b-13fad03ba548
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e3a981690efb0139d8878cab4e13794fdcf44ed7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63199902"
---
# <a name="choose-the-right-sql-server-agent-service-account-for-multiserver-environments"></a>Scegliere l'account di servizio SQL Server Agent adatto ad ambienti multiserver
  L'account di Windows scelto per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent può influenzare il comportamento di un ambiente multiserver, come illustrato di seguito:  
  
-   Se si esegue il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent con un account che non appartiene al gruppo Administrators locale di Windows, è possibile che l'integrazione dei server di destinazione nei server master abbia esito negativo. In questo caso, verrà visualizzato il messaggio di errore seguente:  
  
     "Operazione di integrazione non riuscita."  
  
     Per risolvere il problema, riavviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
-   Quando il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene eseguito con l'account di sistema locale, le operazioni tra server master e server di destinazione sono supportate solo se entrambi risiedono nello stesso computer. Se si utilizza questa configurazione, quando si integrano i server di destinazione in un server master, verrà visualizzato il seguente messaggio:  
  
     "Verifica che l'account di avvio dell'agente per *<target_server_computer_name>* disponga dei diritti per l'accesso come server di destinazione".  
  
     Questo messaggio può essere ignorato. L'operazione di integrazione verrà completata correttamente.  
  
 Per informazioni su come selezionare l'account di avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere [Selezionare un account per il servizio SQL Server Agent](select-an-account-for-the-sql-server-agent-service.md).  
  
  
