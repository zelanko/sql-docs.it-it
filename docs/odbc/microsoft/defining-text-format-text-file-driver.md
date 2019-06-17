---
title: Definizione del formato di testo (Driver File di testo) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00d20f8a6dd4d79b3100549d9286e7534bc8ce6e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240373"
---
# <a name="defining-text-format-text-file-driver"></a>Definizione del formato testo (driver file di testo)
Quando viene usato il driver di testo, è possibile usare la **Definisci formato testo** finestra di dialogo per definire il formato per le colonne in un file selezionato. Questa finestra di dialogo consente di specificare lo schema per ogni tabella di dati. Queste informazioni vengono scritte in un file ini nella directory di origine dati. Viene creato un file di schema. ini separato per ogni directory di origine dei dati di testo.  
  
> [!NOTE]  
>  Lo stesso formato di file predefinito si applica a tutte le nuove tabelle di dati di testo. Tutti i file creati dall'istruzione CREATE TABLE ereditano questi stessi valori di formato predefinito, che vengono impostate selezionando i valori di formato di file nei **definire formato di testo** finestra di dialogo con \<predefinito > scelto nel **Tabelle** elenco. Il driver di testo non modifica il formato del file di testo in base al formato definito nella finestra di dialogo, ma restituisce un errore quando Usa il formato, ad esempio quando tenta di recuperare dati dal file di testo.  
  
 Le opzioni seguenti sono disponibili nel **Definisci formato testo** nella finestra di dialogo:  
  
|Opzione|Informazioni|  
|------------|-----------------|  
|**Aggiungi**|Aggiunge una colonna usando i valori nelle **tipo di dati**, **Name**, e **larghezza** dalla finestra di dialogo, e se applicabile, il separatore della data del valore di schema. ini.|  
|**Caratteri**|**ANSI** oppure **OEM**. OEM specifica un set di caratteri non ANSI. Il valore predefinito è OEM se il formato dell'elemento selezionato nel **tabelle** elenco non è stato definito in precedenza da questa finestra di dialogo.|  
|**Intestazione di colonna nome**|Indica se le colonne della prima riga della tabella selezionata devono essere usate come nomi di colonna. Entrambi **TRUE** oppure **FALSE**. Valore predefinito è FALSE se il formato dell'elemento selezionato nel **tabelle** elenco non è stato definito in precedenza da questa finestra di dialogo.|  
|**Colonne**|Elenca i nomi di colonna per ogni colonna della tabella selezionata. L'ordine delle colonne riflette l'ordine delle colonne nella tabella. Questo elenco è abilitato se è selezionato un file nei **tabelle** elenco.|  
|**Tipo di dati**|Può essere BIT, BYTE, CHAR, valuta, data, FLOAT, INTEGER, LONGCHAR, SHORT o singolo. Tipi di dati date possono essere uno dei seguenti formati: "gg-mmm-aa", "mm-dd-yy", "mmm-dd-yy", "aaaa-mm-gg" o "aaaa-mmm-gg". "mm" indica i numeri per mesi; Denota "mmm" lettere per i mesi.|  
|**Delimiter**|Specifica il carattere delimitatore personalizzato da utilizzare per separare le colonne. Abilitato quando la **Custom delimitati** formato viene selezionato. Il delimitatore può essere solo un carattere di lunghezza e racchiusi tra virgolette doppie (") non può essere utilizzati come il carattere delimitatore. (Il delimitatore non può essere specificato in formato decimale o esadecimale).|  
|**Formato**|Lunghezza fissa o delimitata. Se delimitato, indica il tipo di delimitatore usato: virgole (CSV), tabulazione o un carattere speciale (personalizzato). Il valore predefinito è **CSV delimitati** se il formato dell'elemento selezionato nel **tabelle** elenco non è stato definito in precedenza da questa finestra di dialogo.<br /><br /> Se **formato** a lunghezza fissa e **intestazione di colonna nome** è TRUE, la prima riga deve essere delimitato da virgole.|  
|**Indovinare**|Genera automaticamente i valori della colonna dati tipo, nome e la larghezza delle colonne nella tabella selezionata analizzando il contenuto della tabella in base al **formato** casella di selezione. Attivato quando il formato della tabella è delimitato. Qualsiasi definita in precedenza le colonne nel **colonne** vengono eliminate e sostituite con le nuove voci elenco. Se **intestazione di colonna nome** non è selezionata, i nomi delle colonne vengono generate automaticamente come "F1", "F2" e così via. Non viene visualizzato alcun valore predefinito nel **tipo di dati** casella.<br /><br /> Questa funzionalità funziona solo su colonne che sono meno 64.513 byte.|  
|**Modificare**|Modifica della colonna selezionata usando i valori nelle **tipo di dati**, **Name**, e **larghezza**.|  
|**Name**|Visualizza il nome della colonna selezionata. Può essere utilizzato per specificare un nuovo nome di colonna per una colonna esistente o una nuova colonna.<br /><br /> Se **intestazione di colonna nome** è TRUE, la colonna nome visualizzato viene ignorato.|  
|**Rimuovi**|Elimina la colonna selezionata.|  
|**Righe da analizzare**|Il numero di righe che il programma di installazione o il driver analizzerà quando si impostano le colonne e tipi di dati di colonna in base ai dati esistenti.<br /><br /> È possibile immettere un numero compreso tra 1 e 32767 per il numero di righe da analizzare. Il valore predefinito è 25 se il formato dell'elemento selezionato nel **tabelle** elenco non è stato definito in precedenza da questa finestra di dialogo. (Un numero di fuori del limite verrà restituito un errore).|  
|**Tabelle**|Contiene un elenco di tutti i file nella directory selezionata tramite il **il programma di installazione di testo** finestra di dialogo che corrisponde all'elenco delle estensioni specificate.<br /><br /> Quando \<predefinito > è selezionata, e uno dei seguenti è true, i valori degli attributi nella tabella di **tabelle** gruppo vengono scritti in schema. ini (altre voci in ini non vengono modificate):<br /><br /> -Non è ini nella directory specificata.<br />-Il file ini esiste, ma non contiene alcuna sezione Schema. ini per uno dei file di testo (con l'estensione specificata) nella directory.<br />-La sezione file di testo esiste in schema. ini, ma il corpo è vuoto.<br /><br /> Quando \<predefinito > è selezionata, il **colonne** gruppo è disabilitato.|  
|**Width**|La larghezza della colonna può essere modificata per le colonne CHAR o LONGCHAR. La larghezza valore predefinito è 1 se il formato dell'elemento selezionato nel **tabelle** elenco non è stato definito in precedenza da questa finestra di dialogo.<br /><br /> Per altri tipi di dati, la larghezza delle schede è disabilitata e viene visualizzato alcun valore.|
