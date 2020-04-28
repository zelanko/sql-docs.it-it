---
title: Converti limitazioni funzione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, CONVERT function limitations
- Convert function limitations [ODBC]
ms.assetid: 3c81fc58-57f0-4dd7-be16-2b146eb15cbc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63f4258e737327ae11f03a96cfef3cdecf133e53
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281031"
---
# <a name="convert-function-limitations"></a>Limitazioni della funzione CONVERT
Gli errori di conversione dei tipi comportano l'impostazione della colonna interessata su NULL.  
  
 Né il tipo di dati DATE né TIMESTAMP possono essere convertiti in un altro tipo di dati (o in sé) tramite la funzione CONVERT.
