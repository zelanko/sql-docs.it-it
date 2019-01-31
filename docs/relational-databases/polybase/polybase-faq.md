---
title: Domande frequenti in PolyBase| Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: ''
ms.openlocfilehash: 331ac177831b1e07cfab253c363a35f2bab42a6c
ms.sourcegitcommit: ee76381cfb1c16e0a063315c9c7005f10e98cfe6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55072879"
---
# <a name="frequently-asked-questions"></a>Domande frequenti

## <a name="polybase-in-big-data-clusters-vs-polybase-in-stand-alone-instances"></a>PolyBase nei cluster Big Data e PolyBase nelle istanze autonome

|Funzionalità |Cluster Big Data| Istanza autonoma|
|--------------------------|--------------------------|---------|   
|Creare tabelle esterne| X| X|
|Creare origine dati esterna da SQL Server, Oracle, Teradata e Mongo DB |X|X |
|Creare origine dati esterna usando un driver ODBC di terze parti compatibile | | X|
|Gruppi con scalabilità orizzontale di PolyBase | X | |
|Istanze del pool di dati | X| |
|Istanze del pool di archiviazione| X| |

>[!NOTE]
>
>Per altre informazioni sulle connessioni tramite il connettore ODBC generico, visitare la [procedura per la configurazione di tipi generici ODBC](polybase-configure-odbc-generic.md)

## <a name="whats-new-with-polybase-in-sql-server-2019"></a>Novità di PolyBase in SQL Server 2019 

PolyBase in SQL Server 2019 ora può leggere i dati da una più ampia varietà di origini dati. I dati di queste origini dati esterne possono essere archiviati come tabelle esterne in SQL Server. PolyBase supporta anche il calcolo Push Down verso queste origini dati esterne, con l'esclusione dei tipi generici ODBC. 

### <a name="compatible-data-sources"></a>Origini dati compatibili

- SQL Server
- Oracle
- Teradata
- MongoDB
- Tipi generici ODBC **compatibili**

  > [!NOTE]
  >
  >PolyBase consente la connessione a origini dati esterne tramite i driver ODBC di terze parti. Questi driver non sono forniti con PolyBase e potrebbero non funzionare come previsto. Per altre informazioni, visitare la [guida](polybase-configure-odbc-generic.md) per la configurazione dei tipi generici ODBC in PolyBase.  

## <a name="polybase-vs-linked-servers"></a>PolyBase e server collegati

|PolyBase | Server collegati|
|--------------------------|--------------------------|  
|Oggetto con ambito di database|Oggetto con ambito di istanza| 
|Usa driver ODBC|Usa provider OLEDB| 
| Supporta unicamente operazioni di sola lettura. Verrà ampliato in futuro| Supporta unicamente operazioni di sola lettura. Verrà ampliato in futuro| 
|Le query possono essere scalate orizzontalmente e il calcolo Push Down è supportato|Le query sono a thread singolo e il calcolo Push Down è supportato|
|Non è richiesta una configurazione separata per il gruppo di disponibilità Always On|È richiesta una configurazione separata per il gruppo di disponibilità Always On|
|Solo autenticazione di base. Miglioramenti in SQL Server 2019|Autenticazione base e integrata|