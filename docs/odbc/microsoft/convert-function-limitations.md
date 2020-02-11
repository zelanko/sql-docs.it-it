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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65cc8fa7517d3093b7314cacdafd8f607d89bc3a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081991"
---
# <a name="convert-function-limitations"></a>Limitazioni della funzione CONVERT
Gli errori di conversione dei tipi comportano l'impostazione della colonna interessata su NULL.  
  
 Né il tipo di dati DATE né TIMESTAMP possono essere convertiti in un altro tipo di dati (o in sé) tramite la funzione CONVERT.
