---
title: Informazioni sugli errori correlati a recordset | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d3f8e8d9802b5d0c73af73aff20d929c188b9292
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924377"
---
# <a name="recordset-related-error-information"></a>Informazioni sugli errori correlati ai recordset
Durante l'elaborazione batch, la proprietà **status** dell'oggetto **Recordset** fornisce informazioni sui singoli record nel **Recordset**. Prima di eseguire un aggiornamento batch, la proprietà **status** del **Recordset** riflette le informazioni sui record da aggiungere, modificare ed eliminare. Dopo la chiamata di **UpdateBatch** , la proprietà **status** indica l'esito positivo o negativo dell'operazione. Quando si passa da record a record nel **Recordset**, il valore della proprietà **status** viene modificato per descrivere lo stato del record corrente.
