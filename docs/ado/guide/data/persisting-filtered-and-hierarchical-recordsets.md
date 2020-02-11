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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 11ab68775e19ec1d3ce3c888917588f41ad65287
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924632"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>Persistenza di recordset filtrati e gerarchici
Se la proprietà [Filter](../../../ado/reference/ado-api/filter-property.md) è attiva per il **Recordset**, verranno salvate solo le righe accessibili nel filtro. Se il **Recordset** è gerarchico, vengono salvati il **Recordset** figlio corrente e i relativi elementi figlio, incluso il **Recordset**padre. Se viene chiamato il metodo **Save** di un **Recordset** figlio, l'elemento figlio e tutti i relativi elementi figlio vengono salvati, ma l'elemento padre non lo è. Per ulteriori informazioni sui **Recordset**gerarchici, vedere [data shaping](../../../ado/guide/data/data-shaping.md).  
  
> [!NOTE]
>  Alcune limitazioni si applicano quando si salvano **Recordset** gerarchici (forme dati) in formato XML. Per ulteriori informazioni, vedere la pagina relativa [alla permanenza dei record in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).
