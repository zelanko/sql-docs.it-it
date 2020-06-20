---
title: Rimuovere lo schema CDC se si intende abilitare Change Data Capture | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- cdc schema
- change data capture
ms.assetid: 6a84aa25-0f31-4be3-b2dd-4f249b8254ae
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: abdb33fa3d1ff022a65ed569f19d48bcf4468501
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059147"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>Rimuovere lo schema cdc se si intende attivare Change Data Capture
  Un database contiene già uno schema cdc. Se si prevede di abilitare Change Data Capture dopo l'aggiornamento, è necessario innanzitutto eliminare questo schema cdc. Quando si attiva un database per Change Data Capture, il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] creerà un nuovo schema denominato cdc.  
  
  
