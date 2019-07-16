---
title: URL relativi e assoluti | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- relative URLs [ADO]
- absolute URLs [ADO]
- URLs [ADO]
ms.assetid: 6a34a7ef-50cc-4c3d-82f7-106b9a8f3caf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f15c5890300687a2d587a58a586d00bf2c8d0fd8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926369"
---
# <a name="absolute-and-relative-urls"></a>URL relativi e assoluti
Un URL specifica la posizione di una destinazione archiviata in un computer locale o in rete. La destinazione può essere un file, directory, pagina HTML, image, programma e così via.  
  
 Un' *URL assoluto* contiene tutte le informazioni necessarie per individuare una risorsa.  
  
 Oggetto *URL relativo* individua una risorsa tramite un URL assoluto come punto di partenza. In effetti, il "completamento URL" della destinazione viene specificato mediante la concatenazione di URL relativi e assoluti.  
  
 Un' *URL assoluto* Usa il formato seguente: *scheme://server/path/resource*  
  
 Un URL relativo in genere è costituito solo il *percorso*e, facoltativamente, il *risorsa*, ma nessun *schema* o *server*. Nelle tabelle seguenti definiscono le singole parti del formato dell'URL completo.  
  
 *scheme*  
 Specifica come il *risorsa* è accessibile.  
  
 *server*  
 Specifica il nome del computer in cui il *risorsa* si trova.  
  
 *path*  
 Specifica la sequenza di directory che conduce alla destinazione. Se *resource* viene omesso, la destinazione è l'ultima directory nella *percorso*.  
  
 *resource*  
 Se incluso, *risorsa* è la destinazione e in genere è il nome di un file. Potrebbe essere un' *semplice file,* contenente un singolo flusso binario di byte, o una *documenti strutturati,* contenente uno o più risorse di archiviazione e i flussi binari di byte.  
  
## <a name="url-scheme-registration"></a>Registrazione dello schema URL  
 Se un provider supporta gli URL, il provider registrerà uno o più schemi URL. Registrazione significa che qualsiasi URL usando lo schema richiamerà automaticamente il provider registrato. Ad esempio, il *http* lo schema è registrato per il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Si presume di tutti gli URL con "http" preceduti rappresentano cartelle o file da utilizzare con Provider di pubblicazione sul Web. Per informazioni sugli schemi registrati dal provider, vedere la documentazione del provider.  
  
## <a name="defining-context-with-a-url"></a>Definizione del contesto con un URL  
 Una funzione di una connessione aperta, rappresentata da un [connessione](../../../ado/reference/ado-api/connection-object-ado.md) dell'oggetto, per limitare le operazioni successive all'origine dati è rappresentato da tale connessione. Vale a dire, la connessione definisce il contesto per le operazioni successive.  
  
 Con ADO 2.7 o versione successiva, un URL assoluto può anche definire un contesto. Ad esempio, quando un [Record](../../../ado/reference/ado-api/record-object-ado.md) apertura dell'oggetto con un URL assoluto, un **connessione** oggetto viene creato in modo implicito per rappresentare la risorsa specificata dall'URL.  
  
 Un URL assoluto che definisce un contesto può essere specificato nel *ActiveConnection* parametro delle **Record** oggetto [Open](../../../ado/reference/ado-api/open-method-ado-record.md) (metodo). Un URL assoluto può anche essere specificato come valore del "URL =" parola chiave nel **connessione** oggetto [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) metodo *ConnectionString* parametro e il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto [aperto](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodo *ActiveConnection* parametro.  
  
 Contesto può anche essere definito tramite l'apertura di un **Record** oppure **Recordset** che rappresenta una directory, perché questi oggetti dispongono già di un implicitamente o esplicitamente dichiarati **connessione**  oggetto che specifica di contesto.  
  
## <a name="scoped-operations"></a>Operazioni con ambite  
 Il contesto definisce anche l'ambito, vale a dire, la directory e nelle relative sottodirectory che possono partecipare nelle operazioni successive. Il **Record** oggetto ha diversi metodi con ambiti che operano su una directory e tutte le relative sottodirectory. Questi metodi includono [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md), [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md), e [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md).  
  
## <a name="relative-urls-as-command-text"></a>Tutti gli URL come testo del comando  
 È possibile specificare un comando da eseguire sull'origine dati, digitando una stringa nel *CommandText* parametro delle **connessione** dell'oggetto [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) (metodo) e il  *Origine* parametro il **Recordset** dell'oggetto [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) (metodo).  
  
 Un URL relativo può essere specificato nel *CommandText* oppure *origine* parametro. L'URL relativo non rappresentano effettivamente un comando, ad esempio un comando SQL; ma specifica semplicemente i parametri. Il contesto della connessione attiva deve essere un URL assoluto e il *opzione* parametro deve essere impostato su **adCmdTableDirect**.  
  
 Ad esempio, l'esempio di codice seguente viene illustrato come aprire una **Recordset** sul file Readme25. txt della directory/Winnt system32:  
  
```  
recordset.Open "system32/Readme25.txt", "URL=https://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
 L'URL assoluto nella stringa di connessione specifica il server (`YourServer`) e il percorso (`Winnt`). Questo URL definisce anche il contesto.  
  
 L'URL relativo nel testo del comando Usa l'URL assoluto come punto di partenza e specifica il resto del percorso (`system32`) e aprire il file (`Readme25.txt`).  
  
 Il campo di opzioni (`adCmdTableDirect`) indica che il tipo di comando è un URL relativo.  
  
 Come ulteriore esempio, verrà aperto il codice seguente un' **Recordset** sul contenuto del `Winnt` directory:  
  
```  
recordset.Open "", "URL=https://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
## <a name="ole-db-provider-supplied-url-schemes"></a>Schemi di URL fornito dal Provider OLE DB  
 La parte iniziale di un URL completo è il *schema* che viene usato per accedere alla risorsa identificata dal resto dell'URL. Esempi sono HTTP (Hypertext Transfer Protocol) e FTP (File Transfer Protocol).  
  
 ADO supporta i provider OLE DB che riconosce i propri schemi URL. Ad esempio, il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) *,* che accede ai file di Windows 2000 "pubblicati", riconosce lo schema HTTP esistente.  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Oggetto record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
