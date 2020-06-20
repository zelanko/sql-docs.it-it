---
title: Errore WMI 0x8007052f | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- 0x8007052f (WMI error)
ms.assetid: a33f12bd-15c4-42a8-b343-de44c3e87729
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d6e857e0ccaad9b6f34bbdc9b88aea2e6d7291d8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048843"
---
# <a name="wmi-error-0x8007052f"></a>Errore WMI 0x8007052f
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|0x8007052f|  
|Origine evento|Errore del provider WMI|  
|Componente|Gestione configurazione SQL Server|  
|Nome simbolico|ND|  
|Testo del messaggio|Errore durante l'accesso: restrizione sull'account utente. Le possibili cause potrebbero essere: campo della password vuoto non consentito, restrizioni sugli orari di accesso o applicazione di restrizioni di criteri.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo errore può verificarsi se si utilizza Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per passare agli account predefiniti (Servizio di rete, Servizio locale o Sistema locale) quando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è in esecuzione in un cluster o un controller di dominio di Windows Server. Non eseguire i servizi con account predefiniti in un cluster o un controller di dominio di Windows Server 2003. Per informazioni sugli account di servizio, vedere l'argomento "Impostazione di account di servizio Windows" nella documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="user-action"></a>Azione dell'utente  
 Configurare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] affinché utilizzi un account di dominio.  
  
  
