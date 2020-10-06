---
description: Provider di servizi e componenti
title: Provider di servizi e componenti | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
author: rothja
ms.author: jroth
ms.openlocfilehash: 0f0c89d8a7f83bebfa77fb02a282fc21cb6f2dd0
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724942"
---
# <a name="service-providers-and-components"></a>Provider di servizi e componenti
I provider di servizi sono componenti che estendono le funzionalità dei provider di dati implementando interfacce estese che non sono supportate in modo nativo dall'archivio dati.  
  
 Universal Data Access fornisce un' *architettura di componenti* che consente a singoli componenti specializzati di implementare set discreti di funzionalità di database o "servizi" oltre a negozi meno idonei. Quindi, anziché forzare ogni archivio dati a fornire la propria implementazione di funzionalità estese o forzare le applicazioni generiche a implementare internamente la funzionalità del database, i componenti del servizio forniscono un'implementazione comune che qualsiasi applicazione può utilizzare per l'accesso a qualsiasi archivio dati. Il fatto che alcune funzionalità siano implementate in modo nativo dall'archivio dati e alcune tramite componenti generici sono trasparenti per l'applicazione.  
  
 Ad esempio, un motore di cursore, ad esempio [il servizio cursore per OLE DB](/previous-versions/windows/desktop/ms714397(v=vs.85)), è un componente del servizio che può utilizzare i dati di un archivio dati sequenziale e di tipo solo per produrre dati scorrevoli. Altri provider di servizi usati comunemente da ADO includono il provider di [persistenza di microsoft OLE DB (provider di servizi ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) (per salvare i dati in un file), il [servizio Data Shaping Microsoft per OLE DB (provider di servizi ADO) per](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) i **Recordset**gerarchici e il [provider Microsoft OLE DB Remoting (provider di servizi ADO)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) per richiamare i provider di dati in un computer remoto.  
  
 Per ulteriori informazioni sul servizio e sui provider di dati, vedere [Appendice A: Providers](../../../ado/guide/appendixes/appendix-a-providers.md).