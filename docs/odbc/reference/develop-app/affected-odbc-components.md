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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67944859"
---
# <a name="affected-odbc-components"></a>Componenti ODBC interessati
La compatibilità con le versioni precedenti descrive il modo in cui le applicazioni, gestione driver e i driver sono interessati dall'introduzione di una nuova versione di gestione driver. Ciò influiscono sulle applicazioni e sui driver quando uno o entrambi i valori rimangono nella versione precedente. Ci sono pertanto tre tipi di compatibilità con le versioni precedenti da considerare, come illustrato nella tabella seguente.  
  
|Type|Versione di DM|Versione dell'applicazione|Versione del driver|  
|----------|-------------------|----------------------------|-----------------------|  
|Compatibilità con le versioni precedenti di gestione driver|*3.x*|*2.x*|*2.x*|  
|Compatibilità con le versioni precedenti del driver [1]|*3.x*|*2.x*|*3.x*|  
|Compatibilità con le versioni precedenti dell'applicazione|*3.x*|*3.x*|*2.x*|  
  
 [1] la compatibilità con le versioni precedenti dei driver è descritta principalmente in Appendice G: linee guida driver per compatibilità con le versioni precedenti.  
  
> [!NOTE]
>  Un'applicazione conforme agli standard, ad esempio un'applicazione che è stata scritta in base agli standard dell'interfaccia della riga di comando ISO e del gruppo aperto, garantisce l'utilizzo di un driver ODBC *3. x* tramite Gestione driver ODBC *3. x* . Si presuppone che la funzionalità utilizzata dall'applicazione sia disponibile nel driver. Si presuppone inoltre che l'applicazione conforme agli standard sia stata compilata con i file di intestazione ODBC *3. x* .
