---
title: SQLExtendedFetch (driver ODBC di Visual FoxPro) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ecff538198a2b517f980cc63acfc97d29a9f162
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298651"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento sono contenute informazioni specifiche del driver ODBC di Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Completo  
  
 Conformità API ODBC: livello 2ODBC API Conformance: Level 2  
  
 Simile a [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) ma restituisce più righe utilizzando una matrice per ogni colonna. Il set di risultati è scorrevole in avanti e può essere reso scorrevole all'indietro se il cursore è definito come statico, non forward-only.  
  
 Per impostazione predefinita, il driver ODBC di Visual FoxPro non restituisce le righe contrassegnate come eliminate in una tabella FoxPro. Le righe contrassegnate per l'eliminazione ma non ancora rimosse da una tabella non sono incluse nel cursore del set di risultati. È possibile modificare questo comportamento utilizzando il comando [SET DELETED.](../../odbc/microsoft/set-deleted-command.md)  
  
 Per ulteriori informazioni, vedere [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) in *ODBC Programmer's Reference*.
