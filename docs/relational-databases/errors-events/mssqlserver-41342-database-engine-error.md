---
title: MSSQLSERVER_41342 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41342 (Database Engine error)
ms.assetid: 28270d98-c543-4e7d-b40c-2200e38dce1c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d57f619326a36237dac8cbad7eb59bba429ad3af
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68123279"
---
# <a name="mssqlserver_41342"></a>MSSQLSERVER_41342
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|41342|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|HK_HW_NOT_SUPPORTED|  
|Testo del messaggio|Il modello del processore del sistema non supporta la creazione di *costrutto*. Questo errore si verifica in genere nei processori meno recenti.|  
  
## <a name="explanation"></a>Spiegazione  
Per le tabelle con ottimizzazione per la memoria è richiesto un modello di processore che supporta le operazioni di scambio e confronto atomiche su valori a 128 bit, che richiedono l'istruzione di assembly CMPXCHG16B. Alcuni modelli di processore AMD meno recenti non supportano l'istruzione CMPXCHG16B. Inoltre, alcuni ambienti di virtualizzazione non consentono l'utilizzo di questa istruzione per impostazione predefinita.  
  
## <a name="user-action"></a>Azione dell'utente  
Aggiornare il processore. Se il processore supporta l'istruzione e si sta eseguendo SQL Server in una macchina virtuale, modificare la configurazione per supportare l'istruzione CMPXCHG16B.  
  
## <a name="see-also"></a>Vedere anche  
[OLTP in memoria &#40;ottimizzazione per la memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
