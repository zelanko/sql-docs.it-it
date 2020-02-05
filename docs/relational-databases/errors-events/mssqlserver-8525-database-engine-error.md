---
title: MSSQLSERVER_8525 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "8525"
helpviewer_keywords:
- 8525 (Database Engine error)
ms.assetid: 297867c1-691e-4d6b-a3be-a7575015ecfa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 605bb1ae8ff8cd3fb3e5c0e7a096de7aa646730c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68101480"
---
# <a name="mssqlserver_8525"></a>MSSQLSERVER_8525
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|8525|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico||  
|Testo del messaggio|La transazione distribuita è stata completata. Integrare questa sessione in una nuova transazione o nella transazione NULL.|  
  
## <a name="explanation"></a>Spiegazione  
Il modello di programmazione per l'uso di Distributed Transaction Coordinator con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede alle applicazioni l'integrazione esplicita in una transazione distribuita o l'esclusione esplicita da essa.  
  
Questo errore si verifica quando vengono soddisfatte le quattro condizioni seguenti:  
  
-   L'applicazione è stata integrata in una transazione distribuita.  
  
-   La transazione di cui è stato eseguito il commit o il rollback, è stata interrotta per un motivo qualsiasi.  
  
-   L'applicazione utente non è stata esclusa in modo esplicito da una transazione distribuita o integrata in modo esplicito in una nuova transazione distribuita.  
  
-   L'applicazione tenta di eseguire qualsiasi operazione transazionale, ad eccezione dell'esclusione da una transazione distribuita esistente o dell'integrazione in una nuova transazione distribuita, ad esempio l'esecuzione di una query o l'avvio di una transazione locale.  
  
Lo stato di errore 1 viene utilizzato quando l'applicazione esegue un'operazione che consente di creare transazioni locali. Lo stato 2 viene utilizzato quando l'applicazione tenta l'integrazione in una sessione associata.  
  
## <a name="user-action"></a>Azione dell'utente  
Dopo l'integrazione in una transazione distribuita, l'applicazione deve essere esclusa in modo esplicito dalla transazione distribuita o integrata in un'altra transazione distribuita. Ciò determina l'esclusione implicita da una transazione inclusa in precedenza. Per informazioni sulla sintassi esatta da utilizzare per l'esclusione da una transazione distribuita o l'inclusione in essa, vedere il manuale dell'interfaccia di programmazione per l'applicazione.  
  
