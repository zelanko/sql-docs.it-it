---
title: 'Appendice A: Providers | Microsoft Docs'
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
ms.openlocfilehash: 4ffecfc87ec23fc4d62174dae31220511c9f72d4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926975"
---
# <a name="appendix-a-data-and-service-providers"></a>Appendice A: provider di dati e servizi
Questa sezione illustra tre tipi di provider: provider di dati, provider di servizi e componenti del servizio. I provider rientrano in due categorie, ovvero quelle che forniscono i dati e i servizi. Un *provider di dati* possiede i propri dati e li espone in forma tabulare all'applicazione. Un *provider di servizi* incapsula un servizio tramite la produzione e l'utilizzo di dati, aumentando le funzionalità nelle applicazioni ADO. Un provider di servizi può anche essere definito ulteriormente come *componente del servizio*, che deve interagire con altri provider di servizi o componenti.

## <a name="data-providers"></a>Provider di dati
 ADO è potente e flessibile perché può connettersi a uno dei diversi provider di dati e comunque esporre lo stesso modello di programmazione, indipendentemente dalle funzionalità specifiche di un determinato provider.

 Tuttavia, poiché ogni provider di dati è univoco, il modo in cui l'applicazione interagisce con ADO può variare leggermente in base al provider di dati. Le differenze in genere rientrano in una delle tre categorie seguenti:

-   Parametri di connessione nella proprietà [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) .

-   Utilizzo oggetto [comando](../../../ado/reference/ado-api/command-object-ado.md) .

-   Comportamento del [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) specifico del provider.

 I dettagli per ogni provider di dati attualmente disponibile in Microsoft sono elencati di seguito.

|Area|Argomento|
|----------|-----------|
|Database ODBC|[Provider Microsoft OLE DB per ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)|
|Servizio Microsoft Indexing|[Provider OLE DB per il Servizio di indicizzazione Microsoft](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Servizio Active Directory|[Provider Microsoft OLE DB per Microsoft Active Directory Service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Database Microsoft Jet|[Provider di OLE DB per Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Provider Microsoft OLE DB per SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)|
|database Oracle|[Provider Microsoft OLE DB per Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)|
|Pubblicazione su Internet|[Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)|
|Origini dati semplici|[Provider semplice Microsoft OLE DB](../../../ado/guide/appendixes/microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>Proprietà dinamiche specifiche del provider
 Le raccolte [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) degli oggetti [Connection](../../../ado/reference/ado-api/connection-object-ado.md), [Command](../../../ado/reference/ado-api/command-object-ado.md)e [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) includono proprietà dinamiche specifiche del provider. Queste proprietà forniscono informazioni sulle funzionalità specifiche del provider oltre alle proprietà predefinite supportate da ADO.

 Dopo aver stabilito la connessione e aver creato questi oggetti, utilizzare il metodo [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) sulla raccolta **Properties** dell'oggetto per ottenere le proprietà specifiche del provider. Per informazioni dettagliate su queste proprietà dinamiche, vedere la documentazione del provider e la [Guida per programmatori OLE DB](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) .

## <a name="service-providers"></a>Provider di servizi
 Per usare un provider di servizi, è necessario specificare una parola chiave. È inoltre necessario conoscere le proprietà dinamiche specifiche del provider associate a ogni provider di servizi. I dettagli specifici del provider sono elencati per ogni provider di servizi attualmente disponibile da Microsoft:

-   [Servizio Microsoft di modifica della forma dei dati per OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Provider di persistenza Microsoft OLE DB](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Provider Microsoft OLE DB Remoting](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>Componenti del servizio
 Il [servizio cursore per OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) componente del servizio integra le funzioni di supporto del cursore dei provider di dati. Richiede anche una parola chiave e dispone di proprietà dinamiche.

 Per ulteriori informazioni sui provider di OLE DB, vedere [Microsoft OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx).

## <a name="provider-commands"></a>Comandi del provider
 Per ogni provider elencato qui, se le applicazioni consentono agli utenti di immettere istruzioni SQL come comandi del provider, è sempre necessario convalidare l'input dell'utente e vigilare su possibili attacchi di hacker usando istruzioni SQL potenzialmente `DROP TABLE t1`pericolose, ad esempio, come parte dell'input utente.

## <a name="see-also"></a>Vedere anche
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md) [Connection Object (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [provider Microsoft OLE DB per Internet pubblicazione](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) [del provider Microsoft OLE DB per Microsoft Active Directory Service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) provider [microsoft OLE DB per microsoft Indexing Service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md) provider [Microsoft OLE DB per ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md) [provider Microsoft OLE DB per Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) provider Microsoft OLE DB [per SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) provider [Microsoft OLE DB per Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) [Properties Collection (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [Recordset Metodo di aggiornamento Object (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [](../../../ado/reference/rds-api/refresh-method-rds.md)
