---
title: Persistenza di record in formato XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- XML persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: f3113ec4-ae31-428f-89c6-bc1024f128ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c15f4be9d452580cebd6b530f0703f249af17b36
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62913296"
---
# <a name="persisting-records-in-xml-format"></a>Persistenza di record in formato XML
Come formato ADTG **Recordset** con Provider Microsoft OLE DB Persistence viene implementata la persistenza in formato XML. Questo provider genera un set di righe forward-only di sola lettura da un file XML o un flusso che contiene le informazioni sullo schema generate da ADO salvato. Analogamente, può richiedere un oggetto ADO **Recordset**, generano valori XML e salvarlo in un file o su qualsiasi oggetto che implementa il modello COM **IStream** interfaccia. (In effetti, un file è semplicemente un altro esempio di un oggetto che supporta **IStream**.) Per le versioni 2.5 e versioni successive, ADO si basa su Microsoft XML Parser (MSXML) per caricare i dati XML nel **Recordset**; di conseguenza è necessario MSXML.  
  
> [!NOTE]
>  Si applicano alcune limitazioni quando si salva gerarchica **recordset** (forme di dati) in formato XML. Se non è possibile salvare in XML la gerarchica **Recordset** include aggiornamenti, in sospeso e non è possibile salvare un con parametri gerarchici **Recordset**. Per altre informazioni, vedere [persistenza filtrato e Recordset gerarchici](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md).  
  
 Il modo più semplice per rendere persistenti i dati in XML e caricarlo nuovamente nuovamente tramite ADO è con il **salvare** e **Open** metodi, rispettivamente. Esempio di codice ADO seguente viene illustrato il salvataggio dei dati nel **titoli** tabella in un file denominato sav.  
  
```  
Dim rs as new Recordset  
Dim rs2 as new Recordset  
Dim c as new Connection  
Dim s as new Stream  
  
' Query the Titles table.  
c.Open "provider=sqloledb;data source=MySQLServer;initial catalog=pubs;Integrated Security='SSPI'"  
rs.cursorlocation = adUseClient  
rs.Open "select * from titles", c, adOpenStatic  
  
' Save to the file in the XML format. Note that if you don't specify   
' adPersistXML, a binary format (ADTG) will be used by default.  
rs.Save "titles.sav", adPersistXML  
  
' Save the recordset into the ADO Stream object.  
rs.save s, adPersistXML  
rs.Close  
c.Close  
  
set rs = nothing  
  
' Reopen the file.  
rs.Open "titles.sav",,,,adCmdFile  
' Open the Stream back into a Recordset.  
rs2.open s  
```  
  
 ADO persiste sempre l'intera **Recordset** oggetto. Se si vuole rendere persistente un subset di righe del **Recordset** dell'oggetto, utilizzare il **filtro** metodo per limitare le righe o modificare la clausola di selezione. Tuttavia, è necessario aprire una **Recordset** oggetto con un cursore lato client (**CursorLocation** = **adUseClient**) usare il **filtrare** metodo per il salvataggio di un subset di righe. Ad esempio, per recuperare i titoli che iniziano con la lettera "b", è possibile applicare un filtro a un oggetto aperto **Recordset** oggetto:  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO utilizza sempre il set di righe di motore del cursore Client per produrre un scorrevole, supporta **Recordset** oggetto sopra i dati di tipo forward-only generati dal Provider di persistenza.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Formato di persistenza XML](../../../ado/guide/data/xml-persistence-format.md)  
  
-   [Spazi dei nomi](../../../ado/guide/data/namespaces.md)  
  
-   [Sezione schema](../../../ado/guide/data/schema-section.md)  
  
-   [Sezione di dati](../../../ado/guide/data/data-section.md)  
  
-   [Recordset gerarchici in XML](../../../ado/guide/data/hierarchical-recordsets-in-xml.md)  
  
-   [Proprietà dinamiche del recordset in XML](../../../ado/guide/data/recordset-dynamic-properties-in-xml.md)  
  
-   [Trasformazioni XSLT](../../../ado/guide/data/xslt-transformations.md)  
  
-   [Salvataggio nell'oggetto XML DOM](../../../ado/guide/data/saving-to-the-xml-dom-object.md)  
  
-   [Considerazioni sulla sicurezza XML](../../../ado/guide/data/xml-security-considerations.md)  
  
-   [Scenario di persistenza recordset XML](../../../ado/guide/data/xml-recordset-persistence-scenario.md)
