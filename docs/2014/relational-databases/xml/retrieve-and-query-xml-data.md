---
title: Recuperare ed eseguire query su dati XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XML data [SQL Server], retrieving
- XML instance retrieval
ms.assetid: 24a28760-1225-42b3-9c89-c9c0332d9c51
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0f556bfccdd117b23db36bb9551e885f4c38614e
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526574"
---
# <a name="retrieve-and-query-xml-data"></a>Recuperare ed eseguire query su dati XML
  In questo argomento vengono descritte le opzioni query che è necessario specificare per eseguire query sui dati XML. Vengono inoltre descritte le parti di istanze XML che non vengono mantenute quando vengono archiviate nei database.  
  
##  <a name="features"></a> Caratteristiche di un'istanza XML non mantenute  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantiene il contenuto dell'istanza XML, ma non mantiene gli aspetti dell'istanza XML che non sono considerati significativi nel modello di dati XML. Ciò significa che un'istanza XML recuperata potrebbe non essere identica all'istanza archiviata nel server, ma conterrà le stesse informazioni.  
  
### <a name="xml-declaration"></a>Dichiarazione XML  
 La dichiarazione XML in un'istanza non viene mantenuta quando l'istanza viene archiviata nel database. Esempio:  
  
```  
CREATE TABLE T1 (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T1 values (1, '<?xml version="1.0" encoding="windows-1252" ?><doc></doc>')  
GO  
SELECT Col2  
FROM T1  
```  
  
 Il risultato è `<doc/>`.  
  
 La dichiarazione XML, ad esempio `<?xml version='1.0'?>`, non è mantenuta quando si archiviano i dati XML in un'istanza del tipo di dati `xml`. Questo si verifica per motivi strutturali. La dichiarazione XML () e relativi attributi (versione/encoding/stand-alone) vengono persi dopo che i dati viene convertito nel tipo `xml`. La dichiarazione XML viene considerata come una direttiva per il parser XML. I dati XML vengono archiviati internamente come ucs-2. Tutte le altre PI nell'istanza XML vengono mantenute.  
  
  
### <a name="order-of-attributes"></a>Ordine degli attributi  
 L'ordine degli attributi in un'istanza XML non viene mantenuto. Quando si esegue una query nell'istanza XML archiviata nella colonna di tipo `xml`, l'ordine degli attributi nel codice XML risultante può essere diverso rispetto all'istanza XML originale.  
  
  
### <a name="quotation-marks-around-attribute-values"></a>Virgolette che racchiudono i valori attributo  
 Le virgolette singole e le virgolette doppie che racchiudono i valori di attributi non vengono mantenute. I valori degli attributi vengono archiviati nel database come una coppia di nome e valore, senza le virgolette. Quando viene eseguita una query XQuery su un'istanza XML, il codice XML risultante viene serializzato con i valori degli attributi racchiusi tra virgolette doppie.  
  
```  
DECLARE @x xml  
-- Use double quotation marks.  
SET @x = '<root a="1" />'  
SELECT @x  
GO  
DECLARE @x xml  
-- Use single quotation marks.  
SET @x = '<root a=''1'' />'  
SELECT @x  
GO  
```  
  
 Entrambe le query restituiscono = `<root a="1" />`.  
  
  
### <a name="namespace-prefixes"></a>Prefissi degli spazi dei nomi  
 I prefissi degli spazi dei nomi non vengono mantenuti. Quando si specifica XQuery su una colonna di tipo `xml`, il codice XML serializzato risultante può restituire prefissi dello spazio dei nomi diversi.  
  
```  
DECLARE @x xml  
SET @x = '<ns1:root xmlns:ns1="abc" xmlns:ns2="abc">  
            <ns2:SomeElement/>  
          </ns1:root>'  
SELECT @x  
SELECT @x.query('/*')  
GO  
```  
  
 È possibile che il prefisso dello spazio dei nomi nel risultato sia diverso. Esempio:  
  
```  
<p1:root xmlns:p1="abc"><p1:SomeElement/></p1:root>  
```  
  
  
##  <a name="query"></a> Impostazione di opzioni query obbligatorie  
 Quando si eseguono query `xml` usando le variabili o colonne di tipo `xml` metodi con tipo di dati, le opzioni seguenti devono essere impostati come illustrato.  
  
|Opzioni SET|Valori richiesti|  
|-----------------|---------------------|  
|ANSI_NULLS|ON|  
|ANSI_PADDING|ON|  
|ANSI_WARNINGS|ON|  
|ARITHABORT|ON|  
|CONCAT_NULL_YIELDS_NULL|ON|  
|NUMERIC_ROUNDABORT|OFF|  
|QUOTED_IDENTIFIER|ON|  
  
 Se le opzioni non sono impostate come indicato, le query e modifiche su `xml` metodi con tipo di dati avrà esito negativo.  
  
  
## <a name="see-also"></a>Vedere anche  
 [Creare istanze di dati XML](create-instances-of-xml-data.md)  
  
  
