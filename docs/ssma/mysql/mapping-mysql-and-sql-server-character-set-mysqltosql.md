---
title: Mapping caratteri SQL Server e MySQL (MySQLToSQL) dei Set | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: cebdf2ed28287a59ec9d4f0daaa1d0c200f8fe20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312364"
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>Mapping dei set di caratteri MySQL e SQL Server (MySQLToSQL)
Set di caratteri (set di caratteri) può essere specificato per tipi di dati character, espressioni e valori letterali di MySQL.  
  
## <a name="charset-mapping"></a>Mapping di set di caratteri  
Mapping di set di caratteri è definito per ogni set di caratteri MySQL e utilizzato durante la conversione di tipi di dati carattere. Specifica come eseguire la conversione di tipi di dati stringa di caratteri di un particolare set di caratteri:  
  
-   Ai tipi di caratteri nazionali SQL Server (NCHAR/NVARCHAR) o  
  
-   Ai tipi di carattere SQL Server normali (CHAR/VARCHAR)  
  
1.  **National** sono tipi di dati character database di destinazione:  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **regolare** sono tipi di dati character database di destinazione:  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  Mapping dei tipi consente solo il mapping a **national** tipi di dati character. Dopo che il tipo di dati di MySQL carattere viene convertito in base al mapping dei tipi, viene applicato il mapping di set di caratteri.  
  
> [!NOTE]  
> Mapping di set di caratteri possono essere definiti in ogni livello del nodo di Esplora oggetti di metadati e rappresentare tutti i set di caratteri letti da MySQL.  
  
## <a name="charset-mapping-on-different-node-levels"></a>Mapping di set di caratteri in diversi livelli di nodo  
Mapping di set di caratteri varia in base a diversi livelli di nodo, vale a dire:  
  
1.  Nel livello del nodo di metadati principale  
  
2.  Nel Database, categoria e livello di nodi oggetto  
  
> [!NOTE]  
> La scheda selezionata per la modifica del Mapping di set di caratteri, contiene tre pulsanti, qualunque sia il mapping per i livelli di nodo diverso.  
>   
> Sono:  
>   
> 1.  **Applicare:** Applica le modifiche apportate dall'utente, abilitato solo quando il mapping di set di caratteri viene modificato e non ancora salvato.  
> 2.  **Annulla:** Annulla le modifiche apportate dall'utente. Ottiene abilitato il pulsante quando il mapping di set di caratteri viene modificato ma non salvato.  
> 3.  **Ripristina predefiniti:** Reimposta tutti i mapping di valori predefiniti.  
  
1.  **Nel livello del nodo di metadati principale:**  Griglia di mapping di set di caratteri contiene griglia set di caratteri con una colonna separata per ogni set di caratteri. Le colonne della griglia sono:  
  
    1.  La prima colonna della griglia di denominata **nome del set di caratteri** contiene il nome di set di caratteri.  
  
    2.  L'altro denominato **Charset descrizione** contiene descrizione set di caratteri.  
  
    3.  La terza colonna, denominata **tipo di set di caratteri di destinazione** contiene le impostazioni di mapping per set di caratteri specifico. I valori per questa colonna sono:  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > I valori predefiniti per un particolare set di caratteri hanno il prefisso '(default)' dopo CHAR/VARCHAR o NCHAR/NVARCHAR.  
  
    Il mapping di set di caratteri tra il database MySQL e database di destinazione nel livello del nodo radice dei metadati è indicato di seguito:  
  
    ||||  
    |-|-|-|  
    |**Nome del set di caratteri**|**Descrizione set di caratteri**|**Tipo di set di caratteri di destinazione (impostazione predefinita)**|  
    |big5|Cinese tradizionale Big5|NCHAR/NVARCHAR (impostazione predefinita)|  
    |dec8|Europa occidentale dic|CHAR/VARCHAR (impostazione predefinita)|  
    |cp850|Europa occidentale DOS|CHAR/VARCHAR (impostazione predefinita)|  
    |hp8|Europa occidentale HP|CHAR/VARCHAR (impostazione predefinita)|  
    |koi8r|Russo Relcom KOI8-R|CHAR/VARCHAR (impostazione predefinita)|  
    |latin 1|Europa occidentale CP1252|CHAR/VARCHAR (impostazione predefinita)|  
    |Latin2|ISO 8859-2 Europa centrale|CHAR/VARCHAR (impostazione predefinita)|  
    |swe7|a 7 bit svedese|CHAR/VARCHAR (impostazione predefinita)|  
    |ascii|US ASCII|CHAR/VARCHAR (impostazione predefinita)|  
    |ujis|JP EUC giapponese|NCHAR/NVARCHAR (impostazione predefinita)|  
    |sjis|Giapponese Shift-JIS|NCHAR/NVARCHAR (impostazione predefinita)|  
    |Ebraico|ISO 8859-8 Ebraico|CHAR/VARCHAR (impostazione predefinita)|  
    |tis620|TIS620 Thai|CHAR/VARCHAR (impostazione predefinita)|  
    |eucKR|Coreano EUC-KR|NCHAR/NVARCHAR (impostazione predefinita)|  
    |koi8u|Ukrainian KOI8-U|CHAR/VARCHAR (impostazione predefinita)|  
    |gb2312|GB2312 Cinese semplificato|NCHAR/NVARCHAR (impostazione predefinita)|  
    |Greco|ISO 8859-7 Greco|CHAR/VARCHAR (impostazione predefinita)|  
    |cp 1250|Europa centrale di Windows|CHAR/VARCHAR (impostazione predefinita)|  
    |gbk|Cinese semplificato GBK|NCHAR/NVARCHAR (impostazione predefinita)|  
    |Latin5|ISO 8859-9 Turco|CHAR/VARCHAR (impostazione predefinita)|  
    |armscii8|Armeno ARMSCII-8|CHAR/VARCHAR (impostazione predefinita)|  
    |utf8|Unicode UTF-8|NCHAR/NVARCHAR (impostazione predefinita)|  
    |ucs2|Unicode UCS-2|NCHAR/NVARCHAR (impostazione predefinita)|  
    |cp866|Russo DOS|CHAR/VARCHAR (impostazione predefinita)|  
    |keybcs2|Ceco-Slovak Kamenicky di DOS|CHAR/VARCHAR (impostazione predefinita)|  
    |macce|Europa centrale Mac|CHAR/VARCHAR (impostazione predefinita)|  
    |MacRoman|Europa occidentale Mac|CHAR/VARCHAR (impostazione predefinita)|  
    |cp852|Europa centrale DOS|CHAR/VARCHAR (impostazione predefinita)|  
    |Latin7|ISO 8859-13 Baltic|CHAR/VARCHAR (impostazione predefinita)|  
    |cp 1251|Windows Cyrillic|CHAR/VARCHAR (impostazione predefinita)|  
    |cp 1256|Arabo di Windows|CHAR/VARCHAR (impostazione predefinita)|  
    |cp 1257|Pobaltské Jazyky Windows|CHAR/VARCHAR (impostazione predefinita)|  
    |BINARY|Binary pseudo charset|CHAR/VARCHAR (impostazione predefinita)|  
    |geostd8|GEOSTD8 Georgian|CHAR/VARCHAR (impostazione predefinita)|  
    |cp932|SJIS per il giapponese di Windows|NCHAR/NVARCHAR (impostazione predefinita)|  
    |eucjpms|UJIS per il giapponese di Windows|NCHAR/NVARCHAR (impostazione predefinita)|  
  
2.  **Nel Database di, categoria o i livelli dei nodi oggetto:** A livello di Database, categoria o nodi oggetto, griglia di mapping di set di caratteri contiene le stesse righe come quella nel livello del nodo radice dei metadati, una visualizzazione dei.:  
  
    1.  La prima colonna della griglia, intitolata **imposta il nome del carattere** contiene il nome di set di caratteri.  
  
    2.  La seconda colonna, denominata **descrizione di carattere impostato** contiene descrizione set di caratteri.  
  
    3.  L'unica differenza è i valori nella terza colonna della griglia. La terza colonna, denominata **tipo di dati di destinazione** contiene le impostazioni di mapping per set di caratteri specifico. I valori della colonna sono:  
  
        -   Ereditato (CHAR/VARCHAR o NCHAR/NVARCHAR)  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   Nel mapping dei set di caratteri compreso tra il database MySQL e database di destinazione nel Database, categoria e i livelli dei nodi oggetto, i valori predefiniti per un particolare set di caratteri in ciascun livello, diversa dalla radice per la colonna **tipo di dati di destinazione** deve essere ' Ereditato '.  
> -   Nella griglia, il valore **ereditato** viene aggiunto il suffisso con '(CHAR/VARCHAR)' o '(NCHAR/NVARCHAR)' a seconda di quale valore è ereditato dal padre per questo particolare set di caratteri.  
  
