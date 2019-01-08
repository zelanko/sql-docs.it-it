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
manager: craigg
ms.openlocfilehash: 72e004e6fd41ee74643fc05ec9020e6ac1933e09
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53208570"
---
# <a name="affected-odbc-components"></a>Componenti ODBC interessati
Compatibilità con le versioni precedenti viene descritto come le applicazioni, gestione Driver e i driver sono interessati dall'introduzione di una nuova versione di gestione Driver. Questo influisce sulle applicazioni e driver quando uno o entrambi gli elementi rimangono nella versione precedente. Vi sono, pertanto, tre tipi di garantire la compatibilità da prendere in considerazione, come illustrato nella tabella seguente.  
  
|Tipo|Versione di gestione dei dispositivi|Versione dell'applicazione|Versione del driver|  
|----------|-------------------|----------------------------|-----------------------|  
|Garantire la compatibilità di gestione Driver|3 *. x*|2.*x*|2.*x*|  
|Compatibilità con le versioni precedenti del Driver [1]|3 *. x*|2.*x*|3.*x*|  
|Compatibilità con le versioni precedenti dell'applicazione|3.*x*|3.*x*|2.*x*|  
  
 [1] la compatibilità con le versioni precedenti dei driver viene illustrata principalmente in appendice g: Driver linee guida per la compatibilità con le versioni precedenti.  
  
> [!NOTE]
>  Un'applicazione conforme agli standard, ad esempio, un'applicazione che è stata scritta in conformità con gli standard Open Group o ISO CLI - sarà sicuramente funzionante con un'applicazione ODBC 3 *. x* driver tramite ODBC 3 *. x*Gestione driver. Si presuppone che la funzionalità che usa l'applicazione è disponibile nel driver. Si presuppone inoltre che l'applicazione e conformi agli standard è stato compilato con ODBC 3*x* i file di intestazione.
