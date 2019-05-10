---
title: FREETEXTTABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- FREETEXTTABLE_TSQL
- FREETEXTTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- search conditions [SQL Server], meaning matches
- meaning matches [full-text search]
- FREETEXTTABLE function (Transact-SQL)
- ranked results [full-text search]
- column searches [full-text search]
ms.assetid: 4523ae15-4260-40a7-a53c-8df15e1fee79
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8f61daaedb3aa0157c872e6b1e9441d6523b8601
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65097279"
---
# <a name="freetexttable-transact-sql"></a>FREETEXTTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  È una funzione utilizzata nella [clausola FROM](../../t-sql/queries/from-transact-sql.md) di un [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione SELECT per eseguire un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] colonne contenenti tipi di dati basati su caratteri con indicizzazione full-text: ricerca full-text. Questa funzione restituisce una tabella di zero, uno o più righe per le colonne contenenti valori che corrispondono al significato e non solo all'esatta formulazione, del testo nell'oggetto specificato *freetext_string*. Viene fatto riferimento a FREETEXTTABLE come se fosse un normale nome di tabella.  
  
 La funzione FREETEXTTABLE è utile per gli stessi tipi di corrispondenze come le [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md),  
  
 Le query che utilizzano FREETEXTTABLE restituiscono un valore di classificazione per pertinenza (RANK) e una chiave full-text (KEY) per ogni riga.  
  
> [!NOTE]  
>  Per informazioni sulle forme di ricerca full-text supportate da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Eseguire query con ricerca full-text](../../relational-databases/search/query-with-full-text-search.md).  
  
(https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).|  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
FREETEXTTABLE (table , { column_name | (column_list) | * }   
          , 'freetext_string'   
     [ , LANGUAGE language_term ]   
     [ , top_n_by_rank ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *table*  
 Nome della tabella contrassegnata per query full-text. *Nella tabella* oppure *visualizzazione*può essere un una, due o nome di oggetto di database di tre parti. L'esecuzione della ricerca in una vista può interessare solo una tabella di base con indicizzazione full-text.  
  
 *tabella* non è possibile specificare un nome di server e non può essere usato nelle query su server collegati.  
  
 *column_name*  
 Nome di una o più colonne indicizzate full-text della tabella specificata nella clausola FROM. La colonna o le colonne possono essere di tipo **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** r **varbinary(max)**.  
  
 *column_list*  
 Viene indicato che è possibile specificare più colonne, separate da virgola. *column_list*deve essere racchiuso tra parentesi. La lingua di tutte le colonne di *column_list* deve essere la stessa, a meno che non sia specificato *language_term*.  
  
 \*  
 Specifica che la ricerca della stringa specificata in *freetext_string* deve essere eseguita in tutte le colonne registrate per la ricerca full-text. A meno che *language_term* viene specificato, la lingua di tutte le colonne indicizzate full-text nella tabella deve essere lo stesso.  
  
 *freetext_string*  
 Testo da cercare nella colonna specificata in *column_name*. È possibile specificare qualsiasi testo, comprese parole e frasi. Vengono generate corrispondenze se nell'indice full-text viene trovato un termine o vengono trovate le forme di un termine.  
  
 A differenza di CONTAINS ricerca condizione where ed è una parola chiave, se utilizzata in *freetext_string* la parola 'and' viene considerata una parola non significativa, o [parola non significativa](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)e verrà ignorata.  
  
 Non è consentito utilizzare WEIGHT, FORMSOF, caratteri jolly, NEAR e altra sintassi. *freetext_string* viene sottoposta alla sillabazione, all'analisi morfologica e al thesaurus.  
  
 LANGUAGE *language_term*  
 Lingua le cui risorse verranno utilizzate per il word breaking, lo stemming, il thesaurus e la rimozione di parole non significative come parte della query. Questo parametro è facoltativo e può essere specificato come valore stringa, intero o esadecimale corrispondente all'identificatore delle impostazioni locali (LCID) di una lingua. Se si specifica *language_term*, la lingua rappresentata dall'argomento verrà applicata a tutti gli elementi della condizione di ricerca. Se non si specifica alcun valore, verrà utilizzata la lingua full-text della colonna.  
  
 Se documenti di lingue diverse vengono archiviati insieme come oggetti BLOB in una singola colonna, l'identificatore delle impostazioni locali (LCID) di un documento specifico determina la lingua da utilizzare per indicizzarne il contenuto. Se quando si esegue una query su una colonna di questo tipo si specifica *LANGUAGE language_term* è possibile aumentare la probabilità di una corrispondenza soddisfacente.  
  
 Se l'argomento *language_term* viene specificato come stringa, corrisponde al valore della colonna**alias** nella vista di compatibilità [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).  La stringa deve essere racchiusa tra virgolette singole chiuse, come in '*language_term*'. Se l'argomento *language_term* viene specificato come valore intero, corrisponde all'LCID effettivo che identifica la lingua. Se si specifica un valore esadecimale, *language_term* è 0x seguito dal valore esadecimale di LCID. Il valore esadecimale non deve superare le otto cifre, inclusi gli zeri iniziali.  
  
 Se il valore è in formato DBCS (Double-Byte Character Set), [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo convertirà in Unicode.  
  
 Se la lingua specificata non è valida o non vi sono risorse installate corrispondenti a tale lingua, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce un errore. Per usare le risorse della lingua neutra, specificare 0x0 per *language_term*.  
  
 *top_n_by_rank*  
 Specifica che solo le *n*corrispondenze di pertinenza maggiore in ordine decrescente, vengono restituite. Si applica solo quando un valore intero, *n*, viene specificato. Se il parametro *top_n_by_rank* viene combinato con altri parametri, la query potrebbe restituire un numero inferiore di righe rispetto al numero di righe effettivamente corrispondenti a tutti i predicati. *top_n_by_rank* consente di migliorare le prestazioni delle query richiamando solo le occorrenze più attinenti.  
  
## <a name="remarks"></a>Note  
 I predicati e le funzioni full-text possono essere utilizzati in una singola tabella, specificata in modo implicito nel predicato FROM. Per cercare in più tabelle, utilizzare una tabella unita in join nella clausola FROM, che consente di eseguire una ricerca in un set di risultati prodotto da due o più tabelle.  
  
 La funzione FREETEXTTABLE utilizza le stesse condizioni di ricerca del predicato FREETEXT.  
  
 Come per CONTAINSTABLE, la tabella restituita include le colonne denominate **KEY** e **RANK**, cui viene fatto riferimento nella query per ottenere le righe appropriate e utilizzare i valori di pertinenza della riga.  
  
## <a name="permissions"></a>Permissions  
 La funzione FREETEXTTABLE può essere richiamata soltanto dagli utenti che dispongono delle autorizzazioni SELECT appropriate per la tabella specificata o per le colonne della tabella a cui viene fatto riferimento.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-simple-example"></a>A. Esempio semplice  
 Nell'esempio seguente crea e popola una tabella semplice delle due colonne, elenco di 3 provincie e i colori nei flag. L'it crea e popola un catalogo full-text e un indice nella tabella. L'oggetto **FREETEXTTABLE** viene illustrata la sintassi.  
  
```  
CREATE TABLE Flags (Country nvarchar(30) NOT NULL, FlagColors varchar(200));  
CREATE UNIQUE CLUSTERED INDEX FlagKey ON Flags(Country);  
INSERT Flags VALUES ('France', 'Blue and White and Red');  
INSERT Flags VALUES ('Italy', 'Green and White and Red');  
INSERT Flags VALUES ('Tanzania', 'Green and Yellow and Black and Yellow and Blue');  
SELECT * FROM Flags;  
GO  
  
CREATE FULLTEXT CATALOG TestFTCat;  
CREATE FULLTEXT INDEX ON Flags(FlagColors) KEY INDEX FlagKey ON TestFTCat;  
GO   
  
SELECT * FROM Flags;  
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Blue');  
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Yellow');  
```  
  
### <a name="b-using-freetext-in-an-inner-join"></a>B. Utilizzo di FREETEXT in INNER JOIN  
 L'esempio seguente restituisce la descrizione e il numero di dimensioni di tutti i prodotti con una descrizione che corrisponda il significato di `high level of performance`.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance') AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
### <a name="c-specifying-language-and-highest-ranked-matches"></a>C. Specifica della lingua e delle corrispondenze di pertinenza maggiore  
 Nell'esempio seguente è identico e viene illustrato come utilizzare il `LANGUAGE` *language_term* e *top_n_by_rank* parametri.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance',  
    LANGUAGE N'English', 2) AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
> [!NOTE]
>  Il linguaggio *language_term* paramete*r* non è necessario usare il *top_n_by_rank* parametro *.*  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione alla ricerca full-text](../../relational-databases/search/get-started-with-full-text-search.md)   
 [Creare e gestire cataloghi full-text](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [Creazione e gestione di indici full-text](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [Eseguire query con ricerca full-text](../../relational-databases/search/query-with-full-text-search.md)   
 [Creare query di ricerca full-text &#40;Visual Database Tools&#41;](https://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [Funzioni per i set di righe &#40;Transact-SQL&#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [Opzione di configurazione del server precompute rank](../../database-engine/configure-windows/precompute-rank-server-configuration-option.md)  
  
  
