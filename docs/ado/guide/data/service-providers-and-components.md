---
title: Provider di servizi e componenti | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9bebbf4c89a04474cbf2d0c88704603cb4c3fef3
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700385"
---
# <a name="service-providers-and-components"></a>Provider di servizi e componenti
I provider di servizi sono componenti che estendono la funzionalità del provider di dati mediante l'implementazione di interfacce estese che non sono supportate in modo nativo dall'archivio dati.  
  
 Fornisce l'accesso ai dati universale una *architettura dei componenti* che consente ai componenti singoli, specializzati implementare un set discreto di funzionalità del database o i "servizi" in archivi meno avanzati. Quindi, anziché forzare ogni archivio dati per fornire la propria implementazione di estendere le funzionalità o imporre applicazioni generiche per implementare la funzionalità database internamente, i componenti del servizio di fornire un'implementazione comune che può essere di qualsiasi applicazione Utilizzare l'accesso a qualsiasi archivio dati. Il fatto che alcune funzionalità viene implementata in modo nativo dall'archivio dati e alcune attraverso componenti generici è trasparente per l'applicazione.  
  
 Ad esempio, un cursore del motore, ad esempio [The Cursor Service per OLE DB](https://msdn.microsoft.com/57638feb-4ecd-4051-becb-8f828d21cf44), è un componente del servizio che può usare dati da un archivio dati sequenziali e forward-only per generare i dati scorrevoli. Altri provider di servizi usati comunemente dagli ADO includono la [Provider Microsoft OLE DB Persistence (ADO Service Provider)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) (per il salvataggio dei dati in un file), il [Microsoft Data shaping per OLE DB (ADO Service Provider) ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (per gerarchici **recordset**) e il [Provider Microsoft OLE DB remota (ADO Service Provider)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) (per il richiamo di provider di dati in un computer remoto).  
  
 Per altre informazioni sui provider di servizi e dati, vedere [appendice a: Providers](../../../ado/guide/appendixes/appendix-a-providers.md).
