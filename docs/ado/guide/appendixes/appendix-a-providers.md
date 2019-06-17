---
title: 'Appendice A: I provider | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- providers [ADO]
- ADO, providers
- service providers [ADO]
- service components [ADO]
ms.assetid: e2581b47-b11e-4e1e-b96c-d39c77c5b48a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3f31e5522fdac506e31ffe0bbaa5ad76e3fae87b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701552"
---
# <a name="appendix-a-data-and-service-providers"></a>Appendice A: Provider di servizi e dati
Questa sezione vengono illustrati tre tipi di provider: provider di dati, i provider di servizi e componenti del servizio. I provider possono essere suddivise in due categorie: quelli che forniscono i dati e quelli che forniscono servizi. Oggetto *provider di dati* possiede i propri dati e la espone in formato tabulare per l'applicazione. Oggetto *provider di servizi* incapsula un servizio tramite producono e usano i dati, in modo da integrare le funzionalità nelle applicazioni ADO. Un provider di servizi può inoltre essere definito un *componente servizio*, che è necessario collaborare con altri provider di servizi o componenti.

## <a name="data-providers"></a>Provider di dati
 ADO è potente e flessibile perché può connettersi a una qualsiasi di diversi provider di dati diversi e ancora esporre il modello di programmazione stesso, indipendentemente dalle funzionalità specifiche di qualsiasi altro provider specificato.

 Tuttavia, poiché ogni provider di dati è univoco, come l'applicazione interagisce con ADO variano leggermente dal provider di dati. Le differenze in genere rientrano in una delle tre categorie:

-   Parametri di connessione nel [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) proprietà.

-   [Comando](../../../ado/reference/ado-api/command-object-ado.md) sull'utilizzo dell'oggetto.

-   Specifica del provider [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) comportamento.

 Come indicato di seguito sono elencati i dettagli per ogni provider di dati attualmente disponibili da Microsoft.

|Area|Argomento|
|----------|-----------|
|Database ODBC|[Provider Microsoft OLE DB per ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)|
|Servizio di indicizzazione Microsoft|[Provider Microsoft OLE DB per Microsoft Indexing Service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Servizio Active Directory|[Provider Microsoft OLE DB per il servizio Microsoft Active Directory](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Database Microsoft Jet|[Provider OLE DB per Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Provider Microsoft OLE DB per SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)|
|database Oracle|[Provider Microsoft OLE DB per Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)|
|Pubblicazione su Internet|[Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)|
|Origini dati semplice|[Provider Microsoft OLE DB semplice](../../../ado/guide/appendixes/microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>Proprietà dinamiche specifiche del provider
 Il [le proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolte del [connessione](../../../ado/reference/ado-api/connection-object-ado.md), [comando](../../../ado/reference/ado-api/command-object-ado.md), e [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) gli oggetti includono le proprietà dinamiche specifiche per il provider. Queste proprietà forniscono informazioni sulle funzionalità specifiche per il provider rispetto alle proprietà predefinite che supporta ADO.

 Dopo aver stabilito la connessione e la creazione di questi oggetti, usare il [aggiornare](../../../ado/reference/ado-api/refresh-method-ado.md) metodo sul **proprietà** insieme dell'oggetto per ottenere le proprietà specifiche del provider. Consultare la documentazione del provider e il [Guida per programmatori OLE DB](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) per informazioni dettagliate su queste proprietà dinamiche.

## <a name="service-providers"></a>Provider di servizi
 Per usare un provider di servizi, è necessario specificare una parola chiave. È anche necessario conoscere le proprietà dinamiche specifiche del provider associate a ogni provider di servizi. Dettagli specifici del provider elencati per ogni provider di servizi che è attualmente disponibile da Microsoft:

-   [Servizio Microsoft di modifica della forma dei dati per OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Provider Microsoft OLE DB Persistence](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Provider Microsoft OLE DB remota](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>Componenti del servizio
 Il [Cursor Service per OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) componente servizio integra le funzioni di supporto del cursore del provider di dati. Inoltre, richiede una parola chiave e dispone di proprietà dinamiche.

 Per altre informazioni sui provider OLE DB, vedere [OLE DB per Microsoft](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx).

## <a name="provider-commands"></a>Comandi del provider
 Per ogni provider elencati in questo caso, se le applicazioni consentono agli utenti di immettere istruzioni SQL come comandi del provider, è necessario sempre convalidare l'input dell'utente e prestare attenzione ai tentativi possibili pirata informatico utilizzando istruzioni SQL potenzialmente pericolose, ad esempio `DROP TABLE t1`, come parte dell'input dell'utente.

## <a name="see-also"></a>Vedere anche
 [Oggetto (ADO) Command](../../../ado/reference/ado-api/command-object-ado.md) [oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) [Provider Microsoft OLE DB per il servizio Microsoft Active Directory ](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [Provider Microsoft OLE DB per Microsoft Indexing Service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md) [Provider Microsoft OLE DB per ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md) [Provider Microsoft OLE DB per Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) [Provider Microsoft OLE DB per SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) [Provider Microsoft OLE DB per Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) [raccolta di proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [ Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [metodo Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
