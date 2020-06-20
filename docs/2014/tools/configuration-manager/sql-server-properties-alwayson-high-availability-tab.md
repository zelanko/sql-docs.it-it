---
title: Proprietà SQL Server (scheda disponibilità elevata AlwaysOn) | Microsoft Docs
description: Informazioni su come attivare o disattivare la funzionalità Gruppi di disponibilità AlwaysOn in SQL Server 2014. Visualizzare i prerequisiti che l'istanza del server deve soddisfare per questa funzionalità.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: d8630923-a600-4f1c-aca1-027453a3ec82
author: mikeraymsft
ms.author: mikeray
ms.openlocfilehash: cc145da0b6296d3f6e048905e4ab4e649294d38a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048486"
---
# <a name="sql-server-properties-alwayson-high-availability-tab"></a>Proprietà SQL Server (scheda Disponibilità elevata AlwaysOn)
  Utilizzare la scheda **Disponibilità elevata AlwaysOn** della finestra di dialogo **Proprietà SQL Server** in Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per abilitare o disabilitare la caratteristica dei gruppi di disponibilità AlwaysOn in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. L'abilitazione dei gruppi di disponibilità AlwaysOn rappresenta un prerequisito per consentire a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di utilizzare i gruppi di disponibilità come soluzione a disponibilità elevata e di ripristino di emergenza.  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
 Per poter essere abilitato per i gruppi di disponibilità AlwaysOn, un'istanza di server deve soddisfare i prerequisiti seguenti:  
  
-   L'istanza del server deve trovarsi in un nodo WSFC (Windows Server Failover Clustering).  
  
-   Per trovarsi nello stesso gruppo di disponibilità, tutte le istanze del server devono trovarsi nello stesso cluster WSFC. Un gruppo di disponibilità non può essere esteso ai cluster WSFC.  
  
-   L'istanza del server deve eseguire un'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui è supportato [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].  
  
-   Abilitare i gruppi di disponibilità AlwaysOn per una sola istanza di server per volta. Dopo aver abilitato i gruppi di disponibilità AlwaysOn, attendere il riavvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prima di abilitare la successiva istanza di server.  
  
> [!NOTE]  
>  Per informazioni sul supporto delle caratteristiche e su altri prerequisiti, restrizioni e consigli per [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], vedere la documentazione online di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
## <a name="dialog-options"></a>Opzioni della finestra di dialogo  
 **Nome cluster di failover Windows**  
 Consente di visualizzare il nome del cluster WSFC in cui il computer locale è un nodo.  
  
 **Abilitare Gruppi di disponibilità AlwaysOn in Azure**  
 Utilizzare questa casella di controllo per abilitare o disabilitare i gruppi di disponibilità AlwaysOn in questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nel modo seguente:  
  
-   Se la casella è deselezionata, i gruppi di disponibilità AlwaysOn sono attualmente disabilitati. Per abilitarli, selezionare la casella di controllo, fare clic su **OK**e riavviare manualmente il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Se la casella è già selezionata, i gruppi di disponibilità AlwaysOn sono attualmente abilitati. Per disabilitarli, deselezionare la casella di controllo e fare clic su **OK**. L'istanza del server verrà riavviata.  
  
    > [!TIP]  
    >  Dopo aver disabilitato i gruppi di disponibilità AlwaysOn, è opportuno rimuovere eventuali repliche di disponibilità dall'istanza del server. Se si rimuove l'ultima replica di un determinato gruppo di disponibilità, è opportuno rimuovere anche il gruppo.  
  
## <a name="ui-element-list"></a>Elenco elementi dell'interfaccia utente  
  
> [!NOTE]  
>  Per ulteriori informazioni su come procedere dopo aver disabilitato i gruppi di disponibilità AlwaysOn e su come creare e configurare gruppi di disponibilità, vedere la documentazione online di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
  
