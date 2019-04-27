---
title: SQLColumns (Access Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColumns function [ODBC], Access Driver
- Access driver [ODBC], SQLColumns
ms.assetid: 1eac255c-6110-4805-a1bc-feee1eec35d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0e0977aebfe16b9274df8e93260eb98a24742cf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62666108"
---
# <a name="sqlcolumns-access-driver"></a>SQLColumns (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni di accesso specifici del Driver. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|colonna|Commenti|  
|------------|--------------|  
|TABLE_QUALIFIER|Viene restituito il percorso di un file di database.|  
|TABLE_OWNER|Poiché il nome del proprietario non è supportato in questa colonna viene restituito NULL.|  
|NULLABLE|SQL_NO_NULLS viene restituito per le colonne che fanno parte di una chiave primaria o un indice univoco.|
