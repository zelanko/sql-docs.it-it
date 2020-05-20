---
title: Salvataggio permanente di recordset filtrati e gerarchici | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5fa3fdd55fb78f16629907c174b08aab64ceb86e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763112"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>Persistenza di recordset filtrati e gerarchici
Se la proprietà [Filter](../../../ado/reference/ado-api/filter-property.md) è attiva per il **Recordset**, verranno salvate solo le righe accessibili nel filtro. Se il **Recordset** è gerarchico, vengono salvati il **Recordset** figlio corrente e i relativi elementi figlio, incluso il **Recordset**padre. Se viene chiamato il metodo **Save** di un **Recordset** figlio, l'elemento figlio e tutti i relativi elementi figlio vengono salvati, ma l'elemento padre non lo è. Per ulteriori informazioni sui **Recordset**gerarchici, vedere [data shaping](../../../ado/guide/data/data-shaping.md).  
  
> [!NOTE]
>  Alcune limitazioni si applicano quando si salvano **Recordset** gerarchici (forme dati) in formato XML. Per ulteriori informazioni, vedere la pagina relativa [alla permanenza dei record in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).
