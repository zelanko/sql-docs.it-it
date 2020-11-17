---
title: FOR XML (SQL Server)
description: Informazioni sulla clausola FOR XML usata nelle query SQL per recuperare i risultati sotto forma di codice XML.
ms.prod: sql
ms.prod_service: database-engine
ms.technology: xml
ms.topic: conceptual
f1_keywords:
- FOR_XML_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FOR XML clause, about FOR XML clause
- PATH FOR XML mode, construction
- EXPLICIT FOR XML mode
- RAW FOR XML mode
- retrieving XML data
- XML [SQL Server], FOR XML clause
- AUTO FOR XML mode
- XML [SQL Server], construction
ms.assetid: 2b6b5c61-c5bd-49d2-8c0c-b7cf15857906
author: RothJa
ms.author: jroth
ms.reviewer: ''
ms.custom: fresh2019may
ms.date: 04/03/2020
ms.openlocfilehash: 974da804e79a6c571b7543caec230984296f6a8e
ms.sourcegitcommit: 2bf83972036bdbe6a039fb2d1fc7b5f9ca9589d3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2020
ms.locfileid: "94674153"
---
# <a name="for-xml-sql-server"></a>FOR XML (SQL Server)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Una query SELECT restituisce i risultati sotto forma di set di righe. È possibile recuperare facoltativamente i risultati di una query SQL come codice XML specificando la clausola FOR XML nella query. È possibile usare la clausola FOR XML nelle query di livello principale e nelle sottoquery. La clausola FOR XML di livello principale può essere utilizzata solo nell'istruzione SELECT. Nelle sottoquery è possibile usare FOR XML nelle istruzioni INSERT, UPDATE e DELETE. È possibile usare FOR XML anche nelle istruzioni di assegnazione.

In una clausola FOR XML, è necessario specificare una delle modalità seguenti:

- RAW
- AUTO
- EXPLICIT
- PATH

Nella modalità RAW viene generato un singolo elemento \<row> per ogni riga del set di righe restituito dall'istruzione SELECT. È possibile generare la gerarchia XML tramite la formulazione di query FOR XML nidificate.

Nella modalità AUTO, il codice XML risultante è nidificato tramite l'approccio euristico determinato dalla modalità con cui viene specificata l'istruzione SELECT. Il controllo sulla forma del codice XML generato è minimo. È possibile formulare query FOR XML nidificate che generano una gerarchia XML che esula dalla forma XML generata dall'approccio euristico della modalità AUTO.

La modalità EXPLICIT consente un maggiore controllo sulla forma del codice XML, grazie alla possibilità di combinare gli attributi e gli elementi che definiscono tale forma. È richiesto un formato specifico per il set di righe generato in seguito all'esecuzione della query, del quale viene quindi eseguito il mapping alla forma del codice XML. La modalità EXPLICIT consente di combinare elementi e attributi, di creare wrapper e proprietà complesse nidificate, di creare valori separati da spazi (ad esempio, l'attributo OrderID può includere un elenco di ID di ordine) e contenuti misti.

La formulazione di query nella modalità EXPLICIT può tuttavia essere complessa. Per generare le gerarchie, anziché utilizzare la modalità EXPLICIT è possibile utilizzare le nuove funzionalità di FOR XML, ad esempio la formulazione di query FOR XML nidificate in modalità RAW/AUTO/PATH e la direttiva TYPE. Le query FOR XML nidificate consentono di generare qualsiasi codice XML generabile tramite la modalità EXPLICIT. Per altre informazioni, vedere [Utilizzo di query FOR XML nidificate](../../relational-databases/xml/use-nested-for-xml-queries.md) e [Direttiva TYPE nelle query FOR XML](../../relational-databases/xml/type-directive-in-for-xml-queries.md).

L'utilizzo congiunto della modalità PATH e delle funzionalità per le query FOR XML nidificate consente di ottenere lo stesso livello di versatilità della modalità EXPLICIT, ma in un modo più semplice.

Queste modalità sono valide solo per l'esecuzione della query per la quale sono state impostate e non influiscono sui risultati di eventuali query successive.

FOR XML non è valida per qualsiasi selezione utilizzata con una clausola FOR BROWSE.

## <a name="example"></a>Esempio

L'istruzione `SELECT` seguente recupera informazioni dalle tabelle `Sales.Customer` e `Sales.SalesOrderHeader` del database `AdventureWorks2012` . La query seguente specifica la modalità `AUTO` nella clausola `FOR XML` :

```sql
USE AdventureWorks2012
GO
SELECT Cust.CustomerID,
       OrderHeader.CustomerID,
       OrderHeader.SalesOrderID,
       OrderHeader.Status
FROM Sales.Customer Cust 
INNER JOIN Sales.SalesOrderHeader OrderHeader
ON Cust.CustomerID = OrderHeader.CustomerID
FOR XML AUTO;
```

## <a name="the-for-xml-clause-and-server-names"></a>Clausola FOR XML e nomi di server

Se un'istruzione SELECT con una clausola FOR XML specifica un nome in quattro parti nella query, il nome del server non viene restituito nel documento XML risultante quando la query viene eseguita nel computer locale. Viene tuttavia restituito come nome in quattro parti se la query viene eseguita in un server di rete.

Ad esempio, si consideri la query seguente:

```sql
SELECT TOP 1 LastName
  FROM ServerName.AdventureWorks2012.Person.Person
  FOR XML AUTO;
```

&nbsp;

**Server locale**: &nbsp; Se `ServerName` è un server locale, la query restituisce il testo seguente:

```xml
<AdventureWorks2012.Person.Person LastName="Achong" />  
```

&nbsp;

**Server di rete**: &nbsp; Se `ServerName` è un server di rete, la query restituisce il testo seguente:

```xml
<ServerName.AdventureWorks2012.Person.Person LastName="Achong" />
```

&nbsp;

**Evitare ambiguità**: &nbsp; È possibile evitare questa ambiguità specificando l'alias seguente:

```sql
SELECT TOP 1 LastName
  FROM ServerName.AdventureWorks2012.Person.Person x
  FOR XML AUTO;
```

Con la risoluzione dell'ambiguità, la query restituisce ora il testo seguente:

```xml
<x LastName="Achong"/>
```

## <a name="see-also"></a>Vedere anche

[Sintassi di base della clausola FOR XML](../../relational-databases/xml/basic-syntax-of-the-for-xml-clause.md)  
[Usare la modalità RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
[Usare la modalità AUTO con FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
[Usare la modalità EXPLICIT con FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
[Utilizzare la modalità PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
[OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
[Aggiungere spazi dei nomi alle query con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)
