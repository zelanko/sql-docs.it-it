---
title: Definizione del formato di testo (driver file di testo) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: 3af46dad-52cc-4d5c-a27e-6315d65a74e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 29dc46525f3c81e5abffe5076988716a01df06df
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307662"
---
# <a name="defining-text-format-text-file-driver"></a>Definizione del formato testo (driver file di testo)
Quando si utilizza il driver di testo, è possibile utilizzare la finestra di dialogo **Definisci formato testo** per definire il formato per le colonne in un file selezionato. Questa finestra di dialogo consente di specificare lo schema per ogni tabella di dati. Queste informazioni vengono scritte in un file schema. ini nella directory dell'origine dati. Viene creato un file schema. ini separato per ogni directory di origine dati di testo.  
  
> [!NOTE]  
>  Lo stesso formato di file predefinito si applica a tutte le nuove tabelle di dati di testo. Tutti i file creati dall'istruzione CREATE TABLE ereditano gli stessi valori di formato predefiniti, che vengono impostati selezionando i valori del formato di file nella finestra di \<dialogo **Definisci formato testo** con> predefiniti scelti nell'elenco **tabelle** . Il driver di testo non modifica il formato di un file di testo esistente in modo che corrisponda al formato definito in questa finestra di dialogo, ma restituisce un errore quando usa il formato, ad esempio quando tenta di recuperare dati dal file di testo.  
  
 Nella finestra di dialogo **Definisci formato testo** sono disponibili le opzioni seguenti:  
  
|Opzione|Informazioni|  
|------------|-----------------|  
|**Aggiungere**|Aggiunge una colonna utilizzando i valori in **tipo di dati**, **nome**e **larghezza** dalla finestra di dialogo e, se applicabile, il valore del separatore di data da schema. ini.|  
|**Caratteri**|**ANSI** o **OEM**. OEM specifica un set di caratteri non ANSI. Il valore predefinito è OEM se il formato dell'elemento selezionato nell'elenco **tabelle** non è stato definito in precedenza da questa finestra di dialogo.|  
|**Intestazione nome colonna**|Indica se le colonne della prima riga della tabella selezionata devono essere utilizzate come nomi di colonna. **True** o **false**. Il valore predefinito è FALSE se il formato dell'elemento selezionato nell'elenco **tabelle** non è stato definito in precedenza da questa finestra di dialogo.|  
|**Colonne**|Elenca i nomi di colonna per ogni colonna della tabella selezionata. L'ordine delle colonne riflette l'ordine delle colonne nella tabella. Questo elenco è abilitato se è stato selezionato un file nell'elenco **tabelle** .|  
|**Tipo di dati**|Può essere BIT, BYTE, CHAR, CURRENCY, DATE, FLOAT, INTEGER, LONGCHAR, SHORT o SINGLE. I tipi di dati relativi alla data possono essere nei formati seguenti: "gg-mmm-aa", "mm-dd-yy", "MMM-DD-YY", "aaaa-mm-gg" o "aaaa-MMM-GG". "mm" indica i numeri per i mesi; "mmm" indica le lettere per i mesi.|  
|**Delimitatore**|Specifica il carattere di delimitazione personalizzato da utilizzare per separare le colonne. Abilitata quando viene selezionato il formato **delimitato personalizzato** . Il delimitatore può essere costituito da un solo carattere di lunghezza e le virgolette doppie (") non possono essere usate come carattere delimitatore. Il delimitatore non può essere specificato in formato esadecimale o decimale.|  
|**Format**|Lunghezza delimitata o fissa. Se delimitato, indica il tipo di delimitatore utilizzato: virgola (CSV), tabulazione o carattere speciale (personalizzato). Il valore predefinito è **CSV** se il formato dell'elemento selezionato nell'elenco **tabelle** non è stato definito in precedenza da questa finestra di dialogo.<br /><br /> Se **Format** è a lunghezza fissa e l' **intestazione del nome di colonna** è true, la prima riga deve essere delimitata da virgole.|  
|**Indovinare**|Genera automaticamente il tipo di dati della colonna, il nome e i valori di larghezza per le colonne nella tabella selezionata analizzando il contenuto della tabella in base alla selezione della casella **formato** . Abilitata quando il formato della tabella è delimitato. Tutte le colonne definite in precedenza nell'elenco di **colonne** vengono cancellate e sostituite con nuove voci. Se l' **intestazione nome colonna** non è selezionata, i nomi di colonna vengono generati automaticamente come "F1", "F2" e così via. Nessun valore predefinito visualizzato nella casella **tipo di dati** .<br /><br /> Questa funzionalità funziona solo su colonne che sono inferiori a 64.513 byte.|  
|**Modificare**|Consente di modificare la colonna selezionata utilizzando i valori in **tipo di dati**, **nome**e **larghezza**.|  
|**Nome**|Visualizza il nome della colonna selezionata. Può essere utilizzato per specificare un nuovo nome di colonna per una colonna esistente o una nuova colonna.<br /><br /> Se l' **intestazione del nome di colonna** è true, il nome della colonna visualizzato viene ignorato.|  
|**Rimuovi**|Elimina la colonna selezionata.|  
|**Righe da analizzare**|Il numero di righe analizzate dal programma di installazione o dal driver quando si impostano i tipi di dati Columns e Column in base ai dati esistenti.<br /><br /> È possibile immettere un numero compreso tra 1 e 32767 per il numero di righe da analizzare. Il valore predefinito è 25 se il formato dell'elemento selezionato nell'elenco **tabelle** non è stato definito in precedenza da questa finestra di dialogo. (Un numero al di fuori del limite restituirà un errore).|  
|**Tabelle**|Contiene un elenco di tutti i file nella directory selezionata nella finestra di dialogo di **configurazione del testo** corrispondente all'elenco di estensioni specificate.<br /><br /> Quando \<si seleziona default> e una delle condizioni seguenti è true, i valori degli attributi della tabella nel gruppo **Tables** vengono scritti in Schema. ini (non vengono interessate altre voci in Schema. ini):<br /><br /> -Non è presente alcun schema. ini nella directory specificata.<br />-Il file schema. ini esiste, ma non è presente alcuna sezione in Schema. ini per uno dei file di testo (con l'estensione specificata) nella directory.<br />-La sezione per un file di testo esiste in Schema. ini, ma il corpo è vuoto.<br /><br /> Quando \<si seleziona> predefinito, il gruppo **Columns** è disabilitato.|  
|**Larghezza**|La larghezza della colonna può essere modificata per le colonne CHAR o LONGCHAR. Per impostazione predefinita, la larghezza è 1 se il formato dell'elemento selezionato nell'elenco **tabelle** non è stato definito in precedenza da questa finestra di dialogo.<br /><br /> Per gli altri tipi di dati, il controllo Width è disabilitato e non viene visualizzato alcun valore.|
