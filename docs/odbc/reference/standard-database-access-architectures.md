---
title: Architetture standard per l'accesso al database Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a9d41800-9068-4b76-895a-32b2853692dd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e78202eff69e6b30dc1e97d80f464dad75bb201
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280034"
---
# <a name="standard-database-access-architectures"></a>Architetture standard di accesso ai database
Esaminando i componenti di accesso al database descritti nella sezione precedente, si scopre che due di essi - interfacce di programmazione e protocolli di flusso di dati - sono buoni candidati per la standardizzazione. Gli altri due componenti - meccanismo IPC e protocolli di rete - non solo risiedono a un livello troppo basso, ma sono entrambi fortemente dipendenti dalla rete e dal sistema operativo. C'è anche un terzo approccio - gateway - che offre possibilità di standardizzazione.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Interfaccia di programmazione standard](../../odbc/reference/standard-programming-interface.md)  
  
-   [Protocollo del flusso di dati standard](../../odbc/reference/standard-data-stream-protocol.md)  
  
-   [Gateway standard](../../odbc/reference/standard-gateway.md)
