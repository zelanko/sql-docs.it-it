---
title: Persistenza di recordset filtrati e gerarchici | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- filtered Recordset persistence [ADO]
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: d01aeb4d-4e43-450b-b3f2-0c27eaaf9f86
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 11ab68775e19ec1d3ce3c888917588f41ad65287
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924632"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>Persistenza di recordset filtrati e gerarchici
Se il [filtro](../../../ado/reference/ado-api/filter-property.md) proprietà è valida per il **Recordset**, vengono salvate solo le righe accessibili in base al filtro. Se il **Recordset** è di tipo gerarchico, il membro figlio corrente **Recordset** e i relativi elementi figlio viene salvati, incluso l'elemento padre **Recordset**. Se il **salvare** metodo di un elemento figlio **Recordset** viene chiamato, l'elemento figlio e i relativi elementi figlio viene salvati, ma non è l'elemento padre. Per altre informazioni sulle gerarchica **recordset**, vedere [Data Shaping](../../../ado/guide/data/data-shaping.md).  
  
> [!NOTE]
>  Si applicano alcune limitazioni quando si salva gerarchica **recordset** (forme di dati) in formato XML. Per altre informazioni, vedere [record di persistenza in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).
