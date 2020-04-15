---
title: Definizione del formato di testo (Driver di file di testo) Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307662"
---
# <a name="defining-text-format-text-file-driver"></a>Definizione del formato testo (driver file di testo)
Quando si utilizza il driver di testo, è possibile utilizzare la finestra di dialogo **Definisci formato** testo per definire il formato per le colonne in un file selezionato. Questa finestra di dialogo consente di specificare lo schema per ogni tabella dati. Queste informazioni vengono scritte in un file Schema.ini nella directory dell'origine dati. Viene creato un file Schema.ini separato per ogni directory dell'origine dati di testo.  
  
> [!NOTE]  
>  Lo stesso formato di file predefinito si applica a tutte le nuove tabelle di dati di testo. Tutti i file creati dall'istruzione CREATE TABLE ereditano gli stessi valori di formato predefiniti, \<che vengono impostati selezionando i valori del formato di file nella finestra di dialogo **Definisci formato testo** con> predefiniti selezionati nell'elenco **Tabelle.** Il driver di testo non modifica il formato di un file di testo esistente in modo che corrisponda al formato definito in questa finestra di dialogo, ma restituisce un errore quando utilizza il formato, ad esempio quando tenta di recuperare i dati dal file di testo.  
  
 Nella finestra di dialogo **Definisci formato testo** sono disponibili le seguenti opzioni:  
  
|Opzione|Informazioni|  
|------------|-----------------|  
|**Aggiungere**|Aggiunge una colonna utilizzando i valori in **Tipo di dati**, **Nome**e **Larghezza** dalla finestra di dialogo e, se applicabile, il valore Separatore data da Schema.ini.|  
|**personaggi**|**ANSI** o **OEM**. OEM specifica un set di caratteri non ANSI. Per impostazione predefinita, il formato dell'elemento selezionato nell'elenco **Tabelle** non è stato definito in precedenza da questa finestra di dialogo.|  
|**Intestazione nome colonna**|Indica se le colonne della prima riga della tabella selezionata devono essere utilizzate come nomi di colonna. TRUE **TRUE** o **FALSE**. Il valore predefinito è FALSE se il formato dell'elemento selezionato nell'elenco **Tabelle** non è stato definito in precedenza da questa finestra di dialogo.|  
|**colonne**|Elenca i nomi di colonna per ogni colonna della tabella selezionata. L'ordine delle colonne riflette l'ordine delle colonne nella tabella. Questo elenco è abilitato se è stato selezionato un file nell'elenco **Tabelle.**|  
|**Tipo di dati**|Può essere BIT, BYTE, CHAR, CURRENCY, DATE, FLOAT, INTEGER, LONGCHAR, SHORT o SINGLE. I tipi di dati data possono essere nei seguenti formati: "dd-mmm-yy", "mm-dd-yy", "mmm-dd-yy", "yyyy-mm-dd" o "yyyy-mmm-dd". "mm" indica i numeri per i mesi; "mmm" indica le lettere per mesi.|  
|**Delimitatore**|Specifica il carattere delimitatore personalizzato da utilizzare per separare le colonne. Attivato quando è selezionato il formato **Delimitato personalizzato.** Il delimitatore può essere di lunghezza solo e le virgolette doppie (") non possono essere utilizzate come carattere delimitatore. Il delimitatore non può essere specificato in formato esadecimale o decimale.|  
|**Formato**|Lunghezza delimitata o fissa. Se delimitato, indica il tipo di delimitatore utilizzato: virgola (CSV), tabulazione o carattere speciale (personalizzato). L'impostazione predefinita è **Delimitato da CSV** se il formato dell'elemento selezionato nell'elenco **Tabelle** non è stato definito in precedenza da questa finestra di dialogo.<br /><br /> Se Format è **a** lunghezza fissa e **Intestazione nome colonna** è TRUE, la prima riga deve essere delimitata da virgole.|  
|**Indovinare**|Genera automaticamente i valori di tipo di dati, nome e larghezza della colonna per le colonne della tabella selezionata analizzando il contenuto della tabella in base alla selezione della casella **Formato.** Abilitato quando il formato della tabella è delimitato. Tutte le colonne definite in precedenza nell'elenco **Colonne** vengono cancellate e sostituite con nuove voci. Se **Intestazione nome colonna** non è selezionata, i nomi delle colonne vengono generati automaticamente come "F1", "F2" e così via. Nella casella **Tipo di dati** non viene visualizzato alcun valore predefinito.<br /><br /> Questa funzionalità funziona solo su colonne inferiori a 64.513 byte.|  
|**Modificare**|Modifica la colonna selezionata utilizzando i valori in **Tipo di dati**, **Nome**e **Larghezza**.|  
|**Nome**|Visualizza il nome della colonna selezionata. Può essere utilizzato per specificare un nuovo nome di colonna per una colonna esistente o per una nuova colonna.<br /><br /> Se **L'intestazione** del nome di colonna è TRUE, il nome della colonna visualizzato viene ignorato.|  
|**Rimuovi**|Elimina la colonna selezionata.|  
|**Righe da scansionare**|Il numero di righe che verrà analizzato dal programma di installazione o dal driver durante l'impostazione delle colonne e dei tipi di dati delle colonne in base ai dati esistenti.<br /><br /> È possibile immettere un numero compreso tra 1 e 32767 per il numero di righe da scansionare. Il valore predefinito è 25 se il formato dell'elemento selezionato nell'elenco **Tabelle** non è stato definito in precedenza da questa finestra di dialogo. (Un numero al di fuori del limite restituirà un errore.)|  
|**Tabelle**|Contiene un elenco di tutti i file nella directory selezionata nella finestra di dialogo **Impostazione testo** che corrispondono all'elenco delle estensioni specificate.<br /><br /> Quando \<è selezionata l'opzione predefinita> e si verifica una delle seguenti condizioni, i valori degli attributi della tabella nel gruppo **Tabelle** vengono scritti in Schema.ini (non vengono toccate altre voci in Schema.ini):<br /><br /> - Nella directory specificata non è presente alcun file Schema.ini.<br />- Il file Schema.ini esiste, ma non esiste alcuna sezione in Schema.ini per uno dei file di testo (con l'estensione specificata) nella directory.<br />- La sezione per un file di testo è presente in Schema.ini, ma il corpo è vuoto.- The section for a Text file exists in Schema.ini, but the body is empty.<br /><br /> Quando \<è selezionata l'opzione> predefinita, il gruppo **Colonne** è disabilitato.|  
|**Larghezza**|La larghezza della colonna può essere modificata per le colonne CHAR o LONGCHAR. Il valore predefinito della larghezza è 1 se il formato dell'elemento selezionato nell'elenco **Tabelle** non è stato definito in precedenza da questa finestra di dialogo.<br /><br /> Per altri tipi di dati, il controllo della larghezza è disabilitato e non viene visualizzato alcun valore.|
