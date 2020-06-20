---
title: Determinazione delle caratteristiche di un set di risultati (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], characteristics
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- SQLDescribeCol function
- metadata [ODBC]
- SQLColAttribute function
- SQLNumResultCols function
ms.assetid: 90be414c-04b3-46c0-906b-ae7537989b7d
author: rothja
ms.author: jroth
ms.openlocfilehash: 5957092cdddfbcbce904d9a6483914672565d337
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "84999110"
---
# <a name="determining-the-characteristics-of-a-result-set-odbc"></a>Determinazione delle caratteristiche di un set di risultati (ODBC)
  I metadati sono dati che descrivono altri dati. I metadati dei set di risultati, ad esempio, descrivono le caratteristiche di un set di risultati, ad esempio il numero di colonne nel set di risultati, i tipi di dati di tali colonne, i nomi, la precisione e il supporto di valori Null.  
  
 ODBC fornisce metadati alle applicazioni tramite le funzioni API di catalogo. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client implementa molte delle funzioni del catalogo delle API ODBC come chiamate a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedura di catalogo corrispondente.  
  
 Le applicazioni richiedono metadati per la maggior parte delle operazioni sui set di risultati. L'applicazione, ad esempio, utilizza il tipo di dati di una colonna per determinare il tipo di variabile da associare alla colonna. L'applicazione utilizza la lunghezza in byte di una colonna di tipo carattere per determinare lo spazio necessario per visualizzare dati dalla colonna. Il modo in cui un'applicazione determina i metadati per una colonna dipende dal tipo dell'applicazione.  
  
 Le applicazioni verticali utilizzano in genere tabelle predefinite ed eseguono operazioni predefinite in tali tabelle. Poiché i metadati dei set di risultati per tali applicazioni vengono definiti persino prima che l'applicazione sia scritta e sono controllati dallo sviluppatore, possono essere specificati a livello di codice nell'applicazione. Se, ad esempio, una colonna di ID ordine viene definita come valore integer a 4 byte nell'origine dati, l'applicazione può sempre associare un valore integer a 4 byte alla colonna. Quando i metadati vengono specificati a livello di codice nell'applicazione, una modifica apportata alle tabelle utilizzate dall'applicazione comporta in genere una modifica al codice dell'applicazione.  
  
 Nelle applicazioni generiche, in particolare nelle applicazioni che supportano query ad hoc, i metadati dei set di risultati creati non sono in genere noti fino alla fase di esecuzione.  
  
 Per determinare le caratteristiche di un set di risultati, un'applicazione può chiamare le funzioni seguenti:  
  
-   [SQLNumResultCols](../native-client-odbc-api/sqlnumresultcols.md) per determinare il numero di colonne restituite da una richiesta.  
  
-   [SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md) o [SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md) per descrivere una colonna nel set di risultati.  
  
 Un'applicazione progettata correttamente viene scritta presupponendo che il set di risultati non sia noto e utilizza le informazioni restituite da tali funzioni per associare le colonne nel set di risultati. Un'applicazione può chiamare tali funzioni in qualsiasi momento in seguito alla preparazione o all'esecuzione di un'istruzione. Tuttavia, per ottenere prestazioni ottimali, un'applicazione deve chiamare **SQLColAttribute**, **SQLDescribeCol**e **SQLNumResultCols** dopo l'esecuzione di un'istruzione.  
  
 È possibile disporre di più chiamate simultanee per i metadati. Le procedure di catalogo di sistema sottostanti alle implementazioni delle API di catalogo ODBC possono essere chiamate dal driver ODBC mentre utilizza cursori del server statici. In questo modo, le applicazioni possono elaborare simultaneamente più chiamate alle funzioni di catalogo ODBC.  
  
 Se un'applicazione utilizza un set specifico di metadati più volte, potrà utilizzare in modo proficuo la memorizzazione nella cache delle informazioni nelle variabili private quando tali informazioni vengono ottenute per la prima volta. In questo modo è possibile evitare chiamate alle funzioni di catalogo ODBC per le stesse informazioni, evitando in tal modo l'esecuzione di round trip al server da parte del driver.  
  
## <a name="see-also"></a>Vedere anche  
 [Elaborazione dei risultati &#40;&#41;ODBC](processing-results-odbc.md)  
  
  
