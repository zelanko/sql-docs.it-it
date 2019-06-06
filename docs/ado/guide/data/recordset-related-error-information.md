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
manager: jroth
ms.openlocfilehash: ef5f6cc4a262cecc81a8dd72f2d3e3f6a7e2fded
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700416"
---
# <a name="recordset-related-error-information"></a>Informazioni sugli errori correlati ai recordset
Durante l'elaborazione batch, il **lo stato** proprietà delle **Recordset** oggetto fornisce informazioni relative ai singoli record nel **Recordset**. Prima di un aggiornamento batch viene eseguita, il **lo stato** proprietà delle **Recordset** riflette informazioni sui record a essere aggiunte, modificate ed eliminate. Dopo aver **UpdateBatch** è stato chiamato, il **stato** proprietà indica l'esito positivo o negativo dell'operazione. Durante lo spostamento tra i vari record nel **Recordset**, il valore della **stato** le modifiche alle proprietà per descrivere lo stato del record corrente.
