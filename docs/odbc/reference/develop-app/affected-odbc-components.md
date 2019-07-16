---
title: Componenti ODBC interessati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 08997f610b00f22d436a5c91d34beb2a8fc2cc1d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944859"
---
# <a name="affected-odbc-components"></a>Componenti ODBC interessati
Compatibilità con le versioni precedenti viene descritto come le applicazioni, gestione Driver e i driver sono interessati dall'introduzione di una nuova versione di gestione Driver. Questo influisce sulle applicazioni e driver quando uno o entrambi gli elementi rimangono nella versione precedente. Vi sono, pertanto, tre tipi di garantire la compatibilità da prendere in considerazione, come illustrato nella tabella seguente.  
  
|type|Versione di gestione dei dispositivi|Versione dell'applicazione|Versione del driver|  
|----------|-------------------|----------------------------|-----------------------|  
|Garantire la compatibilità di gestione Driver|*3.x*|*2.x*|*2.x*|  
|Compatibilità con le versioni precedenti del Driver [1]|*3.x*|*2.x*|*3.x*|  
|Compatibilità con le versioni precedenti dell'applicazione|*3.x*|*3.x*|*2.x*|  
  
 [1] la compatibilità con le versioni precedenti dei driver viene illustrata principalmente in appendice g: Driver linee guida per la compatibilità con le versioni precedenti.  
  
> [!NOTE]
>  Un'applicazione conforme agli standard, ad esempio, un'applicazione che è stata scritta in conformità con gli standard Open Group o ISO CLI - sarà sicuramente funzionante con un database ODBC *3.x* driver tramite ODBC *3.x*Gestione driver. Si presuppone che la funzionalità che usa l'applicazione è disponibile nel driver. Si presuppone inoltre che l'applicazione e conformi agli standard è stato compilato con ODBC *3.x* i file di intestazione.
