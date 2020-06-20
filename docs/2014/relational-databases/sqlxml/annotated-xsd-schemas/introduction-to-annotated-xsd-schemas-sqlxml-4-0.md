---
title: Introduzione agli schemi XSD con annotazioni (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- namespaces [SQLXML], annotated XSD schemas
- mapping schema [SQLXML], about mapping schema
- views [SQLXML]
- valid XSD schemas [SQLXML]
- annotations [SQLXML]
- XSD schemas [SQLXML], creating XML views
- annotated XSD schemas, creating XML views
- minimum XSD schema
- annotated XSD schemas, examples
- XML views [SQLXML]
ms.assetid: 15282db1-65c4-43be-bdb7-e9ef49cb33a2
author: rothja
ms.author: jroth
ms.openlocfilehash: d3f3764a8f41d0d6ce8d59cc5aa727676d9282e9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85043045"
---
# <a name="introduction-to-annotated-xsd-schemas-sqlxml-40"></a>Introduzione agli schemi XSD con annotazioni (SQLXML 4.0)
  È possibile creare viste XML di dati relazionali mediante il linguaggio di definizione di XML Schema (XSD). In tali viste è possibile eseguire query utilizzando le query XPath (XML Path language). La procedura è simile a quella utilizzata per creare viste mediante le istruzioni CREATE VIEW e quindi specificare query SQL in tali viste.  
  
 Un elemento XML Schema descrive la struttura di un documento XML e i vari vincoli presenti sui dati del documento. Quando si specificano query XPath nello schema, la struttura del documento XML restituita è determinata dallo schema nel quale viene eseguita la query XPath.  
  
 In uno schema XSD l' **\<xsd:schema>** elemento racchiude l'intero schema. tutte le dichiarazioni di elemento devono essere contenute all'interno dell' **\<xsd:schema>** elemento. È possibile descrivere gli attributi che definiscono lo spazio dei nomi in cui si trova lo schema e gli spazi dei nomi utilizzati nello schema come proprietà dell' **\<xsd:schema>** elemento.  
  
 Uno schema XSD valido deve contenere l' **\<xsd:schema>** elemento definito come segue:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<!-- additional schema definitions here -->  
</xsd:schema>  
```  
  
 L' **\<xsd:schema>** elemento è derivato dalla specifica dello spazio dei nomi XML Schema in http://www.w3.org/2001/XMLSchema .  
  
## <a name="annotations-to-the-xsd-schema"></a>Annotazioni dello schema XSD  
 È possibile utilizzare uno schema XSD con annotazioni che descrivono il mapping a un database, eseguire query nel database e restituire i risultati nel formato di un documento XML. Le annotazioni vengono fornite per eseguire il mapping di uno schema XSD a colonne e tabelle di database. È possibile specificare le query XPath nella vista XML creata dallo schema XSD per eseguire query nel database e ottenere risultati in formato XML.  
  
> [!NOTE]  
>  In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 il linguaggio dello schema XSD supporta le annotazioni introdotte con il linguaggio dello schema XDR (XML-Data Reduced) con annotazioni in [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]. Lo schema XDR con annotazioni è deprecato in SQLXML 4.0.  
  
 Nel contesto del database relazionale risulta utile per eseguire il mapping dello schema XSD arbitrario a un archivio relazionale. Un modo per ottenere questo risultato è annotare lo schema XSD. Uno schema XSD con annotazioni viene definito *schema di mapping*, che fornisce informazioni relative alla modalità di mapping dei dati XML all'archivio relazionale. Uno schema di mapping è, di fatto, una vista XML dei dati relazionali. I mapping possono essere utilizzati per recuperare dati relazionali come documento XML.  
  
## <a name="namespace-for-annotations"></a>Spazio dei nomi per le annotazioni  
 In uno schema XSD le annotazioni vengono specificate tramite lo spazio dei nomi **urn: schemas-microsoft-com: mapping-schema**. Come illustrato nell'esempio seguente, il modo più semplice per specificare lo spazio dei nomi consiste nel specificarlo nel **\<xsd:schema>** tag.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
...  
</xsd:schema>  
```  
  
 Il prefisso dello spazio dei nomi utilizzato è arbitrario. In questa documentazione viene usato il prefisso **SQL** per indicare lo spazio dei nomi di annotazione e per distinguere le annotazioni in questo spazio dei nomi da quelle di altri spazi dei nomi.  
  
## <a name="example-of-an-annotated-xsd-schema"></a>Esempio di schema XSD con annotazioni  
 Nell'esempio seguente lo schema XSD è costituito da un **\<Person.Contact>** elemento. L' **\<Employee>** elemento ha un attributo **ContactID** e **\<FirstName>** **\<LastName>** gli elementi figlio:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
  <xsd:element name="Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"    
                     type="xsd:string" />   
        <xsd:element name="LName"  
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ConID" type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 A questo schema XSD vengono aggiunte annotazioni per eseguire il mapping degli elementi e degli attributi alle colonne e alle tabelle di database:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Contact" sql:relation="Person.Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"  
                     sql:field="FirstName"   
                     type="xsd:string" />   
        <xsd:element name="LName"    
                     sql:field="LastName"    
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ConID"   
                       sql:field="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Nello schema di mapping **\<Contact>** viene eseguito il mapping dell'elemento alla tabella Person. Contact nel database AdventureWorks di esempio tramite l' `sql:relation` annotazione. Viene eseguito il mapping degli attributi ConID, il FName e LName alle colonne ContactID, FirstName e LastName nella tabella Person.Contact mediante le annotazioni `sql:field`.  
  
 Questo schema XSD con annotazioni fornisce la vista XML dei dati relazionali. In questa vista XML possono essere eseguite query mediante il linguaggio XPath. Una query XPath restituisce come risultato un documento XML anziché il set di righe restituito dalle query SQL.  
  
> [!NOTE]  
>  Nello schema di mapping la distinzione tra maiuscole e minuscole per i valori relazionali specificati (ad esempio il nome di tabella e il nome di colonna) dipende dall'eventuale utilizzo delle impostazioni delle regole di confronto con distinzione tra maiuscole e minuscole da parte di SQL Server. Per altre informazioni, vedere [Collation and Unicode Support](../../collations/collation-and-unicode-support.md).  
  
## <a name="other-resources"></a>Risorse aggiuntive  
 Ulteriori informazioni sul linguaggio di definizione di XML Schema (XSD), sul linguaggio XML Path (XPath) e su Extensible Stylesheet Language Transformations (XSLT) sono disponibili nei siti Web seguenti:  
  
-   XML Schema Part 0: primer, raccomandazione W3C (http://www.w3.org/TR/xmlschema-0/)  
  
-   XML Schema Part 1: Structures, raccomandazione W3C (http://www.w3.org/TR/xmlschema-1/)  
  
-   XML Schema Part 2: Datatypes, raccomandazione W3C (http://www.w3.org/TR/xmlschema-2/)  
  
-   XPath (XML Path Language) (http://www.w3.org/TR/xpath)  
  
-   Trasformazioni XSL (XSLT) (http://www.w3.org/TR/xslt)  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza dello schema con annotazioni &#40;SQLXML 4,0&#41;](../../sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)   
 [Schemi XDR con annotazioni &#40;deprecati in SQLXML 4,0&#41;](annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)  
  
  
