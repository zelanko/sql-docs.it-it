---
title: Linee guida e limitazioni per gli Updategram XML (SQLXML 4.0) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ce4187ca3dfa49d98e70396cdaee5aa7f9439d72
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56033902"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>Linee guida e limitazioni per gli updategram XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Quando si utilizzano updategram XML, tenere presenti le considerazioni seguenti:  
  
-   Se si utilizza un updategram per un'operazione di inserimento con solo una singola coppia di  **\<prima di >** e  **\<dopo >** blocchi, il  **\<prima >** blocco può essere omesso. Viceversa, in caso di un'operazione di eliminazione, il  **\<dopo >** blocco può essere omesso.  
  
-   Se si utilizza un updategram con più  **\<prima di >** e  **\<dopo >** blocchi nel  **\<sincronizzazione >** tag, entrambi  **\<prima di >** blocchi e  **\<dopo >** blocchi devono essere specificati al form  **\<prima >** e  **\<dopo >** coppie.  
  
-   Gli aggiornamenti in un updategram vengono applicati alla vista XML fornita da XML Schema. Ai fini della corretta esecuzione del mapping predefinito, è pertanto necessario specificare il nome del file dello schema nell'updategram o, se il nome di file non viene fornito, i nomi di elemento e di attributo devono corrispondere ai nomi di tabella e di colonna nel database.  
  
-   SQLXML 4.0 richiede che tutti i valori di colonna in un updategram vengano mappati in modo esplicito nello schema (XDR o XSD) fornito per creare la vista XML per i relativi elementi figlio. Questo comportamento differisce dalle versioni precedenti di SQLXML che è consentito un valore per una colonna non mappata nello schema se definita in modo implicito come parte della chiave esterna in una **SQL: Relationship** annotazione. Si noti che questa modifica non influisce sulla propagazione dei valori di chiave primaria negli elementi figlio, che si verifica tuttora per SQLXML 4.0 se non viene specificato in modo esplicito alcun valore per l'elemento figlio.  
  
-   Se si utilizza un updategram per modificare i dati in una colonna binaria (ad esempio la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **immagine** tipo di dati), è necessario fornire uno schema di mapping in cui il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo di dati (ad esempio, **SQL: DataType = "image"** ) e il tipo di dati XML (ad esempio **dt: Type = "binhex"** oppure **dt: Type = "binbase64**) deve essere specificato. I dati per la colonna binaria devono essere specificati nell'updategram. il **SQL: url-encode** annotazione specificata nello schema di mapping viene ignorata dall'updategram.  
  
-   Quando si scrive uno schema XSD, se il valore specificato per il **Relation** oppure **SQL: field** annotazione include un carattere speciale, ad esempio un carattere spazio (ad esempio, in "Dettagli ordine" nome della tabella), questo valore deve essere racchiuso tra parentesi (ad esempio, "[Dettagli ordine]").  
  
-   Quando si utilizzano updategram, le relazioni a catena non sono supportate. Se, ad esempio, le tabelle A e C sono correlate tramite una relazione a catena che utilizza la tabella B, si verifica l'errore seguente quando si tenta di eseguire l'updategram:  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     Anche se lo schema e l'updategram sono entrambi altrimenti corretti e hanno un formato valido, l'errore si verifica se è presente una relazione a catena.  
  
-   Gli updategram non permettono il passaggio dei **immagine** digitare dati come parametri durante gli aggiornamenti.  
  
-   I tipi di oggetto binario di grandi dimensioni (BLOB), ad esempio **text/ntext** e le immagini non devono essere utilizzati nel  **\<prima >** bloccare quando si utilizzano updategram, perché in questo caso verrà inclusi per l'utilizzo in controllo della concorrenza. Ciò può provocare problemi con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a causa delle limitazioni applicate al confronto per i tipi BLOB. Ad esempio, viene usata la parola chiave LIKE nella clausola WHERE per il confronto tra le colonne del **testo** del tipo di dati; tuttavia, i confronti avrà esito negativo nel caso dei tipi BLOB in cui la dimensione dei dati è maggiore di 8 KB.  
  
-   Caratteri speciali nei **ntext** dati possono causare problemi con SQLXML 4.0 a causa delle limitazioni applicate al confronto per i tipi BLOB. Ad esempio, l'utilizzo di "[Serializable]" nel  **\<prima di >** blocco di un updategram, se utilizzato nel controllo della concorrenza di una colonna di **ntext** tipo avrà esito negativo con il provider SQLOLEDB seguente Descrizione dell'errore:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza degli updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
