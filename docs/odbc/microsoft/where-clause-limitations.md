---
title: Limitazioni della clausola WHERE Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, WHERE clause limitations
- WHERE clause limitations [ODBC]
ms.assetid: 46b54f74-e4a3-4318-87cf-8a97c38a2718
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1699397db81d6fe702f60f6953fe7a0ae3726fe3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307562"
---
# <a name="where-clause-limitations"></a>Limitazioni della clausola WHERE
Il numero massimo di clausole in una clausola WHERE è 40.  
  
 Le colonne LONGVARBINARY e LONGVARCHAR possono essere confrontate con valori letterali di lunghezza massima di 255 caratteri, ma non possono essere confrontate utilizzando parametri.
