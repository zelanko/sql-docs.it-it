---
title: Proprietà - Protocolli client (scheda Ordine)
description: Informazioni su come abilitare o disabilitare i protocolli client e su come riorganizzare l'ordine in cui i protocolli vengono usati quando i client provano a connettersi a SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- client protocols [SQL Server]
ms.assetid: 64fd7135-1756-4885-bed9-9ab8997ecc6c
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 841c923899900ecac354356c9599d5aad61d8cfd
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892067"
---
# <a name="client-protocols-properties-order-tab"></a>Proprietà - Protocolli client (scheda Ordine)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  Usare la pagina **Ordine** della finestra di dialogo **Proprietà protocolli client** per visualizzare e abilitare i protocolli client.  
  
 Fare clic su un protocollo e quindi su **Abilita** o **Disabilita** per spostare il protocollo selezionato nell'elenco **Protocolli disabilitati** o **Protocolli abilitati** .  
  
 I protocolli vengono utilizzati nell'ordine dell'elenco, ovvero viene effettuato un tentativo di connessione con il primo protocollo, quindi con il secondo e così via. Per spostare un protocollo verso l'alto o verso il basso nell'elenco **Protocolli abilitati** , fare clic sui pulsanti freccia. Se ci si connette a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da un client installato nello stesso computer, verrà sempre eseguito un primo tentativo di connessione con il protocollo **Shared Memory**, se abilitato.  
  
> [!NOTE]  
>  Queste impostazioni non vengono usate da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET SqlClient. L'ordine dei protocolli per .NET SqlClient è TCP, quindi named pipe e non può essere modificato.  
  
## <a name="options"></a>Opzioni  
 **Protocolli disabilitati**  
 Include un elenco dei protocolli installati ma non in uso.  
  
 **Protocolli abilitati**  
 Include un elenco dei protocolli disponibili per i client [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel computer corrente.  
  
 **>**  
 Abilita il protocollo selezionato nella casella **Protocolli disabilitati** , spostandolo nella casella **Protocolli abilitati** .  
  
 **\<**  
 Disabilita il protocollo selezionato nella casella **Protocolli abilitati** , spostandolo nella casella **Protocolli disabilitati** .  
  
 Freccia in su  
 Sposta il protocollo selezionato verso l'alto nell'elenco. In tal modo, è possibile aumentare le priorità in base alla quale la libreria di rete tenterà di utilizzare il protocollo selezionato per le connessioni.  
  
 Freccia GIÙ  
 Sposta il protocollo selezionato verso il basso nell'elenco. In tal modo, è possibile diminuire il grado di priorità in base alla quale la libreria di rete tenterà di utilizzare il protocollo selezionato per le connessioni.  
  
 **Abilita protocollo di memoria condivisa**  
 Abilita il protocollo di memoria condivisa, che, se abilitato, viene sempre usato per primo per tentare una connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da un client installato nello stesso computer.  
  
> [!NOTE]  
>  Se il protocollo viene specificato tramite un prefisso o come parte della stringa di connessione, viene eseguito un tentativo solo con il protocollo specificato.  
  
## <a name="see-also"></a>Vedere anche  
 [Scelta di un protocollo di rete](https://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
