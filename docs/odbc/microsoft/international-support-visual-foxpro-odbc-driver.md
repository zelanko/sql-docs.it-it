---
title: Supporto internazionale (Driver ODBC di Visual FoxPro) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4b0c758bb478ea6a468e6756c3d6f0f52c766f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299971"
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>Supporto multilingue (driver ODBC Visual FoxPro)
Il driver ODBC di Microsoft Visual FoxPro supporta:  
  
-   Set di caratteri a byte doppio (DBCS)  
  
-   Sequenze di confronto multiple  
  
 Una sequenza di confronto definisce *l'ordinamento* per i dati archiviati in una tabella o database di Visual FoxPro. Per impostazione predefinita, il driver è configurato per utilizzare le sequenze di confronto che supportano la versione in lingua del sistema operativo.  
  
 Per un elenco delle sequenze di confronto supportate, vedere [SET COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
## <a name="locale"></a>locale  
 Insieme di informazioni che corrisponde a una determinata lingua e paese.The set of information that corresponds to a given language and country/region. Le impostazioni locali indicano impostazioni specifiche, ad esempio separatori decimali, formati di data e ora e ordinamento dei caratteri.  
  
## <a name="sort-order"></a>ordinamento  
 Gli ordinamenti incorporano le regole di ordinamento delle *diverse impostazioni locali,* consentendo di ordinare correttamente i dati in tali lingue. In Visual FoxPro, l'ordinamento corrente determina i risultati dei confronti delle espressioni di caratteri e l'ordine in cui i record vengono visualizzati nelle tabelle indicizzate o ordinate.
