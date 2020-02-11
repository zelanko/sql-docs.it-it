---
title: Supporto internazionale (driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- double-byte character sets [ODBC]
- FoxPro ODBC driver [ODBC], international support
- DBCS [ODBC]
- international support [ODBC]
- sort order [ODBC]
- collating sequences [ODBC]
- Visual FoxPro ODBC driver [ODBC], international support
ms.assetid: cd3fab32-13f1-4a86-abc4-5e18667669fc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e987c224f2d716fcab3bf898b1cb276e922e48ef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085498"
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>Supporto multilingue (driver ODBC Visual FoxPro)
Il driver ODBC di Microsoft Visual FoxPro supporta:  
  
-   Set di caratteri a doppio byte (DBCS)  
  
-   Più sequenze di confronto  
  
 Una sequenza di confronto definisce il *tipo di ordinamento* per i dati archiviati in una tabella o un database Visual FoxPro. Per impostazione predefinita, il driver è configurato per l'utilizzo delle sequenze di confronto che supportano la versione della lingua del sistema operativo.  
  
 Per un elenco delle sequenze di confronto supportate, vedere [SET COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
## <a name="locale"></a>locale  
 Set di informazioni che corrisponde a una lingua e a un paese specificati. Le impostazioni locali indicano impostazioni specifiche, ad esempio separatori decimali, formati di data e ora e ordinamento caratteri.  
  
## <a name="sort-order"></a>ordinamento  
 Gli ordinamenti incorporano le regole di ordinamento delle diverse *impostazioni locali*, consentendo di ordinare correttamente i dati in tali lingue. In Visual FoxPro, l'ordinamento corrente determina i risultati dei confronti delle espressioni di caratteri e l'ordine in cui i record vengono visualizzati nelle tabelle indicizzate o ordinate.
