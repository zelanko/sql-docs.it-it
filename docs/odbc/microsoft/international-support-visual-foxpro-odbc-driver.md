---
title: Supporto internazionale (Driver ODBC Visual FoxPro) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 50d65520e74a4e11bada88795fedc0b2f2e82628
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62471044"
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>Supporto multilingue (driver ODBC Visual FoxPro)
Il Driver ODBC Microsoft Visual FoxPro supporta:  
  
-   Double-byte character set (DBCS)  
  
-   Più sequenze di collazione  
  
 Definisce una sequenza di confronto di *ordinamento* per i dati archiviati nel database o tabella di Visual FoxPro. Per impostazione predefinita, il driver è configurato per usare le sequenze di collazione che supportano la lingua del sistema operativo.  
  
 Per un elenco di sequenze di collazione supportati, vedere [SET COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
## <a name="locale"></a>impostazioni locali  
 Il set di informazioni che corrisponde a una determinata lingua e paese/area geografica. Le impostazioni locali indica le impostazioni specifiche, ad esempio separatori decimali, date e formati di ora e ordinamento dei caratteri.  
  
## <a name="sort-order"></a>ordinamento  
 Gli ordinamenti incorporano le regole di ordinamento di diverse *delle impostazioni locali*s, consentendo di ordinare correttamente i dati in tali lingue. In Visual FoxPro, l'ordinamento corrente determina i risultati dei confronti di espressione di caratteri e l'ordine in cui i record visualizzati in indicizzate o tabelle di ordinamento.
