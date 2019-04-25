---
title: Comando INDEX | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- index command [ODBC]
ms.assetid: 694e8cf5-2f69-4001-9c1e-b735a4da3aff
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 864f6fa78ab1ef23b7db3a0be4c85738b95ea72d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62471259"
---
# <a name="index-command"></a>INDEX (comando)
Crea un file di indice per visualizzare e accedere ai record di tabella in ordine logico.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
INDEX ON eExpression TO IDXFileName | TAG TagName [OF CDXFileName]  
   [FOR lExpression]  
   [COMPACT]  
   [ASCENDING | DESCENDING]  
   [UNIQUE | CANDIDATE]  
   [ADDITIVE]  
```  
  
## <a name="arguments"></a>Argomenti  
 *eExpression*  
 Specifica un'espressione di indice che può includere il nome di uno o più campi dalla tabella corrente. Nel file di indice per ogni record nella tabella viene creata una chiave di indice in base all'espressione di indice. Queste chiavi utilizzate da Visual FoxPro per visualizzare e accedere ai record nella tabella.  
  
> [!NOTE]  
>  Anche se non è consigliata *eExpression* può anche essere una variabile di memoria, un elemento della matrice o un campo o l'espressione di campo da una tabella in un'altra area di lavoro. Campi di tipo Memo non possono essere usati da solo in espressioni di file di indice. devono essere combinati con altre espressioni di caratteri. Se si accede a un indice che contiene una variabile o campo che non esiste o non è possibile individuare, Visual FoxPro genera un messaggio di errore.  
  
 Se si prova a compilare un indice con una chiave che varia in lunghezza, la chiave verrà riempita con spazi. Chiavi di indice a lunghezza variabile non sono supportate in Visual FoxPro.  
  
 È possibile creare una chiave di indice con lunghezza pari a zero. Ad esempio, una chiave di indice pari a zero lunghezza viene creata quando l'espressione di indice è una sottostringa di un campo di tipo memo vuoto. Una chiave di indice pari a zero lunghezza genera un messaggio di errore. Quando Visual FoxPro viene creato un indice, la valuta i campi nel primo record nella tabella. Se un campo è vuoto, potrebbe essere necessario immettere alcuni dati temporanei nel campo del primo record per evitare che una chiave di indice di lunghezza 0.  
  
 TO *IDXFileName*  
 Crea un file di indice IDX. Il file di indice viene assegnato l'IDX di estensione predefinito.  
  
 TAG *TagName*[OF *CDXFileName*]  
 Crea un file di indice composto. Un file di indice composto è un file singolo indice costituito da un numero qualsiasi di tag separato (voci di indice). Ogni tag è identificata dal relativo nome di tag univoco. I nomi di tag devono iniziare con una lettera o un carattere di sottolineatura e possono contenere qualsiasi combinazione di lettere, cifre o caratteri di sottolineatura fino a 10. Il numero di tag in un file di indice composto è limitato solo dalla memoria disponibile e lo spazio su disco.  
  
 Indice composto per l'immissione di più file sono sempre compact. Non è necessario includere COMPACT durante la creazione di un file di indice composto. Un'estensione cdx vengono forniti nomi di file di indice composto.  
  
 Due tipi di file di indice composto è possono crearle: strutturale e non strutturali.  
  
 **File di indice composto strutturale** è possibile creare un file di indice composto strutturali con TAG *TagName* escludendo nel facoltativo *CDXFileName* clausola. Un file di indice composto strutturale sempre ha lo stesso nome di base della tabella e viene aperto automaticamente quando viene aperto nella tabella.  
  
 **File di indice composto non strutturali** è possibile creare un file di indice composto non strutturali includendo OF *CDXFileName* dopo il TAG *TagName*. A differenza di un file di indice composto strutturale, un file di indice composto non strutturali deve essere aperta in modo esplicito con la clausola di indice in uso.  
  
 Se già creato e aperto un file di indice composto, indice con TAG di emissione *TagName* aggiunge un tag per il file di indice composto.  
  
 FOR *lExpression*  
 Specifica una condizione in base al quale solo i record che soddisfano l'espressione filtro *lExpression* sono disponibili per la visualizzazione e l'accesso; le chiavi di indice vengono create nel file di indice per solo i record corrispondenti all'espressione di filtro.  
  
 Visual FoxPro Rushmore tecnologia Ottimizza un indice... PER la *lExpression* dei comandi *lExpression* è un'espressione ottimizzabile. Per prestazioni ottimali, utilizzare un'espressione ottimizzabile nella clausola FOR.  
  
 COMPACT  
 Crea un file IDX compact.  
  
 ORDINE CRESCENTE  
 Specifica un ordine crescente per il file cdx. Per impostazione predefinita, i tag cdx vengono creati in ordine crescente. (È possibile includere crescente come promemoria dell'ordine del file di indice). Una tabella può essere indicizzata in ordine inverso, includendo DECRESCENTE.  
  
 ORDINE DECRESCENTE  
 Specifica un ordine decrescente per il file cdx. Durante la creazione di file di indice IDX non è possibile includere DECRESCENTE.  
  
 UNIQUE  
 Specifica che solo il primo record rilevato con un valore di chiave di indice specifico sia incluso in un file IDX o un tag cdx. UNIQUE è utilizzabile per impedire la visualizzazione di o l'accesso per i record duplicati. Tutti i record aggiunti con chiavi di indice duplicati vengono esclusi dal file di indice. Utilizzando l'opzione di indice univoco è identico per l'esecuzione di SET UNIQUE ON prima di rilasciare REINDEX o indice.  
  
 Quando un indice univoco o un tag di indice è attivo e un record duplicato è stato modificato in modo che cambia la relativa chiave di indice, l'indice o un tag di indice viene aggiornato. Tuttavia, il record duplicato avanti con la chiave di indice originale Impossibile accedere o visualizzato fino a quando non si reindicizzare il file usando REINDICIZZAZIONE.  
  
 CANDIDATO  
 Crea un tag di indice strutturale candidato. La parola chiave CANDIDATA può essere inclusa solo durante la creazione di un tag di indice strutturale; in caso contrario, Visual FoxPro genera un messaggio di errore.  
  
 Valori duplicati del campo o una combinazione di campi specificati nell'espressione di indice impedisce a un tag di indice candidato *eExpression*. Il termine *candidato* fa riferimento al tipo di indice, perché gli indici candidato evitare valori duplicati, siano qualificati come "candidato" indice primario.  
  
 Visual FoxPro genera un errore se si crea un tag di indice candidato per un campo o una combinazione di campi che già contiene valori duplicati.  
  
 ADDITIVE  
 Mantiene aprire qualsiasi file di indice aperto in precedenza. Se si omette la clausola ADDITIVE quando si crea un file di indice o i file per una tabella con indice, vengono chiusi tutti i file di indice aperto in precedenza (eccetto struttura indice composto).  
  
## <a name="remarks"></a>Note  
 I record in una tabella che dispone di un file di indice sono visualizzati e accessibili nell'ordine specificato dall'espressione di indice. L'ordine fisico dei record nella tabella non viene modificato da un file di indice.  
  
## <a name="index-types"></a>Tipi di indice  
 Visual FoxPro consente di creare due tipi di file di indice:  
  
-   File di indice cdx contenente più voci di indice denominate tag compositi  
  
-   file di indice IDX contenente una voce di indice  
  
 È anche possibile creare un file di indice composto strutturale, che viene aperto automaticamente con la tabella.  
  
> [!NOTE]  
>  Poiché i file di indice composto strutturale vengono aperti automaticamente quando viene aperto nella tabella, sono il tipo di indice preferito.  
  
 Includere COMPATTA per creare i file di indice IDX compact. File di indice composto sono sempre compact.  
  
## <a name="index-order-and-updating"></a>Ordine di indice e l'aggiornamento  
 Tag (tag master) o un solo indice (il file indice master) controlla l'ordine in cui la tabella viene visualizzata o si accede. Alcuni comandi (ad esempio, SEEK) usano i tag di file di indice master per cercare i record. Tuttavia, tutti aprire IDX e i file di indice cdx vengono aggiornati quando vengono apportate modifiche alla tabella.  
  
## <a name="user-defined-functions"></a>Funzioni definite dall'utente  
 Sebbene un'espressione di indice può contenere una funzione definita dall'utente, è consigliabile non utilizzare funzioni definite dall'utente in un'espressione di indice. Funzioni definite dall'utente in un'espressione di indice aumentare il tempo che necessario per creare o aggiornare l'indice. Inoltre, gli aggiornamenti dell'indice non potrebbero verificarsi quando viene usata una funzione definita dall'utente per un'espressione di indice.  
  
 Se si usa una funzione definita dall'utente in un'espressione di indice, Visual FoxPro deve essere in grado di individuare la funzione definita dall'utente. Quando Visual FoxPro viene creato un indice, l'espressione di indice viene salvata nel file di indice, ma solo un riferimento alla funzione definita dall'utente è incluso nell'espressione di indice.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER TABLE - comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Comando TAG DELETE](../../odbc/microsoft/delete-tag-command.md)   
 [SET COLLATE (comando)](../../odbc/microsoft/set-collate-command.md)   
 [SET UNIQUE (comando)](../../odbc/microsoft/set-unique-command.md)
