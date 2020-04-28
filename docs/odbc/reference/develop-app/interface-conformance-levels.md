---
title: Livelli di conformità dell'interfaccia | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fff555324746fcb92641126ddf11ea91ce5e3f89
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304601"
---
# <a name="interface-conformance-levels"></a>Livelli di conformità di interfaccia
Lo scopo del livellamento è informare l'applicazione quali funzionalità sono disponibili dal driver. Uno schema di livellamento basato sulle funzioni non è sufficiente a raggiungere questo obiettivo. In ODBC 3. *x*, i driver vengono classificati in base alle funzionalità che possiedono. Il supporto della funzionalità può includere il supporto della funzione; può inoltre includere il supporto di un campo del descrittore, un attributo di istruzione, un valore "Y" per un tipo di informazioni restituito da **SQLGetInfo**e così via.  
  
 Per semplificare la specifica della conformità dell'interfaccia, ODBC definisce tre livelli di conformità. Per soddisfare un particolare livello di conformità, è necessario che un driver soddisfi tutti i requisiti del livello di conformità. La conformità a un determinato livello implica una conformità completa a tutti i livelli inferiori.  
  
 I livelli di conformità non sono sempre suddivisi in modo accurato in supporto per un elenco specifico di funzioni ODBC, ma specificano le funzionalità supportate elencate nelle sezioni riportate di seguito. Per fornire supporto per una funzionalità, un driver deve supportare alcune o tutte le forme di chiamate a determinate funzioni ODBC (per altre informazioni, vedere conformità della [funzione](../../../odbc/reference/develop-app/function-conformance.md)), impostazione di determinati attributi (vedere [conformità degli attributi](../../../odbc/reference/develop-app/attribute-conformance.md)) e alcuni campi di descrizione (vedere [conformità del campo del descrittore](../../../odbc/reference/develop-app/descriptor-field-conformance.md)).  
  
 L'applicazione individua il livello di conformità dell'interfaccia di un driver connettendosi a un'origine dati e chiamando **SQLGetInfo** con l'opzione SQL_ODBC_INTERFACE_CONFORMANCE.  
  
 I driver sono liberi di implementare funzionalità oltre il livello a cui rivendicano la conformità completa. Le applicazioni individuano le funzionalità aggiuntive chiamando **SQLGetFunctions** (per determinare quali funzioni ODBC sono presenti) e **SQLGetInfo** (per eseguire query su diverse altre funzionalità ODBC).  
  
 Sono disponibili tre livelli di conformità dell'interfaccia ODBC: Core, Level 1 e Level 2.  
  
> [!NOTE]
>  Questi livelli di conformità hanno requisiti diversi rispetto ai livelli di conformità dell'API ODBC con lo stesso nome in ODBC 2 *. x*. In particolare, tutte le funzionalità implicite dal livello di conformità dell'API ODBC 2 *. x* sono ora parte del livello di conformità dell'interfaccia di base. Di conseguenza, molti driver ODBC possono segnalare la conformità di interfaccia di livello principale.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Conformità di interfaccia Core](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [Conformità di interfaccia di livello 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [Conformità di interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [Conformità della funzione](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [Conformità dell'attributo](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [Conformità del campo descrittore](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
