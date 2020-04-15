---
title: Supporto per i tipi di dati Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3abfe85ee32fb9ff4a8499c9949c0685563fec70
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284428"
---
# <a name="data-type-support"></a>Supporto dei tipi di dati
I driver ODBC devono supportare almeno una delle SQL_CHAR e dei SQL_VARCHAR. Il supporto per altri tipi di dati è determinato dal livello di conformità SQL-92 del driver o dell'origine dati. Un'applicazione deve chiamare **SQLGetTypeInfo** per determinare i tipi di dati supportati dal driver.  
  
 Per ulteriori informazioni sui tipi di dati, vedere [Appendice D: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).
