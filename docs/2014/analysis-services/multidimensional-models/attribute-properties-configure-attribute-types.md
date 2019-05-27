---
title: Configurare i tipi di attributo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time dimensions [Analysis Services]
- attributes [Analysis Services], types
- slowly changing dimensions
- account dimensions [Analysis Services]
- currency dimensions [Analysis Services]
- Type property
ms.assetid: c2c6a3da-555e-4362-a83f-88da28427520
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e5223444f58326b7530388f3fe2fc06d72488a5e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077407"
---
# <a name="configure-attribute-types"></a>Configurare tipi di attributi
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] i tipi di attributi consentono di classificare un attributo in termini di funzionalità aziendali. Sono disponibili numerosi tipi di attributi, la maggior parte dei quali viene utilizzata dalle applicazioni client per visualizzare o supportare un attributo. Alcuni tipi di attributi, tuttavia, hanno un significato specifico in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Alcuni tipi identificano ad esempio attributi che rappresentano periodi di tempo in calendari diversi per le dimensioni temporali.  
  
##  <a name="setting_attibute_types"></a> Impostazione dei tipi di attributi  
 Il valore della proprietà `Type` per un attributo determina il tipo dell'attributo stesso. Diverse procedure guidate di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consentono di impostare i tipi di attributi durante la definizione di dimensioni o attributi. Tali procedure guidate di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consentono inoltre di impostare i tipi di attributi durante l'aggiunta di funzionalità alle dimensioni. Tramite la Configurazione guidata funzionalità di Business Intelligence, ad esempio, vengono applicati numerosi tipi di attributi agli attributi in una dimensione durante l'aggiunta di funzionalità di Business Intelligence per la contabilità, per identificare attributi contenenti nomi, codici, numeri e struttura dei conti nella dimensione. Nella Configurazione guidata funzionalità di Business Intelligence vengono inoltre utilizzati i tipi di attributi, ad esempio per la conversione di valuta. Per altre informazioni, vedere [Creare una dimensione di tipo Valuta](database-dimensions-create-a-currency-type-dimension.md).  
  
 Nelle tabelle seguenti sono inclusi i tipi di attributi disponibili in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Nelle tabelle i tipi di attributi sono organizzati nelle categorie seguenti:  
  
|Nome|Definizione|  
|----------|----------------|  
|[Tipi di attributi generali](#general_attribute_types)|Questi valori sono disponibili per tutti gli attributi e hanno l'unico scopo di consentire la classificazione degli attributi ai fini delle applicazioni client.|  
|[Tipi di attributi delle dimensioni di tipo Conto](#account_dimension_attribute_types)|Questi valori identificano un attributo appartenente a una dimensione di tipo Conto. Per altre informazioni sulle dimensioni di tipo Conto, vedere [Creare un conto finanziario della dimensione di tipo padre-figlio](database-dimensions-finance-account-of-parent-child-type.md).|  
|[Tipi di attributi delle dimensioni di tipo Valuta](#currency_dimension_attribute_types)|Questi valori identificano un attributo appartenente a una dimensione di tipo Valuta. Per altre informazioni sulle dimensioni di tipo Valuta, vedere [Creare una dimensione di tipo Valuta](database-dimensions-create-a-currency-type-dimension.md).|  
|[Tipi di attributi delle dimensioni a modifica lenta](#slowly_changing_dimension_attribute_types)|Questi valori identificano un attributo appartenente a una dimensione a modifica lenta.|  
|[Tipi di attributi delle dimensioni temporali](#time_dimension_attribute_types)|Questi valori identificano un attributo appartenente a una dimensione temporale. Per altre informazioni sulle dimensioni temporali, vedere [Creare una dimensione di tipo Date](database-dimensions-create-a-date-type-dimension.md).|  
  
###  <a name="general_attribute_types"></a> General Attribute Types  
  
|Valore del tipo di attributo|Descrizione|  
|--------------------------|-----------------|  
|`Address`|Rappresenta un indirizzo.|  
|`AddressBuilding`|Rappresenta l'identificatore di edificio per un indirizzo.|  
|`AddressCity`|Rappresenta la città per un indirizzo.|  
|`AddressCountry`|Rappresenta il paese/area geografica per un indirizzo.|  
|`AddressFax`|Rappresenta un numero di fax.|  
|`AddressFloor`|Rappresenta l'identificatore di piano per un indirizzo.|  
|`AddressHouse`|Rappresenta il numero civico per un indirizzo.|  
|`AddressPhone`|Rappresenta un numero di telefono.|  
|`AddressQuarter`|Rappresenta il quartiere per un indirizzo.|  
|`AddressRoom`|Rappresenta l'identificatore di stanza per un indirizzo.|  
|`AddressStateOrProvince`|Rappresenta lo stato o la provincia per un indirizzo.|  
|`AddressStreet`|Rappresenta la via per un indirizzo.|  
|`AddressZip`|Rappresenta il CAP per un indirizzo.|  
|`BomResource`|Rappresenta una risorsa per una distinta base.|  
|`Caption`|Rappresenta una didascalia.|  
|`CaptionAbbreviation`|Rappresenta un'abbreviazione.|  
|`CaptionDescription`|Rappresenta una descrizione.|  
|`Channel`|Rappresenta un canale.|  
|`City`|Rappresenta una città.|  
|`Company`|Rappresenta una società.|  
|`Continent`|Rappresenta un continente.|  
|`Country`|Rappresenta un paese/area geografica.|  
|`County`|Rappresenta una regione.|  
|`CustomerGroup`|Rappresenta un gruppo di clienti.|  
|`CustomerHousehold`|Rappresenta l'unità familiare dei clienti.|  
|`Customers`|Rappresenta un cliente.|  
|`DateCanceled`|Rappresenta una data di annullamento.|  
|`DateDuration`|Rappresenta una durata.|  
|`DateEnded`|Rappresenta una data di fine.|  
|`DateModified`|Rappresenta una data di modifica.|  
|`DateStart`|Rappresenta una data di inizio.|  
|**DeletedFlag**|Indica se un membro è o deve essere eliminato, in relazione alla funzionalità business.<br /><br /> Nota: in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non viene usato questo tipo di attributo per determinare se un membro debba essere eliminato. Questo tipo di attributo è invece destinato all'utilizzo da parte delle applicazioni client esclusivamente ai fini della visualizzazione.|  
|`FormattingColor`|Rappresenta il colore utilizzato per la formattazione.|  
|`FormattingFont`|Rappresenta il tipo di carattere utilizzato per la formattazione.|  
|`FormattingFontEffects`|Rappresenta gli effetti di carattere utilizzati per la formattazione.|  
|`FormattingFontSize`|Rappresenta le dimensioni del carattere utilizzate per la formattazione.|  
|`FormattingOrder`|Rappresenta l'ordinamento utilizzato per la formattazione.|  
|`FormattingSubtotal`|Rappresenta un sottototale.|  
|`GeoBoundaryBottom`|Rappresenta il valore inferiore di un confine geografico.|  
|`GeoBoundaryFront`|Rappresenta il valore anteriore di un confine geografico.|  
|`GeoBoundaryLeft`|Rappresenta il valore più a sinistra di un confine geografico.|  
|`GeoBoundaryPolygon`|Rappresenta la definizione di poligono di un confine geografico.|  
|`GeoBoundaryRear`|Rappresenta il valore posteriore di un confine geografico.|  
|`GeoBoundaryRight`|Rappresenta il valore più a destra di un confine geografico.|  
|`GeoBoundaryTop`|Rappresenta il valore superiore di un confine geografico.|  
|`GeoCentroidX`|Rappresenta il centro dell'asse X per un'area geografica.|  
|`GeoCentroidY`|Rappresenta il centro dell'asse Y per un'area geografica.|  
|`GeoCentroidZ`|Rappresenta il centro dell'asse Z per un'area geografica.|  
|`ID`|Rappresenta un identificatore (ID) o una chiave.|  
|`Image`|Rappresenta un'immagine in un formato grafico non definito.|  
|`ImageBmp`|Rappresenta un'immagine nel formato grafico bitmap.|  
|`ImageGif`|Rappresenta un'immagine nel formato grafico GIF (Graphics Interchange Format).|  
|`ImageJpg`|Rappresenta un'immagine nel formato grafico JPEG (Joint Photographic Experts Group).|  
|`ImagePng`|Rappresenta un'immagine nel formato grafico PNG (Portable Network Graphics).|  
|`ImageTiff`|Rappresenta un'immagine nel formato grafico TIFF (Tagged Image File Format).|  
|`OrganizationalUnit`|Rappresenta un'unità organizzativa.|  
|`OrgTitle`|Rappresenta una posizione organizzativa.|  
|`PercentOwnership`|Rappresenta una percentuale di proprietà.|  
|`PercentVoteRight`|Rappresenta una percentuale di diritti di voto.|  
|`Person`|Rappresenta una persona.|  
|`PersonContact`|Rappresenta le informazioni di recapito per una persona.|  
|`PersonDemographic`|Rappresenta le informazioni demografiche per una persona.|  
|`PersonFirstName`|Rappresenta il nome di una persona.|  
|`PersonFullName`|Rappresenta il nome e cognome di una persona.|  
|`PersonLastName`|Rappresenta il cognome di una persona.|  
|`PersonMiddleName`|Rappresenta il secondo nome di una persona.|  
|`PhysicalColor`|Rappresenta un colore.|  
|`PhysicalDensity`|Rappresenta la densità.|  
|`PhysicalDepth`|Rappresenta la profondità.|  
|`PhysicalHeight`|Rappresenta l'altezza.|  
|`PhysicalSize`|Rappresenta la dimensioni.|  
|`PhysicalVolume`|Rappresenta il volume.|  
|`PhysicalWeight`|Rappresenta il peso.|  
|`PhysicalWidth`|Rappresenta la larghezza.|  
|`Point`|Rappresenta un punto.|  
|`PostalCode`|Rappresenta un CAP.|  
|`Product`|Rappresenta un prodotto.|  
|`ProductBrand`|Rappresenta una marca di prodotto.|  
|`ProductCategory`|Rappresenta una categoria di prodotti.|  
|`ProductGroup`|Rappresenta un gruppo di prodotti.|  
|`ProductSKU`|Rappresenta il codice di riferimento di un prodotto (SKU).|  
|`Project`|Rappresenta un progetto.|  
|`ProjectCode`|Rappresenta un codice di progetto.|  
|`ProjectCompletion`|Rappresenta lo stato di completamento di un progetto.|  
|`ProjectEndDate`|Rappresenta la data di fine di un progetto.|  
|`ProjectName`|Rappresenta un nome di progetto.|  
|`ProjectStartDate`|Rappresenta la data di inizio di un progetto.|  
|`Promotion`|Rappresenta una promozione.|  
|`QtyRangeHigh`|Rappresenta il valore massimo in un intervallo di quantità.|  
|`QtyRangeLow`|Rappresenta il valore minimo in un intervallo di quantità.|  
|`Quantitative`|Rappresenta un attributo quantitativo.|  
|`Rate`|Rappresenta un tasso.|  
|`RateType`|Rappresenta un tipo di tasso.|  
|`Region`|Rappresenta una regione definita dal cliente.|  
|`Regular`|Rappresenta un attributo regolare.|  
|`RelationToParent`|Rappresenta una relazione con un elemento padre.|  
|`Representative`|Rappresenta un rappresentante.|  
|`Scenario`|Rappresenta uno scenario.|  
|`Sequence`|Rappresenta un attributo di sequenza.|  
|`ShortCaption`|Rappresenta una didascalia breve.|  
|`StateOrProvince`|Rappresenta uno stato o una provincia.|  
|`Utility`|Rappresenta un'utilità.|  
|`Version`|Rappresenta una versione.|  
|`WebHtml`|Rappresenta contenuto HTML.|  
|`WebMailAlias`|Rappresenta un alias di posta elettronica.|  
|`WebUrl`|Rappresenta un indirizzo URL.|  
|`WebXmlOrXsl`|Rappresenta contenuto XML o XSL.|  
  
###  <a name="account_dimension_attribute_types"></a> Account Dimension Attribute Types  
  
|Valore del tipo di attributo|Descrizione|  
|--------------------------|-----------------|  
|`Account`|Rappresenta l'elemento padre di un conto. Questo attributo viene in genere applicato all'attributo padre di una dimensione di tipo Conto.|  
|`AccountName`|Rappresenta il nome di un conto. Questo attributo viene in genere applicato agli attributi chiave di una dimensione di tipo Conto.|  
|`AccountNumber`|Rappresenta il numero di un conto.|  
|`AccountType`|Rappresenta il tipo di un conto. Questo tipo di attributo identifica la funzione di aggregazione di un membro di conto in una dimensione di tipo Conti nel database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
  
###  <a name="currency_dimension_attribute_types"></a> Tipi di attributi delle dimensioni di tipo Valuta  
  
|Valore del tipo di attributo|Descrizione|  
|--------------------------|-----------------|  
|`CurrencyDestination`|Rappresenta la valuta di destinazione di un cambio di valuta. Questo attributo viene in genere applicato all'attributo chiave di una dimensione di tipo Valuta per l'utilizzo in una conversione di valuta. Per altre informazioni sulla conversione di valuta, vedere [conversioni di valuta &#40;Analysis Services&#41;](../currency-conversions-analysis-services.md).|  
|`CurrencyIsoCode`|Rappresenta il codice ISO (International Standards Organization) di una valuta. Per altre informazioni sulla conversione di valuta, vedere [conversioni di valuta &#40;Analysis Services&#41;](../currency-conversions-analysis-services.md).|  
|`CurrencyName`|Rappresenta il nome di una valuta. Per altre informazioni sulla conversione di valuta, vedere [conversioni di valuta &#40;Analysis Services&#41;](../currency-conversions-analysis-services.md).|  
|`CurrencySource`|Rappresenta la valuta di origine di un cambio di valuta. Questo attributo viene in genere applicato all'attributo chiave di una dimensione di tipo Valuta per l'utilizzo in una conversione di valuta. Per altre informazioni sulla conversione di valuta, vedere [conversioni di valuta &#40;Analysis Services&#41;](../currency-conversions-analysis-services.md).|  
  
###  <a name="slowly_changing_dimension_attribute_types"></a> Tipi di attributi delle dimensioni a modifica lenta  
  
|Valore del tipo di attributo|Descrizione|  
|--------------------------|-----------------|  
|**ScdEndDate**|Rappresenta la data di fine effettiva per un membro in una dimensione a modifica lenta.|  
|**ScdOriginalID**|Rappresenta l'identificatore originale per un membro in una dimensione a modifica lenta.|  
|**ScdStartDate**|Rappresenta la data di inizio effettiva per un membro in una dimensione a modifica lenta.|  
|`ScdStatus`|Rappresenta lo stato effettivo di un membro in una dimensione a modifica lenta.|  
  
###  <a name="time_dimension_attribute_types"></a> Tipi di attributi delle dimensioni temporali  
  
|Valore del tipo di attributo|Descrizione|  
|--------------------------|-----------------|  
|`Date`|Rappresenta una data. Questo tipo di attributo viene in genere applicato all'attributo chiave di una dimensione temporale o di una dimensione temporale del server.|  
|`DayOfHalfYear`|Rappresenta il numero ordinale di giorno di un semestre.|  
|`DayOfMonth`|Rappresenta il numero ordinale di giorno di un mese.|  
|`DayOfQuarter`|Rappresenta il numero ordinale di giorno di un trimestre.|  
|`DayOfTenDays`|Rappresenta il numero ordinale di giorno di una decade.|  
|`DayOfTrimester`|Rappresenta il numero ordinale di giorno di un quadrimestre.|  
|`DayOfWeek`|Rappresenta il numero ordinale di giorno di una settimana.|  
|`DayOfYear`|Rappresenta il numero ordinale di giorno di un anno.|  
|`Days`|Rappresenta i giorni.|  
|`FiscalDate`|Rappresenta una data in un calendario fiscale.|  
|`FiscalDayOfHalfYear`|Rappresenta il numero ordinale di giorno di un semestre in un calendario fiscale.|  
|`FiscalDayOfMonth`|Rappresenta il numero ordinale di giorno di un mese in un calendario fiscale.|  
|`FiscalDayOfQuarter`|Rappresenta il numero ordinale di giorno di un trimestre in un calendario fiscale.|  
|`FiscalDayOfTrimester`|Rappresenta il numero ordinale di giorno di un quadrimestre in un calendario fiscale.|  
|`FiscalDayOfWeek`|Rappresenta il numero ordinale di giorno di una settimana in un calendario fiscale.|  
|`FiscalDayOfYear`|Rappresenta il numero ordinale di giorno di un anno in un calendario fiscale.|  
|`FiscalHalfYears`|Rappresenta i semestri in un calendario fiscale.|  
|`FiscalHalfYearOfYear`|Rappresenta il numero ordinale di semestre di un anno in un calendario fiscale.|  
|`FiscalMonths`|Rappresenta i mesi in un calendario fiscale.|  
|`FiscalMonthOfHalfYear`|Rappresenta il numero ordinale di mese di un semestre in un calendario fiscale.|  
|`FiscalMonthOfQuarter`|Rappresenta il numero ordinale di mese di un trimestre in un calendario fiscale.|  
|`FiscalMonthOfTrimester`|Rappresenta il numero ordinale di mese di un quadrimestre in un calendario fiscale.|  
|`FiscalMonthOfYear`|Rappresenta il numero ordinale di mese di un anno in un calendario fiscale.|  
|`FiscalQuarters`|Rappresenta i trimestri in un calendario fiscale.|  
|`FiscalQuarterOfHalfYear`|Rappresenta il numero ordinale di trimestre di un semestre in un calendario fiscale.|  
|`FiscalQuarterOfYear`|Rappresenta il numero ordinale di trimestre di un anno in un calendario fiscale.|  
|`FiscalTrimesters`|Rappresenta i quadrimestri in un calendario fiscale.|  
|`FiscalTrimesterOfYear`|Rappresenta il numero ordinale di quadrimestre di un anno in un calendario fiscale.|  
|`FiscalWeeks`|Rappresenta le settimane in un calendario fiscale.|  
|`FiscalWeekOfHalfYear`|Rappresenta il numero ordinale di settimana di un semestre in un calendario fiscale.|  
|`FiscalWeekOfMonth`|Rappresenta il numero ordinale di settimana di un mese in un calendario fiscale.|  
|`FiscalWeekOfQuarter`|Rappresenta il numero ordinale di settimana di un trimestre in un calendario fiscale.|  
|`FiscalWeekOfTrimester`|Rappresenta il numero ordinale di settimana di un quadrimestre in un calendario fiscale.|  
|`FiscalWeekOfYear`|Rappresenta il numero ordinale di settimana di un anno in un calendario fiscale.|  
|`FiscalYears`|Rappresenta gli anni in un calendario fiscale.|  
|`HalfYears`|Rappresenta i semestri.|  
|`HalfYearOfYear`|Rappresenta il numero ordinale di semestre di un anno.|  
|`Hours`|Rappresenta le ore.|  
|`IsHoliday`|Indica se la data rappresenta un giorno festivo.|  
|`ISO8601Date`|Rappresenta una data in un calendario ISO 8601.|  
|`ISO8601DayOfWeek`|Rappresenta il numero ordinale di giorno di una settimana in un calendario ISO 8601.|  
|`ISO8601DayOfYear`|Rappresenta il numero ordinale di giorno di un anno in un calendario ISO 8601.|  
|`ISO8601Weeks`|Rappresenta le settimane in un calendario ISO 8601.|  
|`ISO8601WeekOfYear`|Rappresenta il numero ordinale di settimana di un anno in un calendario ISO 8601.|  
|`ISO8601Years`|Rappresenta gli anni in un calendario ISO 8601.|  
|`IsPeakDay`|Indica se la data rappresenta un giorno di punta.|  
|`IsWeekDay`|Indica se la data rappresenta un giorno feriale.|  
|`IsWorkingDay`|Indica se la data rappresenta un giorno lavorativo.|  
|`ManufacturingDate`|Rappresenta una data in un calendario di produzione.|  
|`ManufacturingDayOfHalfYear`|Rappresenta il numero ordinale di giorno di un semestre in un calendario di produzione.|  
|`ManufacturingDayOfMonth`|Rappresenta il numero ordinale di giorno di un mese in un calendario di produzione.|  
|`ManufacturingDayOfQuarter`|Rappresenta il numero ordinale di giorno di un trimestre in un calendario di produzione.|  
|`ManufacturingDayOfTrimester`|Rappresenta il numero ordinale di giorno di un quadrimestre in un calendario di produzione.|  
|`ManufacturingDayOfWeek`|Rappresenta il numero ordinale di giorno di una settimana in un calendario di produzione.|  
|`ManufacturingDayOfYear`|Rappresenta il numero ordinale di giorno di un anno in un calendario di produzione.|  
|`ManufacturingHalfYears`|Rappresenta i semestri in un calendario di produzione.|  
|`ManufacturingHalfYearOfYear`|Rappresenta il numero ordinale di semestre di un anno in un calendario di produzione.|  
|`ManufacturingMonths`|Rappresenta i mesi in un calendario di produzione.|  
|`ManufacturingMonthOfHalfYear`|Rappresenta il numero ordinale di mese di un semestre in un calendario di produzione.|  
|`ManufacturingMonthOfQuarter`|Rappresenta il numero ordinale di mese di un trimestre in un calendario di produzione.|  
|`ManufacturingMonthOfTrimester`|Rappresenta il numero ordinale di mese di un quadrimestre in un calendario di produzione.|  
|`ManufacturingMonthOfYear`|Rappresenta il numero ordinale di mese di un anno in un calendario di produzione.|  
|`ManufacturingQuarters`|Rappresenta i trimestri in un calendario di produzione.|  
|`ManufacturingQuarterOfHalfYear`|Rappresenta il numero ordinale di trimestre di un semestre in un calendario di produzione.|  
|`ManufacturingQuarterOfYear`|Rappresenta il numero ordinale di trimestre di un anno in un calendario di produzione.|  
|`ManufacturingWeeks`|Rappresenta le settimane in un calendario di produzione.|  
|`ManufacturingWeekOfHalfYear`|Rappresenta il numero ordinale di settimana di un semestre in un calendario di produzione.|  
|`ManufacturingWeekOfMonth`|Rappresenta il numero ordinale di settimana di un mese in un calendario di produzione.|  
|`ManufacturingWeekOfQuarter`|Rappresenta il numero ordinale di settimana di un trimestre in un calendario di produzione.|  
|`ManufacturingWeekOfTrimester`|Rappresenta il numero ordinale di settimana di un quadrimestre in un calendario di produzione.|  
|`ManufacturingWeekOfYear`|Rappresenta il numero ordinale di settimana di un anno in un calendario di produzione.|  
|`ManufacturingYears`|Rappresenta gli anni in un calendario di produzione.|  
|`Minutes`|Rappresenta i minuti.|  
|`Months`|Rappresenta i mesi.|  
|`MonthOfHalfYear`|Rappresenta il numero ordinale di mese di un semestre.|  
|`MonthOfQuarter`|Rappresenta il numero ordinale di mese di un trimestre.|  
|`MonthOfTrimester`|Rappresenta il numero ordinale di mese di un quadrimestre.|  
|`MonthOfYear`|Rappresenta il numero ordinale di mese di un anno.|  
|`Quarters`|Rappresenta i trimestri.|  
|`QuarterOfHalfYear`|Rappresenta il numero ordinale di trimestre di un semestre.|  
|`QuarterOfYear`|Rappresenta il numero ordinale di trimestre di un anno.|  
|`ReportingDate`|Rappresenta una data in un calendario di report.|  
|`ReportingDayOfHalfYear`|Rappresenta il numero ordinale di giorno di un semestre in un calendario di report.|  
|`ReportingDayOfMonth`|Rappresenta il numero ordinale di giorno di un mese in un calendario di report.|  
|`ReportingDayOfQuarter`|Rappresenta il numero ordinale di giorno di un trimestre in un calendario di report.|  
|`ReportingDayOfTrimester`|Rappresenta il numero ordinale di giorno di un quadrimestre in un calendario di report.|  
|`ReportingDayOfWeek`|Rappresenta il numero ordinale di giorno di una settimana in un calendario di report.|  
|`ReportingDayOfYear`|Rappresenta il numero ordinale di giorno di un anno in un calendario di report.|  
|`ReportingHalfYears`|Rappresenta i semestri in un calendario di report.|  
|`ReportingHalfYearOfYear`|Rappresenta il numero ordinale di semestre di un anno in un calendario di report.|  
|`ReportingMonths`|Rappresenta i mesi in un calendario di report.|  
|`ReportingMonthOfHalfYear`|Rappresenta il numero ordinale di mese di un semestre in un calendario di report.|  
|`ReportingMonthOfQuarter`|Rappresenta il numero ordinale di mese di un trimestre in un calendario di report.|  
|`ReportingMonthOfTrimester`|Rappresenta il numero ordinale di mese di un quadrimestre in un calendario di report.|  
|`ReportingMonthOfYear`|Rappresenta il numero ordinale di mese di un anno in un calendario di report.|  
|`ReportingQuarters`|Rappresenta i trimestri in un calendario di report.|  
|`ReportingQuarterOfHalfYear`|Rappresenta il numero ordinale di trimestre di un semestre in un calendario di report.|  
|`ReportingQuarterOfYear`|Rappresenta il numero ordinale di trimestre di un anno in un calendario di report.|  
|`ReportingTrimesters`|Rappresenta i quadrimestri in un calendario di report.|  
|`ReportingTrimesterOfYear`|Rappresenta il numero ordinale di quadrimestre di un anno in un calendario di report.|  
|`ReportingWeeks`|Rappresenta le settimane in un calendario di report.|  
|`ReportingWeekOfHalfYear`|Rappresenta il numero ordinale di settimana di un semestre in un calendario di report.|  
|`ReportingWeekOfMonth`|Rappresenta il numero ordinale di settimana di un mese in un calendario di report.|  
|`ReportingWeekOfQuarter`|Rappresenta il numero ordinale di settimana di un trimestre in un calendario di report.|  
|`ReportingWeekOfTrimester`|Rappresenta il numero ordinale di settimana di un quadrimestre in un calendario di report.|  
|`ReportingWeekOfYear`|Rappresenta il numero ordinale di settimana di un anno in un calendario di report.|  
|`ReportingYears`|Rappresenta gli anni in un calendario di report.|  
|`Seconds`|Rappresenta i secondi.|  
|`TenDayOfHalfYear`|Rappresenta il numero ordinale di decade di un semestre.|  
|`TenDayOfMonth`|Rappresenta il numero ordinale di decade di un mese.|  
|`TenDayOfQuarter`|Rappresenta il numero ordinale di decade di un trimestre.|  
|`TenDayOfTrimester`|Rappresenta il numero ordinale di decade di un quadrimestre.|  
|`TenDayOfYear`|Rappresenta il numero ordinale di decade di un anno.|  
|`TenDays`|Rappresenta le decadi.|  
|`Trimesters`|Rappresenta i quadrimestri.|  
|`TrimesterOfYear`|Rappresenta il numero ordinale di quadrimestre di un anno.|  
|`UndefinedTime`|Rappresenta un periodo di tempo indefinito.|  
|`WeekOfYear`|Rappresenta il numero ordinale di settimana di un anno.|  
|`Weeks`|Rappresenta le settimane.|  
|**WinterSummerSeason**|Indica se la data fa parte della stagione invernale o estiva.|  
|`Years`|Rappresenta gli anni.|  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi e gerarchie di attributi](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Riferimento alle proprietà degli attributi delle dimensioni](dimension-attribute-properties-reference.md)  
  
  
