---
title: Informazioni sugli errori associati ai recordset | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924377"
---
# <a name="recordset-related-error-information"></a>Informazioni sugli errori correlati ai recordset
Durante l'elaborazione batch, il **lo stato** proprietà delle **Recordset** oggetto fornisce informazioni relative ai singoli record nel **Recordset**. Prima di un aggiornamento batch viene eseguita, il **lo stato** proprietà delle **Recordset** riflette informazioni sui record a essere aggiunte, modificate ed eliminate. Dopo aver **UpdateBatch** è stato chiamato, il **stato** proprietà indica l'esito positivo o negativo dell'operazione. Durante lo spostamento tra i vari record nel **Recordset**, il valore della **stato** le modifiche alle proprietà per descrivere lo stato del record corrente.
