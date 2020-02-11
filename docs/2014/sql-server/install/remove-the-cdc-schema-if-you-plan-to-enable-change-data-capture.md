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
manager: craigg
ms.openlocfilehash: cc580a6032a19eb8248759669278f8730fc617cb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66092944"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>Rimuovere lo schema cdc se si intende attivare Change Data Capture
  Un database contiene già uno schema cdc. Se si prevede di abilitare Change Data Capture dopo l'aggiornamento, è necessario innanzitutto eliminare questo schema cdc. Quando si attiva un database per Change Data Capture, il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] creerà un nuovo schema denominato cdc.  
  
  
