---
title: Comando INDICE Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bcb30a49cb9f11ddd4c61621116aa4bd8ddcf186
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300031"
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
 *eExpression (espressione)*  
 Specifica un'espressione di indice che può includere il nome di uno o più campi della tabella corrente. Nel file di indice viene creata una chiave di indice basata sull'espressione di indice per ogni record della tabella. Visual FoxPro utilizza questi tasti per visualizzare e accedere ai record nella tabella.  
  
> [!NOTE]  
>  Sebbene non sia consigliato, *eExpression* può essere anche una variabile di memoria, un elemento di matrice o un campo o espressione di campo da una tabella in un'altra area di lavoro. I campi Memo non possono essere utilizzati da soli nelle espressioni dei file di indice. devono essere combinati con altre espressioni carattere. Se si accede a un indice che contiene una variabile o un campo che non esiste più o che non può essere individuato, Visual FoxPro genera un messaggio di errore.  
  
 Se si tenta di creare un indice con una chiave di lunghezza varia, la chiave verrà riempita con spazi. Le chiavi di indice a lunghezza variabile non sono supportate in Visual FoxPro.  
  
 È possibile creare una chiave di indice con lunghezza zero. Ad esempio, viene creata una chiave di indice di lunghezza zero quando l'espressione di indice è una sottostringa di un campo memo vuoto. Una chiave di indice di lunghezza zero genera un messaggio di errore. Quando Visual FoxPro crea un indice, valuta i campi nel primo record della tabella. Se un campo è vuoto, potrebbe essere necessario immettere alcuni dati temporanei nel campo nel primo record per evitare una chiave di indice di lunghezza 0.  
  
 A *IDXFileName*  
 Crea un file di indice con estensione idx. Al file di indice viene assegnata l'estensione predefinita .idx.  
  
 TAG *TagName*[DI *CDXFileName*]  
 Crea un file di indice composto. Un file di indice composto è un singolo file di indice costituito da un numero qualsiasi di tag separati (voci di indice). Ogni tag è identificato dal nome univoco del tag. I nomi dei tag devono iniziare con una lettera o un segno di sottolineatura e possono essere costituiti da qualsiasi combinazione di un massimo di 10 lettere, cifre o caratteri di sottolineatura. Il numero di tag in un file di indice composto è limitato solo dalla memoria disponibile e dallo spazio su disco.  
  
 I file di indice composto a più voci sono sempre compatti. Non è necessario includere COMPACT durante la creazione di un file di indice composto. Ai nomi dei file di indice composto viene assegnata un'estensione cdx.  
  
 È possibile creare due tipi di file di indice composto: strutturale e non strutturale.  
  
 **File di indice composto strutturale** È possibile creare un file di indice composto strutturale con TAG *TagName* escludendo la clausola facoltativa OF *CDXFileName.* Un file di indice composto strutturale ha sempre lo stesso nome di base della tabella e viene aperto automaticamente all'apertura della tabella.  
  
 **File di indice composto non strutturali** È possibile creare un file di indice composto non strutturale includendo DI *CDXFileName* dopo TAG *TagName*. A differenza di un file di indice composto strutturale, un file di indice composto non strutturale deve essere aperto in modo esplicito con la clausola INDEX in USE.  
  
 Se un file di indice composto è già stato creato e aperto, l'emissione di INDEX con TAG *TagName* aggiunge un tag al file di indice composto.  
  
 PER *lEspressione*  
 Specifica una condizione in base alla quale solo i record che soddisfano l'espressione di filtro *lExpression* sono disponibili per la visualizzazione e l'accesso. Le chiavi di indice vengono create nel file di indice solo per i record corrispondenti all'espressione di filtro.  
  
 La tecnologia Visual FoxPro Rushmore ottimizza un... FOR *lExpression* se *lExpression* è un'espressione ottimizzabile. Per ottenere prestazioni ottimali, utilizzare un'espressione ottimizzabile nella clausola FOR.  
  
 Compact  
 Crea un file CON estensione idx compatto.  
  
 Ascendente  
 Specifica un ordine crescente per il file con estensione cdx. Per impostazione predefinita, i tag .cdx vengono creati in ordine crescente. È possibile includere ASCENDING come promemoria dell'ordine del file di indice. Una tabella può essere indicizzata in ordine inverso includendo DESCENDING.  
  
 Discendente  
 Specifica un ordine decrescente per il file con estensione cdx. Non è possibile includere DESCENDING durante la creazione di file di indice .idx.  
  
 UNIQUE  
 Specifica che solo il primo record rilevato con un particolare valore di chiave di indice viene incluso in un file con estensione idx o in un tag cdx. UNIQUE può essere utilizzato per impedire la visualizzazione o l'accesso a record duplicati. Tutti i record aggiunti con chiavi di indice duplicate vengono esclusi dal file di indice. L'utilizzo dell'opzione UNIQUE di INDEX è identico all'esecuzione di SET UNIQUE ON prima di emettere INDEX o REINDEX.  
  
 Quando un indice UNIQUE o un tag di indice è attivo e un record duplicato viene modificato in modo da modificare la chiave di indice, il tag di indice o di indice viene aggiornato. Tuttavia, il record duplicato successivo con la chiave di indice originale non è accessibile o visualizzato fino a quando non si reindicizza il file utilizzando REINDEX.  
  
 Candidato  
 Crea un tag di indice strutturale candidato. La parola chiave CANDIDATE può essere inclusa solo quando si crea un tag di indice strutturale; in caso contrario, Visual FoxPro genera un messaggio di errore.  
  
 Un tag di indice candidato impedisce valori duplicati nel campo o nella combinazione di campi specificati nell'espressione di indice *eExpression*. Il termine *candidato* si riferisce al tipo di indice; Poiché gli indici candidati impediscono valori duplicati, si qualificano come "candidato" come un indice primario.  
  
 Visual FoxPro genera un errore se si crea un tag di indice candidato per un campo o una combinazione di campi che contiene già valori duplicati.  
  
 Additivo  
 Mantiene aperti tutti i file di indice aperti in precedenza. Se si ostoca la clausola ADDITIVE quando si crea uno o più file per una tabella con INDEX, tutti i file di indice aperti in precedenza (ad eccezione dell'indice composto strutturale) vengono chiusi.  
  
## <a name="remarks"></a>Osservazioni  
 I record in una tabella che dispone di un file di indice vengono visualizzati e accessibili nell'ordine specificato dall'espressione di indice. L'ordine fisico dei record nella tabella non viene modificato da un file di indice.  
  
## <a name="index-types"></a>Tipi di indiceIndex Types  
 Visual FoxPro consente di creare due tipi di file di indice:  
  
-   File di indice .cdx composti contenenti più voci di indice denominate tag  
  
-   File di indice .idx contenenti una voce di indice  
  
 È inoltre possibile creare un file di indice composto strutturale, che viene aperto automaticamente con la tabella.  
  
> [!NOTE]  
>  Poiché i file di indice composto strutturale vengono aperti automaticamente all'apertura della tabella, sono il tipo di indice preferito.  
  
 Includere COMPACT per creare file di indice .idx compatti. I file di indice composto sono sempre compatti.  
  
## <a name="index-order-and-updating"></a>Ordine e aggiornamento degli indici  
 Solo un file di indice (il file di indice principale) o un tag (il tag master) controlla l'ordine in cui viene visualizzata o accessibile la tabella. Alcuni comandi (SEEK, ad esempio) utilizzano il file di indice master o il tag per cercare i record. Tuttavia, tutti i file di indice .idx e .cdx aperti vengono aggiornati man mano che vengono apportate modifiche alla tabella.  
  
## <a name="user-defined-functions"></a>Funzioni definite dall'utente  
 Anche se un'espressione di indice può contenere una funzione definita dall'utente, non è consigliabile usare funzioni definite dall'utente in un'espressione di indice. Le funzioni definite dall'utente in un'espressione di indice aumentano il tempo necessario per creare o aggiornare l'indice. Inoltre, gli aggiornamenti dell'indice potrebbero non verificarsi quando una funzione definita dall'utente viene utilizzata per un'espressione di indice.  
  
 Se si utilizza una funzione definita dall'utente in un'espressione di indice, Visual FoxPro deve essere in grado di individuare la funzione definita dall'utente. Quando Visual FoxPro crea un indice, l'espressione di indice viene salvata nel file di indice, ma solo un riferimento alla funzione definita dall'utente viene incluso nell'espressione di indice.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER TABLE - Comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Comando DELETE TAG](../../odbc/microsoft/delete-tag-command.md)   
 [Comando SET COLLATE](../../odbc/microsoft/set-collate-command.md)   
 [SET UNIQUE (comando)](../../odbc/microsoft/set-unique-command.md)
