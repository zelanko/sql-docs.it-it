---
title: Rimuovere i tipi definiti dall'utente&#39;s denominata in base al tipo di dati riservato ORDPATH | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 474e910a-6abb-4e28-acc2-055338c011d4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3ee155c70a8b10d4437d6b2f374c8b9497bf3faa
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092914"
---
# <a name="remove-udt39s-named-after-the-reserved-ordpath-data-type"></a>Rimuovere i tipi definiti dall'utente&#39;s denominata in base al tipo di dati ORDPATH riservato
  Tramite Preparazione aggiornamento è stato rilevato un tipo definito dall'utente denominato in base a un termine riservato per i tipi di dati `ORDPATH`.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 I termini utilizzati per i tipi di dati predefiniti non devono essere utilizzati come nomi per Common Language Runtime (CLR) o per tipi di dati definiti dall'utente alias.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Rimuovere il tipo definito dall'utente denominato in base al tipo di dati e ricreare il tipo con un nome non riservato.  
  
## <a name="external-resources"></a>Risorse esterne  
 [Creazione di un tipo definito dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
