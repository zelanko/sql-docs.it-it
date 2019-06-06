---
title: Modifica di record esistenti | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6bd1e02bf406906cc8a893ccee66a408b38510f3
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702070"
---
# <a name="editing-existing-records"></a>Modifica di record esistenti
Per modificare i record esistenti, spostarsi sulla riga in cui si desidera modificare e cambiare il **valore** proprietà dei campi che si desidera modificare. Per altre informazioni sul **campo** dell'oggetto **valore** proprietà, vedere [analisi dei dati](../../../ado/guide/data/examining-data.md). A seconda del tipo di cursore, si userà **Update** oppure **UpdateBatch** per inviare le modifiche all'origine dati. Per altre informazioni, vedere [aggiornamento e salvataggio permanente dei dati](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 È in genere preferibile usare una stored procedure con un oggetto command per eseguire aggiornamenti, nonché altre operazioni, perché una stored procedure non richiede la creazione di un cursore. Per altre informazioni sui cursori, vedere [informazioni su cursori e blocchi](../../../ado/guide/data/understanding-cursors-and-locks.md).
