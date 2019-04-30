---
title: Accedi ad architetture di Database standard | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a9d41800-9068-4b76-895a-32b2853692dd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a0a8457dfde0090ac0d88d12079e88995b39efb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232399"
---
# <a name="standard-database-access-architectures"></a>Architetture standard di accesso ai database
Osservando i componenti di accesso di database descritti nella sezione precedente, si scopre che due di essi - programmazione interfacce e protocolli di flusso di dati: sono buoni candidati per la standardizzazione. Gli altri due componenti, il meccanismo IPC e protocolli di rete, non solo si trovano a un livello troppo basso, ma sono entrambi altamente dipendente nella rete e sistema operativo. È inoltre disponibile un terzo approccio - gateway - che offre opportunità di standardizzazione.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Interfaccia di programmazione standard](../../odbc/reference/standard-programming-interface.md)  
  
-   [Protocollo del flusso di dati standard](../../odbc/reference/standard-data-stream-protocol.md)  
  
-   [Gateway standard](../../odbc/reference/standard-gateway.md)
