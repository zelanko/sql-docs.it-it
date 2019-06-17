---
title: Report Definition Language (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Reporting Services, RDL
- Reporting Services, RDL
- RDL [Reporting Services], about Report Definition Language
- SSRS, RDL
- Report Definition Language, about Report Definition Language
- Report Definition Language
- RDL [Reporting Services]
- reports [Reporting Services], definitions
ms.assetid: b18b025e-f4bd-4744-8f86-0ac9fb967548
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6480a8cefee9b71149c61bf952896a739526cf55
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102501"
---
# <a name="report-definition-language-ssrs"></a>Report Definition Language (SSRS)
  Report Definition Language (RDL) è una rappresentazione XML di una definizione di un report di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Una definizione del report contiene informazioni sul layout e sul recupero dei dati per un report. RDL è costituito da elementi XML che corrispondono a una grammatica XML creata per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. È possibile aggiungere funzioni personalizzate per il controllo dei valori degli elementi del report, degli stili e della formattazione mediante l'accesso agli assembly di codice all'interno dei file di definizione dei report.  
  
 RDL promuove l'interoperabilità di prodotti per la creazione di report commerciali mediante la definizione di un schema comune che consente lo scambio di definizioni dei report. Con RDL è possibile utilizzare qualsiasi protocollo o interfaccia programmatica appropriato per XML. RDL consiste in:  
  
-   XML Schema per le definizioni dei report.  
  
-   Un formato di interscambio per aziende e terze parti.  
  
-   Uno schema estensibile e aperto che supporta spazi dei nomi aggiuntivi ed elementi personalizzati.  
  
##  <a name="bkmk_RDL_Specifications"></a> Specifiche RDL  
 Per scaricare le specifiche per versioni dello schema specifiche, vedere [Specifica del linguaggio RDL](https://go.microsoft.com/fwlink/?linkid=116865).  
  
##  <a name="bkmk_RDL_XML_Schema_Definition"></a> XML Schema Definition RDL  
 Un file RDL (Report Definition Language) di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene convalidato tramite un file XSD (XML Schema Definition). Lo schema definisce le regole relative alla posizione degli elementi RDL in un file rdl. Un elemento include il tipo di dati e la cardinalità, ovvero il numero di occorrenze consentite. Un elemento può essere semplice o complesso. Un elemento semplice non dispone di attributi o elementi figlio. Un elemento complesso dispone di elementi figlio e, facoltativamente, di attributi.  
  
 Ad esempio, lo schema seguente include l'elemento RDL `ReportParameters` che è il tipo complesso `ReportParametersType`. Per convenzione, un tipo complesso per un elemento è il nome dell'elemento seguito dalla parola `Type`. Un elemento `ReportParameters` può essere contenuto dall'elemento `Report` (un tipo complesso) e contenere elementi `ReportParameter`. Un `ReportParameterType` è un tipo semplice che può essere solo uno dei seguenti valori: `Boolean`, `DateTime`, `Integer`, `Float` o `String`. Per altre informazioni sui tipi di dati dell'elemento XML Schema, vedere [XML Schema Part 2: Datatypes Second Edition](https://go.microsoft.com/fwlink/?linkid=4871) (XML Schema Parte 2: Tipi di dati seconda edizione).  
  
 L'XSD RDL è disponibile nel file ReportDefinition.xsd, contenuto nella cartella Extras nel CD-ROM del prodotto. È anche disponibile nel server di report tramite l'URL seguente: http://servername/reportserver/reportdefinition.xsd.  
  
##  <a name="bkmk_Creating_RDL"></a> Creazione di RDL  
 La natura aperta ed estensibile di RDL consente di compilare una varietà di strumenti e applicazioni per la generazione di codice RDL in base al relativo XML Schema.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornisce più strumenti per compilare i file RDL. Per altre informazioni, vedere [Strumenti di Reporting Services](../tools/reporting-services-tools.md).  
  
 Uno dei modi più semplici per generare codice RDL da un'applicazione consiste nell'usare le classi [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] dello spazio dei nomi <xref:System.Xml> e dello spazio dei nomi <xref:System.Linq> . In particolare, la classe **XmlTextWriter** può essere usata per scrivere codice RDL. Con **XmlTextWriter**è possibile generare una definizione di report completa in qualsiasi applicazione [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . Gli sviluppatori possono inoltre estendere il linguaggio RDL aggiungendo elementi del report personalizzati con proprietà personalizzate. Per altre informazioni sulla classe **XmlTextWriter** e sullo spazio dei nomi <xref:System.Xml> , vedere la Guida per gli sviluppatori di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . Per ulteriori informazioni su LINQ (Language-Integrated Query), cercare "LINQ to XML" in MSDN.  
  
 L'estensione di file standard per i file di definizione dei report è rdl. È inoltre possibile sviluppare file di definizione dei report del client la cui estensione è rdlc. Il tipo MIME per entrambe le estensioni è text/xml. Per altre informazioni sui report, vedere [Report di Reporting Services &#40;SSRS&#41;](reporting-services-reports-ssrs.md).  
  
##  <a name="bkmk_RDL_Types"></a> Tipi RDL  
 Nella tabella seguente vengono elencati i tipi utilizzati negli elementi e negli attributi RDL.  
  
|Type|Descrizione|  
|----------|-----------------|  
|`Binary`|Proprietà con valore binario codificato in base 64.|  
|`Boolean`|Proprietà con `true` o `false` come valore dell'oggetto. Se non diversamente specificato, il valore di un oggetto booleano facoltativo omesso è `False`.|  
|`Date`|Proprietà con un valore di data o ora specificato per intero nel formato di data ISO8601: AAAA-MM-GG[THH:MM[:SS[.S]]].|  
|`Enum`|Proprietà con un valore di testo stringa che deve essere presente in un elenco di valori designati.|  
|`Float`|Proprietà con un valore float. La virgola (,) viene utilizzata come separatore decimale facoltativo.|  
|`Integer`|Proprietà con un valore intero (int32).|  
|`Language`|Proprietà con un valore di testo che contiene un codice di lingua e di paese, ad esempio en-us per Inglese (Stati Uniti). Il valore deve essere una lingua specifica o neutra per la quale è definita una lingua predefinita in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].|  
|`Name`|Proprietà con un valore di testo stringa. I nomi devono essere univoci nello spazio dei nomi dell'elemento. Se non viene specificato, lo spazio dei nomi per un elemento è l'oggetto contenitore più interno con un nome.|  
|`NormalizedString`|Proprietà con un valore di testo stringa normalizzato.|  
|`Size`|Un elemento Size deve contenere un numero, con un carattere punto (.) utilizzato come un separatore decimale facoltativo. Il numero deve essere seguito da un identificatore per un'unità di lunghezza CSS, ad esempio cm, mm, in, pt o pc. La presenza di uno spazio tra il numero e l'identificatore è facoltativa. Per altre informazioni sugli identificatori della proprietà Size, vedere [CSS Length Units Reference](https://www.w3schools.com/CSSref/css_units.asp).<br /><br /> In RDL, il valore massimo per `Size` è 406,4 cm. La dimensione minima è 0 cm.|  
|`String`|Proprietà con un valore di testo stringa.|  
|`UnsignedInt`|Proprietà con un valore intero (uint32) senza segno.|  
|`Variant`|Proprietà con qualsiasi tipo XML semplice.|  
  
##  <a name="bkmk_RDL_Data_Types"></a> Tipi di dati RDL  
 L'enumerazione DataType definisce il tipo di dati di un attributo, di un'espressione o di un parametro in RDL. Nella tabella seguente viene illustrato come i tipi di dati Common Language Runtime (CLR) corrispondono ai tipi di dati RDL.  
  
|**Tipi CLR**|**Tipo di dati corrispondente**|  
|-----------------------|---------------------------------|  
|Boolean|Boolean|  
|DateTime, DateTimeOffset|DateTime|  
|Int16, Int32, UInt16, Byte, SByte|Valore intero|  
|Single, Double|float|  
|String, Char, GUID, Timespan|String|  
  
## <a name="see-also"></a>Vedere anche  
 [Individuare la versione dello schema di definizione del report &#40;SSRS&#41;](find-the-report-definition-schema-version-ssrs.md)   
 [Utilizzo di assembly personalizzati con i report](../custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Elementi dei report personalizzati](../custom-report-items/custom-report-items.md)  
  
  
