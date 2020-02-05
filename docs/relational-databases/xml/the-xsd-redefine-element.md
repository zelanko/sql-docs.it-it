---
title: Elemento &lt;xsd:redefine&gt; | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f32e6952634e5bd4d376ac06d6c3f067fb75a0c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "72907555"
---
# <a name="the-ltxsdredefinegt-element"></a>Elemento &lt;xsd:redefine&gt;
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  L'elemento **redefine** dello schema XSD W3C rende disponibile il supporto per la ridefinizione dei componenti di schema. Il supporto per tale direttiva, tuttavia, può influire negativamente sulle prestazioni e richiede che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegua nuovamente la convalida di tutte le istanze del tipo di dati **xml** associate allo schema ridefinito. Di conseguenza, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta questo elemento. XML Schema che includono l'elemento **\<xsd:redefine>** verranno rifiutati dal server.  
  
 In alternativa, per aggiornare uno schema o i relativi componenti, è possibile eseguire le operazioni seguenti.  
  
1.  Creare una nuova raccolta XML Schema con i componenti di schema modificati.  
  
2.  Riscrivere tutti i tipi di dati **xml** (XML DT) che usano la raccolta XML Schema da ridefinire per usare in sostituzione la nuova raccolta XML Schema. A questo scopo, utilizzare l'opzione ALTER COLUMN del comando ALTER TABLE per riscrivere colonne o modificare i vincoli della raccolta XML Schema su variabili o parametri.  
  
3.  Eliminare la versione obsoleta della raccolta XML Schema.  

## <a name="see-also"></a>Vedere anche  
 [Requisiti e limitazioni per le raccolte di XML Schema nel server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
