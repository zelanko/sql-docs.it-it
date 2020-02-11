---
title: Miglioramenti di data e ora | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 9b1d0d9d-1f6e-4399-8f61-e23f9a486a7a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 160731a6749b3741a68dcccafedd3499db465349
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "75231756"
---
# <a name="date-and-time-improvements"></a>Miglioramenti relativi a data e ora
  In questo argomento viene descritto il supporto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client per i tipi di dati di data e ora aggiunti in [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
 Per ulteriori informazioni sui miglioramenti relativi a data e ora, vedere [miglioramenti di data e ora &#40;OLE DB&#41;](../../native-client-ole-db-date-time/date-and-time-improvements-ole-db.md) e [miglioramenti di data e ora &#40;ODBC&#41;](../../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
 Per informazioni sulle applicazioni di esempio in cui viene illustrata questa funzionalità, vedere la pagina relativa agli [esempi di programmazione dati di SQL Server](https://msftdpprodsamples.codeplex.com/).  
  
## <a name="usage"></a>Uso  
 Nelle sezioni seguenti vengono descritte le diverse modalità di utilizzo dei nuovi tipi di data e ora.  
  
### <a name="use-date-as-a-distinct-data-type"></a>Utilizzare il tipo date come tipo di dati distinto  
 A partire da [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], il supporto migliorato per i tipi di data/ora consente un utilizzo più efficiente del tipo SQL_TYPE_DATE ODBC (SQL_DATE per le applicazioni ODBC 2.0) e del tipo DBTYPE_DBDATE OLE DB.  
  
### <a name="use-time-as-a-distinct-data-type"></a>Utilizzare il tipo time come tipo di dati distinto  
 OLE DB include già un tipo di dati che contiene solo l'ora, ovvero DBTYPE_DBTIME, che garantisce precisione pari a 1 secondo. Il tipo equivalente in ODBC è SQL_TYPE_TIME (SQL_TIME per le applicazioni ODBC 2.0).  
  
 Il nuovo tipo di dati time di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ha una precisione frazionaria dei secondi pari a 100 nanosecondi. Sono necessari nuovi tipi in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client: DBTYPE_DBTIME2 (OLE DB) e SQL_SS_TIME2 (ODBC). Le applicazioni esistenti scritte per utilizzare le ore senza secondi frazionari possono utilizzare colonne time(0). I tipi OLE DB DBTYPE_TIME e ODBC SQL_TYPE_TIME esistenti e le strutture corrispondenti funzioneranno correttamente, a meno che le applicazioni non si basino sul tipo restituito nei metadati.  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>Utilizzare il tipo time come tipo di dati distinto con precisione frazionaria dei secondi estesa  
 Alcune applicazioni, ad esempio le applicazioni di controllo dei processi e di produzione, richiedono la possibilità di gestire i dati di tipo time con una precisione pari a fino 100 nanosecondi. I nuovi tipi a tale scopo sono DBTYPE_DBTIME2 (OLE DB) e SQL_SS_TIME2 (ODBC).  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>Utilizzare il tipo datetime con precisione frazionaria dei secondi estesa  
 OLE DB definisce già un tipo con una precisione pari fino a 1 nanosecondo. Questo tipo, tuttavia, è già utilizzato dalle applicazioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esistenti, che garantiscono una probabile precisione pari solo a 1/300 di secondo. Il nuovo tipo `datetime2(3)` non è direttamente compatibile con il tipo datetime esistente. Se vi è un rischio che tale tipo di dati influisca negativamente sul comportamento dell'applicazione, le applicazioni devono utilizzare un nuovo flag DBCOLUMN per determinare il tipo di server effettivo.  
  
 Anche ODBC definisce già un tipo con una precisione pari fino a 1 nanosecondo. Questo tipo, tuttavia, è già utilizzato dalle applicazioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esistenti, che garantiscono una probabile precisione pari solo a 3 millisecondi. Il nuovo tipo `datetime2(3)` non è direttamente compatibile con il tipo `datetime` esistente. 
  `datetime2(3)` dispone di una precisione di un millisecondo e `datetime` dispone di una precisione di 1/300 di secondo. In ODBC le applicazioni possono determinare il tipo di server in uso tramite il campo di descrizione SQL_DESC_TYPE_NAME. Il tipo SQL_TYPE_TIMESTAMP (SQL_TIMESTAMP per le applicazioni ODBC 2.0) esistente può essere utilizzato per entrambi i tipi.  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>Utilizzare il tipo datetime con precisione frazionaria dei secondi estesa e fuso orario  
 Alcune applicazioni richiedono valori datetime con informazioni sul fuso orario. Questo requisito è supportato dai nuovi tipi DBTYPE_DBTIMESTAMPOFFSET (OLE DB) e SQL_SS_TIMESTAMPOFFSET (ODBC).  
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>Utilizzare dati di tipo date/time/datetime/datetimeoffset con conversioni sul lato client coerenti con le conversioni esistenti  
 Lo standard ODBC descrive il funzionamento delle conversioni tra tipi di data, ora e timestamp. Tali tipi sono estesi in modo coerente per includere conversioni tra tutti i tipi di data e ora introdotti in [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](sql-server-native-client-features.md)  
  
