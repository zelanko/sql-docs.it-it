---
title: Introduzione agli schemi XSD con annotazioni (SQLXML)
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 81791c2b48e414f4f147bfff47cf1d9166d4a2a5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "75247063"
---
# <a name="introduction-to-annotated-xsd-schemas-sqlxml-40"></a>Introduzione agli schemi XSD con annotazioni (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  È possibile creare viste XML di dati relazionali mediante il linguaggio di definizione di XML Schema (XSD). In tali viste è possibile eseguire query utilizzando le query XPath (XML Path language). La procedura è simile a quella utilizzata per creare viste mediante le istruzioni CREATE VIEW e quindi specificare query SQL in tali viste.  
  
 Un elemento XML Schema descrive la struttura di un documento XML e i vari vincoli presenti sui dati del documento. Quando si specificano query XPath nello schema, la struttura del documento XML restituita è determinata dallo schema nel quale viene eseguita la query XPath.  
  
 In uno schema XSD l' ** \<elemento xsd: schema>** racchiude l'intero schema. tutte le dichiarazioni di elemento devono essere contenute all'interno dell' ** \<elemento xsd: schema>** . È possibile descrivere gli attributi che definiscono lo spazio dei nomi in cui si trova lo schema e gli spazi dei nomi utilizzati nello schema come proprietà dell'elemento ** \<xsd: schema>** .  
  
 Uno schema XSD valido deve contenere l' ** \<elemento xsd: schema>** definito come segue:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<!-- additional schema definitions here -->  
</xsd:schema>  
```  
  
 L' ** \<elemento xsd: schema>** deriva dalla specifica dello spazio dei nomi XML schema http://www.w3.org/2001/XMLSchemain.  
  
## <a name="annotations-to-the-xsd-schema"></a>Annotazioni dello schema XSD  
 È possibile utilizzare uno schema XSD con annotazioni che descrivono il mapping a un database, eseguire query nel database e restituire i risultati nel formato di un documento XML. Le annotazioni vengono fornite per eseguire il mapping di uno schema XSD a colonne e tabelle di database. È possibile specificare le query XPath nella vista XML creata dallo schema XSD per eseguire query nel database e ottenere risultati in formato XML.  
  
> [!NOTE]  
>  In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 il linguaggio dello schema XSD supporta le annotazioni introdotte con il linguaggio dello schema XDR (XML-Data Reduced) con annotazioni in [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]. Lo schema XDR con annotazioni è deprecato in SQLXML 4.0.  
  
 Nel contesto del database relazionale risulta utile per eseguire il mapping dello schema XSD arbitrario a un archivio relazionale. Un modo per ottenere questo risultato è annotare lo schema XSD. Uno schema XSD con annotazioni viene definito *schema di mapping*, che fornisce informazioni relative alla modalità di mapping dei dati XML all'archivio relazionale. Uno schema di mapping è, di fatto, una vista XML dei dati relazionali. I mapping possono essere utilizzati per recuperare dati relazionali come documento XML.  
  
## <a name="namespace-for-annotations"></a>Spazio dei nomi per le annotazioni  
 In uno schema XSD le annotazioni vengono specificate tramite lo spazio dei nomi **urn: schemas-microsoft-com: mapping-schema**. Come illustrato nell'esempio seguente, il modo più semplice per specificare lo spazio dei nomi consiste nel specificarlo nel tag ** \<xsd: schema>** .  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
...  
</xsd:schema>  
```  
  
 Il prefisso dello spazio dei nomi utilizzato è arbitrario. In questa documentazione viene usato il prefisso **SQL** per indicare lo spazio dei nomi di annotazione e per distinguere le annotazioni in questo spazio dei nomi da quelle di altri spazi dei nomi.  
  
## <a name="example-of-an-annotated-xsd-schema"></a>Esempio di schema XSD con annotazioni  
 Nell'esempio seguente lo schema XSD è costituito da un ** \<elemento Person. Contact>** . L' ** \<elemento Employee>** ha un attributo **ContactID** e ** \<FirstName>** e ** \<LastName>** elementi figlio:  
  
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
  
 Nello schema di mapping, l' ** \<elemento Contact>** viene mappato alla tabella Person. Contact nel database AdventureWorks di esempio tramite l'annotazione **SQL: relation** . Gli attributi ConId, FName e LName vengono mappati alle colonne ContactID, FirstName e LastName nella tabella Person. Contact usando le annotazioni **SQL: Field** .  
  
 Questo schema XSD con annotazioni fornisce la vista XML dei dati relazionali. In questa vista XML possono essere eseguite query mediante il linguaggio XPath. Una query XPath restituisce come risultato un documento XML anziché il set di righe restituito dalle query SQL.  
  
> [!NOTE]  
>  Nello schema di mapping la distinzione tra maiuscole e minuscole per i valori relazionali specificati (ad esempio il nome di tabella e il nome di colonna) dipende dall'eventuale utilizzo delle impostazioni delle regole di confronto con distinzione tra maiuscole e minuscole da parte di SQL Server. Per altre informazioni, vedere [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="other-resources"></a>Risorse aggiuntive  
 Ulteriori informazioni sul linguaggio di definizione di XML Schema (XSD), sul linguaggio XML Path (XPath) e su Extensible Stylesheet Language Transformations (XSLT) sono disponibili nei siti Web seguenti:  
  
-   XML Schema Part 0: primer, raccomandazione W3C (https://www.w3.org/TR/xmlschema-0/)  
  
-   XML Schema Part 1: Structures, raccomandazione W3C (https://www.w3.org/TR/xmlschema-1/)  
  
-   XML Schema Part 2: Datatypes, raccomandazione W3C (https://www.w3.org/TR/xmlschema-2/)  
  
-   XPath (XML Path Language) (https://www.w3.org/TR/xpath)  
  
-   Trasformazioni XSL (XSLT) (https://www.w3.org/TR/xslt)  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza dello schema con annotazioni &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)   
 [Schemi XDR con annotazioni &#40;deprecati in SQLXML 4,0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)  
  
  
