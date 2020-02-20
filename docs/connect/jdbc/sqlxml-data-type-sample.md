---
title: Esempio di tipo di dati SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8f2ff25b-71fd-46d7-b6de-d656095d2aad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f0cc8e3e48024e6d5af789919173454d0ee05e56
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027654"
---
# <a name="sqlxml-data-type-sample"></a>esempio di tipo di dati SQLXML

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Questa applicazione [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] di esempio illustra come archiviare dati XML in un database relazionale, come recuperare dati XML da un database e come analizzare dati XML con il tipo di dati Java **SQLXML**.

Negli esempi di codice di questa sezione viene utilizzato un parser Simple API for XML (SAX). SAX è uno standard sviluppato pubblicamente per l'analisi di documenti XML basata su eventi, che offre inoltre un'API per la gestione dei dati XML. Si noti che nelle applicazioni è possibile utilizzare anche altri parser XML, ad esempio Document Object Model (DOM), Streaming API for XML (StAX) o altri.

DOM fornisce una rappresentazione a livello di programmazione di documenti, frammenti, nodi e set di nodi XML, che offre inoltre un'API per la gestione dei dati XML. Analogamente, StAX è un'API basata su Java per l'analisi di tipo pull di codice XML.

> [!IMPORTANT]  
> Per poter utilizzare l'API del parser SAX, è necessario importare l'implementazione standard di SAX dal pacchetto javax.xml.

Il file di codice per questo esempio è denominato SqlXmlDataType.java ed è disponibile nella posizione seguente:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\datatypes
```

## <a name="requirements"></a>Requisiti

Per eseguire questa applicazione di esempio, è necessario impostare il classpath per includere il file sqljdbc4.jar. Se nel classpath manca una voce per il file sqljdbc4.jar, nell'applicazione di esempio verrà generata un'eccezione di classe non trovata. Per altre informazioni su come impostare il classpath, vedere [Uso del driver JDBC](../../connect/jdbc/using-the-jdbc-driver.md).

Per eseguire questa applicazione di esempio, è inoltre necessario accedere al database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)].

## <a name="example"></a>Esempio

Nell'esempio seguente il codice di esempio esegue una connessione al database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] e quindi chiama il metodo createSampleTables.

Il metodo createSampleTables elimina le eventuali tabelle di test TestTable1 e TestTable2 esistenti, quindi inserisce due righe in TestTable1.

L'esempio di codice include inoltre i tre metodi seguenti e una classe aggiuntiva denominata ExampleContentHandler.

La classe ExampleContentHandler implementa un gestore di contenuto personalizzato che definisce i metodi per gli eventi del parser.

Il metodo showGetters indica come analizzare i dati dell'oggetto SQLXML usando SAX, ContentHandler e XMLReader. Nell'esempio di codice viene innanzitutto creata un'istanza del gestore di contenuto personalizzato ExampleContentHandler. Viene quindi creata ed eseguita un'istruzione SQL che restituisce un set di dati da TestTable1. Viene infine ottenuto un parser SAX e vengono analizzati i dati XML.

Il metodo showSetters indica come impostare la colonna **xml** usando SAX, ContentHandler e ResultSet. Viene innanzitutto creato un oggetto SQLXML vuoto usando il metodo [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) della classe Connection. Viene quindi ottenuta un'istanza di un gestore di contenuto per scrivere i dati nell'oggetto SQLXML e i dati vengono successivamente scritti in TestTable1. Viene infine eseguita un'iterazione nelle righe di dati incluse nel set di risultati e viene usato il metodo [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) per leggere i dati XML.

Il metodo showTransformer indica come ottenere i dati XML da una tabella e inserirli in un'altra tabella utilizzando SAX e Transformer. Viene innanzitutto recuperato l'oggetto SQLXML di origine da TestTable1. Viene quindi creato un oggetto SQLXML di destinazione vuoto usando il metodo [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) della classe Connection. Viene quindi aggiornato l'oggetto SQLXML di destinazione e i dati XML vengono scritti in TestTable2. Viene infine eseguita un'iterazione nelle righe di dati incluse nel set di risultati e viene usato il metodo [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) per leggere i dati XML in TestTable2.

[!code[JDBC#UsingSQLXML1](../../connect/jdbc/codesnippet/Java/sqlxml-data-type-sample_1.java)]

## <a name="see-also"></a>Vedere anche

[Uso dei tipi di dati &#40;JDBC&#41;](../../connect/jdbc/working-with-data-types-jdbc.md)
