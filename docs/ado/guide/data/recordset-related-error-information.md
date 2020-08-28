---
description: Informazioni sugli errori correlati ai recordset
title: Informazioni sugli errori correlati a recordset | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
author: rothja
ms.author: jroth
ms.openlocfilehash: 454c62b969ee69e6186792ce77873c8c8fbb5704
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979812"
---
# <a name="recordset-related-error-information"></a>Informazioni sugli errori correlati ai recordset
Durante l'elaborazione batch, la proprietà **status** dell'oggetto **Recordset** fornisce informazioni sui singoli record nel **Recordset**. Prima di eseguire un aggiornamento batch, la proprietà **status** del **Recordset** riflette le informazioni sui record da aggiungere, modificare ed eliminare. Dopo la chiamata di **UpdateBatch** , la proprietà **status** indica l'esito positivo o negativo dell'operazione. Quando si passa da record a record nel **Recordset**, il valore della proprietà **status** viene modificato per descrivere lo stato del record corrente.
