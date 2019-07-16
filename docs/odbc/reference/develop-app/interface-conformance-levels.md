---
title: Livelli di conformità di interfaccia | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 2c470e54-0600-4b2b-b1f3-9885cb28a01a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 185e68ed8d083e3ccfbab99369f6a778766a4c09
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138907"
---
# <a name="interface-conformance-levels"></a>Livelli di conformità di interfaccia
Lo scopo di livellamento è informare l'applicazione di quali funzionalità sono disponibili a esso dal driver. Uno schema di livellamento basato sulle funzioni non sufficientemente raggiungere tale obiettivo. In ODBC 3. *x*, i driver sono classificati in base alle funzionalità di cui dispongono. La funzionalità di supporto può includere che supportano la funzione. può inoltre includere il supporto di un campo di descrizione, un attributo di istruzione, un valore "Y" per un tipo di informazioni restituito da **SQLGetInfo**e così via.  
  
 Per semplificare la specifica di conformità di interfaccia, ODBC definisce tre livelli di conformità. Per soddisfare un livello di conformità specifico, un driver deve soddisfare tutti i requisiti di tale livello di conformità. Conformità con un determinato livello implica la conformità completa con tutti i livelli inferiori.  
  
 Livelli di conformità non sempre dividere accuratamente il supporto per un elenco specifico di funzioni ODBC, ma specificare le funzionalità supportate, come indicato nelle sezioni seguenti. Per fornire supporto per una funzionalità, un driver deve supportare alcune o tutte le forme di chiamate ad alcune funzioni ODBC (per altre informazioni, vedere [conformità della funzione](../../../odbc/reference/develop-app/function-conformance.md)), l'impostazione di determinati attributi (vedere [conformità dell'attributo ](../../../odbc/reference/develop-app/attribute-conformance.md)) e alcuni campi di descrizione (vedere [conformità del campo descrittore](../../../odbc/reference/develop-app/descriptor-field-conformance.md)).  
  
 L'applicazione individua i livello di conformità di interfaccia del driver per la connessione a un'origine dati e la chiamata **SQLGetInfo** con l'opzione SQL_ODBC_INTERFACE_CONFORMANCE.  
  
 I driver sono liberi di implementare le funzionalità oltre il livello a cui che sostengono la conformità completa. Applicazioni di individuare eventuali funzionalità aggiuntive chiamando **SQLGetFunctions** (per stabilire quali funzioni ODBC sono presenti) e **SQLGetInfo** (eseguire una query diverse altre funzionalità ODBC).  
  
 Esistono tre livelli di conformità di interfaccia ODBC: Core, livello 1 e Level 2.  
  
> [!NOTE]
>  Questi livelli di conformità hanno requisiti diversi rispetto i livelli di conformità API ODBC lo stesso nome in ODBC 2*x*. In particolare, tutte le funzionalità di cui è inclusa l'API ODBC 2*x* conformità API livello 1 fanno ora parte di livello la conformità di interfaccia di Core. Di conseguenza, molti driver ODBC può segnalare la conformità di interfaccia a livello di base.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Conformità di interfaccia Core](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [Conformità di interfaccia di livello 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [Conformità di interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [Conformità della funzione](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [Conformità dell'attributo](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [Conformità del campo descrittore](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
