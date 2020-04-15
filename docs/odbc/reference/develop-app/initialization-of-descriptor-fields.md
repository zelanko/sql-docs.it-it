---
title: Inizializzazione dei campi del descrittore Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4ed6479a60f1d0695107c216b2f0c94a55f68ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300121"
---
# <a name="initialization-of-descriptor-fields"></a>Inizializzazione dei campi di descrizione
Quando viene allocato un descrittore di riga dell'applicazione, i relativi campi ricevono i valori iniziali come indicato in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Viene SQL_DEFAULT il valore iniziale del campo SQL_DESC_TYPE. Ciò prevede un trattamento standard dei dati del database per la presentazione all'applicazione. L'applicazione può specificare un trattamento diverso dei dati impostando i campi del record del descrittore.  
  
 Il valore iniziale di SQL_DESC_ARRAY_SIZE nell'intestazione del descrittore è 1.The initial value of can in the descriptor header is 1. L'applicazione può modificare questo campo per abilitare il recupero multiriga.  
  
 Il concetto di valore predefinito non è valido per i campi di un IRD. Un'applicazione può accedere ai campi di un IRD solo quando è associata un'istruzione preparata o eseguita.  
  
 Alcuni campi di un IPD vengono definiti solo dopo che l'IPD è stato popolato automaticamente dal driver. In caso contrario, non sono definiti. Questi campi sono SQL_DESC_CASE_SENSITIVE, SQL_DESC_FIXED_PREC_SCALE, SQL_DESC_TYPE_NAME, SQL_DESC_UNSIGNED e SQL_DESC_LOCAL_TYPE_NAME.
